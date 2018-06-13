<!-- TITLE: Matlab Variables (Spot Price) -->
<!-- SUBTITLE: A quick summary of Matlab Variables -->

# Variables in MAT file

The following variables are stored in the MAT file uploaded onto Amazon S3.

Due to memory limitations, out of 1,000 simulations, the MAT file currently only contains the output from the first 300 simulations. These 300 simulations relate to the “Medium” case scenario, which is the scenario of most interest to the client.

## **N**
This variable contains the total number of simulations in the dataset, in this case, 1,000.

## **TS**
This variable is short for TimeStamp (TS), and contains the half hourly time stamp of the simulation period from 1-Jan-2019 to 7-Jan-2031 in MATLAB’s datenum format. 
Size: 210672 x 1 double

## **Spot_Sims**
This variable contains the forecasted half hourly spot prices across the simulation period. Only the first 300 columns are populated with data, where each column represents data from one simulation run.
Size: 210672 x 1000 double

## **SPS_expanded_N**
This variable contains the Spot Price Sensitivity (SPS) lookup table. It is structured as a 1000 x 1 cell array, where each cell contains a 210672 x 46 matrix. The first 45 columns contain the resultant spot price if demand is shifted by the levels described below. The last column contains the half hourly demand profile from the historical “reference” period. Similarly, only the first 300 cells contain data, where each cell represents the SPS lookup table for one simulation run.
[-9500, -9000, -8500, -8000, -7500, -7000, -6500, -6000, -5500, -5000, -4500, -4000, -3500, -3000, -2500, -2000, -1700, -1400, -1100, -800, -500, -200, -100, 0, +100, +200, +500, +1000, +1500, +2000, +2500, +3000, +3500, +4000, +4500, +5000, +5500, +6000, +6500, +7000, +7500, +8000, +8500, +9000, +9500]

## **Final_Adjusted_Dem_N**
This variable contains the half hourly demand profile by which the historical “reference” period is to be shifted from looking up the SPS_expanded_N table. It accounts for the shift in demand due to changes in demand from AEMO’s forecast, additional generation from new projects and newly installed rooftop PV, retirements from existing generation projects and adjustments to the demand profile from the historical “reference” period due to forecasted temperature not observed during the “reference” period. Only the first 300 columns are populated with data. Each column represents data from one simulation run.
Size: 210672 x 1000 double
 
## **NewGen**
This variable is a MATLAB structure array containing the forecasted half hourly MW output of new generation projects. For fields which contain 1000 columns, each column represents data from one simulation run. This variable is generated from running the simulate_NewGenProjects_VIC_10yr_yyyymmdd.m script.
**TV**		210672 x 6 double 
Field containing the MATLAB datevec of the half hourly period starting definition of the simulation period.
**Output**		210672 x 1000 double
Field containing the simulated half hourly total MW output of all new generation projects.
**Output_Wind**		210672 x 1000 double
Field containing the simulated half hourly MW output of all new wind generation projects.
**Output_Solar**		210672 x 1000 double
Field containing the simulated half hourly MW output of all new large scale solar generation projects.
**Output_Elaine**		210672 x 1000 double
Field containing the simulated half hourly MW output of Elaine Wind Farm.
**Output_Yendon**	210672 x 1000 double
Field containing the simulated half hourly MW output of Yendon Wind Farm.
**Output_GoldenPlains**	210672 x 1000 double
Field containing the simulated half hourly MW output of Golden Plains Wind Farm.
**ScalingMatrix**		210672 x 49 double
Field containing the half hourly scaling variable to scale each new generation project to it’s nameplate capacity based on the proxy generation’s nameplate capacity. Each column represents a new generation project.
**Output_Wind_Curtail**	210672 x 1000 double
Field containing the half hourly MW curtailment of all new wind generation projects. The half hourly curtailment is set such that the total output from new wind projects do not contribute more than a predefined percentage of total system demand.
**Output_BrownCoal**	210672 x 1000 double
Field containing the simulated half hourly MW output of all new brown coal projects, mainly related to the upgrade of Loy Yang B.

## **SysDem**
This variable is a MATLAB structure array with 4 fields related to system demand and generation retirements. 
**GenClosure_Date**		2 x 1 double
This field contains the MATLAB datenum of the start date of when particular power stations are retiring. In this case, there are 2 power stations in the simulation period that will be retiring.
**GenClosure_Pct_Impact**	2 x 1 double
This field contains the percentage of the nameplate capacity of the retiring power station that will impact the region in the NEM being simulated.
**GenClosure**		210672 x 1000 double
This field contains the simulated half hourly impact (MW) of generation retirements. The profile is derived from the historical profile of the existing generation during the “reference” period, scaled to the GenClosure_Pct_Impact.
**Output_Adjusted**	210672 x 1000 double
This field contains the simulated half hourly system demand (MW), after adding the shift in demand due to changes in demand from AEMO’s forecast, and adjustments due to forecasted temperature not observed during the “reference” period. Each column represents data from one simulation run.


