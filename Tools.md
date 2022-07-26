# Labs & VM's

- [Flare VM](https://www.fireeye.com/services/freeware/flare-vm.html)
- [REMnux](https://docs.remnux.org/install-distro/get-virtual-appliance)
- [Sentinel Labs](https://www.sentinelone.com/labs/building-a-custom-malware-analysis-lab-environment/)

# Checking IP Reputation

- [AbuseIPDB](https://www.abuseipdb.com/)
- [urlscan.io](https://urlscan.io/)
- [URLhaus Database](https://urlhaus.abuse.ch/browse/)
- [Cyren IP Reputation Check](https://www.cyren.com/security-center/cyren-ip-reputation-check-gate)
- [Virus Total](https://www.virustotal.com/gui/home/search)
- [Talos IP and Domain Reputation Center](https://talosintelligence.com/reputation_center/)

# Tools

If you wish to build you lab from scratch, you can install the following tools.

- [HxD hex editor](https://mh-nexus.de/en/hxd/)
  - [Comparison_of_hex_editors](https://en.wikipedia.org/wiki/Comparison_of_hex_editors)
- [CFF Explorer](https://ntcore.com/?page_id=388)


# Registry Forensic Tools

- [KAPE](https://www.kroll.com/en/insights/publications/cyber/kroll-artifact-parser-extractor-kape)

_KAPE (Kroll Artifact Parser And Extractor) is a live data acquisition and analysis tool which can be used to acquire registry data. It is primarily a command-line tool but also comes with a GUI._ 
- [Autopsy](https://www.autopsy.com/)

_Autopsy gives you the option to acquire data from both live systems or from a disk image. After adding your data source, navigate to the location of the files you want to extract, then right-click and select the Extract File(s) option._

- [FTK Image](https://www.exterro.com/ftk-imager)

_FTK Imager is similar to Autopsy and allows you to extract files from a disk image or a live system by mounting the said disk image or drive in FTK Imager. Another way you can extract Registry files from FTK Imager is through the Obtain Protected Files option. This option is only available for live systems_

# Tools to Exploring Windows Registry

- [AccessData's Registry Viewer](https://accessdata.com/product-download/registry-viewer-2-0-0)
- [Zimmerman's Registry Explorer](https://ericzimmerman.github.io/#!index.md)

_Eric Zimmerman has developed a handful of tools that are very useful for performing Digital Forensics and Incident Response. One of them is the Registry Explorer.  It can load multiple hives simultaneously and add data from transaction logs into the hive to make a more 'cleaner' hive with more up-to-date data. It also has a handy 'Bookmarks' option containing forensically important registry keys often sought by forensics investigators. Investigators can go straight to the interesting registry keys and values with the bookmarks menu item._ 

- [RegRipper](https://github.com/keydet89/RegRipper3.0)

_RegRipper is a utility that takes a registry hive as input and outputs a report that extracts data from some of the forensically important keys and values in that hive. The output report is in a text file and shows all the results in sequential order.RegRipper is available in both a CLI and GUI form_


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
