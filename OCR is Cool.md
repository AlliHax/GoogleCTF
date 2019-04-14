# OCR is Cool

You are given an attachment that contains a screenshot of an email that is encrypted. The objective is giving us some hints that caesar might be involved. Let's see what we can find!

## 
First let's through the email and located what might look like the flag format.
Oh, check line 8, it looks promising!

```
VMY{vtxltkvbiaxkbltlnulmbmnmbhgvbiaxk}
```

That could definitely be it. Let's check a ceaserchipher decoder to see if we can find out what the flag is.

## Decoding the Cipher
There are many ways one can decode caesar cipher. Below I have demonstrated two ways to accomplish it. Probably the easiest way to decode it is using an online premade decoder. However, for more of a challenge you can create your own decoding tool.

### Using an Online Decoder
You can find and online caesar cipher encoder/decoder tool such as https://cryptii.com/pipes/caesar-cipher
You select the decode option and paste the cipher text into the textbox. Then, we can start modifying the rotation settings to determine the key to the cipher. 
Eventually, you will find that the key is 19 and the decoded flag is:

```
CTF{caesarcipherisasubstitutioncipher}
```


### Using Shell
I wanted to challenge myself to program my own caesar cipher decoder.
This took me a bit of tweaking before I could get it just right.

First I needed to get the input to decode from the user, then send it through a translate command that would give me all possible outcomes (up to 25 rotations).

```
read -p "Enter Cipher: " CC
for i in $(seq 25); do
	echo $i $CC | tr $(printf %${i}s | tr ' ' '.')\a-z a-za-z
 done
```
Which would produce the outcome

```
alli@kali:~/Documents/HackSource$ ./ceaserdecoder.sh 
Enter Cipher: VMY{vtxltkvbiaxkbltlnulmbmnmbhgvbiaxk}
1 VMY{wuymulwcjbylcmumovmncnoncihwcjbyl}
2 VMY{xvznvmxdkczmdnvnpwnodopodjixdkczm}
3 VMY{ywaownyeldaneowoqxopepqpekjyeldan}
4 VMY{zxbpxozfmebofpxprypqfqrqflkzfmebo}
5 VMY{aycqypagnfcpgqyqszqrgrsrgmlagnfcp}
6 VMY{bzdrzqbhogdqhrzrtarshstshnmbhogdq}
7 VMY{caesarcipherisasubstitutioncipher}
8 VMY{dbftbsdjqifsjtbtvctujuvujpodjqifs}
9 VMY{ecguctekrjgtkucuwduvkvwvkqpekrjgt}
10 VMY{fdhvduflskhulvdvxevwlwxwlrqflskhu}
11 VMY{geiwevgmtlivmwewyfwxmxyxmsrgmtliv}
12 VMY{hfjxfwhnumjwnxfxzgxynyzyntshnumjw}
13 VMY{igkygxiovnkxoygyahyzozazoutiovnkx}
14 VMY{jhlzhyjpwolypzhzbizapabapvujpwoly}
15 VMY{kimaizkqxpmzqaiacjabqbcbqwvkqxpmz}
16 VMY{ljnbjalryqnarbjbdkbcrcdcrxwlryqna}
17 VMY{mkockbmszrobsckcelcdsdedsyxmszrob}
18 VMY{nlpdlcntaspctdldfmdetefetzyntaspc}
19 VMY{omqemdoubtqduemegnefufgfuazoubtqd}
20 VMY{pnrfnepvcurevfnfhofgvghgvbapvcure}
21 VMY{qosgofqwdvsfwgogipghwhihwcbqwdvsf}
22 VMY{rpthpgrxewtgxhphjqhixijixdcrxewtg}
23 VMY{squiqhsyfxuhyiqikrijyjkjyedsyfxuh}
24 VMY{trvjritzgyvizjrjlsjkzklkzfetzgyvi}
25 VMY{uswksjuahzwjakskmtklalmlagfuahzwj}
```
From this output we can tell that line 7 is the correct flag, however, the program isn't perfect.
The biggest issue I had when making the decoder was getting both the upper case and lower case values to decode. To remedy this, I put the input through an initial filter that would make all values lowercase automatically before feeding it through the decoder.

```
CC=$(echo "$CC" | tr '[:upper:]' '[:lower:]')
```

The final, working decoder ended up looking as follows:
```
#!/bin/sh

# CC = Cipher to be Decoded
read -p "Enter Cipher: " CC
 CC=$(echo "$CC" | tr '[:upper:]' '[:lower:]')
for i in $(seq 25); do
	echo $i $CC | tr $(printf %${i}s | tr ' ' '.')\a-z a-za-z
done
```
When inputting the flag into googleCTF for validation, I did have to change the "ctf" back to "CTF". Other than that, it is a functioning caesar cipher decoder! 


