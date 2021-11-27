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
![[Pasted image 20211127120227.png]]

Then, we remove the picture and the flag is hidden under the picture. 

![[Pasted image 20211127120318.png]]