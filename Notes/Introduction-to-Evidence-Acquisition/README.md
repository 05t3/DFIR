# Understanding Data Acquisition > Data Acquisition Concepts

The acquired forensic image will be the foundation of your analysis; any mistake may tamper with the evidence, rendering it inadmissible in court. You may have two or more chances on the analysis part, but the acquisition is a single-shot chance. Just by looking through the files or by booting up the computer, you may destroy or even lose your evidence. Therefore, following theright steps of evidence acquisition will guarantee sound evidence and will make you confident about the evidence between your hands.

In data acquisition you will deal with three types of data: 

- active -  information  that  you  can  actually  see.  The  active  data  includes  files data, programs, and operating system files. Acquiring such a data type is the easiest.
- archival -  Data, which is backed up and stored, this includes tapes, CDs, or an entire hard drive.
- latent data - data, such as deleted or partially overwritten data. The latent type of data  requires  special  tools  to  access  it.  


According to the case, you may deal with one or all  these types of data.

No  matter  the  type  of data,  you  should  always  keep  in  mind  that  digital  evidence  is  fragile  and volatile. Hence,  methodological  procedures should  be followed toensure  the  integrity  of the  data during the acquisition process, this includes:

- Understanding the order of volatility
- Understanding imaging methods
- knowing available forensic image files formats
- Be familiar with the capabilities of imaging tools
- Keep continuity in mind. 
- Understand and know how to use write-blockers●Understand and know how to validate acquired images.
- Last but most important documentation aka CoC.


## ORDER OF VOLATILITY

The evidence  acquisition  must  be based  on  the  volatility  of  the evidence  data, this  guarantees  no or   minimum   data   modification.   Therefore,   the order   of   volatility is   important   in   forensic investigation.  Knowing  which  evidence  drive  is  more  volatile,  determines  which  evidence  will  be captured first. The order is as follows:

|Cache and registers|
|-----|
|ARP cache, routing table, memory, kernel statistics, process table|
|Temporary files|
|Disks|
|Monitoring data and remote logging about the computer in question|
|Physical configurations, network topology|
|Archival media|


The first row of evidence types can only be captured in case the investigated machine was running. However, in  some  cases, a  part of the memory (PageFile)  may  be  found  on  the  hard  disk. Many applications store files as temporary, which holds valuable evidence for investigation. When  you  capture  digital  evidence,  the  evidence  is saved in a form of a forensic image. So what is a forensic image?

## COPY OR IMAGE

During a forensic investigation, we cannot perform tasks directly on the original evidence, since it will be considered contaminated. If I cannot work on the original evidence, should I copy or clone the drive or should I capture an image? What is the difference between these three concepts? First, copying a piece of evidence  provides the actual data of a particular file. Therefore, you just copy the data without any extra information, such as the file’s metadata. Due to the importance of metadata and other information on the drive, digital forensic investigators capture an image of the drive. Imaging an evidence drive allows capturing the entire drive bit-by-bit, including actual files, data in slack space, swap files, and unallocated space (which may contain deleted files). Often, the term  cloning  is  used  in  the  place of imaging, and both create a replica of your drive. If you clone the drive, all files will be copied along with the Master Boot Record (MBR) and all other files needed for booting. Cloning is creating a one-to-one copy of the drive, thus, if a drive fails, you can just replace it with a cloned drive.  This  means that you can  insert the drive into another machine and boot the machine from this drive.  However,  imaging  beats  cloning  in  performance,  since  drive imaging creates compressed replicas of your drive, it provides more flexibility. Frequently, forensic images  are  compressed  to  save  space  and  maybe  fragmented  into  several  files  that  make  it  more manageable. Uncompressing a compressed image or recombining a fragmented image will generate the  replica  of  the  source.  Besides,  a  cloned  disk  presents  problems  associated  with  guaranteeing the  forensic  integrity  of  the  evidence  on  the  destination  drive.  Except  if  it  is  mounted  read-only, hence, is not commonly used as an imaging technique. Another thing to keep in mind is `Contiguity`, which considers a backup plan in case your acquisition plan cannot be applied or an issue occurs during the acquisition. To ensure Contiguity, follow these guidelines:

1. Create  two  copies/images  from  the  evidence  drive,  hence,  in  case  one  got  corrupted,  the second one can be used for further analysis.
2. Use two different tools for image acquisition.

## CHAIN OF CUSTODY

The chain of custody is a series of documents that describes the evidence. It is used to keep track of  evidence  and  ensure  its  integrity  through  forensic  investigation.  The  contents  in  the  chain  of custody document will differ according to the law enforcement agency. However, some information is necessary, such as time and location of collection, details of collected evidence, and the reason it was collected. 

Some chain of custody documents may contain the information of several evidence items. In such a document, the quantity and description of the item may be added.

The  chain  of  custody  document  should  be  filled  accurately  with  information  about  who  is responsible  for  securing  the  digital  evidence  in  every  step  during  the  investigation.  Also,  photos can  be  attached  to  this  document  to  show  the  evidence  state  at  the  collection  time.  This  is  very important in case of acquiring a powered-on machine, which has running applications on its screen.

You can also include a photo of the disk label for example.

Examples of CoC:

