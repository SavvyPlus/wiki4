<!-- TITLE: WPT Trading Operations Loans - Excel Spreadsheet -->
<!-- SUBTITLE: A quick summary of WPT Trading Operations Loans - Excel Spreadsheet -->



WPT Trading Operations : Loans – Excel Spreadsheet
==================================================


Loans made to WPT can be found in the "Loans" sheet, from columns B to J. Additional loans can be added up to row 30 before the MATLAB script in line 62 needs to be updated.  

```matlab
\[num,txt,Loans\] = xlsread(strcat(path, inputFilename), 'Loans', 'C3:J30');  
```

  