# smartsheet_replace-sheet-content-python
A python application to update a sheet in Smartsheet using an Excel file. Things to note:
  - code deletes all current content from the sheet and updates with the content from the Excel file
  - code is written to run after GLOBAL VARIABLES are updated at the top of the page, but be prepared to troubleshoot
  - the columns in the sheet and the Excel file must have the same name and be in the same order
     - additional columns can be added after the last column in Smartsheet
  - the Excel can not have blank values -- replace with NULL values
  - as written, the code uploads all data to Smartsheet as a string value 
     - in the append function, the cell value is wrapped in a str() function -- leave it to start, troubleshoot later.
  
