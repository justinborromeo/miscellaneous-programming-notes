# Linux Shell Commands
## File System
- ls: List directory contents
- cp sourcefile targetfile: Copy sourcefile and paste as targetfile
- mv sourcefile targetfile: Cut sourcefile and paste as targetfile
- rm file1 file2 ... : Delete files
- rm -r directory: Delete folder recursively
- mkdir directoryname: Create a directory
- chown username.group file: Change file ownership
- chgrp groupname file(s): Change group ownership
- chmod mode file(s): Mode is 3 numbers (1st number is for user, 2nd is for group, and 3rd is for others).  Each number is the decimal representation of the binary value [r][w][x] (read, write, execute).  For example, the permission that allows reading and executing (but not writing) would be 6 (decimal for 101)
- tar options archive file: archives directory or unarchives tarball (with -u flag)
- find [starting dir] -name "[regex pattern]": find file (. to start in current directory)
- mount, umount: mount and unmount any data media to Linux file system

## Files
- cat filename: print file
- less filename: print file (scrollable)
- grep regexstring filenames: finds a specific search string in the specified files
- diff file1 file2: shows difference between the two files

## System
- df: shows data usage on all mounted drives
- du path: shows size of all files and subdirectories in the specified directory
- free: shows RAM usage
- ps [option] [pid]: displays a table of processes started by user.  Use the option "aux" to show all processes
- kill pid: kill process w/ ID pid
- killall processname: kill process w/ name processname