---
description: 良友
---

# 生成带有公式的 Excel 表格

在 Java 中，可以使用 **Apache POI** 库来生成带有公式的 Excel 表格。Apache POI 支持在 Excel 单元格中设置公式，并会在 Excel 打开时自动计算公式的结果。

以下是一个完整的示例，展示如何生成一个带有公式的 Excel 表格。

***

#### 实现步骤

1. **添加依赖**：
   * 在 `pom.xml` 中添加 Apache POI 的依赖。
2. **创建 Excel 文件**：
   * 使用 `XSSFWorkbook` 创建一个 Excel 文件。
   * 在单元格中设置公式。
3. **写入文件**：
   * 将生成的 Excel 文件保存到磁盘。

***

#### 代码实现

**1. 添加依赖**

在 `pom.xml` 中添加 Apache POI 的依赖：

```xml
<dependencies>
    <!-- Apache POI for Excel -->
    <dependency>
        <groupId>org.apache.poi</groupId>
        <artifactId>poi-ooxml</artifactId>
        <version>5.2.3</version>
    </dependency>
</dependencies>
```

运行 HTML

***

**2. 生成带有公式的 Excel 文件**

以下代码生成一个包含公式的 Excel 文件：

```java
import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
​
import java.io.FileOutputStream;
import java.io.IOException;
​
public class ExcelWithFormula {
​
    public static void main(String[] args) {
        // 创建一个新的工作簿
        try (Workbook workbook = new XSSFWorkbook()) {
            // 创建一个工作表
            Sheet sheet = workbook.createSheet("Sheet1");
​
            // 创建表头
            Row headerRow = sheet.createRow(0);
            headerRow.createCell(0).setCellValue("数值1");
            headerRow.createCell(1).setCellValue("数值2");
            headerRow.createCell(2).setCellValue("求和");
            headerRow.createCell(3).setCellValue("平均值");
​
            // 填充数据
            for (int i = 1; i <= 5; i++) {
                Row row = sheet.createRow(i);
​
                // 设置数值
                row.createCell(0).setCellValue(i * 10); // 数值1
                row.createCell(1).setCellValue(i * 20); // 数值2
​
                // 设置公式：求和
                Cell sumCell = row.createCell(2);
                sumCell.setCellFormula("A" + (i + 1) + "+B" + (i + 1)); // 例如：A2+B2
​
                // 设置公式：平均值
                Cell avgCell = row.createCell(3);
                avgCell.setCellFormula("AVERAGE(A" + (i + 1) + ":B" + (i + 1) + ")"); // 例如：AVERAGE(A2:B2)
            }
​
            // 自动调整列宽
            for (int i = 0; i < 4; i++) {
                sheet.autoSizeColumn(i);
            }
​
            // 写入文件
            try (FileOutputStream outputStream = new FileOutputStream("ExcelWithFormula.xlsx")) {
                workbook.write(outputStream);
            }
​
            System.out.println("Excel 文件生成完成！");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

***

#### 代码说明

1. **创建工作簿和工作表**：
   * 使用 `XSSFWorkbook` 创建一个新的 Excel 工作簿。
   * 使用 `createSheet` 方法创建一个工作表。
2. **设置表头**：
   * 在第一行设置表头，包括 "数值1"、"数值2"、"求和" 和 "平均值"。
3. **填充数据和公式**：
   * 使用循环填充数据，并在相应的单元格中设置公式。
   * 公式使用 Excel 的公式语法，例如：
     * `A2+B2`：计算 A2 和 B2 单元格的和。
     * `AVERAGE(A2:B2)`：计算 A2 和 B2 单元格的平均值。
4. **自动调整列宽**：
   * 使用 `autoSizeColumn` 方法自动调整列宽，以便内容能够完整显示。
5. **写入文件**：
   * 使用 `FileOutputStream` 将工作簿写入到磁盘文件。

***

#### 生成的 Excel 文件

运行程序后，生成的 `ExcelWithFormula.xlsx` 文件内容如下：

| 数值1 | 数值2 | 求和  | 平均值 |
| --- | --- | --- | --- |
| 10  | 20  | 30  | 15  |
| 20  | 40  | 60  | 30  |
| 30  | 60  | 90  | 45  |
| 40  | 80  | 120 | 60  |
| 50  | 100 | 150 | 75  |

* **求和列**：使用公式 `A2+B2`、`A3+B3` 等计算。
* **平均值列**：使用公式 `AVERAGE(A2:B2)`、`AVERAGE(A3:B3)` 等计算。

***

#### 支持的公式

Apache POI 支持大多数 Excel 公式，例如：

* 数学公式：`SUM`、`AVERAGE`、`MIN`、`MAX` 等。
* 逻辑公式：`IF`、`AND`、`OR` 等。
* 文本公式：`CONCATENATE`、`LEFT`、`RIGHT` 等。
* 日期公式：`TODAY`、`NOW` 等。

***

#### 注意事项

1. **公式计算**：
   * Apache POI 不会在生成文件时计算公式的结果。公式的结果会在 Excel 打开文件时自动计算。
2. **性能问题**：
   * 如果公式较多或数据量较大，生成文件的速度可能会变慢。
3. **文件格式**：
   * 使用 `XSSFWorkbook` 生成的是 `.xlsx` 格式的文件。如果需要生成 `.xls` 格式的文件，可以使用 `HSSFWorkbook`，但 `.xls` 格式的功能较为有限。

***

#### 总结

通过 Apache POI，可以轻松生成带有公式的 Excel 表格。以上示例展示了如何设置公式、填充数据并生成 Excel 文件。根据实际需求，可以扩展更多功能，例如动态生成数据、支持更多公式等。
