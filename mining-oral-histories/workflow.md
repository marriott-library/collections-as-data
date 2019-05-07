# Sample Workflows

As part of this project, the team experimented with different workflows for bulk downloading the PDFs from the University of Utah Digital Collections site and then extracting text for topic modeling. While there are undoubtably more efficient or elegant solutions, this is what worked for us at the time. We're including workflow details here in case it might be useful for anyone undertaking similar projects.

## Mac Process

This required some basic knowledge of navigating the computer through the command line and using Terminal.

### Get IDs for PDFs

Digital objects have a unique identifier that correspond to the link pattern used to download them. For example, the link to download a PDF transcript of an oral history looks like: https://collections.lib.utah.edu/file?id=#######&nocache=true

1. We download the metadata for the collections we wanted to explore and concatenated the IDs with the link pattern above with a basic excel formula to create a list of download links.
2. Next, we created a txt file that contained a list of the download links for the pdf documents.
3. Create a directory for the files, eg mkdir pdf_folder
4. Put the text file in it, cd to the directory
5. Run command: $ xargs -n 1 curl -O < bulkdownloadpdfs.txt
6. Then, we used [Mac Automator](https://www.engadget.com/2013/02/11/mac-101-use-automater-to-extract-text-from-pdfs/) to extract the OCR from the PDFs as text


## PC Process

1. Download metadata from the digital library
2. In a new Excel file, create a list of setname_s in column A and item IDs in column B
3. In column C, enter the path of the folder that you want to save the files to (e.g. C:\Users\u0468989\Downloads\test\)
4. In column D, enter the following formula (this includes the path and filename that you want to save as well as the URL of the file. Curl -o says to download the file and use the filename in the command)
=CONCATENATE("curl -o ",C1,A1,"_",B1,".pdf file?id=",B1)
    * This will create a cmd line query like:
curl -o C:\Users\u0468989\Downloads\test\uum_aep_759152.pdf https://collections.lib.utah.edu/file?id=7591525
5. In column E, enter the following formula
=CONCATENATE("C:\Users\u0468989\Documents\xpdf-tools-win-4.00\bin64\pdftotext.exe ",C1,A1,"_",B1,".pdf")
    * This will create a cmd query like:.
C:\Users\u0468989\Documents\xpdf-tools-win-4.00\bin64\pdftotext.exe C:\Users\u0468989\Downloads\test\uum_gasp_852822.pdf
6. Copy column D to a plain text document in Notepad or Notepad++
7. On the line below the last item in Notepad++, copy and paste column E
8. Save this file as a batch file (e.g. download.bat)
Double click the batch file and a cmd prompt will automatically open and start downloading the files and then extract the 9. text.

### Before the above workflow will work you need to install Xpdftools
1. Download Xpdftools (https://xpdfreader-dl.s3.amazonaws.com/xpdf-tools-win-4.00.zip)
2. Extract this zip file to a folder on your computer where you have editing rights (e.g. Documents folder)

