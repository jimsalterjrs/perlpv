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
jim@elden:~$ sudo ./perlpv /dev/nvme0n1 /dev/null
    Transferred 7.6GiB of 1.8TiB (at average rate 4.9GiB/sec), estimated completion in 00:06:21
^C
jim@elden:~$
````

The averate rate (and estimated completion) are derived by keeping separate running averages for transfer rates:
    * last five minutes
    * last minute
    * last ten seconds
    * most recently transferred block
These four queues are then averaged together to get the displayed average transfer rate, which is then used to estimate
time to completion.

