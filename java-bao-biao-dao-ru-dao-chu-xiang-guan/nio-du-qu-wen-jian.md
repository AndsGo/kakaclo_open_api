---
description: 良友
---

# NIO读取文件

基于 **NIO（Non-blocking I/O）** 的高性能 CSV 解析可以通过利用 Java 的 `java.nio` 包来实现。NIO 提供了更高效的文件读写方式，特别适合处理大文件或需要高性能的场景。

以下是一个基于 NIO 的高性能 CSV 解析器的实现示例：

***

#### 1. 实现思路

1. **使用 java.nio.file.Files 和 java.nio.file.Paths**：
   * 通过 `Files.lines()` 方法逐行读取文件，避免一次性加载整个文件到内存。
2. **使用 java.nio.charset.StandardCharsets**：
   * 指定字符编码（如 UTF-8），确保文件读取正确。
3. **逐行解析 CSV**：
   * 使用简单的字符串分割（如 `split(",")`）或更复杂的 CSV 解析逻辑（如处理引号、转义字符等）。
4. **高性能处理**：
   * 使用流式处理（`Stream`）和并行流（`parallel()`）来加速解析。

***

#### 2. 代码实现

```java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Stream;
​
public class NioCsvParser {
​
    public static void main(String[] args) {
        String filePath = "data.csv"; // CSV 文件路径
        List<String[]> parsedData = parseCsv(filePath);
​
        // 打印解析结果
        parsedData.forEach(row -> {
            for (String cell : row) {
                System.out.print(cell + " | ");
            }
            System.out.println();
        });
    }
​
    /**
     * 解析 CSV 文件
     *
     * @param filePath CSV 文件路径
     * @return 解析后的数据（每行是一个 String[]）
     */
    public static List<String[]> parseCsv(String filePath) {
        List<String[]> data = new ArrayList<>();
​
        try (Stream<String> lines = Files.lines(Paths.get(filePath), StandardCharsets.UTF_8)) {
            lines.forEach(line -> {
                // 解析每一行
                String[] row = parseCsvLine(line);
                data.add(row);
            });
        } catch (IOException e) {
            e.printStackTrace();
        }
​
        return data;
    }
​
    /**
     * 解析单行 CSV 数据
     *
     * @param line CSV 文件的一行
     * @return 解析后的字符串数组
     */
    private static String[] parseCsvLine(String line) {
        // 简单的 CSV 解析逻辑（假设字段中没有逗号和引号）
        return line.split(",");
​
        // 如果需要处理复杂的 CSV（如字段中有逗号或引号），可以使用以下逻辑：
        // List<String> cells = new ArrayList<>();
        // StringBuilder cell = new StringBuilder();
        // boolean inQuotes = false;
        // for (char ch : line.toCharArray()) {
        //     if (ch == '"') {
        //         inQuotes = !inQuotes; // 切换引号状态
        //     } else if (ch == ',' && !inQuotes) {
        //         cells.add(cell.toString().trim());
        //         cell.setLength(0); // 清空当前单元格
        //     } else {
        //         cell.append(ch);
        //     }
        // }
        // cells.add(cell.toString().trim()); // 添加最后一个单元格
        // return cells.toArray(new String[0]);
    }
}
```

***

#### 3. 代码说明

1. **Files.lines()**：
   * 使用 `Files.lines()` 逐行读取文件，返回一个 `Stream<String>`，避免一次性加载整个文件到内存。
   * 支持指定字符编码（如 `StandardCharsets.UTF_8`）。
2. **parseCsvLine()**：
   * 简单的 CSV 解析逻辑：使用 `split(",")` 分割每一行。
   * 如果需要处理复杂的 CSV（如字段中有逗号或引号），可以使用更复杂的解析逻辑（见注释部分）。
3. **高性能处理**：
   * 使用 `Stream` 流式处理，可以轻松扩展为并行流（`parallel()`）以加速解析。
4. **结果存储**：
   * 解析后的数据存储在 `List<String[]>` 中，每行是一个 `String[]`，每个字段是一个字符串。

***

#### 4. 示例 CSV 文件

**`data.csv`**

复制

```
Name,Age,Location
Alice,25,Beijing
Bob,30,Shanghai
Carol,28,Guangzhou
```

**解析结果**

复制

```
Name | Age | Location | 
Alice | 25 | Beijing | 
Bob | 30 | Shanghai | 
Carol | 28 | Guangzhou | 
```

***

#### 5. 性能优化

1. **并行流处理**：
   *   如果文件较大，可以使用并行流加速解析：

       java

       复制

       ```java
       lines.parallel().forEach(line -> {
           String[] row = parseCsvLine(line);
           data.add(row);
       });
       ```
2. **批量处理**：
   * 如果需要进一步优化性能，可以将数据分批处理，避免频繁操作集合。
3. **内存映射文件**：
   * 对于超大文件，可以使用 `java.nio.MappedByteBuffer` 将文件映射到内存中，直接操作内存数据。

#### 1. **NIO 的高性能特性**

NIO 的高性能主要体现在以下几点：

1. **非阻塞 I/O**：
   * NIO 支持非阻塞模式，可以在等待数据时执行其他任务，适合高并发场景。
2. **缓冲区（Buffer）**：
   * NIO 使用缓冲区（`Buffer`）来批量读写数据，减少系统调用的次数，提高效率。
3. **通道（Channel）**：
   * NIO 使用通道（`Channel`）来传输数据，通道是双向的，可以同时支持读写操作。
