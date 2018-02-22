
## Linked server

```
 * SSMS --> Server Objects --> linked servers
 * right click on linked server --> new Linked server
 * Linked server: friendly name
 * Server type: other data source
 * Provider: Microsoft OLD DB Provider for SQL Server
 * Product name: SQLSERVER
 * Data source: Server name
 * Security --> For login not defined in the list: Be made using login's current security context
```

Active directory

# Brent Ozar - FirstaidResponderKit
## [DAC](https://www.brentozar.com/archive/2011/08/dedicated-admin-connection-why-want-when-need-how-tell-whos-using/)
* during crisis

```sql
EXEC sp_configure 'remote admin connections', 1;
GO
RECONFIGURE
GO
 ```



