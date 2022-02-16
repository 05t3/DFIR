# Investigating Windows Recycle Bin

# INTRODUCTION

Windows  Recycle  Bin  is  a  location  on  a  Windows  computer  that  temporarily  stores  deleted  files. The Recycle Bin utility is reinforced with a lot of precautionary data that make files easier to recover in  the  case  that  a  user  tries  to  retrieve  a  file  that  was  deleted.  This  artifact  is  important  to understand  and  utilize  because  it  stores  a  lot  of  information  that  can  be  pertinent  to  an investigation. The Recycle Bin is stored at `C:\$Recycle.Bin\` on Windows Vista/7/8/10 systems, and `C:\RECYCLER` on Windows XP systems. 


When  files  are  deleted  on  Windows  Vista/7/8/10,  through  the  means  of  clicking  on  a  file and pressing  the Deletekey  or  right-clicking  and  selecting Delete , the  file's information gets separated into two separate files inside the Recycle Bin directory.

Windows  Vista/7/8/10  implements  separate  directories  inside  the `C:\$Recycle.Bin` directory  for each  user on  the system,  notated by  that  user's **Security Identifier  (SID)**. These directories will be hidden  by  default.  For  example,  there  may  be  three  users  on  the  system,  so  each  will  have  their own  Recycle  Bin  directory  inside `C:\$Recycle.Bin`,  which  can  be  demonstrated  by  issuing `dir  /ah`

The following software's may be necessary for this investigation.

- FTK Imager by (Access Data)
- RBCmd by (Eric Zimmerman)
- 010 Editor by (Sweetscape)
- HxD Editor by (NH-NEXUS)
- Rifiuiti2 by (Rifiuiti)


