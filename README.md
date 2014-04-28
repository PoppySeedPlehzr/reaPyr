 Nick Anderson 02/24/2014

 Digital Forensics, Spring 2014 - CS 6963 Final Project

```
               ______           
               | ___ \          
 _ __ ___  __ _| |_/ /   _ _ __ 
| '__/ _ \/ _` |  __/ | | | '__|
| | |  __/ (_| | |  | |_| | |   
|_|  \___|\__,_\_|   \__, |_|   
                      __/ |     
                     |___/  
```



###About
    
reaPyr utilizes the pytsk3 framework to carve off of a specified
disk image the credential hashes for Windows, Mozilla, Chrome, and
various other accounts.  The purpose of this software is to aid in
investigations in which one may not have access to account credentials.

The hope being that as many often use the same account credentials
for multiple accounts, if we can glean one set of credentials we
may be able to unlock other accounts as well using the same credential
sets.


###Usage

```bash
user@system:~$ reaPyr.py [-h] -f FILENAME -d DISKNAME [-o OFFSET] [-ss SECTSIZE]

File carving from disk images.

optional arguments:
  -h, --help            show this help message and exit
  -f FILENAME, --filename FILENAME
                        File name to be carved out of the disk image.
  -d DISKNAME, --diskname DISKNAME
                        Name of the disk image to reap.
  -o OFFSET, --offset OFFSET
                        Offset into disk where OS resides. Default is 0.
  -ss SECTSIZE, --sectsize SECTSIZE
                        Sector size of OS. Default is 512 bytes.
```

###Notes

* reaPyr needs all arguments to stand up the disk correctly

* Once the disk is ready, call each reaping function handing
the disk image as the only(?) argument


###Future Work

* Make a 'Disk' class out of the functionality in the fs_walk,
so that reaPyr's only job is to make the Disk object, and then
hand that off to each reaper.

* Add support for running on multiple OS

* Add reapers for multiple OS

###Author

Nick Anderson - nba237@nyu.edu