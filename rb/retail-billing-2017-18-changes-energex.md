<!-- TITLE: Retail Billing: 2017-18 Changes (Energex) -->
<!-- SUBTITLE: A quick summary of Retail Billing: 2017-18 Changes (Energex) -->


Retail Billing : 2017-18 Changes (Energex)
==========================================


NEW Tariffs:

<div class="table-wrap"><table class="wrapped confluenceTable"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th class="highlight-green confluenceTh" colspan="1" data-highlight-colour="green"><p>Tariff Code</p></th><th class="highlight-green confluenceTh" data-highlight-colour="green"><p>Name</p></th><th class="highlight-green confluenceTh" data-highlight-colour="green"><p>Eligibility</p></th><th class="highlight-green confluenceTh" colspan="1" data-highlight-colour="green"><p>Structure &amp; Suitability</p></th></tr></thead><tbody><tr><td colspan="1" class="confluenceTd">7100</td><td class="confluenceTd">Business Demand</td><td class="confluenceTd"><p>This tariff is available to business customers with consumption less than 100 MWh/year and cannot be used in conjunction with Business flat (NTC8500).</p></td><td colspan="1" class="confluenceTd">This tariff uses a supply charge ($/day), a flat usage charge for energy (c/kWh) and a demand charge ($/kW/month).</td></tr><tr><td colspan="1" class="confluenceTd">7400</td><td colspan="1" class="confluenceTd">Demand ToU 11kV</td><td colspan="1" class="confluenceTd"><p>This tariff is offered from <strong>1 July 2017</strong>. It is offered on a voluntary basis for all existing 11kV Line customers on legacy tariffs. This will become the <strong>default</strong> tariff from 1 July 2017 for new customers that share an 11kV feeder with other customers.</p></td><td colspan="1" class="confluenceTd">This tariff applies a supply charge (<strong>see below**</strong>), a flat usage rate for energy (c/kWh), a Peak Demand charge ($/kVA/month) and an Excess Demand Charge ($/kVA/month).</td></tr></tbody></table></div>
  

****Supply Charge**

###### _Capital:_

###### Unit: $/day/$M of noncontributed asset value (NCCAV).

###### Quantity: NCCAV ($M) and number of days in billing period.

###### Operating and maintenance:

###### Unit: $/day/$M connection asset value (CAV).

###### Quantity: NCCAV ($M) and number of days in billing period.  

  

**DEMAND Definitions:**
![Headers](/uploads/headers.png "Headers")
![Deamnd Definitions 7100 7400](/uploads/deamnd-definitions-7100-7400.png "Deamnd Definitions 7100 7400")

<br>

###### **7100 Business Demand:**



DEMAND\_ENERGEX\_9-21

Maximum kilowatt demand measured as a single **peak** over a 30 minute period during peak billing period.

  

###### **7400 Demand ToU 11kV:**

DEMAND\_ENERGEX\_9-21

Peak Demand Charge

Maximum kilowatt demand measured as a single **peak** over a 30 minute period during billing period.
<br>

  

Excess Demand Charge

DEMAND\_ENERGEX\_EXCESS

Quantity: The maximum of:

*   Zero,
    
*   Maximum kilowatt demand measured as a single peak over a 30 minute period outside the peak charging windows, minus the peak demand quantity as described above.