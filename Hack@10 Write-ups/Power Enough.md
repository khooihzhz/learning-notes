Challenge : MISC
Points : 150

## Power Enough 
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
![Pasted image 20211127120227.png](https://github.com/khooihzhz/learning-notes/blob/9e515d9b21549c90b12b9c21e8f00b293d9979eb/Hack@10%20Write-ups/Images/Pasted%20image%2020211127120227.png)

Then, we remove the picture and the flag is hidden under the picture. 

![Pasted image 20211127120318.png](https://github.com/khooihzhz/learning-notes/blob/9e515d9b21549c90b12b9c21e8f00b293d9979eb/Hack@10%20Write-ups/Images/Pasted%20image%2020211127120318.png)
