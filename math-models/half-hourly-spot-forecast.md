<!-- TITLE: Half Hourly Spot Forecast -->
<!-- SUBTITLE: A quick summary of Half Hourly Spot Forecast -->

# Methodology

SavvyPlus uses a probabilistic ‘learning’ approach for modelling electricity spot prices, where recent and relevant historical data are used as inputs to the model. The electricity price forecasts are developed based on a view that:
*1.   The forecast must reflect the latest information available to the market, particularly in the current period of unprecedented rapid change
2.	The forecast should reflect the current regulatory conditions and not involve assumptions that require a significant change of law event (e.g. carbon pricing)
3.	The forecast should be based on market-standard assumptions, and relate to credible, independently verifiable public studies that are developed for a similar purpose.*

These three factors shape the methodology used for the spot price forecast. It is in SavvyPlus’s view that spot prices before 2017 have little relevance now in predicting the future following the re-valuation of domestic gas and thermal coal. As a result, the forecasting methodology relies heavily on 2017 spot prices, as well as the spot sensitivity data provided by AEMO at half hour resolution. This large dataset allows modelling of consequential spot price if demand or supply changes. It therefore incorporates strategic behaviour as well as the nuances of running a physical market. This dataset is grouped by season (see Table 1), and into buckets according to the temperature statistics of the day.

![Screen Shot 2018 05 22 At 10 34 30 Am](/uploads/matlab/screen-shot-2018-05-22-at-10-34-30-am.png "Screen Shot 2018 05 22 At 10 34 30 Am")

Simulations are built using weather in the last 10 years as climate change makes longer term weather records less relevant. The historical weather dataset incorporates daily weather statistics such as temperature, wind speed and solar irradiance. This dataset is then grouped into weeks for each calendar month. Bootstrap sampling is then applied to these monthly datasets to generate weekly weather strips for the simulation period (1 July 2023 to 30 June 2033). A total of 1,000 sets of these weather strips are produced to form the basis of the spot price simulations. The monthly grouping ensures that the seasonal changes in weather pattern are reflected.
A list of upcoming generation projects is also compiled. Upcoming renewable projects (wind and solar farms) are mapped to existing projects with similar technologies (onshore vs offshore, tracking vs non-tracking) to serve as a proxy when creating a simulated generation profile for each new project. The growth of roof-top solar PVs installations is also considered. Historical half hourly roof-top solar PV generation profiles published by AEMO are normalised according to output figures published Clean Energy Regulator (CER) and grouped into weeks for each calendar month. These normalised profiles are then scaled to the projected forecasts prepared by AEMO and bootstrap sampling is again applied.
Battery storage market capacity is estimated using various sources. Demand forecasts are sourced from AEMO’s Electricity Statement of Opportunities (ESOO) report published in Sep-17 and are weighted across the simulations according to Table 2 shown below. Generation plant closures are considered and sourced from AEMO’s National Transmission Network Development Plan (NTNDP) report published in Dec-16.


![Screen Shot 2018 05 22 At 10 34 37 Am](/uploads/matlab/screen-shot-2018-05-22-at-10-34-37-am.png "Screen Shot 2018 05 22 At 10 34 37 Am")


Using the weather simulations, a similar temperature day from the spot price sensitivity dataset is selected. The demand from the dataset is then adjusted according to the demand growth forecasted, factoring generation closures and new generation coming online, as well as roof-top solar PV, and the impact of batteries and the consequential half hourly spot price is derived. Using this methodology, 1,000 spot forecast simulations are built at a half hourly resolution across the simulation period.


# Assumptions & Data Source

This section documents the key input assumptions used in the modelling as well as the source of the data.

### Weather Data

Weather statistics were sourced from Bureau of Meteorology (BOM).
Daily weather statistics such as minimum temperature, maximum temperature and solar irradiance was sourced from January 2011 onwards.


### Renewable Projects

Upcoming Renewable projects up to 2023 were sourced from the both the Clean Energy Regulator  (CER) and AEMO . With the CER projects, only financially committed projects were included in the list, these are projects that have received all development approvals and reach a final investment decision. With the AEMO projects, only the proposed projects under development with a commercial use date were considered. 
Details of renewable projects past 2023 were sourced from AEMO’s National Transmission Network Development Plan (NTNDP) report published Dec-16 . 


### Baseload Generation Closures

Baseload generation closures were also sourced from AEMO’s NTNDP report published Dec-163

### Rooftop Solar 

Rooftop solar PV growth was also sourced from AEMO’s NTNDP report published Dec-163. The forecast is for rooftop solar PV to reach installed capacities of 5696MW in 2034, with current installation capacity at approximately 2000MW.

### Annual Consumption

The annual electricity consumption for the different NEM states was sourced from AEMO’s Electricity Statement of Opportunities (ESOO) report published in Sep-17 . Three scenarios were considered, these are documented in Table 3 below. The Neutral scenario is in SavvyPlus’s opinion the most likely scenario to eventuate, thus 55% of the simulations reflected this scenario, the Strong Growth scenario was given a lower probability of occurrence at 30% and the Weak Scenario, 15%.


