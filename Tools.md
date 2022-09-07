# Labs & VM's

- [Flare VM](https://www.fireeye.com/services/freeware/flare-vm.html)
- [REMnux](https://docs.remnux.org/install-distro/get-virtual-appliance)
- [Sentinel Labs](https://www.sentinelone.com/labs/building-a-custom-malware-analysis-lab-environment/)

# Checking IP/URL Reputation

- [AbuseIPDB](https://www.abuseipdb.com/)
- [urlscan.io](https://urlscan.io/)
- [URLhaus Database](https://urlhaus.abuse.ch/browse/)
- [Cyren IP Reputation Check](https://www.cyren.com/security-center/cyren-ip-reputation-check-gate)
- [Virus Total](https://www.virustotal.com/gui/home/search)
- [Talos IP and Domain Reputation Center](https://talosintelligence.com/reputation_center/)
- [Censys Search](https://search.censys.io/)
- [GreyNoise](https://viz.greynoise.io)
- [PhishTank](https://www.phishtank.com/)


# Tools

If you wish to build you lab from scratch, you can install the following tools.

- [HxD hex editor](https://mh-nexus.de/en/hxd/)
  - [Comparison_of_hex_editors](https://en.wikipedia.org/wiki/Comparison_of_hex_editors)
- [CFF Explorer](https://ntcore.com/?page_id=388)


# Registry Forensic Acquisition Tools

- [KAPE](https://www.kroll.com/en/insights/publications/cyber/kroll-artifact-parser-extractor-kape)

_KAPE (Kroll Artifact Parser And Extractor) is a live data acquisition and analysis tool which can be used to acquire registry data. It is primarily a command-line tool but also comes with a GUI._ 
- [Autopsy](https://www.autopsy.com/)

_Autopsy gives you the option to acquire data from both live systems or from a disk image. After adding your data source, navigate to the location of the files you want to extract, then right-click and select the Extract File(s) option._

- [FTK Image](https://www.exterro.com/ftk-imager)

_FTK Imager is similar to Autopsy and allows you to extract files from a disk image or a live system by mounting the said disk image or drive in FTK Imager. Another way you can extract Registry files from FTK Imager is through the Obtain Protected Files option. This option is only available for live systems_

- [SQLite viewer software](https://www.foxtonforensics.com/sqlite-database-examiner/)

_Free tool for inspecting the contents of SQLite databases._

  - Automatically load all SQLite databases from a folder or subfolders.
  - Images stored within a database are automatically extracted and displayed within the built-in image gallery.
  - Common file types stored within a database are automatically detected.
  - BLOBs can be examined using the built-in hex viewer or exported to a file for further analysis.

- [Windows File Analyzer](https://www.mitec.cz/wfa.html)

_This application decodes and analyzes some special files used by Windows OS. In these files is interesting information for forensic analysis.
Every analysis results can be printed in user-friendly form._

Here are described individual analyzers:

  - Windows XP Thumbnail Database Analyzer
    
    _This analyzer reads Thumbs.db file and displays its content with stored data include image preview._
  - ACDSee Thumbnail Database Analyzer
    
    _This analyzer reads ACDSee *.fpt file and displays its content with stored data include image preview._
  - Google Picasa Thumbnail Database Analyzer
   
   _This analyzer reads Picasa *.db file and displays its content with stored data include image preview._
  - FastStone Viewer Thumbnail Database Analyzer
    
    _This analyzer reads fsviewer.db file and displays its content with stored data include image preview._
  - HP Digital Imaging Thumbnail Database Analyzer
    
    _This analyzer reads *.db or *.dat file and displays its content with stored data include image preview._
  - Prefetch Analyzer
    
    _It reads files stored usually in Prefetch folder and diggs out stored informaton._
  - Shortcut Analyzer
    
    _This tool reads all shortcut files in specified folder and displays data stored in them._
  - Index.DAT Analyzer
    
    _This analyzer reads specified Index.Dat file and displays its content. Index.Dat files store usually data of Internet Explorer cookies, temporary files or history._
  - Recycle Bin Analyzer
    
    _This analyzer decodes and displays Info2 files that hold WinXP recycle bin content information or $I files holding Vista and above recycle bin information._ 

  Here you can download [WFA Guidance by Allan S. Hay](https://www.mitec.cz/Downloads/WFA%20Guidance.pdf)


# Tools for Exploring Windows Registry

- [AccessData's Registry Viewer](https://accessdata.com/product-download/registry-viewer-2-0-0)
- [Zimmerman's Registry Explorer](https://ericzimmerman.github.io/#!index.md)

_Eric Zimmerman has developed a handful of tools that are very useful for performing Digital Forensics and Incident Response. One of them is the Registry Explorer.  It can load multiple hives simultaneously and add data from transaction logs into the hive to make a more 'cleaner' hive with more up-to-date data. It also has a handy 'Bookmarks' option containing forensically important registry keys often sought by forensics investigators. Investigators can go straight to the interesting registry keys and values with the bookmarks menu item._ 

- [RegRipper](https://github.com/keydet89/RegRipper3.0)

_RegRipper is a utility that takes a registry hive as input and outputs a report that extracts data from some of the forensically important keys and values in that hive. The output report is in a text file and shows all the results in sequential order.RegRipper is available in both a CLI and GUI form_


# Browser Artifact Aquisition & Analysis Tools

- Browser History Capturer

_Browser History Capturer allows you to easily capture web browser history from a Windows computer. The tool can be run from a USB dongle or via a Remote Desktop connection to capture history from Chrome, Edge, Firefox and Internet Explorer web browsers._

  [Download Here](https://www.foxtonforensics.com/browser-history-capturer/)

- Browser History Viewer

_Browser History Viewer (BHV) is a forensic software tool for extracting and viewing internet history from the main desktop web browsers while Identify peaks in internet activity using the interactive timeline, find relevant data faster with filtering by keywords and date/time range & Browse the images a user has viewed online using the built-in image gallery._

  [Download Here](https://www.foxtonforensics.com/browser-history-viewer/)

- Browser History Examiner (_Trial Version_)

_Browser History Examiner (BHE) is a forensic software tool for capturing, analysing and reporting internet history from the main desktop web browsers._

  [Download Here](https://www.foxtonforensics.com/browser-history-examiner/)


# Eric Zimmerman's tools (Forensic tools)

- Use [Get-ZimmermanTools](https://f001.backblazeb2.com/file/EricZimmermanTools/Get-ZimmermanTools.zip) to download all programs at once and keep your tool set current
- DO NOT RUN ANYTHING FOUND HERE FROM 'C:\PROGRAM FILES' DIRECTORY (unless you run them as administrator)!
- DO NOT USE WINDOWS TO EXTRACT THINGS. Use 7-Zip or WinRAR as Windows will block the DLLs!

|Name|Purpose|
|-----|-----|
|AmcacheParser|Amcache.hve parser with lots of extra features. Handles locked files|
|AppCompatCacheParser|AppCompatCache aka ShimCache parser. Handles locked files|
|bstrings|Find them strings yo. Built in regex patterns. Handles locked files|
|EvtxECmd|Event log (evtx) parser with standardized CSV, XML, and json output! Custom maps, locked file support, and more!|
|EZViewer|Standalone, zero dependency viewer for .doc, .docx, .xls, .xlsx, .txt, .log, .rtf, .otd, .htm, .html, .mht, .csv, and .pdf. Any non-supported files are shown in a hex editor (with data interpreter!)|
|Hasher|Hash all the things|
|JLECmd|Jump List parser|
|JumpList Explorer|GUI based Jump List viewer |
|LECmd|Parse lnk files|
|MFTECmd|$MFT, $Boot, $J, $SDS, $I30, and $LogFile (coming soon) parser. Handles locked files|
|MFTExplorer|Graphical $MFT viewer|
|PECmd|Prefetch parser|
|RBCmd|Recycle Bin artifact (INFO2/$I) parser|
|RecentFileCacheParser|RecentFileCache parser|
|RECmd|Powerful command line Registry tool searching, multi-hive support, plugins, and more|
|Registry Explorer|Registry viewer with searching, multi-hive support, plugins, and more. Handles locked files|
|RLA|Replay transaction logs and update Registry hives so they are no longer dirty. Useful when tools do not know how to handle transaction logs|
|SDB Explorer|Shim database GUI|
|SBECmd|ShellBags Explorer, command line edition, for exporting shellbag data|
|ShellBags Explorer|GUI for browsing shellbags data. Handles locked files|
|SQLECmd|Find and process SQLite files according to your needs with maps!|
|SrumECmd|Process SRUDB.dat and (optionally) SOFTWARE hive for network, process, and energy info!|
|SumECmd|Process Microsoft User Access Logs found under 'C:\Windows\System32\LogFiles\SUM'|
|Timeline Explorer|View CSV and Excel files, filter, group, sort, etc. with ease|
|VSCMount|Mount all VSCs on a drive letter to a given mount point|
|WxTCmd|Windows 10 Timeline database parser|
|Get-ZimmermanTools|PowerShell script to auto discover and update everything above.|
|iisGeoLocate|Geolocate IP addresses found in IIS logs, extracts unique IPs, records bad data from logs|
|KAPE|Kroll Artifact Parser/Extractor: Flexible, high speed collection of files as well as processing of files. Many many features|
|TimeApp|A simple app that shows current time (local and UTC) and optionally, public IP address. Great for testing|
|XWFIM|X-Ways Forensics installation manager|


# Sysinternals

## File and Disk Utilities

_The tools can be found [here](https://docs.microsoft.com/en-us/sysinternals/downloads/file-and-disk-utilities)_

|Tool|Description|
|-----|-----|
|AccessChk|This tool shows you the accesses the user or group you specify has to files, Registry keys or Windows services.|
|AccessEnum|This simple yet powerful security tool shows you who has what access to directories, files and Registry keys on your systems. Use it to find holes in your permissions.|
|CacheSet|CacheSet is a program that allows you to control the Cache Manager's working set size using functions provided by NT. It's compatible with all versions of NT.|
|Contig|Wish you could quickly defragment your frequently used files? Use Contig to optimize individual files, or to create new files that are contiguous.|
|Disk2vhd|Disk2vhd simplifies the migration of physical systems into virtual machines (p2v).|
|DiskExt|Display volume disk-mappings.|
|DiskMon|This utility captures all hard disk activity or acts like a software disk activity light in your system tray.|
|DiskView|Graphical disk sector utility.|
|Disk Usage (DU)|View disk usage by directory.|
|EFSDump|View information for encrypted files.|
|FindLinks|FindLinks reports the file index and any hard links (alternate file paths on the same volume) that exist for the specified file.  A file's data remains allocated so long as at it has at least one file name referencing it.|
|Junction|Create Win2K NTFS symbolic links.|
|LDMDump|Dump the contents of the Logical Disk Manager"s on-disk database, which describes the partitioning of Windows 2000 Dynamic disks.|
|MoveFile|Schedule file rename and delete commands for the next reboot. This can be useful for cleaning stubborn or in-use malware files.|
|NTFSInfo|Use NTFSInfo to see detailed information about NTFS volumes, including the size and location of the Master File Table (MFT) and MFT-zone, as well as the sizes of the NTFS meta-data files.|
|PendMoves|See what files are scheduled for delete or rename the next time the system boots.|
|Process Monitor|Monitor file system, Registry, process, thread and DLL activity in real-time.|
|PsFile|See what files are opened remotely.|
|PsTools|The PsTools suite includes command-line utilities for listing the processes running on local or remote computers, running processes remotely, rebooting computers, dumping event logs, and more.|
|SDelete|Securely overwrite your sensitive files and cleanse your free space of previously deleted files using this DoD-compliant secure delete program.|
|ShareEnum|Scan file shares on your network and view their security settings to close security holes.|
|Sigcheck|Dump file version information and verify that images on your system are digitally signed.|
|Streams|Reveal NTFS alternate streams.|
|Sync|Flush cached data to disk.|
|VolumeID|Set Volume ID of FAT or NTFS drives.|


## Networking Utilities

_The tools can be found [here](https://docs.microsoft.com/en-us/sysinternals/downloads/networking-utilities)_

|Tool|Description|
|-----|-----|
|AD Explorer|Active Directory Explorer is an advanced Active Directory (AD) viewer and editor.|
|AD Insight|AD Insight is an LDAP (Light-weight Directory Access Protocol) real-time monitoring tool aimed at troubleshooting Active Directory client applications.|
|AdRestore|Undelete Server 2003 Active Directory objects.|
|PipeList|Displays the named pipes on your system, including the number of maximum instances and active instances for each pipe.|
|PsFile|See what files are opened remotely.|
|PsPing|Measures network performance.|
|PsTools|The PsTools suite includes command-line utilities for listing the processes running on local or remote computers, running processes remotely, rebooting computers, dumping event logs, and more.|
|ShareEnum|Scan file shares on your network and view their security settings to close security holes.
|TCPView|Active socket command-line viewer.|
|Whois|See who owns an Internet address.|
