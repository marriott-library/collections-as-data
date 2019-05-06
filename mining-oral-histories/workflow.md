# Sample Workflows

As part of this project, the team experimented with different workflows for bulk downloading the PDFs from the University of Utah Digital Collections site. While there are undoubtably more efficient or elegant solutions, this is what worked for us at the time. We're including workflow details here in case it might be useful for anyone undertaking similar projects.

## Mac process

This required some basic knowledge of navigating the computer through the command line.

### Get IDs for PDFs

Digital objects have a unique identifier that correspond to the link pattern used to download them. For example, the link to download a PDF transcript of an oral history looks like: https://collections.lib.utah.edu/file?id=#######&nocache=true

We download the metadata for the collections we wanted to explore and concatenated the IDs with the link pattern above with a basic excel formula to create a list of download links.
Next, we created a txt file that contained a list of the download links for the pdf documents.
Create a directory for the files, eg mkdir pdf_folder
Put the text file in it, cd to the directory
Run command: $ xargs -n 1 curl -O < bulkdownloadpdfs.txt
Then, we used [Mac Automator](https://www.engadget.com/2013/02/11/mac-101-use-automater-to-extract-text-from-pdfs/) to extract the OCR from the PDFs as text


## PC Process
