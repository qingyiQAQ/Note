# SOA PartII Chapter 4

## 从Application和Service Bus Project开始

创建一个新的Application

选择Application-> Service Bus application with Service Bus project

![image-20231224154831160](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231224154831160.png)

将Application命名为ReferenceDataServices

![image-20231224155438717](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231224155438717.png)

将Project命名为AirportService

![image-20231224155614002](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231224155614002.png)

创建完后

![image-20231224155726570](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231224155726570.png)

创建一个类似的文件结构：包含schemas,business service,proxy,WSDLs,pipeline,transformations,Adapters，共7个文件夹

schemas内有AirportService.xsd,common.xsd,reference.xsd，3个文件

WSDLs内有AirportService.wsdl，1个文件

这三个文件是从AirportServiceInitialResources.jar导入的

如何创建文件夹？new->from Gallery->folder

![image-20231224160134345](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231224160134345.png)

![image-20231224161047132](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231224161047132.png)

完成后如下

![image-20231224183954297](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231224183954297.png)

### 数据库适配器——读取SQL语句

点开编辑栏的AirportService

将右侧的Database拖到External Services

![image-20231224203711287](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231224203711287.png)

出现DataAdapter的编辑器

将名字命名为QueryAirportsDB，点击Next

![image-20231224204148019](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231224204148019.png)

下一步如下填写

![image-20231224211353620](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231224211353620.png)

将JNDI name设置为SaibotCommonDB，点击Next

![image-20231224211905783](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231224211905783.png)

如下选择

![image-20231224212129376](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231224212129376.png)

点击Query查询所有可用的表，点击双箭头全部移到右侧，点击OK

![image-20231224212612516](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231224212612516.png)

两个表的primary key都指定为id

![image-20231224213531676](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231224213531676.png)

点击创建

![image-20231224213614416](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231224213614416.png)

如下

![image-20231224213800690](C:\Users\CC507\AppData\Roaming\Typora\typora-user-images\image-20231224213800690.png)
