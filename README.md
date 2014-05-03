![alt tag](https://github.com/PoppySeedPlehzr/reaPyr/raw/master/imgs/reaper.jpg)
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

Digital Forensics, Spring 2014 - CS 6963 Final Project

###About

reaPyr is designed to carve credential sets from Windows XP, however
the foundation is currently in place to attempt to harvest credentials
from Windows Vista+, however this functionality has not been thoroughly
tested and as such may be quite buggy.

reaPyr utilizes the [pytsk3 framework](https://code.google.com/p/pytsk/wiki/pytsk3) to carve off of a specified
disk image the credential hashes and encrypted credential databases
for Windows, Mozilla, Google, and various other programs that allow
you the option of caching credentials. The purpose of this software is 
to aid in forensic investigations in which one may not have access to
specific account credentials. The hope being that as many users often 
utilize the same account credentials for multiple accounts, if we can 
glean one set of credentials we may be able to unlock other accounts 
as well using the same credential sets.

Currently reaPyr simply carves out encrypted databases and looks for
cleartext credential sets. Any data recovered by reaPyr is designed
to be handed off to other 3rd party applications designed for cracking
or getting around software encryption for stored databases.

###Implementation Notes

* Each reaper should be stored in it's own respective directory, for
example the win_rpr.py file lives in the './windows' directory, where
a __init__.py folder lives.  This allows for reaper isolation.

* Each reaper should write, if any, files out to the './disk_rec'
folder, and make use of the clean() function in the main reaPyr script.
After each reaper is run, the clean() function is called, which moves
all carved files in disk_rec to ./harvest/'reaper_name'.  There is
no logic behind this, it was simply a design decision, and I welcome
better formats for who should call 'clean'

* If you'd like to change the recovery directory, change the rec_dir
value in the disk.py class.  Most of the reaper code relies on this
class variable to carve files, write out data, etc...

* Each reaper file, i.e. win_rpr.py, is designed to be run in the same
directory as reaPyr.py.  Many of the file locations are relative, and
based around the reaPyr.py root directory.  As such, if you implement
additional reapers, take note of this fact.

###Installation
To install reaPyr you must have the following python packages installed

* Python 2.7
* pytsk3 - I recommend installing [The Sleuth Kit Frameork 4.1.2](http://sourceforge.net/projects/sleuthkit/files/sleuthkit/4.1.2/) as pytsk3 in TSK 4.1.3 is still quite buggy

###Usage

A Makefile has been included for ease of operation, however it relies on a
test disk image named 'winxp_sample.dd' existing in a directory titled 'test_images'
in order to run.  In the event you have the image provided, contact me if you'd like
the sample image, you can simply type `make` and reaPyr will run.  To wipe all existing
data and run clean type `make clean && make`

```bash
user@system:~$ reaPyr.py [-h] -d DISKNAME [-o OFFSET] [-ss SECTSIZE]

This program carves, or reaps, user credentials from a specified disk image.

optional arguments:
  -h, --help            show this help message and exit
  -d DISKNAME, --diskname DISKNAME
                        Name of the disk image to reap.
  -o OFFSET, --offset OFFSET
                        Offset into disk where OS resides. Default is 0.
  -ss SECTSIZE, --sectsize SECTSIZE
                        Sector size of OS. Default is 512 bytes.
```

###Future Work
* Add support for running on multiple OS
* Add reapers for multiple OS

###Author

Nick Anderson - nba237@nyu.edu

###Citations

* Thanks to someone awesome for the baller image of an SC2 Reaper.  Link [here](http://static.giantbomb.com/uploads/original/15/155745/2263839-terran_reaper__starcraft_ii_by_oxoxoxo.jpg)

* [creddump](https://code.google.com/p/creddump/)

* [pytsk3](https://code.google.com/p/pytsk/wiki/pytsk3)


