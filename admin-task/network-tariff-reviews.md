<!-- TITLE: Admin Task: Network Tariff Reviews  -->


Admin Task : Network Tariff Reviews
====================================

**PBI Report**

When completing a NTR for Procurement Australia, use a pre-existing PBI report located in:

_S:\\IT\\Power BI\\Beta version\\PA_ (choose one from a member eg. Barwon Water)

Rename this and save as the new report

  <br>
<br>


**NTR Template File**

Open the template file:

_S:\\Consulting\\Procurement Australia\\1612 NTR\\NTR Template/xlsx_

This file will already be linked with the report, so it's just a case of updating the Template with the appropriate data to the member that you are reporting on.

If you need to move this file, just remember that you will need to update the PBI report to the new file location (Edit Query).

  <br>
<br>


**Calculations File**

Open the file with all of the NTR calculations. James C will have this info, but for reference, the last one was saved in the same folder as above and titled: Powercor NTR 2016-12-20.xlsm

This file will contain all of the information for ALL of the PA Members. It will be necessary to filter by Member, to select the client that you are interested in seeing.

Filter on this file by Member (ie. Barwon Water) for the 3 tables:

1.  Cost Results (Detailed)
2.  PIVOT
3.  Gap Analysis - Final Table

Copy all of this info into the corresponding sheets on the NTR Template. Once all 3 sheets have been copied across, click Save.

Go back to the PBI report and click Refresh. This will now refresh all of the visuals with the corresponding data as per that Member.

  <br>
<br>


**TIPS:**

*   One report needs to be done one at a time, and ensure that it is completed fully. As we are using the same NTR Template folder for all, once you have changed the data to a different member, you won't be able to hit 'Refresh' without starting from the beginning. So finish it, then move on.
*   PBI hates any field with a N/A, so replace them with either a blank or a 0
*   Make sure all names correspond between the tables (ie. that all 3 sheets are called "Member" and not one as "Client")
*   Once you have saved the Template and refreshed the report, rename the Template file to that member and save it in the same folder. This way, we have the necessary data saved individually. Eg. NTR Template - Barwon Water
*   If one of the visuals in PBI isn't working, check the links between the tables. This is a common issue for the Tariff Comparison visual. If the link is a dotted line, double click it to and select the option "Make this relationship active"  
      
