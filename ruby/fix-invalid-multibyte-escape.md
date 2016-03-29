# Fix invalid multibyte escape.

While migrating a legacy system, I found some ruby scripts not to be working anymore.
One of the scripts died with message:

<pre>invalid multibyte escape: /[\177-\377]/</pre>

The original line:

```ruby
(word =~ /[\177-\377]/) != nil
```

At the time the script was written, ruby accepted this perfectly. With some ruby version
this changed. The fix is easy. Add this line as the first line in the ruby file (unless you have a #! statement as the first line):

<pre># encoding: US-ASCII</pre>

