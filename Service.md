# 基础服务之Service

Service服务主要分为四块，分别为 **repoManager**，**addCommit**，**updateCommit**，**bufferManager**。其中：



- ## **repoManager**模块负责

从**KAFKA_TOPIC_2**中获取message，然后获取该repo的元信息，如若成功，则判断是否已经下载完毕，并将消息传给KAFKA_TOPIC_1；



- ## **addCommit**模块负责

从**KAFKA_TOPIC_COMPLETE_DOWNLOAD**中获取repo的部分元信息，判断是否已经在库中添加已存在，如若没有则将commit_info的信息写进相应数据库的表里；最后将信息传给**KAFKA_TOPIC_UPDATE_COMMIT**；



- ## **updateCommit**模块

负责将从数据库中获取到的repo信息进行加工，从而得到该repo的commit总数，并将其与数据库表中的commit总数进行比较，如若前者大，将关于该repo的msg发给**KAFKA_TOPIC_COMPLETE_DOWNLOAD**，并将其备份三份；



- ## **bufferManager**模块

负责如果出现分配空间的资源出现死锁或其他异常情况，将其重新释放的问题。





## 所用组件：

- ### Kafka：

  ```python
  [KafkaHost]
  host-1 = 10.141.221.85:9092
  ```

  ```python
  [KafkaTopic]
  topic-1 = RepoManager
  topic-2 = ProjectManager
  topic-3 = CompleteDownload
  topic-4 = Scan
  topic-5 = UpdateCommit
  topic-6 = DuplicateRepo
  ```

  

- ### Mysql：

  ```python
  [IssueTrackerMysqlDB]
  host = 10.131.252.160
  db = issueTracker
  user = root
  passwd = root
  charset = utf8mb4
  ```



- ### Redis:

  ```python
  [redis]
  host = 10.141.221.85
  password = 85redis
  db = 5
  ```