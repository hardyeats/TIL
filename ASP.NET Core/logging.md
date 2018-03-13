https://mitchelsellers.com/blogs/2017/10/09/real-world-aspnet-core-logging-configuration



https://blog.bitscry.com/2018/02/01/adding-serilog-to-an-asp-net-core-2-web-application/





serilog mssql 관련 버그. 버전 명시해서 가필 할 것.

```mssql
USE [Serilog]
CREATE TABLE [dbo].[Serilog] (
    [Id]              INT            IDENTITY (1, 1) NOT NULL,
    [Message]         NVARCHAR (MAX) NOT NULL,
    [MessageTemplate] NVARCHAR (MAX) NOT NULL,
    [Level]           NVARCHAR (128) NOT NULL,
    [TimeStamp]       DATETIME       NOT NULL,
    [Exception]       NVARCHAR (MAX),
    [Properties]      NVARCHAR (MAX) NOT NULL,
    CONSTRAINT [PK_Serilog.WebAPI] PRIMARY KEY CLUSTERED ([Id] ASC)
);


```

