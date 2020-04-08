---
title: Tender Unbundled Rate Card Template
description: Rate card template to convert the offers to Service Agreement
published: true
date: 2020-04-08T00:55:59.457Z
tags: 
---

The retailers will be provided with the standard rate card template to respond with their offers. Having the retailer's response and rather than entering the offers manually to the Service Agreement template, this template will be able to automatically transform the data and fill up the Service Agreement template

The following are the steps to use the template

- Template location 
	**G:\Shared drives\SavvyPlus\Energy Accounting Operations\Automated Operational Script\Unbundled Rate Card Conversion Template\Template**
- Copy the "**Unbundled Rate Card Conversion Template.v.?.xlsm**", "**Elec Service Agreement.xlsm**", "**Gas Service Agreement.xlsm**" to your Project folder
- Open the template files on your Project folder
- Copy the retailer's offer to "**Elec -unbundled**", "**Elec - Enviro....**", "**Gas - Unbundled**", "**Gas - Veet**"
- Go to "**Data - Elec Rate List**" or "**Data - Gas Rate List**"
- Click on the "**Click to Refresh @@@**" button. The table should refresh with updated data. Otherwise try clicking the button again, if this happen, let me know so that I can fix it
- If the data is fine, open (if not yet) the Service Agreement template (Elec or Gas)
- Then click on the "**Copy to Template >>>>**"
- Watch the magic happens

**Additional Note**
- The Rate Card table's header has the option to change the rate type as per retailer's offer. For instance, the SME offer for Electricity is usually in c/kWh while the Large can be in $/MWh. So, select the rate type according and the conversion will take place automatically.
- In order to change the rate type on the header, you'll need to "Unprotect" the sheet

**Offer variations for same State or Distribution**
- It is possible for the retailer to provide multiple offers for "Same region/state for Large" or "Same distribution (possibly different network code) for small"
- As per the point above, similar could occur for Environmental
- This can be resolved by defining unique value to the "Distribution/Category" or "Category" column
- For retailer's, the rates (different periods) will be grouped together by "Distribution/Category" distinct value
- For environmental's, if the "Category" is defined then the process will look for the same value on the retailer's "Distribution/Category" to map. Otherwise leaving the "Category" as blank is deemed to be generic by Region/State, hence will map to the retailer's rate by Region/State regardless of the "Distribution/Category"