>  http://www.cleanenergyregulator.gov.au/RET/Pages/About%20the%20Renewable%20Energy%20Target/How%20the%20scheme%20works/Large-scale-Renewable-Energy-Target-Supply-Data.aspx
  http://www.aemo.com.au/-/media/Files/Electricity/NEM/Planning_and_Forecasting/Generation_Information/June-2017/Generation_Information_QLD_05062017.xlsx
  http://www.aemo.com.au/Electricity/National-Electricity-Market-NEM/Planning-and-forecasting/National-Transmission-Network-Development-Plan/NTNDP-database, “2016 Generation Outlook – Neutral Scenario – Base Case QNI VIC-NSW.xslx”, “NEMInstalled Capacity Data” sheet
  http://forecasting.aemo.com.au/Electricity/AnnualConsumption/Operational

![Screen Shot 2018 05 22 At 10 34 47 Am](/uploads/matlab/screen-shot-2018-05-22-at-10-34-47-am.png "Screen Shot 2018 05 22 At 10 34 47 Am")

# Data Source List
As a supplement to the explaination in the above section Assumptions&Data Sourse, all the data sources are listed below.

### Database Sources
* [MarketData].[dbo].[BOM_Daily]
* [MarketData].[dbo].[Public_Holidays]
* [MarketData].[dbo].[AEMO_ROOFTOP_PV_ACTUAL]
* [OperationalReporting]
	* [OperationalReporting].[NEM].[PreDispatchPriceSensitivities]
	* [OperationalReporting].[NEM].[SpotPriceDemand_30min]
	* [OperationalReporting].[NEM].[GenerationByUnit_30min]

Note: The OperationalReporting is a bunch of views pointing to ElecMMS + EnergyAccounting

### Excel Spreadsheet Sources
* Assumption Inputs - yyyy-mm-dd .xlsx   
This is the main assumption data sourse including new generation list, battery storage rates, PV forecast data, consumption growth, etc. This file would be updated frequently by Carl/Jay/Will to reflect the specific requirements in certain project.
* Wind Summary.xlsx
This is the historical wind generation data and some are derived from the power curve of given wind farms. This file will be used in the wind generation simulation.
* Solar Generation.xlsx
This is the historical (or estimated historical) solar generation data, which is derived from Bir's model, and this file will be used in the solar generation simulation.

Note: file names may be different sometimes.
# Summary of Results

This section provides a brief description of the spot price simulation results.

### Explanation of Box-and-Whisker Charts

Box-and-whisker plots are used to present the simulation results as they are a useful way to graphically present the findings, and provide an easy visual aid to recognise the length of the tails of a distribution. Figure 1 provides an illustration of a box-and-whisker plot.

*Figure 1: Example of Box and Whisker Chart*
![Screen Shot 2018 05 22 At 10 34 54 Am](/uploads/matlab/screen-shot-2018-05-22-at-10-34-54-am.png "Screen Shot 2018 05 22 At 10 34 54 Am")

The electricity market spot market has a long tailed distribution where the average price might be about $80/MWh, but the maximum price is more than $13,000/MWh, yet the minimum is -$1,000/MWh. Consequently, the distribution of the spot market is not symmetrical, and not a classical bell-shape distribution.

All distributions presented as a box-and-whisker plot have 7 percentile points marked:

1.	100th percentile (best case) – top of upper whisker
2.	95th percentile – marked as a dash on the upper whisker
3.	75th percentile – top of box
4.	50th percentile (median) –where the colour changes in the box from grey to green
5.	25th percentile – bottom of box
6.	5th percentile – marked as a dash on the lower whisker
7.	0 percentile (worst case) – bottom of lower whisker

In addition, the average is shown as a black dot on the plot. To summarise, the box of a box-and-whisker chart represents the middle 50% of the cases, and the two whiskers (or tails) represent the upper and lower 25% of the cases. A long whisker means the distribution has a long tail, and conversely a short whisker means the distribution is compressed. 

### Spot Forecast

A total of 1,000 simulations at half hourly resolution were created across the simulation period (1 July 2023 to 30 June 2033). At a half hourly resolution, the modelling indicated that prices fall during the middle of the day, in most cases below $0/MWh. This pattern can be observed from July 2023 and is attributed to the abundance of solar generation from both large scale projects and rooftop PV. SavvyPlus expects market players to respond to manage such an outcome, and therefore, for the modelling it would be reasonable to assume zero instead of negative outcomes; although such a modification has not been undertaken in this preliminary run.
Aggregating the half hourly data into a quarterly resolution, the distribution spot forecast from Q3-23 to Q2-33 is shown below in Figure 2. The general trend that can be observed is that median prices are below $100/MWh until Q1-27, where there is a jump and then again in Q1-29 before prices fall gradually year on year. The jump in prices in Q1-27 and Q1-29 is due to baseload generation closures. Another observable trend is that the distribution tails grow longer further into the simulation years, with the spread in Q1 and Q4 significantly larger than the spread observed in Q2 and Q3. There are also a significant number of quarters where the average simulated price ended up below $0/MWh


![Screen Shot 2018 05 22 At 10 35 01 Am](/uploads/matlab/screen-shot-2018-05-22-at-10-35-01-am.png "Screen Shot 2018 05 22 At 10 35 01 Am")

Figure 3 below shows the distribution of the spot forecast aggregated into financial years. The median price in the first 3 financial years hover around $45/MWh, jumping to $70.10/MWh in FY-27 and increasing yearly to $104.89/MWh in FY-30 and then falling to $91.18/MWh in FY-33. 

![56](/uploads/56.png "56")
