## Hello World
### [challenge link](https://github.com/0xcyberpj/My-Writeup/blob/main/csawctf2021/files/scan.pdf)
**when you start with basics things like strings , binwalk, psdfid, pdf... stuffs**
**Wont gonna help here**
-----

## deep look into pdf file 

```bash
┌──(kali㉿kali)-[~/ctf/csaw2021/foren/MIC]
└─$ file scan.pdf        
scan.pdf: PDF document, version 1.3
```

![image](https://user-images.githubusercontent.com/72292872/134703416-ed52cb9d-c817-4636-ae3b-42c0dc738bb1.png)
**when you zoom in deeper**
- what is the yellow dots refers to ? 
- google is google
![image](https://user-images.githubusercontent.com/72292872/134704157-4bcc5050-f063-4100-8446-f2940dc18698.png)

[read_it](https://en.wikipedia.org/wiki/Machine_Identification_Code)

----
 

![image](https://user-images.githubusercontent.com/72292872/134705421-8c2bc6b1-e99c-47b4-8796-e44777044eb8.png)

**oh yeah seems similar challenge lets go further**

also [deda to extract dots](https://github.com/dfd-tud/deda/blob/master/README.md)

to convert pdf pages into png 

> Pdftoppm is a library that handles the conversion from Portable Document Format (PDF) files to color image Portable Pixmap format (PPM) files, gray scale image Portable Graymap files (PGM) files, and monochrome image Portable Bitmap format (PBM) files.


```bash
git clone https://github.com/dfd-tud/deda
pushd deda && pip3 install --user deda && popd
sudo apt install poppler-utils
```


1. convert pdf pages into png


 ```bash
 ┌──(kali㉿kali)-[~/ctf/csaw2021/foren/MIC]
└─$ pdftoppm scan.pdf -png pj
                                                                                         
┌──(kali㉿kali)-[~/ctf/csaw2021/foren/MIC]
└─$ ls
pj-01.png  pj-06.png  pj-11.png  pj-16.png  pj-21.png  pj-26.png  pj-31.png
pj-02.png  pj-07.png  pj-12.png  pj-17.png  pj-22.png  pj-27.png  pj-32.png
pj-03.png  pj-08.png  pj-13.png  pj-18.png  pj-23.png  pj-28.png  pj-33.png
pj-04.png  pj-09.png  pj-14.png  pj-19.png  pj-24.png  pj-29.png  pj-34.png
pj-05.png  pj-10.png  pj-15.png  pj-20.png  pj-25.png  pj-30.png  scan.pdf
```




"`pdftoppm scan.pdf -png scan.pdf`"


scan.pdf is the challenge file and -png is the output file formate , pj is  the prefix of output png files

- next we have to extarct those dot pattern into using deda
- > Document Colour Tracking Dots, or yellow dots, are small systematic dots which encode information about the printer and/or the printout itself. This process is integrated in almost every commercial colour laser printer. This means that almost every printout contains coded information about the source device, such as the serial number

```python
Installation

    Install Python 3
    Install Deda
 $ pip3 install --user deda

   Optional requirement by deda_anonmask_apply $ pip3 install --user wand   
    
```

- 2.Extract Yellow Dots From Printed Pages

>  Reading tracking data

Tracking data can be read and sometimes be decoded from a scanned image. For good results the input shall use a lossless compression (e.g. png) and 300 dpi. Make sure to set a neutral contrast $ deda_parse_print INPUTFILE


Lets start 
- first output of the png
 ```bash
┌──(kali㉿kali)-[~/ctf/csaw2021/foren/MIC]
└─$ deda_parse_print pj-01.png 
Detected pattern 4


_|0|1|2|3|4|5|6|7
0|                
1|.               
2|.               
3|.               
4|              . 
5|            .   
6|.               
7|.               
8|.         . .   
9|        .   . . 
0|.       .     . 
1|        .       
2|.           . . 
3|.               
4|.               
5|  . . .     . . 
        27 dots.



<TDM of Pattern 4 at 0.00 x 0.00 inches>
Decoded:
        manufacturer: Epson
        serial: -000102-
        timestamp: 2006-11-09 08:00:00
        raw: 0000000102000006110908030000
        minutes: 00
        hour: 08
        day: 09
        month: 11
        year: 06
        unknown1: 00
        unknown3: 00
        unknown4: 00
        unknown5: 00
        printer: 00000102
```
**3.Here you can notice the serial number which is end with 102 : chr(102)= f**
so the flag formate is flag{}
**now you can get idea**
**lets do it for all png's**

```bash
┌──(kali㉿kali)-[~/ctf/csaw2021/foren/MIC]
└─$ for x in {01..34}; do echo -n $(python3 -c "print(chr($(deda_parse_print pj-$x.png | grep serial | cut -d '-' -f2 | sed 's/^0*//')))"); done

flag{watchoutforthepoisonedcoffee}     
``` 
**also**

```bash
┌──(kali㉿kali)-[~/ctf/csaw2021/foren/MIC
└─$ ls |while read line ; do deda_parse_print $line|grep "serial"|cut -d ":" -f2|cut -d "-" -f2|sed 's/000//g';done 
```
102
108
097
103
123
119
097
116
099
104
111
117
116
102
111
114
116
104
101
112
111
105
115
111
110
101
100
099
111
102
102
101
101
125

then copy the ascii code and decode to get the flag
### flag{watchoutforthepoisonedcoffee}

Thank you 
