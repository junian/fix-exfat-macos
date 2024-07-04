# Fix ExFAT macOS

exFAT support on macOS seems to have some bugs because my external drives
with exFAT formatting will randomly get corrupted.

Disk Utility is unable to repair this at first, but the fix is this:

1. Use `diskutil list` to find the right drive id.
  1. You want the id under the IDENTIFIER column, it should look like `disk1s1`
2. Run `sudo fsck_exfat -d <id from above>`. eg `sudo fsck_exfat -d disk1s3`
  1. `-d` is debug so you'll see all your files output as they're processed.
3. Answer `YES` if it gives you the prompt `Main boot region needs to be updated. Yes/No?`
4. Open Disk Utility and you should be able to repair here successfully.

See the apple man page below for details on the `fsck_exfat` utility.

<!--
Sources/Extra Reading:
- https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man8/fsck_exfat.8.html
- https://craigsmith.id.au/2014/07/06/repairing-a-corrupted-mac-osx-exfat-partition/
- https://discussions.apple.com/thread/4154638?tstart=0
- https://gist.github.com/scottopell/595717f0f77ef670f75498bd01f8cab1
-->
