## Objetivo
Matryoshka dolls are a set of wooden dolls of decreasing size placed one inside another. What's the final one? Image: [this](https://mercury.picoctf.net/static/5ef2e9103d55972d975437f68175b9ab/dolls.jpg)
## Solución
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/matryoshkaDoll]
└─$ file dolls.jpg   
dolls.jpg: PNG image data, 594 x 1104, 8-bit/color RGBA, non-interlaced

┌──(armando㉿kali)-[~/picoCTF/forensic/matryoshkaDoll]
└─$ exiftool dolls.jpg 
ExifTool Version Number         : 12.76
File Name                       : dolls.jpg
Directory                       : .
File Size                       : 652 kB
File Modification Date/Time     : 2021:03:15 18:23:04-06:00
File Access Date/Time           : 2024:10:09 10:17:11-06:00
File Inode Change Date/Time     : 2024:10:09 10:16:14-06:00
File Permissions                : -rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 594
Image Height                    : 1104
Bit Depth                       : 8
Color Type                      : RGB with Alpha
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Profile Name                    : ICC Profile
Profile CMM Type                : Apple Computer Inc.
Profile Version                 : 2.1.0
Profile Class                   : Display Device Profile
Color Space Data                : RGB
Profile Connection Space        : XYZ
Profile Date Time               : 2020:06:09 12:08:45
Profile File Signature          : acsp
Primary Platform                : Apple Computer Inc.
CMM Flags                       : Not Embedded, Independent
Device Manufacturer             : Apple Computer Inc.
Device Model                    : 
Device Attributes               : Reflective, Glossy, Positive, Color
Rendering Intent                : Perceptual
Connection Space Illuminant     : 0.9642 1 0.82491
Profile Creator                 : Apple Computer Inc.
Profile ID                      : 0
Profile Description             : Display
Profile Description ML (hr-HR)  : LCD u boji
Profile Description ML (ko-KR)  : 컬러 LCD
Profile Description ML (nb-NO)  : Farge-LCD
Profile Description ML (hu-HU)  : Színes LCD
Profile Description ML (cs-CZ)  : Barevný LCD
Profile Description ML (da-DK)  : LCD-farveskærm
Profile Description ML (nl-NL)  : Kleuren-LCD
Profile Description ML (fi-FI)  : Väri-LCD
Profile Description ML (it-IT)  : LCD colori
Profile Description ML (es-ES)  : LCD color
Profile Description ML (ro-RO)  : LCD color
Profile Description ML (fr-CA)  : ACL couleur
Profile Description ML (uk-UA)  : Кольоровий LCD
Profile Description ML (he-IL)  : LCD צבעוני
Profile Description ML (zh-TW)  : 彩色LCD
Profile Description ML (vi-VN)  : LCD Màu
Profile Description ML (sk-SK)  : Farebný LCD
Profile Description ML (zh-CN)  : 彩色LCD
Profile Description ML (ru-RU)  : Цветной ЖК-дисплей
Profile Description ML (en-GB)  : Colour LCD
Profile Description ML (fr-FR)  : LCD couleur
Profile Description ML (hi-IN)  : रगन LCD
Profile Description ML (th-TH)  : LCD ส
Profile Description ML (ca-ES)  : LCD en color
Profile Description ML (en-AU)  : Colour LCD
Profile Description ML (es-XL)  : LCD color
Profile Description ML (de-DE)  : Farb-LCD
Profile Description ML          : Color LCD
Profile Description ML (pt-BR)  : LCD Colorido
Profile Description ML (pl-PL)  : Kolor LCD
Profile Description ML (el-GR)  : Έγχρωμη οθόνη LCD
Profile Description ML (sv-SE)  : Färg-LCD
Profile Description ML (tr-TR)  : Renkli LCD
Profile Description ML (pt-PT)  : LCD a Cores
Profile Description ML (ja-JP)  : カラーLCD
Profile Copyright               : Copyright Apple Inc., 2020
Media White Point               : 0.94955 1 1.08902
Red Matrix Column               : 0.51099 0.23955 -0.00104
Green Matrix Column             : 0.29517 0.69981 0.04224
Blue Matrix Column              : 0.15805 0.06064 0.78369
Red Tone Reproduction Curve     : (Binary data 2060 bytes, use -b option to extract)
Video Card Gamma                : (Binary data 48 bytes, use -b option to extract)
Native Display Info             : (Binary data 62 bytes, use -b option to extract)
Chromatic Adaptation            : 1.04861 0.02332 -0.05034 0.03018 0.99002 -0.01714 -0.00922 0.01503 0.75172
Make And Model                  : (Binary data 40 bytes, use -b option to extract)
Blue Tone Reproduction Curve    : (Binary data 2060 bytes, use -b option to extract)
Green Tone Reproduction Curve   : (Binary data 2060 bytes, use -b option to extract)
Exif Byte Order                 : Big-endian (Motorola, MM)
X Resolution                    : 144
Y Resolution                    : 144
Resolution Unit                 : inches
User Comment                    : Screenshot
Exif Image Width                : 594
Exif Image Height               : 1104
Pixels Per Unit X               : 5669
Pixels Per Unit Y               : 5669
Pixel Units                     : meters
XMP Toolkit                     : XMP Core 5.4.0
Apple Data Offsets              : (Binary data 28 bytes, use -b option to extract)
Warning                         : [minor] Trailer data after PNG IEND chunk
Image Size                      : 594x1104
Megapixels                      : 0.656

