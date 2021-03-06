# Excel工具类使用方法
通过set 方法设置文档基本信息。
# 提供以下set方法：
setTitle(String title)
setCreate_by(String create_by)
setCreate_by(Object create_by)【会将object转换为String】
setDateFrom(String dateFrom) [null]
setDateTo(String dateTo) [null]
setSavePath(String savePath) [null]
setHeader(List header)
setHeader(String[] header)
setWidth(Integer width)
【在有设置 header的时候，会自动取其长度，不需要header的需要设置 width】
setCacheRowsInMemory(Integer rows) [10240] 

【设置内存缓存的数据行数。内存小的服务器请调小。如果不理解，请不要设置。】
# 提供的get方法：
以上的set方法均有对应的无参get方法。
add方法：
addRow(ExcelRow row) 
添加行对象【protected】【保护的方法。createXlsx过程会自动添加】
addRowFromCache(ExcelRow row) 
【将缓存对象加入到excel。会将上一个createRow得到的对象立即添加到excel】

# 提供的create方法：
createRow() 
创建行对象【创建row对象，创建前会将上一个行对象添加到excel】
createRowInCache()
创建行对象【不直接添加到excel中，需要调用addRowFromCache(ExcelRow row) 对会被加入到excel】
CreateXlsx() 
创建最终的excel，无返回.
CreateXlsxByFile() 
创建最终的excel在临时目录，并返回 File.
通过 createRow方法创建了行对象row后，可以对行对象进行操作。
提供的单元格操作方法：
addCell(Object cellContent, boolean border, short align, int col, int row) cellContent：cell 
文本内容。必需，将自动设置 cell 宽度。超过一定长度后自动定义为富文本框 
border：cell的边框，默认为true。边框大小不提供自定义 
align：对齐方式，需要从 ExcelUtil里面取static值。仅提货左，中两种常用取值 
col：合并行，需要与row结合使用。 
row：合并列，需要与col结合使用。 
col和row需成对出现或不设置。默认为1。当有行合并时，将不自动设置行宽。 \

# cell 类型支持：
java.lang.Integer. java.lang.String
【默认类型】 java.util.Date【年月日时分秒】 java.sql.Date【年月日】 java.lang.Double【默认保留两位小数】 按上述类型传入的值，将会自动设置到cell中，其他类型的值通不过上述类型判断，将用默认类型处理。

# createXlsx的写入
了解了excel的写入操作，将更便于此工具的使用。


对 excel对象得到的参数进行验证，如果有错误，将返回错误结果。
使用 header 的长度，或者 width 的值，进行标题的合并和设置。
写入文档创建时间。如果创建人有设置，加入创建人。
如果时间范围存在，设置时间范围。
如果存在 header，写入excel的列名
依次对行和进行循环。
如果有行列合并，对所在区域进行合并，并设置空字符串值。如果已经有值，说明已经被合并，找到下一个空值的cell
对cell的内容进行类型判断。不同的类型，将给不同的样式。
将内容写入到cell
内容完全写入到cell后，将excel通过文件流的方式写入到磁盘。完成 excel生成
示例代码：
com.wkclz.util.excel.ExcelTest.main();

# Excel读取类的使用方法：
setStartRow(int rowNum)
setStartCol(int colNum)
setTypes(String[] types)
最后使用 analysisXlsx() 方法，得到所有行数据。

示例代码：
com.wkclz.util.excel.ExcelRdTest.main();


