# OCR is Cool

You are given an attachment that contians a screenshot of an email that is partially encrypted. The objective is giving us some hints that ceaser might be involved. Let's see what we can find!

First let's through the email and located what might look like the flag format.
Oh, check line 8, it looks promising!

```
VMY{vtxltkvbiaxkbltlnulmbmnmbhgvbiaxk}
```

That could defintely be it. Let's check a ceaserchipher decoder to see if we can find out what the flag is.
There are many ways of cracking this code. 

### Using an Online Decoder
You can find and online ceasercipher encoder/decoder tool such as https://cryptii.com/pipes/caesar-cipher


### USing Python
A weapon of choice when trying to automate busy work!
