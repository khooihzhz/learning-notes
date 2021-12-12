# HACK @ 10 Write-ups
### TEAM : h4ppyd0g3
### CTF-TYPE: JEOPARDY
### DATE : 26/11/2021
<div style="page-break-after: always;"></div>

# Challenge Name : 101
Challenge : OSINT
Points : 20

**[Social Media Link](https://www.instagram.com/unitenproc/?hl=en)**

In this instragram page description, we saw a weird string 
**924<\`_LbKA+0=b>_?0dBFbbKJN**

By using ROT 47 from [cyberchef](https://gchq.github.io/CyberChef/), EZPZ indeed


Flag : **hack10{3zpZ_l3m0n_5qu33zy}**


<div style="page-break-after: always;"></div>

# Challenge Name : CheeseCake
Challenge: MISC
Points : (200?)

At first, we looked at what does the resipi means and got nothing. Then under the view tab, we saw hiddensheets !
Then, we downloaded the excel sheet and found a base64 code. 
![[Pasted image 20211127121556.png]]

By baking it for 64hrs with [cyberchef](https://gchq.github.io/CyberChef/), we got the flag

**Hack10{4h_lov3ly_ch33s3c4k3}**


<div style="page-break-after: always;"></div>

# Challenge Name : Garykessler
Challenge: Steg
Points: (150?)

We got an image ![[Pasted image 20211127121850.png]]

The hints says there's something hiding below it. 

```bash
binwalk --dd='.*' metabin.jpg
```
Ran binwalk on the file and we found something interesting

We got the flaggg
![[Pasted image 20211127122530.png]]

Reference : 
[ctfchecklist]([https://fareedfauzi.gitbook.io/ctf-checklist-for-beginner/steganography](https://fareedfauzi.gitbook.io/ctf-checklist-for-beginner/steganography "https://fareedfauzi.gitbook.io/ctf-checklist-for-beginner/steganography"))

<div style="page-break-after: always;"></div>

# Challenge Name : Double P
Challenge : MISC
Points : (100?)

We got a jpeg file and ran binwalk on it to extract the rar file out.
![[Pasted image 20211127123455.png]]

Then, we decipher this picutre.
![[Pasted image 20211127123526.png]]

![[Pasted image 20211127123543.png]]
This is pigpen cipher. 

After decipring, we used the password *avadakedavra* and obtain the flag inside.
![[Pasted image 20211127123622.png]]

<div style="page-break-after: always;"></div>

# Challenge Name : Broken Heart
Challenge : MISC
Points : 300

We got this picture
![[Pasted image 20211127121139.png]]

The hints mentioned, the part of love is hiding. So, we assume that there's something hidden under the picture. We ran stegseek and found a broken QR code.

![[Pasted image 20211127121014.png]]

![[Pasted image 20211127121233.png]]

Then, we use microsoft Paint to repair the broken QR code and love is restored !

![[Pasted image 20211127121317.png]]

<div style="page-break-after: always;"></div>

# Challenge Name : Penat
Challenges :  Steg
points : (150?)

Tools : [Sonic Visualiser](https://www.sonicvisualiser.org/)

We used Sonic Visualiser on the mp3 file we were given.

Then, we found something interesting under the spectogram.
![[Pasted image 20211127123141.png]]

<div style="page-break-after: always;"></div>

# Challenge Name : PowerEnough?
Challenge : MISC
Points : 150

```bash
─[✗]─[root@parrot]─[/home/parrot/hack@10/power]

└──╼ #python3 /opt/oletools/oletools/olevba.py ./powerflag.pptm

olevba 0.60.1.dev3 on Python 3.9.2 - http://decalage.info/python/oletools

======================================================

FILE: ./powerflag.pptm

```

It is a pptm file, so we ran [oletools](https://github.com/decalage2/oletools) to check the macros hidden in the powerpoint file. 

```bash


Sub RandJump()

ActivePresentation.SlideShowWindow.View.GotoSlide Int(Rnd * ActivePresentation.Slides.Count) + 1

End Sub

**
```

This is the macro in the pptm file, there's nothing special, It just jump to random pages in the slide.

Then, we proceed to run the slideshow and found an interesting picture.
![[Pasted image 20211127120227.png]]

Then, we remove the picture and the flag is hidden under the picture. 

![[Pasted image 20211127120318.png]]


<div style="page-break-after: always;"></div>

# Challenge Name : Triple-T
Challenge : Cryptography
Points : 50 
![[Pasted image 20211127120454.png]]
We got this familiar looking crytography

![[Pasted image 20211127120439.png]]
Luckily I studied the secret codes 

![[Pasted image 20211127120526.png]]
Attach the flag format, and we got the flag 
**Flag : hack10{TICKITYTACKITYTOE}**

<div style="page-break-after: always;"></div>

# Challenge Name : Neighbor
Challenge: Forensic
Points: 300

# Analyzing the PCAP with WIRESHARK

We saw alot of different protocols, but the protocols that we are interested in are *TCP*. 

We followed the TCP stream using wireshark and found something interesting.

![[Pasted image 20211127123909.png]]
TCP STREAM 2

This looks like a website that can let u draw on it, records mouse movement and it connects to the websocket.

![[Pasted image 20211127124100.png]]
Then under TCP STREAM 3, we found \[X,Y\] coordinates that indicates the mouse position.

# Filtering the packets

![[Pasted image 20211127124318.png]]
By using this, we are able to filter out all the other packets and only websocket packets are left.

![[Pasted image 20211127124607.png]]
Then we can export the packet dissections as plain text.

![[Pasted image 20211127124701.png]]
Example of exported text file

```bash

cat tset.txt | grep -A1 'Line-based text data(1 lines)' > extracted.txt

```

We can use grep to get the line after 'Line-based text data(1 lines)' for easier view as we only need the X,Y coordinate later. 

![[Pasted image 20211127125023.png]]
RESULTS

# Using Python to do the rest

```python 
import matplotlib.pyplot as plt

  

# READ FILE

f = open("extract.txt", "r")

lines = f.readlines()

  
  
  

# EXTRACT UNTIL X,Y is left

extractedline = []

for line in lines:

 if line == "Line-based text data (1 lines)\n" or line == "--\n":

 pass

 else:

 line = line.strip("\n")

 line = line.strip(" ")

 line = line.strip("[]\"")

 extractedline.append(line)

  

print(len(extractedline))

  

# PUT IN PLOT

for line in extractedline:

 print(line)

 plt.scatter(int(line.split(',')[0]), -int(line.split(',')[1]))

  

# SHOW GRAPH

plt.show()
```

I wrote a simple python script to plot the X,Y coordinates using matplotlib.

![[Pasted image 20211127125230.png]]
First Results, then i have to flip the picture for better read so I applied (-ve sign) on the Y axis
![[Pasted image 20211127125317.png]]
Flag Obtained