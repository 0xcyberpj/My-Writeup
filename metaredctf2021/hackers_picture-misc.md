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
 
