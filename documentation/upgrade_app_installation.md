##### [back to main page](./upgrade_cps_12_2_2.md)

# Before d-day

## Upgrade server specs

|  | Current | Next |
|--|---------|------|
| server | windows server 2008 R2 | windows server 2012 R2 |
| OS size | | 150Gb |

## Checklist

* Rename Staging --> CPS_12_Staging.bak
* .net 4.5
* ie --> tools --> internet options --> security --> uncheck enable protected mode
* firewall --> on


## Installation

**copy files**
 * copy "full_build_12.2.2.4212" to app02
 * launch.exe
 * copy DVD to hard drive
 * path to \\sql02\c$
 
**prerequisites in SQL**
 * c:\CPS_12_Staging\Launch.exe
 * install server prerequisites
 * Database server only
  
  
	
	


  * open launch.exe
    * installs server setup and server configurator
  * Server setup
    * 
  * Server Configurator
    * 