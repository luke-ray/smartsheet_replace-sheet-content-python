# smartsheet_replace-sheet-content-python
Read below and test this code before working on valuable data!

This is Python application to update a sheet in Smartsheet using an Excel file. I'm new to Python, but I wrote this to be simple
to run--you should be able to get going by updating three global variables (API_TOKEN, SHEET_ID, and EXCEL_FILEPATH). However, 
read below before you start. I use this to create and update databases in Smartsheet, not to load information directly into pretty
pages. I source the data from my databases in my pretty pages. If you're just getting started, I strongly recommend loading data
as strings (as this code is natively written) with null values in all your Excel blank cells. It is easier to use helper columns 
in Smartsheet to clean the data than it is to figure out how to write code to clean the data. 

But you be you :)

Summary Notes:
  - code deletes all current content from the sheet (preserving the headers) and updates with the content from the Excel file
  - code is written to run after GLOBAL VARIABLES are updated at the top of the page, but be prepared to troubleshoot
  - the columns in the sheet and the Excel file must have the same name and be in the same order
     - additional columns can be added after the last column in Smartsheet
  - the Excel can not have blank values -- replace with NULL values
  - as written, the code uploads all data to Smartsheet as strings 
     - in the append function, the cell value is wrapped in a str() function -- leave it to start, troubleshoot later.
  - the number of rows to delete and append is restricted by a URL size limit, so this code chunks the delete and append calls by 300
  
Detailed Notes:

This code  deletes the current content of a sheet in Smartsheets and uploads new content from a pandas
dataframe. It is set up to load from an Excel file using the excel_df() function. If you wish to import using another source,
ensure the dateframe is created with the variable 'df', or update variables throughout accordingly.

This code will error out if your source file is empty. 

This code turns all your data into strings. This keeps Smartsheet from erroring out.
The append() funtion has a string wrapper around the variable function for the cell value: 
    'value': str(df.iloc[i,j]) 
You can remove the string function but expect to troubleshoot errors.

Your source file must have the same column headings *and* order as your 
destination Sheet. You *may* add columns in the destination Sheet *after* the last column.

The easiest way to set up your Sheet (in Smartsheets) is to upload the file to Smartsheet as an Excel sheet
(Smartsheets | File | Import | Import Excel). When you do this, consider deleting all but the header row in your 
Excel table and filling one row of cells with "1243" -- this will cause Smartsheet to make them a Text/Number column type,
which are easiest to work with (especially to start). If you don't do this, make sure to update the Column Type 
because Smartsheets tends to make your column type an ordered list, which has data
restrictions that will likely error your code out. To ensure success, turn all the column types 
to "Text/Number" or "Date" (unless it's necassary, don't restrict your "Date" column type to "Date Only"--test first). 
If you turn your column type to anything else, you may need to update the temp_row.cells.append() function to create 
the proper column types. 

NOTE: The API_TOKEN variable is your Smartsheet API Token. To find it, in Smartsheet, select your account icon in 
the lower left corner, select Personal Settings | API Access. Generate a new token if necassary. If you don't see
the option to make an API token, you don't have the right license.

NOTE: The SHEET_ID variable is the ID of the sheet you wish to update. To find it, go to your sheet, 
select File | Properties.

NOTE: You can enter the filepath for your Excel file as your computer natively provides.
