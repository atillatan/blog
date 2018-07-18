---
layout: article
permalink:
name:
file_type:
title: Nightly SQL Server Database Backup with command line batch file and windows scheduler
description: >-
  Nightly SQL Server Database Backup with command line batch file and windows scheduler
tags:  
category:  
sort_order: 21
rating: 300
changefreq: monthly
priority: 0.5
published: true
create_date: 2018-07-15T10:20:00Z
modified_date: 2018-07-15
created_by: atilla
modified_by: atilla
comments: true
redirect_url:
toc: false
---

# Nightly SQL Server Database Backup with command line batch file and windows scheduler


- We create windows scheduled task then select running period for `Backup.bat` file.
- `Backup.bat` file performs database backup then transfers backup file to another servers.
- `Backup.bat` file also performs nightly backup that is named with current date.
- `Backup.sql` called from  `Backup.bat` file.
- `Restore.bat` file performs restoration on target server. `Restore.bat` file schaduled on target server and it will have ran after backup operation.

### Backup.bat

```batch
:: Delete old backup files
del /Q /F D:\Backups\nightly\mydatabase.bak >> log.txt

:: Locate SQL server SQLCMD.exe tool 
"C:\Program Files\Microsoft SQL Server\Client SDK\ODBC\110\Tools\Binn\SQLCMD.EXE" -S HOSTNAME -i "Backup.sql" >> log.txt
echo Backup is starting: %date% %time%  >> log.txt

:: Distribute other servers

:: Target Server: Staging
net use m: \\192.168.1.10\d\backups /U:HOSTNAME1\administrator password /p:Yes >>log.txt
C:\Windows\System32\xcopy "D:\Backup\nightly\mydatabase.bak" m: /E /Y >> log.txt

:: Target Server: Test
:: Target server can restore it nightly
:: Target server can execute some scripts after restoration e.g : update-same-password-to-all-user.sql, manipulate-confidential-data.sql
net use m: \\192.168.1.11\d\backups /U:HOSTNAME2\administrator password /p:Yes >>log.txt
C:\Windows\System32\xcopy "D:\Backup\nightly\mydatabase.bak" m: /E /Y >> log.txt

:: Target Server: Backup Server
net use R: \\192.168.1.12\backups /U:HOSTNAME3\administrator password /p:Yes >>log.txt
echo f|C:\Windows\System32\xcopy "D:\Backup\nightly\mydatabase.bak" R:\mydatabase_%date:~6,4%%date:~3,2%%date:~0,2%.bak /E /Y /I >> log.txt

echo completed >> log.txt

```

### Backup.sql

```sql

DECLARE @dest nvarchar(255)

SET @dest = 'D:\Backups\nightly\mydatabase.bak'
BACKUP DATABASE [mydatabase] TO  DISK =@dest WITH NOFORMAT, COMPRESSION ,NOINIT,  NAME = N'mydatabase-Full Database Backup', SKIP, NOREWIND, NOUNLOAD,  STATS = 10
GO

declare @backupSetId as int
select @backupSetId = position from msdb..backupset where database_name=N'mydatabase' and backup_set_id=(select max(backup_set_id) from msdb..backupset where database_name=N'mydatabase' )
if @backupSetId is null begin raiserror(N'Verify failed. Backup information for database ''mydatabase'' not found.', 16, 1) end
RESTORE VERIFYONLY FROM  DISK =@dest WITH  FILE = @backupSetId,  NOUNLOAD,  NOREWIND
GO

```

### Restore.bat


```sql
echo off
cls
echo -- RESTORE DATABASE --
set BACKUPFILENAME=mydatabase.bak
set DATABASENAME=mydatabase
set SERVERNAME=HOSTNAME2
sqlcmd -E -S %SERVERNAME% -d master -Q "ALTER DATABASE [%DATABASENAME%] SET SINGLE_USER WITH ROLLBACK IMMEDIATE"

:: WARNING - delete the database, suits me
sqlcmd -E -S %SERVERNAME% -d master -Q "IF EXISTS (SELECT * FROM sysdatabases WHERE name=N'%DATABASENAME%' ) DROP DATABASE [%DATABASENAME%]"
sqlcmd -E -S %SERVERNAME% -d master -Q "CREATE DATABASE [%DATABASENAME%]"


:: restore
sqlcmd -E -S %SERVERNAME% -d master -Q "RESTORE DATABASE [%DATABASENAME%] FROM DISK = N'F:\backups\%BACKUPFILENAME%' WITH  FILE = 1,  MOVE N'mydatabase' TO N'F:\data\mydb.mdf',  MOVE N'mydatabase_log' TO N'F:\data\mydb_1.ldf', NOUNLOAD,  REPLACE,  STATS = 10"
::sqlcmd -E -S %SERVERNAME% -d master -Q "RESTORE DATABASE [%DATABASENAME%] FROM DISK = N'F:\backups\%BACKUPFILENAME%' WITH  REPLACE"

sqlcmd -E -S %SERVERNAME% -d master -Q "ALTER DATABASE [%DATABASENAME%] SET MULTI_USER"
sqlcmd -E -S %SERVERNAME% -d master -Q "use mydatabase"
sqlcmd -E -S %SERVERNAME% -d master -Q "GO"

:: Executing custom sql statements
sqlcmd -E -S %SERVERNAME% -d master -Q "UPDATE mydatabase.dbo.Users set Password='098f6bcd4621d373cade4e832627b4f6'"
::sqlcmd -E -S %SERVERNAME% -d master -Q "truncate table mydatabase.dbo.BigLogTable"
sqlcmd -E -S %SERVERNAME% -d master -Q "update mydatabase.dbo.Config set Val = 'new config' where Id = 'DD46010A-9581-4096-9406-BEEE87A16B8A'"
sqlcmd -E -S %SERVERNAME% -d master -Q "update mydatabase.dbo.Sabit set Val = new config' where Id = 'BF0BCE43-74CF-435F-A787-6A77BCC6A4DA'"

:: Create Test Users
sqlcmd -E -S %SERVERNAME% -d mydatabase -Q "CREATE USER testuser1 FOR LOGIN [testuser1]"
sqlcmd -E -S %SERVERNAME% -d mydatabase -Q "EXEC sp_addrolemember 'db_datareader', 'testuser1'"
sqlcmd -E -S %SERVERNAME% -d mydatabase -Q "ALTER LOGIN testuser1 WITH PASSWORD='DTCFdtcf1*'"


```