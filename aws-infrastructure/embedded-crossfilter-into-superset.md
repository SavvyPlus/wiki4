<!-- TITLE: Embedded Crossfilter Into Superset -->
<!-- SUBTITLE: A quick summary of Embedded Crossfilter Into Superset -->

# Embedded Crossfilter into Superset
## 1. Add Packages into Superset environment.
 __DC.JS__ is a great library which has implemented lots of charts which integrated with Crossfilter.JS. See [examples](http://dc-js.github.io/dc.js/examples/) from __DC.JS__.

Under folder `'superset_home'/superset/assets`, open file __package.json__. Add 
```javascript
"dc": "^3.0",
"crossfilter": "^1.3.12"
```
into the __dependencies__ section

---
## 2. Add new visualization page into superset
Under folder `'superset_home'/superset/assets/src/visualization`, create new file __DC_Crossfilter.js__. In __DC_Crossfilter.js__, add these into the file:

```jsx
import dc from 'dc';
import crossfilter from 'crossfilter'

function DC_CrossfilterVis(slice, payload) {

    const div = d3.select(slice.selector);

    const sliceId = 'dc_crossfilter_' + slice.formData.slice_id;

// Constucting the html page
    const html = '\
\<div id=' + sliceId + ' style="width:' + slice.width() + 'px;height:' + slice.height() + 'px;">\
\<div class="col-md-6">\
  <div id="chart-ring-year" style="width:100%; height:330px">\
    <div class="reset" style="visibility: hidden;">selected: <span class="filter"></span>\
      <a href="javascript:yearRingChart.filterAll();dc.redrawAll();">reset</a>\
    </div>\
  </div>\
  \</div>\
  \<div class="col-md-6">\
  <div id="chart-hist-spend" style="width:100%; height:330px">\
    <div class="reset" style="visibility: hidden;">range: <span class="filter"></span>\
      <a href="javascript:spendHistChart.filterAll();dc.redrawAll();">reset</a>\
    </div>\
  </div>\
  \</div>\
  <div class="col-md-6">\
  <div id="chart-row-spenders" style="width:100%; height:330px">\
    <div class="reset" style="visibility: hidden;">selected: <span class="filter"></span>\
      <a href="javascript:spenderRowChart.filterAll();dc.redrawAll();">reset</a>\
    </div>\
  </div>\
  \ </div>\
  <!-- not sure why all these styles necessary, not the point of this -->\
  \<div class="col-md-6">\
  <div style="clear: both; margin: 30px; float: left">\
    <div id="table" style="width:100%; height:100%"></div>\
    <div id="download-type" style="clear: both; float: left">\
      <div><label><input type=radio name="operation" value="raw" checked="true">&nbsp;all data</label></div>\
      <div><label><input type=radio name="operation" value="table">&nbsp;table data</label></div>\
    </div>\
  </div>\
  \</div>\
</div>';

    div.html(html); // reset

    // initialise charts
    var yearRingChart = dc.pieChart('#chart-ring-year'),
        spendHistChart = dc.barChart('#chart-hist-spend'),
        spenderRowChart = dc.rowChart('#chart-row-spenders');
    var table = dc.dataTable('#table');
    
    // fetch the data from payload
    var spendData = payload.data;

    // set crossfilter
    var ndx = crossfilter(spendData),
        yearDim = ndx.dimension(function (d) {
            return +d.Year;
        }),
        spendDim = ndx.dimension(function (d) {
            return Math.floor(d.Spent / 10);
        }),
        nameDim = ndx.dimension(function (d) {
            return d.Name;
        }),
        spendPerYear = yearDim.group().reduceSum(function (d) {
            return +d.Spent;
        }),
        spendPerName = nameDim.group().reduceSum(function (d) {
            return +d.Spent;
        }),
        spendHist = spendDim.group().reduceCount();
    yearRingChart
        .width(300)
        .height(300)
        .dimension(yearDim)
        .group(spendPerYear)
        .innerRadius(50)
        .controlsUseVisibility(true);
    spendHistChart
        .dimension(spendDim)
        .group(spendHist)
        .x(d3.scale.linear().domain([0,10]))
        .elasticY(true)
        .controlsUseVisibility(true);
    spendHistChart.xAxis().tickFormat(function (d) {
        return d * 10
    }); // convert back to base unit
    spendHistChart.yAxis().ticks(2);
    spenderRowChart
        .dimension(nameDim)
        .group(spendPerName)
        .elasticX(true)
        .controlsUseVisibility(true);
    var allDollars = ndx.groupAll().reduceSum(function (d) {
        return +d.Spent;
    });
    table
        .dimension(spendDim)
        .group(function (d) {
            return d.value;
        })
        .sortBy(function (d) {
            return +d.Spent;
        })
        .showGroups(false)
        .columns(['Name',
            {
                label: 'Spent',
                format: function (d) {
                    return '$' + d.Spent;
                }
            },
            'Year',
            {
                label: 'Percent of Total',
                format: function (d) {
                    return Math.floor((d.Spent / allDollars.value()) * 100) + '%';
                }
            }]);

    dc.renderAll();
}

// exports module
module.exports = DC_CrossfilterVis;
```
---
## 3. Add new type into __vizMap__.
Under folder `'superset_home'/superset/assets/src/visualization`, open file __index.js__, add new type into __VIZ_TYPES__:
```javascript
dc_crossfilter: 'dc_crossfilter'
```
then add new reference into __vizMap__:
```javascript
[VIZ_TYPES.dc_crossfilter]: require('./DC_Crossfilter')
```
---
## 4. Add query configuration of the new visualization type
Under `'superset_home'/superset/assets/src/explore` , open file __visTypes.js__, add the new type's configuration:
```javascript
dc_crossfilter: {
    label: t('DC_Crossfilter Example'),
    showOnExplore: true,
    controlPanelSections: [
      {
        label: t('Query'),
        expanded: true,
        controlSetRows: [
          ['metrics', 'groupby'],
          ['limit'],
        ],
      },
      {
        label: t('Chart Options'),
        controlSetRows: [
          ['color_scheme'],
        ],
      },
    ],
  },
```
---
## 5. Add new data model of the new type.
Under folder `'superset_home'/superset`, open file __viz.py__,
add the new data model into the file:
```python
class DCCrossfilterViz(BaseViz):
    """ Funnel Chart"""
    viz_type = 'dc_crossfilter'
    is_timeseries = False

    def get_data(self, df):
        fd = self.form_data
        df = df.reset_index()
        df.columns = ['Spent','Name',  'Year']
        s = df.to_dict(orient='records')
        return s
```
---
## Notes:
After adding all these changes, run command
```
npm run dev
```
under folder `'superset_home'/superset/assests` to load changes.