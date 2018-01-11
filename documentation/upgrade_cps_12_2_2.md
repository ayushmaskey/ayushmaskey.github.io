# Goal
  * Centricity upgrade from 12.0.13 to 12.2.2
  * January 15th, 2017

## Demo Prep

## Announcements
  * blog
  * resolve link logic errors
 
## Before upgrade
  * snapshot --> svrsql01, srvapp01, doc-man, e-script
  * stop HDRS --> Let them know
  * stop service in srvdocman
    * iNexxPlatform
	* LinkLogicDTS
	* AtlasConnect
	* QIEService64
  * back up llogic folder in srvdocman
  * backup files
    * "\\kphc-srvdocman\c$\Program Files (x86)\Centricity Practice Solution\Client\emr.ini"
	* "\\kphc-srvapp01\c$\Program Files\Centricity Practice Solution\jboss\jsw\wrapper.conf"
	  * minHeap (6144) ==> wrapper.java.additional.5=-Xms6G
	  * maxHeap (6144) ==> wrapper.java.additional.6=-Xmx6G
	  * maxPermSize(512)  ==> wrapper.java.additional.7=-XX:MaxPermSize=512m
	  * reserved code cache size (128) ==> 
	  * wrapper ping timeout (60) ==> 
	* "\\kphc-srvapp01\c$\Program Files\Centricity Practice Solution\jboss\server\default\conf\jboss-service.xml"
	  * Maximum pool zie (10)
	* "\\kphc-srvapp01\c$\Program Files\Centricity Practice Solution\jboss\server\default\deploy\DefaultDS-ds.xml"
	  * min-pool-size (10) ==>
	  * max-pool-size (300) ==>
	* "\\kphc-srvapp01\c$\Program Files\Centricity Practice Solution\jboss\server\default\deploy\centricityps-ds.xml"
	  * min-pool-size (17) ==>
	  * max-pool-size (34) ==>
	* "\\kphc-srvapp01\c$\Program Files\Centricity Practice Solution\jboss\server\default\deploy\jbossweb.sar\server.xml"
	  * max thread (365)
	  * connection timeout mx (60000)
	  * accept count (100)

[SQL Server](./upgrade_database_migration.md)
[App Server](./upgrade_app_server.md) 
  


## Visualutions
  * license, visintaller download, documentation can be found here; https://visualutions.com/ and C:\VisInstaller
    * 1233-527 production code
    * 1233-779 test code
  * C:\VisInstaller\VisInstaller.exe (run as administrator)
  * verify version - c:\programdata\visualutions\visinstaller\packages
  * EMR /PM instance: amaskey, sa
  * License Manager : Database Connection --> LicenseManagerUser :  6355, Admin user --> admin : admin 
  * CHC Option : MN
  * Analytics: prodcps --> C3ntr1c1ty@1
    * URL: http://kphc-svrsql01/ReportServer 
	* verify: sqlserver --> reporting service --> config manager
	* Subscription share: \\kphc-srvapp01\reports (\\kphc-srvapp01\chcupdate\reports) 
		* move to new app server
		* kprootadmin: G2%
	* Database: prodcps
	* Product: kphc\amaskey ?? 




## DTS
  * install from hyperV

## Terminal Servers
  * restart all terminal servers
  * shutdown kphc-srvterm06
  * uninstall from control panel
  * delete "C:\Program Files(x86)\Centricity Practice Solution"
  * run "C:\Program Files(x86)\iexplorer.exe" as admin
  * url ==> http:\\centricity:9080\centricityps\cps
  * copy ccc packages
  * update.bat
  * restart

## CCC packages

## SMPP

## esm

## document management scanning

## link logic

## qvera

## CQR

## MIK

## hybrid fax

## biscom fax server

## midmark

## warehouse

## i2i