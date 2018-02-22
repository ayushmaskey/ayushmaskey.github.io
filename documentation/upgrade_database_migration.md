##### [back to main page](./upgrade_cps_12_2_2.md)

# Before d-day

## Upgrade server specs

|  | Current | Next |
|--|---------|------|
| server | windows server 2008 R2 | windows server 2012 R2 |
| database | sql server 2008 R2 | SQLServer2014SP1-KB3058865-x64-ENU |
| OS size | 300 Gb | 350 Gb |
| Data drive | 1Tb | 1Tb |
| Backup drive | - | 300Gb |
| Temp | 200Gb | 50Gb |
| Logs | 200Gb | 200Gb |
| Processors | 40 | 40 |
| VM Max RAM |  | 256Gb = 262144Mb |
| VM Min RAM |  | 256Gb = 262144Mb |
| DB Min RAM |  | 150Gb = 153600Mb |
| DB max RAM |  | 230Gb = 235520Mb |
| OS + Others |  | 26Gb |

 * diable IPv6

 * .NET 3.5 and 4.5

[**Run upgrade advisor**](https://technet.microsoft.com/en-us/library/ms144256(v=sql.110).aspx)
* analyze current sql server
* reports on issue to fix before or after updgrade
  
## create login
```
* create new login: me
* server roles: sysadmin
```

## configurations

**Services**
```
SQL server configuration manager 

--> SQL Services --> SQL Server Agent (MSSQLSERVER) 
	--> right click properties --> service tab --> start mode "Automatic"

--> SQL Server Network config --> Protocols for MSSQLSERVER
	--> TCP/IP enable
	
Reboot server



  * Automatic: SQL server Agent, SQL server, SQL Server Reporting services
  * Manual: SQL Server Analysis Services, SQL Server Integration Services
```  

** backup **
```
full permission to backup drive NT Service\MSSQLSERVER
```



## Database files
```
SSMS --> server properties --> database settings --> change path
  Data: E:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\
  Log: G:\logs
  Backup: H:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Backup
```

## multiple tempdb files.
```
USE [master]; 
GO 
alter database tempdb modify file (name=N'tempdev', size = 8GB, FILEGROWTH = 0);
GO
  
USE [master];
GO
ALTER DATABASE [tempdb] ADD FILE (NAME = N'tempdev2', FILENAME = N'F:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\tempdev2.ndf' , SIZE = 8GB , FILEGROWTH = 0);
ALTER DATABASE [tempdb] ADD FILE (NAME = N'tempdev3', FILENAME = N'F:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\tempdev3.ndf' , SIZE = 8GB , FILEGROWTH = 0);
ALTER DATABASE [tempdb] ADD FILE (NAME = N'tempdev4', FILENAME = N'F:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\tempdev4.ndf' , SIZE = 8GB , FILEGROWTH = 0);
GO
```



# On d-day
**SHUTDOWN app, docman, esm, all terminal, smpp-ap, smpp-we**
**snapshot SQL**

## [Backup and restore](https://www.experts-exchange.com/articles/18667/SQL-Server-database-migration-The-Backup-Restore-method.html)
**full backup**
```
SSMS -->right-click database_name --> tasks --> backup --> Type: full --> destination: cant have shared
```

**copy to new server**
```
copy (NOT move) backup to new server
```

**take old database offline**
```
SSMS --> right click on database_name --> Task --> take offline
```


**restore**
```
SSMS 

--> right-click database folder --> restore database 
  * Source: device --> location of .bak
  * Destination: CentricityPS
 
* Click Verify backup media

* Files: point .mdf and .ldf

* Database property --> option --> recovery model --> full
```

**compatibility**
get version of database engine
```
SELECT SERVERPROPERTY('ProductVersion');
```
get compatibility level
```
SELECT name, compatibility_level FROM sys.databases; 
```
SQL server 2014 compatibility level would be at 120
```
alter database CentricityPS
set compatibility_level = 120
```
trust
```
USE CentricityPSDemo
GO
EXEC sp_changedbowner 'sa'
ALTER DATABASE CentricityPSDemo SET trustworthy ON 
```

## log files
```
```

## JOBS 
rebuild index - weekly
```
```
backup database
```
```
backup logs - every 2 hours
```
```

DBCC
```sql
# check db for consistency error - lot of diffferent things
# weekly (1 hour)
dbcc checkdb

# dbcc updateusage -  weekly (10 minutes)
SELECT name,database_id
FROM sys.databases;

DBCC UPDATEUSAGE (database_id)

# update statistics on whole database - weekly (5 min)
exec sp_updatestats
# log size of all data base
DBCC SQLPerf(logspace)
```

## ALERTS


### moving user / jobs / alerts / operators / login and passwords
  * need to test in demo if I need to move users
  https://support.microsoft.com/en-us/help/314546/how-to-move-databases-between-computers-that-are-running-sql-server
  * not moving system db --> master, model, tempdb or msdb
  * transfer login??
    * necessary logins
	  * amaskey
	  * sa
	  * prodcps
	  * cys

	  
## detect index fragmentation
```
SELECT dbschemas.[name] AS 'Schema',
dbtables.[name] AS 'Table',
dbindexes.[name] AS 'Index',
indexstats.avg_fragmentation_in_percent AS 'Frag (%)',
indexstats.page_count AS 'Page count'

FROM sys.dm_db_index_physical_stats (DB_ID(), NULL, NULL, NULL, NULL) AS indexstats
INNER JOIN sys.tables dbtables ON dbtables.[object_id] = indexstats.[object_id]
INNER JOIN sys.schemas dbschemas ON dbtables.[schema_id] = dbschemas.[schema_id]
INNER JOIN sys.indexes AS dbindexes ON dbindexes.[object_id] = indexstats.[object_id]
AND indexstats.index_id = dbindexes.index_id
WHERE indexstats.database_id = DB_ID()

ORDER BY indexstats.avg_fragmentation_in_percent DESC
```
