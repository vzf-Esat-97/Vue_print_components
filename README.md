# Vue_print_components
组件名称 PrintBtn（打印表格按钮）
打印按钮项目中要安装插件 print-js / npm install print-js --save
组件名称 ExportBtn（导出Excel按钮）
打印按钮项目中要安装插件 项目中要安装插件 FileSaver和XLSX / npm install --save xlsx file-saver
暴露字段如下：
tabel_label：表头名称
tbody_name：表格内容的名称
thead_data：表头数据
tbody_data：表格数据
special_field：特殊字段(说明：比如要在表格内展示其它内容时才传入此字段)
直接在需使用处引入即可
