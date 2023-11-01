# Book By Its Cover
## Tags: Warmups
**Author: @JohnHammond**
**50 points easy**

They say you aren't supposed to judge a book by its cover, but this is one of my favorites!

Download the attached file *book.rar*

I tried to unzip by using tar but it giving me an error
```console
$ unzip book.rar
Archive:  book.rar
  End-of-central-directory signature not found.  Either this file is not
  a zipfile, or it constitutes one disk of a multi-part archive.  In the
  latter case the central directory and zipfile comment will be found on
  the last disk(s) of this archive.
unzip:  cannot find zipfile directory in one of book.rar or
        book.rar.zip, and cannot find book.rar.ZIP, period.
```
It says in the error that the file might not be zip file, so i check the book.rar with file command.
```console
$ file book.rar 
book.rar: PNG image data, 800 x 200, 8-bit/color RGB, non-interlaced
```
It confirms that the file is not a rar file, but an PNG file.

I tried to open book.rar with xdg-open, but it gives me nothing. So I rename the file to book.png, then open it. The flag has found!
```console
$ mv book.rar book.png
$ xdg-open book.png 
```
![[flagbook.png]]