┌──(armando㉿kali)-[~/picoCTF/forensic/matryoshkaDoll]
└─$ sudo apt install binwalk  

...

┌──(armando㉿kali)-[~/picoCTF/forensic/matryoshkaDoll]
└─$ binwalk dolls.jpg                     

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 594 x 1104, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
272492        0x4286C         Zip archive data, at least v2.0 to extract, compressed size: 378954, uncompressed size: 383940, name: base_images/2_c.jpg
651612        0x9F15C         End of Zip archive, footer length: 22


┌──(armando㉿kali)-[~/picoCTF/forensic/matryoshkaDoll]
└─$ unzip dolls.jpg 
Archive:  dolls.jpg
warning [dolls.jpg]:  272492 extra bytes at beginning or within zipfile
  (attempting to process anyway)
  inflating: base_images/2_c.jpg     

┌──(armando㉿kali)-[~/picoCTF/forensic/matryoshkaDoll]
└─$ ls
base_images  dolls.jpg
    
┌──(armando㉿kali)-[~/picoCTF/forensic/matryoshkaDoll]
└─$ cd base_images   

┌──(armando㉿kali)-[~/picoCTF/forensic/matryoshkaDoll/base_images]
└─$ ls
2_c.jpg

┌──(armando㉿kali)-[~/picoCTF/forensic/matryoshkaDoll/base_images]
└─$ unzip 2_c.jpg  
Archive:  2_c.jpg
warning [2_c.jpg]:  187707 extra bytes at beginning or within zipfile
  (attempting to process anyway)
  inflating: base_images/3_c.jpg     

┌──(armando㉿kali)-[~/picoCTF/forensic/matryoshkaDoll/base_images]
└─$ cd base_images    

┌──(armando㉿kali)-[~/…/forensic/matryoshkaDoll/base_images/base_images]
└─$ ls
3_c.jpg

┌──(armando㉿kali)-[~/…/forensic/matryoshkaDoll/base_images/base_images]
└─$ eog 3_c.jpg       

┌──(armando㉿kali)-[~/…/forensic/matryoshkaDoll/base_images/base_images]
└─$ unzip 3_c.jpg 
Archive:  3_c.jpg
warning [3_c.jpg]:  123606 extra bytes at beginning or within zipfile
  (attempting to process anyway)
  inflating: base_images/4_c.jpg     

┌──(armando㉿kali)-[~/…/forensic/matryoshkaDoll/base_images/base_images]
└─$ cd base_images 

┌──(armando㉿kali)-[~/…/matryoshkaDoll/base_images/base_images/base_images]
└─$ eog 4_c.jpg 

┌──(armando㉿kali)-[~/…/matryoshkaDoll/base_images/base_images/base_images]
└─$ unzip 4_c.jpg 
Archive:  4_c.jpg
warning [4_c.jpg]:  79578 extra bytes at beginning or within zipfile
  (attempting to process anyway)
  inflating: flag.txt                

┌──(armando㉿kali)-[~/…/matryoshkaDoll/base_images/base_images/base_images]
└─$ ls            
4_c.jpg  flag.txt

┌──(armando㉿kali)-[~/…/matryoshkaDoll/base_images/base_images/base_images]
└─$ cat flag.txt  
picoCTF{e3f378fe6c1ea7f6bc5ac2c3d6801c1f}                                                                                                                
┌──(armando㉿kali)-[~/…/matryoshkaDoll/base_images/base_images/base_images]
└─$
```

## Notas Adicionales
## Referencias