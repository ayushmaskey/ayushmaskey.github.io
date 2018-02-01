##### [back to main page](./upgrade_cps_12_2_2.md)

# Before d-day

### App server specs

|  | Current | Next |
|--|---------|------|
| GUI server (app02) | windows server 2008 R2 | windows server 2012 R2 |
| Interop server (app03) | windows server 2008 R2 | windows server 2012 R2 |
| OS size | | 150Gb |
| RAM | | 16GB = 16384 |

### Checklist

* Rename Staging --> CPS_12_Staging.bak
* .net 4.5 and 3.5
* ie --> tools --> internet options --> security --> uncheck enable protected mode
* 32 bit ie --> "C:\Program Files (x86)\Internet Explorer\iexplorer.exe"
* firewall --> on
* disable IPv6
* time sync
* local admin
* hide sql 2014 SP2
* IIS7 in app server


## Installation

**upgrade database**
 * copy "full_build_12.2.2.4212" to c:
 * launch.exe --> copy DVD to hard drive --> finish --> exit
 * CPS 12.2 Launch shortcut in desktop
 * install server prerequisites --> Database server only --> next --> server setup
 * advanced setup options --> upgrade --> next --> next --> sa /2%---- --> check server name
 * validation --> disable trigger --> rerun validation
 * license --> next --> next --> finish --> exit
  
 upgrade completed but it went to 12.2.1.3434 from 12.0.13.2593
 try upgrade again
 
**server configurator**
 * server setup --> server configurator --> user: cps2018 p: 2%----
 * single server --> install in website in app02
 * c:\Program Files\Centricity Practice Solution\jboss\standalone\deployments\Centricity.ear\centricityPracticxeWS.war\encounterForms

** CHC **
 * download visinstaller from https://portal.visualutions.com/CP/Downloads.aspx 
 * code: 
 * install all but visAnalytics
 * EMR Instance Selection: cysx6355 and sa
 * License Manager: adminx2, LicenseManagerUserx6355 
 * Application Center: ApplicationCenterUserx6355
 * visCHC: MN
 * share c:\CHC as CHCUpdate
 * run update.bat in all terminal servers
 
**automatic**
GEMedispan DB --> new one auto created but empty
JBoss DB --> new one created but empty
Jobs --> automatic

** escript **
 * Chuck Capps <charles.d.capps@ge.com>
 * email 1/29/2018 11:05 am
 * open configure escriptmesseger 
 * Leave esmclinic database connection as is. When I move esm to the new server I am guessing I need to reconfigure this.
 * GE centricity connectivity change to new server with new sa account
 * Change the path of link logic IN and ERROR  folder
 * We do not have proxy so leave as is
 * Admin account and clinic registration – no need to change

**smpp**
 * Carlson, William (GE Healthcare) <william.carlson@ge.com>
 * email: 1/30/2018 11:02am
 * Gutierrez, Rodolfo (GE Healthcare) <rodolfo.D.gutierrez@ge.com>
 * email: 2/1/2018 11:02 am
 * smpp app --> surescript smpp config --> integration --> datasource groups --> 
 * EMR tab 
   * EMR --> server name --> 
   * Encounter form --> as is
   * DTS --> as is
   * DM --> as is
   * service layer url: change server name
 * PM tab --> MIK
 * EMR Doc Header tab
 * Image Server tab
 * Doc Indexer tab
 
** hybrid **
 * http://faxserver:88/hfxsettings_sql.asp
 * change sql server name
 * username and password
 * http://faxserver:88/hfxsettings_attachment.asp
 * doc man server path
 
** doc man **
 * Goodwin, Russell (GE Healthcare) <russell.goodwin@ge.com> 
 * email: 2/1/2018 6:24am
 * start --> kyrptic corp --> admin tool --> config editor --> login
 * connection --> modify Centricity EMR and PM connection --> new server name and username DMUser
 * change Kryptic DM info when moving DM database.
 * link logic??
 
** backup job **
```
auto installs after installing the website in app server
NT Service\MSSQLSERVER - need full permission to backup drive
```

GUI and interlop servers 
MIK in SQL server
Analytics 5.0
 
Questions: 
Server Configurator	
contact SMPP team
contact esm team
contact doc man team




