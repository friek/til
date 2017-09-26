# Fluctuating disk usage on XFS filesystems

On one of the database server servers I'm managing, disk usage would increase
a lot, seemingly at random times. Suddenly, disk usage for the ibdata1 file would
increase from 40G to 48G and drop back to 40G after 3 to 6 hours.

It turned out to be a feature called [XFS Dynamic Speculative EOF Preallocation](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=commitdiff;h=055388a3188f56676c21e92962fc366ac8b5cb72), which is also documented
in [this answer](https://serverfault.com/a/406070/67798) on serverfault.com.

A temporary solution for the increased disk space usage, is running the follow command:
```bash
sync && echo 3 > /proc/sys/vm/drop_caches
```
