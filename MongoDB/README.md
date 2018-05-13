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

## C# Driver - System.FormatException

```
System.FormatException: The GuidRepresentation for the reader is CSharpLegacy, which requires the binary sub type to be UuidLegacy, not UuidStandard.
```

`MongoDB.Driver`를 2.5 이상으로 업데이트 한다.

## 윈도우즈 파일 캐시 시스템

### 경고 매시지

```
[initandlisten] ** WARNING: The file system cache of this machine is configured to be greater than 40% of the total memory. This can lead to increased memory pressure and poor performance.
[initandlisten] See http://dochub.mongodb.org/core/wt-windows-system-file-cache
```

> ##### Configure File System Cache Size for Windows
>
> Check the Windows file system cache limit. Having a too high or unbound upper limit can impact performance. Specifically, having a file system cache that uses 40% or more of the total memory can lead to increased memory pressure and poor performance. Use `SetSystemFileCacheSize` to limit the amount of memory that the file system cache can use. (http://dochub.mongodb.org/core/wt-windows-system-file-cache)

[Windows Server 2008 R2에서 파일 케시 한계를 설정하는 법](https://superuser.com/questions/422113/how-could-i-limit-or-even-disable-file-cache-on-windows-server-2008r2)

