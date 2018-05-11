## Access control 적용

### 경고 메시지
```
Server has startup warnings:
[initandlisten]
[initandlisten] ** WARNING: Access control is not enabled for the database.
[initandlisten] **          Read and write access to data and configuration is unrestricted.
[initandlisten]
```

### DB 인스턴스 접속

```bash
mongo --port 27017
```

### 관리자 생성

```bash
use admin
db.createUser(
  {
    user: "myUserAdmin",
    pwd: "abc123",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
)
```

### 관리자로 재접속

```bash
mongo --port 27017 -u "myUserAdmin" -p "abc123" --authenticationDatabase "admin"
```

## Windows Service로 설치

```bash
mongod --auth --dbpath=D:\mongodb --logpath=D:\mongodb\log.txt --install
```

