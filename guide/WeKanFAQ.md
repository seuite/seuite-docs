## 如何删除用户
进入some-wekan-db容器
> $ docker exec -i -t <container_id> /bin/bash

进入wekan数据库
> $ mongo wekan

列出所有用户
> \> db.users.find().toArray()

删除指定用户
>\> db.users.remove({"username": "Test"})