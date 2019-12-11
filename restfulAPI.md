# 基础信息之restfulAPI

该部分主要是提供一些关于code，commit等的api接口，便于调用数据库表里的信息。主要有

**code_views**模块，**commit_views**模块，**error_views**模块，**repository_views**模块；其中：



- ## **code_views**模块：

  有以下接口，具体用法建swagger文件

  ```python
  /code-service
  /code-service/free
  /code-service/ls
  /code-service/refresh
  ```



- ## **commit_views**模块：

  ```python
  /commit
  /commit/<commit_id>
  /commit/developer-lists-by-commits
  /commit/commit-time
  ```



- ## **error_views**模块：

  用来处理404等错误的api；



- ## **repository_views**模块：

  ```python
  /repository
  ```





## 主要组件：

- ### Flask：

主要用到flask框架

- ### Mysql：

```python
HOST = '10.141.221.85'  # IP地址
PORT = '3306'  # 端口
DATABASE = 'github'  # 要连接的数据库
USERNAME = 'root'  # 数据库用户
PASSWORD = 'root'  # 数据库密码
```

- ### Redis：

  ```python
  HOST = '10.141.221.85'
  PASSWORD = '85redis'
  DB = 5
  ```