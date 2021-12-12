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