![image](https://user-images.githubusercontent.com/58165365/154335084-601c1026-67c6-4125-b9d5-b7ee9cb22097.png)

![image](https://user-images.githubusercontent.com/58165365/154335139-a783c4ac-2760-452b-ad58-dcfa2f0def99.png)

![image](https://user-images.githubusercontent.com/58165365/154335267-f5265e47-c9f6-48bc-a787-250648751137.png)


## WRITE-BLOCKER

The write blocker is a hardware device or software application that enables read-only access to digital evidence. Write blocker ensures data integrity, since  it  ensures that no data is modified or added to the evidence drive. Windows mounts connected devices automatically, modifying files’ metadata, hence, it is essential to use a write-blocker. Both hardware and software blockers serve the same purpose.

|Write Blocker|How it works|Examples|
|-----|-----|-----|
|Software|Filter any input/output commands that are sent from an application through an access interface. The advantage of this kind of blocker is that you do not    have to carry any additional hardware. However, they are limited by the operating system updates and other similar variables|SAFE  Block  and  MacForensicsLab Write Controller|
|Hardware|They are easily carried portable devices, and work independently from operating systems|FastBloc, WiebeTech USB WriteBlocker and Tableau Forensic Bridges.|

Sample Hardware Write Blockers

![image](https://user-images.githubusercontent.com/58165365/154336659-3d2bf39d-c9f9-4fda-80a6-e256c141f031.png)

![image](https://user-images.githubusercontent.com/58165365/154336786-85e9d3fb-32af-4ff4-a87c-2c8a2801af25.png)


Essential features to search in hardware write blockers include:
1. Available Connection Types:  Does it support SATA, IDE, or both drive  types? Does  it  only support USB 3.0, or 2.0 as well?
2. Writing Capability: Does it allow you to switch between read-only and read/write modes?
3. Compatibility: you need to check if it is compatible with Advanced Drive Formats.


# VALIDATION OF DATA ACQUISITION


The integrity check or acquisition validation is used to ensure that the files have not been changed. This validation  process  is  very  important  not  just  for  digital  forensic.  For  example,  an  important configuration file for a bank system should never be altered, and the alteration of this file means it has  been  manipulated.  This  validation  can  also  be  used  to  validate  the  integrity  of  operating systems  binaries,  to  detect  if  a  malicious  version  of  the  binary  is  introduced  to  the  system.  This technique is commonly used by rootkit viruses.The validation of digital evidence involves using a hashing algorithm to generate a hash value(aka fingerprint),  which  is  a  unique  binary  or  hexadecimal  number.  This  unique  digital  fingerprint represents  a  dataset  such  as  a  file  or  a  disk  drive.  Identical  files  will  always  have  the  same fingerprint  even  if  their  names  differ.  Integrity  check  guarantees  that  the  data  has  not  been corrupted or altered during the acquisition process. Most acquisition tools, such as `FTK` and `Encase`, provide  an  option  to  calculate  the  hash  value  of  both  original  evidence  and  the  image  of  the evidence during the acquisition process. Besides, the `dd` command provides `MD5` and `SHA1` hashing options.


The data integrity should be verified using verification algorithms, such as `Message Digest 5 (MD5)` hash, `Secure  Hash  Algorithm  1  (SHA-1)`,  and `SHA-2`.  In  addition to `Cyclic  Redundancy  Checksum (CRC)`. Commonly, a checksum is the output value of a CRC check, and digest is the output value of a hash function.To use an algorithm for forensic hashes, it should satisfy the following rules:

1. The hash value of a device or file cannot be predicted.
2. Different files/devices generate different hash values.
3. Any change to the file or device must change the hash value.

To drive the point home, Let us download a tool that generates hash values and use it for our analysis. The tool we will use here is the [HashMyFiles](https://www.nirsoft.net/utils/hash_my_files.html#:~:text=HashMyFiles%20is%20small%20utility%20that,more%20files%20in%20your%20system.&text=HashMyFiles%20can%20also%20be%20launched,the%20selected%20file%20or%20folder.). 

The tool has a very simple and easy to use GUIas you can see

![image](https://user-images.githubusercontent.com/58165365/154339704-30d49b3c-1adc-44da-a71b-b07802de3d2a.png)

Notice  that HashMyFiles supports  several  hashing  algorithms, `MD5`, `SHA1`, `SHA-512`, `SHA-265`, and `SHA-384`, and the `CRC` validation. From the `File` menu, in  you can select a file(s),  folder,  process  file,  or  use  the `Add By Wildcard` option  to  add  more  than  one  file. Select any file to calculate its hash value. Here we will select the `suspect.txt` file and calculate its hash value.

![image](https://user-images.githubusercontent.com/58165365/154340717-b1cb1657-9efa-4186-9f99-c9336fa03814.png)

After selecting the file, the tool will generate its hash using several algorithms

Rename the file and calculate its hash again. This is just to show that renaming the file does not change its hash value

![image](https://user-images.githubusercontent.com/58165365/154341133-29624073-69ce-4f0a-a86f-09e66d9e5646.png)

If we now modify contents of the file, we should notice a change in the hash values

![image](https://user-images.githubusercontent.com/58165365/154341757-72a645bc-dae8-4d00-b2fb-76fc67a74634.png)

# ACQUISITION METHODS

//TO modify
