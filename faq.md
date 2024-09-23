---
layout: default
title: FAQ
nav_order: 4
---

# FAQ

## Language Support

### What languages are supported?
The most popular languages that use Latin script are fully supported, including English, Spanish, French, German, and Portuguese, among others.  

Experimental support exists for Simplified Chinese.  Chinese text can be recognized and edited, however character positioning is less accurate, and only one font is currently included.

### Can support for \[x\] language be added?
Additional languages using Latin script can be easily added.  Feel free to request new languages in the [Git Issues](https://github.com/scribeocr/scribeocr/issues).  Languages using other scripts are more difficult to add, as they require new font resources and code.  Therefore, while all languages should be supported eventually, most non-Latin scripts will likely not be added in the near future.

## Recognizing Text with Built-in OCR Engine

### Why is recognition slow on my device/document?
Recognition should be relatively fast.  Even using the "quality" mode, a 20 page document can generally be recognized in 30-40 seconds on a modern desktop.  If recognition is running slowly, it may be for one of the following reasons.

- Recognition is slower on slower devices.
	- All recognition is executed locally in the browser.
	- Recognition will run significantly faster on a fast desktop than on a mobile phone.
- Recognition is slower for complex and/or low-quality documents.
	- Complex documents (multi-column layouts, tables, etc.) will be recognized slower than simple, single-column documents.
	- Low-quality documents will take longer to recognize than high-quality documents, as more fallback strategies and checking must be implemented.
- Recognition is slower when devtools is open.

## Loading Existing OCR Data

### What OCR formats can I edit using ScribeOCR?
ScribeOCR allows for editing existing Tesseract `.hocr` and Abbyy `.xml` files that include character-level metrics.

Character-level metrics are necessary to accurately position text, however unfortunately neither Tesseract nor Abbyy includes them by default.  Therefore, this setting needs to be enabled before recognition.  In Tesseract, character-level metrics in `.hocr` output are enabled by setting `hocr_char_boxes=1`.  In Abbyy, character-level metrics in `.xml` output are enabled by setting the `WriteCharAttributes` option.

### How can I visualize/edit existing OCR data?
When importing files, simply select your Tesseract `.hocr` or Abbyy `.xml` files alongside your image or PDF files.

### Can I visualize/edit the existing OCR data in a PDF file?  
No, this is currently not supported.  Unfortunately, the invisible text added by OCR programs is not precise enough for printing it visibly to be useful.  Overlay text must be generated using the built-in OCR engine, or provided via separate Tesseract .hocr or Abbyy .xml files. 

### Are other OCR engines supported?
It may be possible to use data from other OCR engines that export to .hocr.  However, doing so has not been tested.  If you use Scribe OCR with another engine, feel free to open an issue and report how it went. 

### Why is text being printed on the wrong image?
When multiple image (.png or .jpeg) and/or OCR (.hocr or .xml) files are uploaded, all files of the same type are ordered alphabetically.  Check that your files are named in alphabetical order.  A common mistake is forgetting to pad numbers with leading 0s (remember that “pic_10” comes before “pic_2” in alphabetic order). 

## Reviewing and Editing OCR Text

### Why isn't the overlay text in my document lining up as well as in the examples? 
If your results are significantly worse than the above example, check the following possible explanations.

- Is the image low-quality?
	- Recognition quality and overlay quality will always be worse on low-quality images.
	- Try re-scanning the document at a higher quality.
		- If this is impossible, simply upscaling the existing image may produce significantly better results.
- Is the image distorted?
	- ScribeOCR can print lines at an angle, however the lines will always be straight and parallel.
	- Documents that are warped (the lines are either not straight or not parallel) cannot be accurately represented by the overlay.
- If OCR data was uploaded, does it include granular and accurate positioning data?
	- If uploading Tesseract data, does the data include character-level metrics?
		- These can be enabled by setting `hocr_char_boxes=1`
	- If uploading Tesseract LSTM data, some word bounding boxes may be noticeably incorrect.
		- Unfortunately, this is an issue with Tesseract, so is not something we can resolve here.
- Is the page you are viewing representative of the document as a whole?
	- At present, ScribeOCR optimizes one sans font and one serif font for the entire document.
	- Therefore, if a particular page has a non-standard font, the overlay will be worse for that page.
		- For example, if you are scanning a book and the title page overlays poorly, review the main text before concluding overlay is poor for the document.

If none of these possibilities explain your issue, please open a Git Issue with enough data to reproduce the problem. 

### Is character formatting information (e.g. italics) in OCR data used when printing overlay text? 
Italic text is detected when using the built-in recognition engine.  Additionally, italics reported in uploaded Abbyy .xml data are observed.  Italics reported by uploaded Tesseract `.hocr` data are ignored, as testing found that italics reported by Tesseract were generally incorrect.

When OCR engines report text is bold, this is ignored, regardless of the OCR program being used.  Testing found that no commonly-used OCR engine was capable of reliably identifying bold text.

### How can I save my progress and continue editing later?
Download your current document as HOCR.  This can be imported later (alongside your images/pdfs) to continue editing. 

### Why can't I vertically adjust individual words? 
ScribeOCR stores all words within lines, and all words within a line share the same baseline (superscripts aside).  This model precludes arbitrary glyph/word-level positioning, so it will never be possible to drag around text boxes like in a photo editor like Photoshop or Illustrator.  Rather, the editor is intended to support features similar to a word processor like Microsoft Word.

## Exporting Data

### What output formats can be edited later?
The HOCR format is the only format that allows for editing at a later point.  Therefore, saving a `.hocr` file is strongly recommended, as this will allow for fixing any errors you may catch after closing the application. 

### Why is the PDF I downloaded larger than the PDF I uploaded? 
Scribe OCR is built to use .png and .jpeg images, and does not currently support directly editing PDFs.  When it encounters a .pdf, it simply renders each page to a .png file as a convenience.  In cases when an input .pdf is highly optimized, rendering to a series of .png files can significantly increase file size.    

## Miscellaneous
### Is my data uploaded to a server?
No.  The entire program runs on your browser.  A downloadable/offline version could be offered in the future.
