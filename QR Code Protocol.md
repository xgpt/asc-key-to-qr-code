copyright 2017 (C) Paul Gupta

QR Code Backup and Recovery of Essential Files

Required software:

•	zbar (for “zbarimg --raw" command)
•	imagemagick
•	qrencode
•	linux terminal with
o	split
o	cat
o	gpg
•	https://github.com/4bitfocus/asc-key-to-qr-code scripts cloned at https://github.com/xgpt/asc-key-to-qr-code



##How to split a large file into multiple QR codes for paper backups.
1.	Consider printing the file entirely in addition to the following instructions. Such as SSH keys or GPG/OpenPGP keys. OCR is getting better every day, and painstaking recovery is possible by hand if no such software can be attained.
2.	Symmetrically “encrypt” your file using gpg. This creates a very hardy file that is encoded using standard and printable encodings that are resilient to whitespace that might be introduced in the decoding process. Additionally this is a very standard, widespread, and likely “future-proof” method that both compresses the file entered slightly, as well as encodes it into a printable/scan-able/translatable/simplistic representation of the file. 
a.	gpg -c foo -o foo.asc
i.	(Use the password "password" and remember this for later.)
3.	Use the asc2qr.sh script to create QR output of your file.
a.	“bash asc2qr.sh foo.asc”
i.	This should generate images in the folder named “QR1.png QR2.png QR3.png” and so forth.
ii.	The script CAN and SHOULD be altered to lower the bits per image, and increase the error correction to an amount appropriate for cell phone cameras to restore the scan in case of long term degradation of the image.
4.	Prepare to print these QR codes.
a.	Put your images in a printable order.
i.	This can be done with the use a contact sheet generator / proof sheet generator (photography terms) to generate an image with filenames that are easy to order and reassemble in the future.
ii.	Alternately, they could be hand labeled if you are in a hurry.
b.	Print out the gpg password used to symmetrically encrypt the gpg encoding.
c.	Print out page numbers whenever possible, or hand label the page numbers as appropriate. 6 pages of random digits that turn into a GPG key when finished are very difficult to reassemble out of order. Don’t make the mistake of trying every possible permutation. Make sure you’ve got it right.
5.	TEST scanning it back in. Make notes on the first page of “exactly” how to decrypt the file right there on an attached first page
6.	Staple the thing and put it in a nice envelope. Try not to fold it if possible, even with error correction, try to be the archivist your future desperate self would appreciate!

##How to scan these QR codes and recreate your file!

1.	Read the instructions on the first page. If you were smart, you would have attached some.
2.	Scan the QR codes into a computer using a cell phone or preferably a flatbed scanner. 
3.	Take your ordered QR images, and make them data again.
a.	Use zbar (in --raw mode) to recreate the file as bit-perfect as you can from the scans.
i.	zbarimg –q --raw QR1.png >> recompile.txt
ii.	zbarimg (calls the computer image scanner) –q (removes some non-data output) --raw (removes zbar data-header information) QR1.png (calls the first file) >> (appends data to output file instead of overwriting it) recompile.txt (calls output file)
1.	Consider using a switch to specify that “THIS IS A QR CODE, NOT A REGULAR BARCODE” to make more accurate scans.
2.	Continue until finished. QR{1..9} or QR{1...9} will use the curly brace blob feature to call all images in order to do the above tasks. Google it if you want, or just do one at a time as directed above.
b.	Alternately, try to use the qr2asc.sh script as found above.
4.	Hopefully you’ve got your bits back in order with a sane header and footer showing GPG/openPGP data. 
a.	Feed this into GPG as such 
i.	“cat recompile.txt | gpg”
1.	Type in the password you were thoughtful enough to have put in the margins of your printout, or at least in your instructions.
5.	Enjoy. Hopefully you’ve recovered your file. If not, hopefully you can OCR the printed out file from the first step in the creation instructions.
