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