# FAQ/Support

## Loading Existing OCR Data

### Is character-level OCR data required?  Why?
For Tesseract .hocr, character-level data is highly recommended but not required.  If no character-level data is found, words will still be overlayed, however font optimization will be disabled (as not enough information exists to create an optimized font).

For Abbyy .xml, character-level data is required.  While Tesseract will still report word-level metrics when character-level metrics are disabled, Abbyy does not report where words are positioned. 

### How can I create character-level data in my OCR program? 
For Tesseract, set the config variable `hocr_char_boxes=1`.  For example, the entire command might be `tesseract [input file] [output file] -c hocr_char_boxes=1 hocr`.  Alternatively, all OCR data generated using Scribe OCR's built-in Tesseract engine will utilize character-level data.  

### Are other OCR engines supported?
It may be possible to use data from other OCR engines that export to .hocr.  However, doing so has not been tested.  If you use Scribe OCR with another engine, feel free to open an issue and report how it went. 

### Why is text being printed on the wrong image?
When multiple image (.png or .jpeg) and/or OCR (.hocr or .xml) files are uploaded, all files of the same type are ordered alphabetically.  Check that your files are named in alphabetical order.  A common mistake is forgetting to pad numbers with leading 0s (remember that “pic_10” comes before “pic_2” in alphabetic order). 

## Recognizing Text with Built-in OCR Engine

### What devices support the built-in OCR engine? 
The built-in engine should run on all common device/browser combinations, however performance will vary significantly between devices.  In addition to some devices being faster than others (in terms of clock speed, cores, etc.), there are 2 versions of the built-in Tesseract OCR engine that Scribe OCR chooses between based on what your device supports.  The fast (SIMD-enabled) version is loaded for users with modern Intel/AMD processors (supporting SSE 4.2).  The slower (SIMD disabled) version is loaded on all other devices.  You can confirm which version has been loaded on your device by checking `About > Debug Info > SIMD Support`. 

Notably, while the SIMD-disabled version is much slower using the Tesseract LSTM engine, no such disparity exists using the Tesseract Legacy engine.  Therefore, if you do not have access to a device that supports the SIMD-enabled version and are finding Tesseract LSTM performance unacceptably slow, consider switching to the Tesseract Legacy engine. 

### Why is recognition slow?
If OCR performance is poor, check the following possible explanations. 
1. Are you using a device that supports the faster (SIMD-enabled) version of Tesseract? 
    -	See "What devices support the built-in OCR engine?" section above
1.	Are you using a slow device?
    -	The entire program is executed locally in your browser, so performance will vary significantly by device. 

## Reviewing OCR Text

### Why isn't the overlay text in my document lining up as well as in the examples? 
If your results are significantly worse than the above example, check the following possible explanations.  
1.	Is the appropriate default font being used?
    -	“Libre Baskerville” should be used for serif text, and “Open Sans” for sans serif text. 
1.	Is font optimization enabled?
1.	Is the page you are viewing representative of your document as a whole?
    -	At present, only a single optimized font is created for the entire document.
    -	As books often use different fonts for the initial pages (title page, table of contents, etc.), results are often worse in the first few pages.  Try skipping several pages ahead and see if results improve. 
1.	Is the document image distorted? 
    -	Text is drawn in lines that are straight and parallel. 
    -	Documents that are warped (the lines are either not straight or not parallel to each other) will therefore not align with the text. 

If none of them explain your issue, please open a Git Issue with enough data to reproduce the problem. 

### Is character formatting information (e.g. italics) in OCR data used when printing overlay text? 
Character formatting data (specifically the identification of italics, small caps, and superscripts) is used for Abbyy but not Tesseract.  Testing found this data to be generally reliable for Abbyy.  However, for Tesseract formatting data was found to be so unreliable that including it caused more work than it alleviated.  

### How can I save my progress and continue editing later?
Download your current document as HOCR.  This can be imported later (alongside your images/pdfs) to continue editing. 

## Miscellaneous
### Is my data uploaded to a server?
No.  The entire program runs on your browser.  An downloadable/offline version could be offered in the future.

### Why is the application running slowly?
If performance is poor, check the following possible explanations. 
1.	Are you using a slow device?
    -	The entire program is executed locally in your browser, so performance will vary significantly by device. 
1.	Are you using a .pdf for images (rather than .png or .jpeg)? 
    -	Using a .pdf file is currently significantly slower than using .png or .jpeg files (as pdfs are rendered to images by a separate library).
    -	Consider converting your .pdf to .jpeg or .png images and trying again.
        - This can be accomplished using GhostScript on Linux with the following command:
        -	`gs -dNOPAUSE -dBATCH -sDEVICE=pnggray -dUseCropBox -r300 -sOutputFile="Pic-%03d.png" [pdf file]`
