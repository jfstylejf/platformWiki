# 标题：sonarqube对接文档

## 1）当下接入与待接入的API的总体信息：

- 当前我们接入sonarqube的api主要有以下几个：

  - api/issues/search

  - api/rules/show

  - api/sources/lines

  - api/measures/component

  - api/sources/show

  - api/duplications/show
  
    其中后面三个api还在酝酿中，还未接入。



## 2）当前接入的API：

- ### api/issues/search：

- ![image-20191205110005513](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20191205110005513.png)

| sonar返回的json字段                                |                      存储到数据库的字段                      |
| -------------------------------------------------- | :----------------------------------------------------------: |
| key                                                |                   issue表的sonar_issue_id                    |
| rule                                               | 根据rule再通过api/rules/show来获取name，对应到rawIssue表的type属性 |
| severity                                           |       将其分为-1,0,1,2,3,4,5，对应issue表中的priority        |
| component                                          | location表：file_path(去除project名)（location表的class_name可以通过component取到） |
| textRange：startLine,endLine,startOffset,endOffset | location表:start_line,end_line,start_token,end_token（location表里的bug_lines为start_line到end_line之间的所有行） |
| locations里面的component，textrange，msg           |                 同上，但msg目前没加，待考虑                  |
| status                                             |                     对应issue表的status                      |
| message                                            |                           尚未记录                           |
| debt                                               |                           尚未记录                           |
| type                                               |                           尚未记录                           |



- ### api/rules/show:

- ![image-20191205110106702](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20191205110106702.png)

| sonar返回的json字段 | 存储到数据库的字段   |
| ------------------- | -------------------- |
| name                | rawIssue表的type属性 |



- ### api/sources/lines:

![image-20191206091850505](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20191206091850505.png)

利用该API可以取得isNew字段，判断改文件是否新加。



## 3）当前待接入的API：

- ### api/measures/component:

- ![image-20191205110617098](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20191205110617098.png)

- 该api得到的measure中有complexity，violations，ncloc，分别对应圈复杂度，新增加的issue和代码行数 可以利用，当下尚未记录。



- ### api/sources/show：

- ![image-20191205110729583](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20191205110729583.png)

  可以得到某个文件的对应行数的所有代码（这里需要将返回的标签属性进行剔除等操作进行利用）。



- ### api/duplications/show：

- ![image-20191205110750619](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20191205110750619.png)

- 通过返回的blocks和files对应起来，可以得到代码重复的对应行区间。
