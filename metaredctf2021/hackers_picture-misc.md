# Hello 
# CTF name : Metared
### Link : [click](https://ctf.csirt.cedia.org.ec/)
### Flag : FLAG{P1X3l_Valu3_d1ffERienc1nG.png}
# points : 100

----
  
 1. Given : a zip file 
 ---
 ```bash
 ┌──(root💀kali)-[/home/kali/ctf/metared/hackers_pic]
└─# file chall.zip
chall.zip: Zip archive data, at least v1.0 to extract
                                                                                               
┌──(root💀kali)-[/home/kali/ctf/metared/hackers_pic]
└─# unzip chall.zip 
Archive:  chall.zip
 extracting: flag.png                
                                                                                               
┌──(root💀kali)-[/home/kali/ctf/metared/hackers_pic]
└─# file flag.png     
flag.png: PNG image data, 304 x 304, 8-bit grayscale, non-interlaced

```

basic!
  from exiftool : `Author  : Mr.Heker. Hint: PVD`
 
 **What  is PVD?**
 When searching for some idea about these kinda stuffs i got the nice writeup and script
 ![image](https://user-images.githubusercontent.com/72292872/140547346-68a0e1d6-d90d-4f16-8766-1f68233673cd.png)
 
 ----
 
[Great explanation-tjctf2019](https://github.com/zst-ctf/tjctf-2019-writeups/tree/master/Writeups/Planning_Virtual_Distruction)

**after small modification**
### FLAG !!!
```python
┌──(root💀kali)-[/home/kali/ctf/metared/hackers_pic]
└─# python3 exploit.py|strings | grep FLAG                                               130 ⨯
This is our world now... the world of the electron and the switch, the beauty of the baud. We make use of a service already existing without paying for what could be dirt-cheap if it wasn't run by profiteering gluttons, and you call us criminals. We explore... and you call us criminals. We seek after knowledge... and you call us criminals. We exist without skin color, without nationality, without religious bias... and you call us criminals. FLAG{P1X3l_Valu3_d1ffERienc1nG.png}You build atomic bombs, you wage wars, you murder, cheat, and lie to us and try to make us believe it's for our own good, yet we're the criminals. Yes, I am a criminal. My crime is that of curiosity. My crime is that of judging people by what they say and think, not what they look like. My crime is that of outsmarting you, something that you will never forgive me for. I am a hacker, and this is my manifesto. You may stop this individual, but you can't stop us all... after all, we're all alike.

```
![image](https://user-images.githubusercontent.com/72292872/140547740-7dfbc719-c8fb-4aa6-89b6-cebf654fe24b.png)

**Thats all ,flag : FLAG{P1X3l_Valu3_d1ffERienc1nG.png}**
**Nice!**



 
