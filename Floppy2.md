## Floppy 2

This is part 2 of the original Floppy challenge. This time, we want to investigate the suspicious www.com file.

One thing to note here is that the pervious challenge included a string in the file that contained the flag that read "

```
In case of emergency, run www.com
```

Now, the keyword in that string is the word 'run'. Which indicated to me that the file needed to be executed.
When running it the usual way in our terminal, we get this output:

```
file www.com
www.com: ASCII text, with CR, LF line terminators
```

Well, that's not very helpful. What happens when we read the file?

```
cat www.com
hD7X-t6ug_hl(]Wh8$^15GG1-hbrX5prPYGW^QFIuxYGFK,1-FGIuqZhHIX%A)I!hSLX4SI!{p*S:eTM'~_?o?V;m;CgAA]Ud)HO;{ The Foobanizer9000 is no longer on the OffHub DMZ.
```
Hmm, strange, let's do some research!
[Wikipedia](https://en.wikipedia.org/wiki/COM_file) informs us that .com is a DOS executable binary format. This means we need to find a way to run that file. After some researching, I found a write up on this CTF that suggested dosbox which I installed.

After some more research, I found out how to get to my active file directory using dosbox.

```
mount c .
```

followed by:

```
c:
```

Will get us in our active directory.Let's try running the file in here.

```
www.com
The Foobanizer9000 is no longer on the OffHub DMZ.
```

Shoot, we already got that. What else can we do? 
After yet more research, I stumbled upon a write up that explained that we needed to redirect the file into a .txt file.
Okay, let's give that a go (in dosbox).

```
www.com > www.txt
``` 

Now let's check it in our kali terminal.

```
cat WWW.TXT
The Foobanizer9000 is no longer on the OffHub DMZ.
```

Ugh! Not you again. Hmmm, well it was all special characters before. Let's check it with the -A argument to show all standard output.

```
cat -A WWW.TXT
CTF{g00do1dDOS-FTW}^M^M^M^M^NII4^?\^Mp5K^RW=^N^M)^VP[-`|0gvPY0onQ0geZ0wY5>D0g]h+(X-k&4`P[0/,64"P4APM-C^MThe Foobanizer9000 is no longer on the OffHub DMZ.
```

YES! That took a little research, but thanks to the internet, we have found our flag!

