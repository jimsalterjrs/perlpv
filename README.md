# perlpv
A proof-of-concept pipe viewer similar to Andrew Wood's pv in perl, for eventual use internally in syncoid.

You might be surprised just how finicky it is both getting extremely performant file reads and positioning the cursor
for dynamic display updates in Perl. I wouldn't, because... well, because I've learned otherwise. With any luck,
this working proof of concept will save you the hours of headaches I went through getting it working!

To use the program as-is, the syntax is simple:

````
you@box:~$ /path/to/perlpv sourcefile targetfile
````
and you'll get a dynamic, interactive display that updates itself once per second while the transfer progresses, like so:

````
jim@elden:~/git/perlpv$ ./perlpv ../sourcefile /dev/null
    Transferred 2.0GiB (at average rate 3.3GiB/sec)
jim@elden:~/git/perlpv$ 
````
