---
description: 良友
---

# 分片且有序导出

分片导出确实可能导致数据顺序问题，因为多个线程是并发处理不同的数据段，写入文件的顺序可能和数据的原始顺序不一致。如果需要保持数据的顺序，可以通过以下方法解决：

***

#### 解决方案

**方法 1：按分片顺序写入**

在分片导出的基础上，确保每个分片的数据按顺序写入文件。可以通过以下步骤实现：

1. **为每个分片分配一个唯一的标识**（如分片索引）。
2. **按分片顺序依次写入数据**，确保最终文件的顺序正确。

***

**方法 2：使用排序合并**

1. **每个分片将数据写入临时文件**。
2. **在所有分片任务完成后，按顺序读取临时文件并合并到最终文件**。

***

#### 实现方法 1：按分片顺序写入

以下是改进后的代码，确保数据按顺序写入文件：

```java
import java.io.FileWriter;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
​
public class OrderedShardedExcelExporter {
​
    private static final int TOTAL_RECORDS = 10000; // 总记录数
    private static final int SHARD_SIZE = 1000; // 每个分片的大小
    private static final int THREAD_POOL_SIZE = 10; // 线程池大小
    private static final ExecutorService executor = Executors.newFixedThreadPool(THREAD_POOL_SIZE); // 线程池
​
    public static void main(String[] args) {
        DataService dataService = new DataService();
        String filePath = "output.csv";
​
        try (FileWriter writer = new FileWriter(filePath)) {
            // 写入表头
            writer.write("ID,Data\n");
​
            // 计算分片数量
            int shardCount = (TOTAL_RECORDS + SHARD_SIZE - 1) / SHARD_SIZE;
​
            // 创建分片任务
            List<CompletableFuture<List<String>>> futures = new ArrayList<>();
            for (int shardIndex = 0; shardIndex < shardCount; shardIndex++) {
                int start = shardIndex * SHARD_SIZE;
                int end = Math.min(start + SHARD_SIZE, TOTAL_RECORDS);
​
                // 异步处理每个分片
                CompletableFuture<List<String>> future = CompletableFuture.supplyAsync(() -> {
                    return dataService.fetchData(start, end - start);
                }, executor);
​
                futures.add(future);
            }
​
            // 按分片顺序写入数据
            for (int shardIndex = 0; shardIndex < futures.size(); shardIndex++) {
                List<String> data = futures.get(shardIndex).join(); // 等待分片任务完成
                writeDataToFile(writer, data, shardIndex * SHARD_SIZE);
            }
​
            System.out.println("导出完成！");
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            executor.shutdown(); // 关闭线程池
        }
    }
​
    /**
     * 将数据写入文件
     */
    private static void writeDataToFile(FileWriter writer, List<String> data, int startOffset) {
        try {
            for (int i = 0; i < data.size(); i++) {
                writer.write((startOffset + i + 1) + "," + data.get(i) + "\n");
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
​
/**
 * 模拟数据服务
 */
class DataService {
    /**
     * 模拟从数据库中获取数据
     *
     * @param offset 起始位置
     * @param limit  获取的记录数
     * @return 数据列表
     */
    public List<String> fetchData(int offset, int limit) {
        List<String> data = new ArrayList<>();
        for (int i = 0; i < limit; i++) {
            data.add("Data " + (offset + i + 1));
        }
        return data;
    }
}
```

***

#### 代码说明

1. **按分片顺序写入**：
   * 每个分片的任务返回一个 `List<String>`，表示该分片的数据。
   * 在主线程中，按分片顺序依次调用 `futures.get(shardIndex).join()`，确保数据按顺序写入文件。
2. **异步处理**：
   * 使用 `CompletableFuture.supplyAsync` 异步获取每个分片的数据。
   * 分片任务完成后，返回数据列表。
3. **顺序写入**：
   * 在主线程中，按分片顺序依次将数据写入文件，确保最终文件的顺序正确。

***

#### 实现方法 2：使用排序合并

