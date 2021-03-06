A smart backup perl script that uses various system tools to compress given file types. File type support is user
extensible via perl hash %user_extensions in $HOME/.smart-backup which smart-backup reads. Wave and netpbm PPM files
are supported by default.
In the backup archive, all compressed files will be appended with the '.smrtbak' extension and a 'restore.sh' shell
script will be generated, enabling the archive contents to either be restored to their original location or another
location specified by $1.
Also supported is an experimental differential backup mode, enabled via the -d flag.

###Instructions:
The 'smart-backup' script should be packaged as executable, if not 'chmod +x' it and run it from the command line.
CLI args are as specified:

*For standard archive mode:*<br />
smart-backup \[source-path\] \[destination-path\]

*For 'experimental' diff archive mode:*<br />
smart-backup -d \[old-backup-path\] \[source-path\] \[destination-path\]

###Limitations/TODO:
-   The differential backup mode works for backing up files that have either been modified or are new in the source
directory, but not for new or newly modified files from the old backup directory. i.e, It does a uni-directional diff.
I'm not sure if it was meant to be bi-directional, but implementing it as bi-directional would require lots of changes,
including another double nested loop comparing files in the source and the old-backup directories, and it became far too
messy and irritating to implement at this late of a stage.
-   The differential backup mode doesn't take into account when a file is deleted in the source directory. Again,
implementing this meant putting in that additional double nested loop and changing too much of my current
implementation (which I'm at a point where I'm pretty happy with it).
