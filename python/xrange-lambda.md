# Creating a string with a range of numbers

Sometimes you need to enter a range of numbers separated by some separator. In my case I needed to create
a raid6 array via tw_cli. It takes a disk=<p:p:p..> argument for adding disks to an array. Instead of typing
the range, I figured it'd be possible with a lambda in python, so here it is.

```python
s = ":".join([str(x) for x in xrange(0,23)])
```

Output: 0:1:2:3:4:5:6:7:8:9:10:11:12:13:14:15:16:17:18:19:20:21:22

