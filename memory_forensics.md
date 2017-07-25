### Installation 
https://packages.debian.org/sid/metapackages/forensics-all

Meta-package with:
```bash
  aesfix, aeskeyfind, afflib-tools, bruteforce-salted-openssl, cewl,
  chaosreader, crack, crack-md5, dc3dd, dislocker, ed2k-hash,
  ewf-tools, exifprobe, ext3grep, ext4magic, extundelete, fcrackzip,
  forensics-colorize, galleta, gpart, grokevt, grr-server, guymager,
  hashdeep, hashrat, mac-robber, magicrescue, memdump, metacam,
  missidentify, myrescue, nasty, outguess, pasco, pff-tools,
  pipebench, plaso, pompem, recoverdm, recoverjpeg, reglookup,
  rekall-core, rephrase, rifiuti, rifiuti2, rkhunter, rsakeyfind,
  safecopy, scalpel, scrounge-ntfs, shed, sleuthkit, ssdeep, steghide,
  tableau-parm, undbx, unhide, unhide.rb, vinetto, volatility,
  volatility-tools, winregfs, wipe, yara
```

## Command ref

Don't look here, look here: https://github.com/volatilityfoundation/volatility/wiki/Command-Reference

### Converting from aff4

`$ rekal -f <image>.aff4 imagecopy -O <image>.raw`

### Getting profile

```bash
$ volatility -f <image>.raw imageinfo | tee "`date +%Y%M%d`-imageinfo.txt
Volatility Foundation Volatility Framework 2.6
INFO    : volatility.debug    : Determining profile based on KDBG search...
          Suggested Profile(s) : Win10x64_10586, Win10x64_14393, Win10x64, Win2016x64_14393
                     AS Layer1 : Win10AMD64PagedMemory (Kernel AS)
                     AS Layer2 : FileAddressSpace (/path/<image>.raw)
                      PAE type : No PAE
                           DTB : 0x1aa000L
             KUSER_SHARED_DATA : 0xfffff78000000000L
           Image date and time : 2017-07-24 22:15:03 UTC+0000
     Image local date and time : 2017-07-24 19:15:03 -0300
```

### List processes

```bash
$ volatility--profile=Win10x64_10586 pslist -f <image>.raw | tee "`date +%Y%m%d`-pslist.txt
Volatility Foundation Volatility Framework 2.6
Offset(V)          Name                    PID   PPID   Thds     Hnds   Sess  Wow64 Start                          Exit                          
------------------ -------------------- ------ ------ ------ -------- ------ ------ ------------------------------ ------------------------------
0xffffe001d36b4680 System                    4      0    227        0 ------      0 2017-07-14 14:36:34 UTC+0000                                 
0xffffe001d7671040 smss.exe                376      4      2        0 ------      0 2017-07-14 14:36:34 UTC+0000                                 
0xffffe001d75f27c0 csrss.exe               672    452     14        0      0      0 2017-07-14 14:36:40 UTC+0000                                 
```

### Scan processes
Via pool tag scanning (EPROCESS)

```bash
$ volatility --profile=Win10x64_10586 psscan -f <image>.raw | tee "`date +%Y%m%d`-psscan.txt"
```

### Comparing pslist with psscan
```bash
$ diff <(cat `date "+%Y%m%d"`-pslist.txt | cut -d" " -f2 | sort -n) <(cat `date "+%Y%m%d"`-psscan.txt | cut -d" " -f2 | sort -n)
```

### Display processes as tree

```bash
volatility --profile=Win10x64_10586 -f <image>.raw pstree | tee "`date +%Y%m%d`-pstree.txt"
```

### Finding hidden processes
```bash
$ volatility --profile=Win10x64_10586 psxview -f <image>.raw | tee "`date +%Y%m%d`-psxview.txt"
Offset(P)          Name                    PID pslist psscan thrdproc pspcid csrss session deskthrd ExitTime
------------------ -------------------- ------ ------ ------ -------- ------ ----- ------- -------- --------
0x000000010ee29600 svchost.exe            1152 True   True   True     True   True  True    False    
0x00000001bb678100 ffffff.exe             9344 True   True   True     True   True  True    False    
```

### Checking for code injection
```bash
$ volatility --profile=Win10x64_10586 -f <image>.raw malfind -p <proc_num> | tee "`date +%Y%m%d`-malfind-p<proc_num>.txt"
```

### Analyzing DLLs for process
```bash
$ volatility --profile=Win10x64_10586 -f <image>.raw dlllist -p <proc_num> | tee "`date +%Y%m%d`-ddlist-p<proc_num>.txt"
```

### Network connections
```bash
$ volatility --profile=Win10x64_10586 -f <image>.raw netscan | tee "`date +%Y%m%d`-netscan.txt"
```

### Getting modules

```bash
$ volatility --profile=Win10x64_10586 -f <image>.raw modules | tee "`date +%Y%m%d`-modules.txt"
```

### Dumping modules

```bash
$ volatility --profile=Win10x64_10586 -f <image>.raw moddump -D output/ | tee "`date +%Y%m%d`-moddump.txt"
```