4. **内存映射文件（MappedByteBuffer）**：
   * NIO 支持将文件直接映射到内存中，通过操作内存来读写文件，避免频繁的系统调用。

***

#### 2. **改进后的高性能 CSV 解析器**

为了充分体现 NIO 的高性能特性，我们可以使用 `java.nio.channels.FileChannel` 和 `java.nio.MappedByteBuffer` 来实现一个高性能的 CSV 解析器。

以下是改进后的代码：

```java
import java.io.IOException;
import java.nio.MappedByteBuffer;
import java.nio.channels.FileChannel;
import java.nio.file.Paths;
import java.nio.file.StandardOpenOption;
import java.util.ArrayList;
import java.util.List;
​
public class HighPerformanceCsvParser {
​
    public static void main(String[] args) {
        String filePath = "data.csv"; // CSV 文件路径
        List<String[]> parsedData = parseCsv(filePath);
​
        // 打印解析结果
        parsedData.forEach(row -> {
            for (String cell : row) {
                System.out.print(cell + " | ");
            }
            System.out.println();
        });
    }
​
    /**
     * 解析 CSV 文件
     *
     * @param filePath CSV 文件路径
     * @return 解析后的数据（每行是一个 String[]）
     */
    public static List<String[]> parseCsv(String filePath) {
        List<String[]> data = new ArrayList<>();
​
        try (FileChannel channel = FileChannel.open(Paths.get(filePath), StandardOpenOption.READ)) {
            // 获取文件大小
            long fileSize = channel.size();
            // 将文件映射到内存中
            MappedByteBuffer buffer = channel.map(FileChannel.MapMode.READ_ONLY, 0, fileSize);
​
            // 解析 CSV 数据
            StringBuilder line = new StringBuilder();
            while (buffer.hasRemaining()) {
                char ch = (char) buffer.get();
                if (ch == '\n') {
                    // 解析一行数据
                    String[] row = parseCsvLine(line.toString());
                    data.add(row);
                    line.setLength(0); // 清空当前行
                } else {
                    line.append(ch);
                }
            }
            // 处理最后一行（如果文件没有以换行符结尾）
            if (line.length() > 0) {
                String[] row = parseCsvLine(line.toString());
                data.add(row);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
​
        return data;
    }
​
    /**
     * 解析单行 CSV 数据
     *
     * @param line CSV 文件的一行
     * @return 解析后的字符串数组
     */
    private static String[] parseCsvLine(String line) {
        // 简单的 CSV 解析逻辑（假设字段中没有逗号和引号）
        return line.split(",");
​
        // 如果需要处理复杂的 CSV（如字段中有逗号或引号），可以使用以下逻辑：
        // List<String> cells = new ArrayList<>();
        // StringBuilder cell = new StringBuilder();
        // boolean inQuotes = false;
        // for (char ch : line.toCharArray()) {
        //     if (ch == '"') {
        //         inQuotes = !inQuotes; // 切换引号状态
        //     } else if (ch == ',' && !inQuotes) {
        //         cells.add(cell.toString().trim());
        //         cell.setLength(0); // 清空当前单元格
        //     } else {
        //         cell.append(ch);
        //     }
        // }
        // cells.add(cell.toString().trim()); // 添加最后一个单元格
        // return cells.toArray(new String[0]);
    }
}
```

***

#### 3. 改进点解析

1. **使用 FileChannel 和 MappedByteBuffer**：
   * 通过 `FileChannel.open()` 打开文件通道。
   * 使用 `channel.map()` 将文件映射到内存中，返回一个 `MappedByteBuffer`。
   * 直接操作内存中的数据，避免了频繁的系统调用。
2. **高性能文件读取**：
   * `MappedByteBuffer` 是基于内存映射的，读取速度比传统的 `InputStream` 更快。
   * 适合处理大文件，因为文件内容可以直接映射到内存中，而不需要一次性加载整个文件。
3. **逐行解析**：
   * 通过遍历 `MappedByteBuffer`，逐字符读取并解析 CSV 数据。
   * 当遇到换行符（）时，解析当前行并清空缓冲区。

***

#### 4. 性能对比

| 方法                       | 优点                 | 缺点             |
| ------------------------ | ------------------ | -------------- |
| 传统 I/O（`InputStream`）    | 简单易用，适合小文件         | 频繁的系统调用，性能较低   |
| NIO（`FileChannel`）       | 高性能，适合大文件和高并发场景    | 实现复杂，需要手动管理缓冲区 |
| 内存映射（`MappedByteBuffer`） | 最高性能，直接操作内存，减少系统调用 | 占用较多内存，不适合超大文件 |

***

#### 5. 适用场景

* **大文件处理**：使用 `MappedByteBuffer` 可以高效处理大文件。
* **高并发场景**：NIO 的非阻塞特性适合高并发场景。
* **低延迟需求**：内存映射文件可以减少系统调用，降低延迟。

***

#### 6. 进一步优化

1. **并行处理**：
   * 可以将文件分成多个块，使用多线程并行解析。
2. **零拷贝技术**：
   * 使用 `FileChannel.transferTo()` 或 `FileChannel.transferFrom()` 实现零拷贝文件传输。
3. **复杂 CSV 解析**：
   * 如果需要处理复杂的 CSV 格式（如字段中有逗号或引号），可以使用更复杂的解析逻辑。

***

#### 7. 总结

改进后的代码充分体现了 NIO 的高性能特性，通过 `FileChannel` 和 `MappedByteBuffer` 实现了高效的文件读取和解析。相比传统的 I/O 方式，NIO 在处理大文件和高并发场景时具有明显的性能优势。