## **EG**
This variable is a MATLAB structure array with fields related to Existing Generation (EG) units. The variable is created from running the simulate_SpotPriceSensitivity_VIC_YYYYMMDD.m file.
**FuelType**	1 x 4 cell
This field contains the fuel type of the existing generation units in the particular NEM region (VIC). In this case, the cell contents are “Gas”, “Brown Coal”, “Hydro”, and “Wind”.
**Capacity**	1 x 4 cell
This field contains a 1 x 4 cell, where each cell contains an array that stores the nameplate capacity for each existing generation unit of a particular fuel type. In this case, the first cell contains an array that stores the nameplate capacities for the 23 gas generation units in VIC, the second cell contains an array that stores the nameplate capacities for the 22 brown coal generation units in VIC, the third cell contains an array that stores the nameplate capacities for the 10 hydro generation units in VIC and the fourth cell contains an array that stores the nameplate capacities for the 12 wind generation units in VIC.
**DUID**		1 x 4 cell
This field contains a 1 x 4 cell, where each cell contains a string array that stores the Dispatch Unit ID (DUID) of each existing generation unit of a particular fuel type. It follows the Fuel Type definition listed in the FuelType field. 
**Name**		1 x 4 cell
This field contains a 1 x 4 cell, where each cell contains a string array that stores the name of each existing generation unit of a particular fuel type. It follows the Fuel Type definition listed in the FuelType field. 
**MW**		23376 x 4 double
This field contains the half hourly total output (MW) of each different Fuel Type across the reference period, which is 1-Jan-2017 to when the “simulate_SpotPriceSensitivity_VIC_YYYYMMDD.m” script was run, in this case, 3-May-2018. The first column represents the total output from gas generation units in VIC, the second column from brown coal generation units in VIC, the third column from hydro units in VIC and the fourth column from wind generation units in VIC.
**Retire_Capacity**		1x1 cell
This field contains the nameplate capacity (MW) of any retiring power station that will contribute to the shift in the reference demand during the simulation period. In this case, only Liddell power station is assumed to be retiring, thus a 1x1 cell array. 
**Retire_DUID**			1x1 cell
This field contains the Dispatch Unit ID of the retiring power stations, one string array per cell for each retiring power station.
**Retire_Name**			1x1 cell
This field contains the name of the retiring power stations, one retiring power station per cell.
**Retire_MW**			23376 x 1 double
This field contains the half hourly total output (MW) of each retiring power station across the reference period, which is 1-Jan-2017 to when the “simulate_SpotPriceSensitivity_VIC_YYYYMMDD.m” script was run, in this case, 3-May-2018. Each column represents the output from one retiring power station.
NewBrownCoal_Capacity	1x1 cell
This field contains the nameplate capacity (MW) of any brown coal power stations that will be used as a proxy for estimating new brown coal generation projects. In this case, the Loy Yang B Upgrade is the only new brown coal generation project in VIC and the proxy for this project will be Loy Yang B power station.
**NewBrownCoal_DUID**		1x1 cell
This field contains the Dispatch Unit IDs of any brown coal power stations that will be used as a proxy for estimating new brown coal generation projects.
**NewBrownCoal_Name**		1x1 cell
This field contains the names of any proxy brown coal power stations that will be used for estimating new brown coal generation projects.
**NewBrownCoal_MW**		23376 x 1 double
This field contains the half hourly total output (MW) of any proxy brown coal power stations that will be used for estimating new brown coal generation projects. The half hourly profile is across the reference period, which is 1-Jan-2017 to when the “simulate_SpotPriceSensitivity_VIC_YYYYMMDD.m” script was run, in this case, 3-May-2018. Each column represents the output from one proxy brown coal power station.
**Output**			210672 x 4 x 1000 double
This field contains the simulated half hourly output (MW) of existing generation units grouped by fuel type technologies, across the simulation period. The 4 columns in the 2nd dimension corresponds to the 4 fuel types respectively: gas, brown coal, hydro and wind. The 1000 “columns” in the 3rd dimension correspond to the one thousand simulation runs.
**SolarPV**			210672 x 1000 double
This field contains the simulated half hourly output (MW) of existing rooftop solar PV across the simulation period. Each of the 1000 columns correspond to one simulation run.
**Retire_Output**		210672 x 1000 double
This field contains the simulated half hourly output (MW) of any retiring power station across the simulation period. Each of the 1000 columns correspond to one simulation run.
**NewBrownCoal_Output**	210672 x 1000 double
This field contains the simulated half hourly output (MW) of any proxy brown coal power station across the simulation period. Each of the 1000 columns correspond to one simulation run.


## **PV**
This variable is a MATLAB structure array with fields related to generation from rooftop solar PV installations that came online after 1-Jan-2018. The variable is created from running the simulate_RooftopSolar_VIC.m file.
**DS**	1 x 4389 double
This field contains the daily date stamp of the simulation period from 1-Jan-2019 to 7-Jan-2031 in MATLAB’s datenum format.
**DV**	4389 x 6 double
This field contains the daily date vector of the simulation period from 1-Jan-2019 to 7-Jan-2031 in MATLAB’s datevec format.
**Output**		210672 x 1000 double
This field contains the half hourly generation profile (MW) of rooftop solar PV in VIC that were installed after 1-Jan-2018. Each column represents data from one simulation run.
**ScalingMatrix**	210672 x 1 double
This field contains the half hourly scaling factor used to multiply a normalised 1MW profile to the forecasted capacity of rooftop solar PV installed in VIC, as forecasted by AEMO. A yearly capacity forecast figure is smoothed over 365 days to produce a gradually increasing installed capacity through the forecast period.