如果数据量非常大，可以将每个分片的数据写入临时文件，最后按顺序合并这些临时文件。

以下是实现思路：

1. **每个分片将数据写入临时文件**：
   * 每个分片任务生成一个临时文件，文件名包含分片索引（如 `temp_0.csv`、`temp_1.csv`）。
2. **合并临时文件**：
   * 在所有分片任务完成后，按分片顺序读取临时文件，并将内容写入最终文件。

***

#### 方法 2 示例代码

```java
import java.io.*;
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
​
public class SortedShardedExcelExporter {
​
    private static final int TOTAL_RECORDS = 10000; // 总记录数
    private static final int SHARD_SIZE = 1000; // 每个分片的大小
    private static final int THREAD_POOL_SIZE = 10; // 线程池大小
    private static final ExecutorService executor = Executors.newFixedThreadPool(THREAD_POOL_SIZE); // 线程池
​
    public static void main(String[] args) {
        DataService dataService = new DataService();
        String outputFilePath = "output.csv";
        String tempFilePrefix = "temp_";
​
        try {
            // 计算分片数量
            int shardCount = (TOTAL_RECORDS + SHARD_SIZE - 1) / SHARD_SIZE;
​
            // 创建分片任务
            List<CompletableFuture<Void>> futures = new ArrayList<>();
            for (int shardIndex = 0; shardIndex < shardCount; shardIndex++) {
                int start = shardIndex * SHARD_SIZE;
                int end = Math.min(start + SHARD_SIZE, TOTAL_RECORDS);
​
                // 异步处理每个分片
                CompletableFuture<Void> future = CompletableFuture.runAsync(() -> {
                    List<String> data = dataService.fetchData(start, end - start);
                    writeDataToTempFile(tempFilePrefix + shardIndex + ".csv", data, start);
                }, executor);
​
                futures.add(future);
            }
​
            // 等待所有分片任务完成
            CompletableFuture.allOf(futures.toArray(new CompletableFuture[0])).join();
​
            // 合并临时文件
            mergeTempFiles(outputFilePath, tempFilePrefix, shardCount);
​
            System.out.println("导出完成！");
        } finally {
            executor.shutdown(); // 关闭线程池
        }
    }
​
    /**
     * 将数据写入临时文件
     */
    private static void writeDataToTempFile(String tempFilePath, List<String> data, int startOffset) {
        try (FileWriter writer = new FileWriter(tempFilePath)) {
            for (int i = 0; i < data.size(); i++) {
                writer.write((startOffset + i + 1) + "," + data.get(i) + "\n");
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
​
    /**
     * 合并临时文件
     */
    private static void mergeTempFiles(String outputFilePath, String tempFilePrefix, int shardCount) {
        try (FileWriter writer = new FileWriter(outputFilePath)) {
            writer.write("ID,Data\n"); // 写入表头
​
            for (int shardIndex = 0; shardIndex < shardCount; shardIndex++) {
                String tempFilePath = tempFilePrefix + shardIndex + ".csv";
                try (BufferedReader reader = new BufferedReader(new FileReader(tempFilePath))) {
                    String line;
                    while ((line = reader.readLine()) != null) {
                        writer.write(line + "\n");
                    }
                } catch (IOException e) {
                    e.printStackTrace();
                }
​
                // 删除临时文件
                new File(tempFilePath).delete();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

***

#### 方法 2 说明

1. **临时文件**：
   * 每个分片将数据写入一个临时文件，文件名包含分片索引（如 `temp_0.csv`）。
2. **合并文件**：
   * 在所有分片任务完成后，按分片顺序读取临时文件，并将内容写入最终文件。
3. **清理临时文件**：
   * 合并完成后，删除临时文件以释放磁盘空间。

***

#### 总结

* **方法 1** 适合数据量较小的情况，直接在内存中按顺序写入文件。
* **方法 2** 适合数据量较大的情况，通过临时文件和合并操作来保证顺序。

根据实际需求和数据量选择合适的方法即可！
