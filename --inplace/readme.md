# Guide:
https://superuser.com/questions/576035/does-rsync-inplace-write-to-the-entire-file-or-just-to-the-parts-that-need-to

>TL;DR - You need option --inplace and if copying between local filesystems you also need --no-whole-file.
>
>If you pass rsync two local paths, it will default to using "--whole-file", and not delta-transfer. Rsync assumes that it can write a completely new file and unlink the old one faster than reading both and calculating the changed blocks. If it doesn't calculate the changes, there won't be block-level changes for btrfs to observe. So, what you're looking for is --no-whole-file, in addition to --inplace. You also get delta-transfer if you requested '-c'.

