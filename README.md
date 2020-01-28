![MIKES DATA WORK GIT REPO](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_01.png "Mikes Data Work")        

# SQL Error Cannot Generate SSPI Context
**Post Date: March 22, 2007**        



## Contents    
- [About Process](##About-Process)  
- [SQL Logic](#SQL-Logic)  
- [Build Info](#Build-Info)  
- [Author](#Author)  
- [License](#License)       

## About-Process

<p>Cannot Generate SSPI Context
note:
sspi errors are sometimes fixed (at least in 2005) simply by adjusting the service login
account to "local system" this has worked in many situations regarding connectivity issues
between sql server, and analysis services.
moving on… in other cases..
here is how to fix the SSPI Context error in 2 easy steps.
STEP 1:
you will need the Setspn utility from Microsoft, and you'll need
domain admin rights to run it.
where do you get the Setspn utility? you can download it from this
link:
http://www.microsoft.com/downloads/…laylang=en
or you can get it from the Windows 2003 Server SP1 CD.
it's called: Support Tools for SP1.exe
you could always google for the suptools.msi, or setspn.exe if
you need.
once you get the Support Tools installed either on your workstation,
or on the server it's self you can find the Setspn.exe utility in the
following location:
c:\program files\support tools
the Setspn utility can only be used from the Command Prompt.
STEP 2:
Go to: Start -> Run & type in CMD
type in:
cd program files\support tools
from here you will need to specify the domain user account that you are
using to connect from Management Studio, or Enterprise Manager
type in:
setspn -L MyDomain\MyUserName
now you should see the output which looks something like the following:
C:\Program Files\Support Tools>setspn -L MyDomain\MyUserName
Registered ServicePrincipleNames for CN=MyUserName Service Account, OU=Service Accounts,
DC=MyDomain,DC=com:
mssqlsvc/MyServer1.MyDomain.com:MyPort
mssqlsvc/MyServer2.MyDomain.com:MyPort
mssqlsvc/MyServer3.MyDomain.com:MyPort
mssqlsvc/MyServer4.MyDomain.com:Myport
From the results you should be able to see a list of servers who's SQL SPN has
been successfully registered to the DNS.
Note: not all your servers will be represented here, but what you are looking for
is the Server that you are getting the SSPI error on.
Do you see the Server that you are having
the SSPI Context error for?
If not… Just type in the following:
setspn -a mssqlsvc MyServer MyDomain\MyUserName
if this syntax does not work for you. try this:
setspn -A MSSQLSvc/MyServer.MyDomain.com:1433 MyAccount
once this is done check again to see if your Server is in the list
by running the following:
setspn -L MyDomain\MyUserName
now you should see your Server in there.
try going back to your Management Studio or Enterprise Manager and
connecting to the server.
Thats it. <p>


[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

[![Gist](https://img.shields.io/badge/Gist-MikesDataWork-<COLOR>.svg)](https://gist.github.com/mikesdatawork)
[![Twitter](https://img.shields.io/badge/Twitter-MikesDataWork-<COLOR>.svg)](https://twitter.com/mikesdatawork)
[![Wordpress](https://img.shields.io/badge/Wordpress-MikesDataWork-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

     
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Mikes Data Work](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_02.png "Mikes Data Work")

