# FortID CTF 2025/ Crypto - Days of yore
Writeup for the Challenge `Days of yore` cryptography category in FortID CTF 2025 playing with THEM?!. Well, I won't call it a hard chall but still only 11 people could do it and I didn't see any writeups so I decided to write one (this is my first writeup ever).

***

 <img width="484" height="444" alt="image" src="https://github.com/user-attachments/assets/49a049d4-99cc-459f-b037-d23918bb0b9e" />

***
## Challenge
We were given a file `cyphertext.txt` which had lines with numbers from 1 to 1878 arranged in 54 lines randomly.

## Intuition 
The challenge clearly states that this is a classical cipher with no cryptography or advanced mathematics involved. Each line has different number of values. All the values are unique.
The idea here is that these might be the positions of the actual characters and the plaintext might be 1878 characters long. The 54 lines may be 54 different characters which have to be in the positions arrranged in the lin e corresponding to that number.

## Solution
I asked ChatGPT(the almighty assistant) to arrange all those 54 characters in the positions corresponding to the line number and return a meaningful sentence. And thanks to my superb prompt engineering skills after some tries I could get chatgpt to return the beginning of text as

```ruby
?n the early days of cryutograuhy messages were not urotected by...rs and it will likely contin?e as long as ueoule en?oy u???les?q
```

Now I knew I was on the right path.<br/>
I tried to get chatgpt to print the comlete plaintext and it did so, but there was a problem. Some characters occured just once and hence chatgpt could not decrypt the flag(those stupid chall authors, stripping away my joy).
<br/>

ChatGPT may act all smart, replying to puny questions with huge answers but it is dumb piece of code at the end of the day. So,
I asked Chatgpt to instead of trying to decrypt the ciphertext itself, assign all the characters some token number and give back the file to daddy!!<br/>

The file was here
<img width="1897" height="723" alt="image" src="https://github.com/user-attachments/assets/12c9af15-2a63-4f7d-a63e-c3ade073f69c" />

If this scares you then you are no different, it did scare me too. <br/>
Well I knew the beginning from above which seemed to be like

```
in the early days of cryptography messages were not protected by ...rs and it will likely continue as long as people enjoy puzzles
```
I could not figure out what that word after `by` is but now I had hints. Opened the file in a text editor(notepad, I just can't leave windows!! hate me if you want to), used the ages old find and replace.
<br/> I took each token from the start, put it in the find, and replaced it with what I thought it was. It did take me some time figuring out most of the plaintext manually but now I had what I was doing it for.<br/>
```
...   S o m e   t i m e s      t h e    a n s w e r    i s    r e v e a l e d      t h r o u g h    f r e q u e n c y    a n a l y s i s    a n d    s o m e   t i m e s    b y    l o o k i n g    f o r    a    r e p e a   t i n g    k e y .    T h e    p r o c e s s      t e a c h e s    b o   t h    p a   t i e n c e    a n d    c r e a   t i v i   t y . T08 T08 F o r    e x a m p l e    w i   t h i n      t h i s    v e r y    p a s s a g e      t h e r e    i s    a    h i d d e n    m a r k e r .    T h e    p h r a s e    F o r   t I T54 T46 T40 T19 u T37 T48 T42 v T41 T37 T42 T37 T T42 l T41 n T13 T37 F T19 r T37 T01 r T41 a k T52 n T10 T37 C l T42 s s T52 c T42 l T37 C T52 p h T41 r s T37 T13 T19 T19 T37 T01 T42 d T37 T40 o u T37 T29 e r T41 n T24   t T37 T01 T19 r n T37 T52 n T37 A n c T52 T41 n T13 T37 T43 T19 m T41 T17    d o e s    n o   t    l o o k    l i k e    a n    o r d i n a r y    s e n   t e n c e .    T40 e   t    i n    a    p u z z l e    s e   t   t i n g    i   t    m i g h   t ...
```
I still didn't have the flag and all this part chatGPT already decrypted for me but it did not understand the flag becouse most of the parts in the flag are unique characters.
The problem with chatGPT's output was that it was not giving me the flag in the form I have got it now. It was confusing me by replacing all the tokens, whuich had a frequency of one with `_`(stupid
machine, thinks it can confuse me). I tried so many different prompts but I had to do it manually at the end. Now, I had to use my leet skills and predict what could be the flag, which
 surprisingly wasn't very hard for someone like me who never created a flag before.

```
F o r   t I T54 T46 T40 T19 u T37 T48 T42 v T41 T37 T42 T37 T T42 l T41 n T13 T37 F T19 r T37 T01 r T41 a k T52 n T10 T37 C l T42 s s T52 c T42 l T37 C T52 p h T41 r s T37 T13 T19 T19 T37 T01 T42 d T37 T40 o u T37 T29 e r T41 n T24   t T37 T01 T19 r n T37 T52 n T37 A n c T52 T41 n T13 T37 T43 T19 m T41 T17
```
because of the flag format (FortID{}):
+ T54 - D
+ T46 - {
+ T17 - }

then there was this part ` C l T42 s s T52 c T42 l T37 C T52 p h T41 r s` which has to be classical ciphers and hence I found out T37 is `_`(in your face ChatGPT this is the actual token for underscore)
all these findings and more similar deductions eventually got me the flag:

```
FortID{Y0u_H4v3_4_T4l3n7_F0r_Br3ak1nG_Cl4ss1c4l_C1ph3rs_700_B4d_You_Wer3n't_B0rn_1n_Anc13n7_R0m3}
```
