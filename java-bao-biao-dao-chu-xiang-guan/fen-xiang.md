---
description: 良友
---

# 分享

*   ### 1. 导出表格加密

    在数据导出过程中，为了保护导出的 Excel 文件安全，可以对文件进行加密处理。常见的方法包括：

    * 使用 Apache POI 对 Excel 文件进行密码保护。
    * 通过 ZipOutputStream 压缩并加密 Excel 文件。
    * 结合 AES 等加密算法，对文件内容进行加密存储。

    示例代码（Apache POI 保护 Excel 文件）：

    ```java
    Workbook workbook = new XSSFWorkbook();
    Sheet sheet = workbook.createSheet("ProtectedSheet");
    sheet.protectSheet("passworbad");
    FileOutputStream fileOut = new FileOutputStream("protected.xlsx");
    workbook.write(fileOut);
    fileOut.close();
    workbook.close();
    ```

    ### 2. 保护工作表（禁止编辑）

    为了避免用户随意修改 Excel 文件内容，可以对工作表进行保护：

    * 使用 Apache POI 设定 `protectSheet(String password)` 方法，对 Excel 工作表加密。
    * 通过 `setLocked(true)` 锁定单元格，防止用户误操作。
    * 允许部分单元格可编辑（见下一节）。

    示例代码（设置可编辑单元格）：

    ```java
    Workbook workbook = new XSSFWorkbook();
    Sheet sheet = workbook.createSheet("Sheet1");
    CellStyle lockedStyle = workbook.createCellStyle();
    lockedStyle.setLocked(true);
    CellStyle unlockedStyle = workbook.createCellStyle();
    unlockedStyle.setLocked(false);
    ​
    Row row = sheet.createRow(0);
    Cell cell1 = row.createCell(0);
    cell1.setCellValue("Locked Cell");
    cell1.setCellStyle(lockedStyle);
    ​
    Cell cell2 = row.createCell(1);
    cell2.setCellValue("Editable Cell");
    cell2.setCellStyle(unlockedStyle);
    ​
    sheet.protectSheet("password");
    ```

    ### 3. 大数据量查询导出 xlsx/csv

    对于百万级数据的导出，传统方式容易导致内存溢出或导出速度缓慢。优化方法：

    * **流式写入**：使用 Apache POI 的 SXSSFWorkbook 逐行写入，避免内存占用过大。
    * **分批查询**：数据库查询采用分页策略，减少单次数据加载压力。
    * **基于 NIO 的 CSV 解析**：利用 Java NIO 进行高效 CSV 读写，提高性能。

    示例代码（使用 SXSSFWorkbook 写入大数据）：

    ```java
    SXSSFWorkbook workbook = new SXSSFWorkbook();
    Sheet sheet = workbook.createSheet("Large Data");
    for (int i = 0; i < 1000000; i++) {
        Row row = sheet.createRow(i);
        row.createCell(0).setCellValue("Data " + i);
    }
    FileOutputStream out = new FileOutputStream("large_data.xlsx");
    workbook.write(out);
    out.close();
    workbook.dispose();
    ```

    ### 4. 基于 NIO 的高性能 CSV 解析

    示例代码（使用 Java NIO 解析 CSV 文件）：

    ```java
    Path path = Paths.get("data.csv");
    try (BufferedReader reader = Files.newBufferedReader(path, StandardCharsets.UTF_8)) {
        reader.lines().forEach(line -> {
            String[] values = line.split(",");
            System.out.println(Arrays.toString(values));
        });
    }
    ```

    ### [详细代码](nio-du-qu-wen-jian.md)
*   ### 5. 异步导出数据（基于 CompletableFuture）

    示例代码（使用 CompletableFuture 进行异步导出）：

    ```java
    ExecutorService executor = Executors.newFixedThreadPool(5);
    CompletableFuture<Void> future = CompletableFuture.runAsync(() -> {
        exportData(); // 假设 exportData() 是数据导出方法
    }, executor);
    future.thenRun(() -> System.out.println("导出完成"));
    ```

    ### [详细代码](completablefuture-yi-bu-dao-chu.md)
*   ### 6. 复杂格式导出（合并单元格、多 Sheet 导入）

    #### 6.1 合并单元格导出

    示例代码（合并单元格）：

    ```java
    Workbook workbook = new XSSFWorkbook();
    Sheet sheet = workbook.createSheet("Sheet1");
    Row row = sheet.createRow(0);
    Cell cell = row.createCell(0);
    cell.setCellValue("Merged Cell");
    sheet.addMergedRegion(new CellRangeAddress(0, 0, 0, 2));
    ```

    #### 6.2 多 Sheet 表单导入

    示例代码（读取 Excel 文件中的多个 Sheet）：

    ```java
    Workbook workbook = new XSSFWorkbook(new FileInputStream("multi_sheet.xlsx"));
    for (int i = 0; i < workbook.getNumberOfSheets(); i++) {
        Sheet sheet = workbook.getSheetAt(i);
        System.out.println("Sheet Name: " + sheet.getSheetName());
    }
    workbook.close();
    ```

    ### 7. 分片导出（多线程按顺序分片导出）

    示例代码（多线程分片导出）：

    ```java
    ExecutorService executor = Executors.newFixedThreadPool(4);
    int totalData = 1000000;
    int batchSize = 250000;
    for (int i = 0; i < totalData; i += batchSize) {
        final int start = i;
        final int end = Math.min(i + batchSize, totalData);
        executor.execute(() -> exportDataRange(start, end));
    }
    executor.shutdown();
    ```

    ### [详细代码](fen-pian-dao-chu.md)
*   ### 8. 导出带有公式的表格

    示例代码（在 Excel 单元格中添加公式）：

    ```java
    Workbook workbook = new XSSFWorkbook();
    Sheet sheet = workbook.createSheet("FormulaSheet");
    Row row = sheet.createRow(0);
    Cell cell1 = row.createCell(0);
    cell1.setCellValue(10);
    Cell cell2 = row.createCell(1);
    cell2.setCellValue(20);
    Cell formulaCell = row.createCell(2);
    formulaCell.setCellFormula("A1+B1");
    ```

    ### [详细代码](sheng-cheng-dai-you-gong-shi-de-excel-biao-ge.md)
*   ### 9. 大数据量表格导入和导出（xlsx 和 csv 对比）

    #### 9.1 xlsx 的优缺点：

    **优点**：

    * 支持复杂格式（如合并单元格、公式等）。
    * 支持多个 Sheet，适合结构化数据。

    **缺点**：

    * 解析大文件时占用较多内存。
    * 适用于百万级数据，但处理过亿级数据性能下降。

    #### 9.2 csv 的优缺点：

    **优点**：

    * 轻量级，解析速度快。
    * 适用于超大规模数据导入导出。

    **缺点**：

    * 不支持复杂格式，如合并单元格、公式等。
    * 仅适用于纯文本数据处理。

#### 提高大数据导入导出效率的方法

* 采用 **分页查询** 减少数据库负载。
* 使用 **流式写入**（如 SXSSFWorkbook）降低内存占用。
* 结合 **多线程处理** 提高数据处理能力。
* 采用 **NIO** 进行 CSV 解析，减少 IO 瓶颈。

**Q\&A：** 欢迎提问！
