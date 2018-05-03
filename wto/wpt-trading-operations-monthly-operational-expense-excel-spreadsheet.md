<!-- TITLE: WPT Trading Operations: Monthly Operational Expense Excel - Spreadsheet -->
<!-- SUBTITLE: A quick summary of WPT Trading Operations: Monthly Operational Expense - Excel Spreadsheet -->



WPT Trading Operations : Monthly Operational Expense – Excel Spreadsheet
========================================================================


Operational expenses are modelled at a monthly resolution in the cash flow model. These can be found in the "Mthly Inputs" sheet from Column H to T. If additional columns are added, the MATLAB script in line 54 needs to be updated.  

```matlab
MthlyInputs = xlsread(strcat(path, inputFilename), 'Mthly Inputs', 'C4:T47');  
```

The operational expenses are modelled to occur on the first week of the relevant month.  