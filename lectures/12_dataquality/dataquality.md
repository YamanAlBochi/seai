---
author: Christian Kaestner and Eunsuk Kang
title: "17-645: Data Quality"
semester: Fall 2022
footer: "17-645 Machine Learning in Production • Nadia Nahar / Christian Kaestner, Carnegie Mellon University • Fall 2022"
license: Creative Commons Attribution 4.0 International (CC BY 4.0)
---
<!-- .element: class="titleslide"  data-background="../_chapterimg/12_dataquality.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production


# Data Quality

<!-- image: https://pixabay.com/photos/high-level-rack-warehouse-range-408222/-->


---
## More Quality Assurance...

![Overview of course content](../_assets/overview.svg)
<!-- .element: class="plain stretch" -->



----
## Readings

Required reading:
* Sambasivan, N., Kapania, S., Highfill, H., Akrong, D., Paritosh, P., & Aroyo, L. M. (2021, May). “[Everyone wants to do the model work, not the data work”: Data Cascades in High-Stakes AI](https://dl.acm.org/doi/abs/10.1145/3411764.3445518). In Proc. Conference on Human Factors in Computing Systems (pp. 1-15).



Recommended reading: 
* Schelter, S., et al. [Automating large-scale data quality verification](http://www.vldb.org/pvldb/vol11/p1781-schelter.pdf). Proceedings of the VLDB Endowment, 11(12), pp.1781-1794.



----

## Learning Goals

* Distinguish precision and accuracy; understanding the better models vs more data tradeoffs
* Use schema languages to enforce data schemas
* Design and implement automated quality assurance steps that check data schema conformance and distributions 
* Devise infrastructure for detecting data drift and schema violations
* Consider data quality as part of a system; design an organization that values data quality


---

# Data-Quality Challenges

----

> Data cleaning and repairing account for about 60% of the work of data scientists.


**Own experience?**


<!-- references -->
Quote: Gil Press. “[Cleaning Big Data: Most Time-Consuming, Least Enjoyable Data Science Task, Survey Says](https://www.forbes.com/sites/gilpress/2016/03/23/data-preparation-most-time-consuming-least-enjoyable-data-science-task-survey-says/).” Forbes Magazine, 2016.


----
## Case Study: Inventory Management

![Shelves in a warehouse](warehouse.jpg)
<!-- .element: class="stretch" -->


----
## Data Comes from Many Sources

Manually entered

Actions from IT systems

Logging information, traces of user interactions

Sensor data

Crowdsourced 


----
## Many Data Sources

<svg id="mermaid1" width="100%" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" height="300.4444580078125" style="max-width: 974.0121459960938px;" viewBox="0 0.0000019073486328125 974.0121459960938 300.4444580078125"><style>#mermaid1 {font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid1 .error-icon{fill:#552222;}#mermaid1 .error-text{fill:#552222;stroke:#552222;}#mermaid1 .edge-thickness-normal{stroke-width:2px;}#mermaid1 .edge-thickness-thick{stroke-width:3.5px;}#mermaid1 .edge-pattern-solid{stroke-dasharray:0;}#mermaid1 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid1 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid1 .marker{fill:#333333;stroke:#333333;}#mermaid1 .marker.cross{stroke:#333333;}#mermaid1 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid1 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid1 .cluster-label text{fill:#333;}#mermaid1 .cluster-label span{color:#333;}#mermaid1 .label text,#mermaid1 span{fill:#333;color:#333;}#mermaid1 .node rect,#mermaid1 .node circle,#mermaid1 .node ellipse,#mermaid1 .node polygon,#mermaid1 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid1 .node .label{text-align:center;}#mermaid1 .node.clickable{cursor:pointer;}#mermaid1 .arrowheadPath{fill:#333333;}#mermaid1 .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid1 .flowchart-link{stroke:#333333;fill:none;}#mermaid1 .edgeLabel{background-color:#e8e8e8;text-align:center;}#mermaid1 .edgeLabel rect{opacity:0.5;background-color:#e8e8e8;fill:#e8e8e8;}#mermaid1 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid1 .cluster text{fill:#333;}#mermaid1 .cluster span{color:#333;}#mermaid1 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid1 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}</style><g><g class="output"><g class="clusters"></g><g class="edgePaths"><g class="edgePath LS-Twitter LE-SalesTrends" style="opacity: 1;" id="L-Twitter-SalesTrends"><path class="path" d="M41.55034637451172,44.0069465637207L41.55034637451172,48.17361323038737C41.55034637451172,52.34027989705404,41.55034637451172,60.67361323038737,48.17041761636077,69.0069465637207C54.790488858209834,77.34027989705403,68.03063134190793,85.67361323038737,74.650702583757,89.84027989705403L81.27077382560604,94.0069465637207" marker-end="url(#arrowhead18)" style="fill:none"></path><defs><marker id="arrowhead18" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-AdNetworks LE-SalesTrends" style="opacity: 1;" id="L-AdNetworks-SalesTrends"><path class="path" d="M178.19965362548828,44.0069465637207L178.19965362548828,48.17361323038737C178.19965362548828,52.34027989705404,178.19965362548828,60.67361323038737,171.57958238363923,69.0069465637207C164.95951114179016,77.34027989705403,151.71936865809207,85.67361323038737,145.09929741624302,89.84027989705403L138.47922617439397,94.0069465637207" marker-end="url(#arrowhead19)" style="fill:none"></path><defs><marker id="arrowhead19" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-SalesTrends LE-Prediction" style="opacity: 1;" id="L-SalesTrends-Prediction"><path class="path" d="M109.875,130.0138931274414L109.875,134.18055979410806C109.875,138.34722646077475,109.875,146.68055979410806,166.44622099680836,162.49383973114013C223.0174419936167,178.3071196681722,336.1598839872334,201.600346208903,392.7311049840417,213.24695947926838L449.30232598085007,224.8935727496338" marker-end="url(#arrowhead20)" style="fill:none"></path><defs><marker id="arrowhead20" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-VendorSales LE-Prediction" style="opacity: 1;" id="L-VendorSales-Prediction"><path class="path" d="M269.80555725097656,130.0138931274414L269.80555725097656,134.18055979410806C269.80555725097656,138.34722646077475,269.80555725097656,146.68055979410806,300.0449251591014,161.31758370019978C330.28429306722626,175.9546076062915,390.76302888347595,196.89532208514163,421.0023967916008,207.36567932456668L451.24176469972565,217.83603656399174" marker-end="url(#arrowhead21)" style="fill:none"></path><defs><marker id="arrowhead21" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-ProductData LE-Prediction" style="opacity: 1;" id="L-ProductData-Prediction"><path class="path" d="M429.5885467529297,130.0138931274414L429.5885467529297,134.18055979410806C429.5885467529297,138.34722646077475,429.5885467529297,146.68055979410806,435.70485924925265,157.49039096221438C441.82117174557567,168.30022213032066,454.0537967382217,181.58655113319992,460.17010923454467,188.22971563463955L466.28642173086763,194.87288013607917" marker-end="url(#arrowhead22)" style="fill:none"></path><defs><marker id="arrowhead22" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-Marketing LE-Prediction" style="opacity: 1;" id="L-Marketing-Prediction"><path class="path" d="M579.1371612548828,130.0138931274414L579.1371612548828,134.18055979410806C579.1371612548828,138.34722646077475,579.1371612548828,146.68055979410806,573.0208487585599,157.49039096221438C566.9045362622369,168.30022213032066,554.6719112695909,181.58655113319992,548.5555987732679,188.22971563463955L542.4392862769449,194.87288013607917" marker-end="url(#arrowhead23)" style="fill:none"></path><defs><marker id="arrowhead23" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-Theft LE-Prediction" style="opacity: 1;" id="L-Theft-Prediction"><path class="path" d="M749.1284828186035,130.0138931274414L749.1284828186035,134.18055979410806C749.1284828186035,138.34722646077475,749.1284828186035,146.68055979410806,717.2266872301142,161.43250851168727C685.324891641625,176.18445722926649,621.5213004646463,197.3550213310915,589.619504876157,207.94030338200403L557.7177092876676,218.52558543291656" marker-end="url(#arrowhead24)" style="fill:none"></path><defs><marker id="arrowhead24" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-PastSales LE-Prediction" style="opacity: 1;" id="L-PastSales-Prediction"><path class="path" d="M920.0139007568359,130.0138931274414L920.0139007568359,134.18055979410806C920.0139007568359,138.34722646077475,920.0139007568359,146.68055979410806,859.9340521287166,162.58640451464422C799.8542035005972,178.49224923518037,679.6945062443584,201.97060534291936,619.6146576162391,213.70978339678882L559.5348089881197,225.44896145065835" marker-end="url(#arrowhead25)" style="fill:none"></path><defs><marker id="arrowhead25" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g></g><g class="edgeLabels"><g class="edgeLabel" style="opacity: 1;" transform=""><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-Twitter-SalesTrends" class="edgeLabel L-LS-Twitter' L-LE-SalesTrends"></span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform=""><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-AdNetworks-SalesTrends" class="edgeLabel L-LS-AdNetworks' L-LE-SalesTrends"></span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform=""><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-SalesTrends-Prediction" class="edgeLabel L-LS-SalesTrends' L-LE-Prediction"></span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform=""><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-VendorSales-Prediction" class="edgeLabel L-LS-VendorSales' L-LE-Prediction"></span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform=""><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-ProductData-Prediction" class="edgeLabel L-LS-ProductData' L-LE-Prediction"></span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform=""><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-Marketing-Prediction" class="edgeLabel L-LS-Marketing' L-LE-Prediction"></span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform=""><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-Theft-Prediction" class="edgeLabel L-LS-Theft' L-LE-Prediction"></span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform=""><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-PastSales-Prediction" class="edgeLabel L-LS-PastSales' L-LE-Prediction"></span></div></foreignObject></g></g></g><g class="nodes"><g class="node default" style="opacity: 1;" id="flowchart-Twitter-16" transform="translate(41.55034637451172,26.00347328186035)"><rect rx="0" ry="0" x="-33.55034828186035" y="-18.003472328186035" width="67.1006965637207" height="36.00694465637207" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-23.55034828186035,-8.003472328186035)"><foreignObject width="47.1006965637207" height="16.00694465637207"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Twitter</div></foreignObject></g></g></g><g class="node default" style="opacity: 1;" id="flowchart-SalesTrends-17" transform="translate(109.875,112.01041984558105)"><rect rx="0" ry="0" x="-54.59201431274414" y="-18.003472328186035" width="109.18402862548828" height="36.00694465637207" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-44.59201431274414,-8.003472328186035)"><foreignObject width="89.18402862548828" height="16.00694465637207"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">SalesTrends</div></foreignObject></g></g></g><g class="node default" style="opacity: 1;" id="flowchart-AdNetworks-18" transform="translate(178.19965362548828,26.00347328186035)"><rect rx="0" ry="0" x="-53.098960876464844" y="-18.003472328186035" width="106.19792175292969" height="36.00694465637207" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-43.098960876464844,-8.003472328186035)"><foreignObject width="86.19792175292969" height="16.00694465637207"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">AdNetworks</div></foreignObject></g></g></g><g class="node default" style="opacity: 1;" id="flowchart-Prediction-21" transform="translate(504.36285400390625,236.2291717529297)"><circle x="-56.21527862548828" y="-18.003472328186035" r="56.21527862548828" class="label-container"></circle><g class="label" transform="translate(0,0)"><g transform="translate(-46.21527862548828,-8.003472328186035)"><foreignObject width="92.43055725097656" height="16.00694465637207"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Inventory ML</div></foreignObject></g></g></g><g class="node default" style="opacity: 1;" id="flowchart-VendorSales-22" transform="translate(269.80555725097656,112.01041984558105)"><rect rx="0" ry="0" x="-55.33854293823242" y="-18.003472328186035" width="110.67708587646484" height="36.00694465637207" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-45.33854293823242,-8.003472328186035)"><foreignObject width="90.67708587646484" height="16.00694465637207"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">VendorSales</div></foreignObject></g></g></g><g class="node default" style="opacity: 1;" id="flowchart-ProductData-24" transform="translate(429.5885467529297,112.01041984558105)"><rect rx="0" ry="0" x="-54.4444465637207" y="-18.003472328186035" width="108.8888931274414" height="36.00694465637207" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-44.4444465637207,-8.003472328186035)"><foreignObject width="88.8888931274414" height="16.00694465637207"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">ProductData</div></foreignObject></g></g></g><g class="node default" style="opacity: 1;" id="flowchart-Marketing-26" transform="translate(579.1371612548828,112.01041984558105)"><rect rx="0" ry="0" x="-45.10416793823242" y="-18.003472328186035" width="90.20833587646484" height="36.00694465637207" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-35.10416793823242,-8.003472328186035)"><foreignObject width="70.20833587646484" height="16.00694465637207"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Marketing</div></foreignObject></g></g></g><g class="node default" style="opacity: 1;" id="flowchart-Theft-28" transform="translate(749.1284828186035,112.01041984558105)"><rect rx="0" ry="0" x="-74.88715362548828" y="-18.003472328186035" width="149.77430725097656" height="36.00694465637207" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-64.88715362548828,-8.003472328186035)"><foreignObject width="129.77430725097656" height="16.00694465637207"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Expired/Lost/Theft</div></foreignObject></g></g></g><g class="node default" style="opacity: 1;" id="flowchart-PastSales-30" transform="translate(920.0139007568359,112.01041984558105)"><rect rx="0" ry="0" x="-45.99826431274414" y="-18.003472328186035" width="91.99652862548828" height="36.00694465637207" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-35.99826431274414,-8.003472328186035)"><foreignObject width="71.99652862548828" height="16.00694465637207"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">PastSales</div></foreignObject></g></g></g></g></g></g></svg>

*sources of different reliability and quality*


----
## Inventory Database

<div class="smallish">

Product Database:

| ID | Name | Weight | Description | Size | Vendor |
| - |  - |  - |  - |  - | - | 
| ... |  ... |  ... |  ... |  ... |  ... | 

Stock:

| ProductID | Location | Quantity |
| - |  - |  - |
| ... |  ... |  ... |

Sales history:

| UserID | ProductId | DateTime | Quantity | Price | 
| - |  - |  - | - |- |
| ... |  ... |  ... |... |... |

</div>

----
## *Raw Data* is an Oxymoron

![shipment receipt form](shipment-delivery-receipt.jpg)
<!-- .element: class="stretch" -->



<!-- references_ -->
Recommended Reading: Gitelman, Lisa, Virginia Jackson, Daniel Rosenberg, Travis D. Williams, Kevin R. Brine, Mary Poovey, Matthew Stanley et al. "[Data bite man: The work of sustaining a long-term study](https://ieeexplore.ieee.org/abstract/document/6462156)." In "Raw Data" Is an Oxymoron, (2013), MIT Press: 147-166.

----
## What makes good quality data?

**Accuracy:** The data was recorded correctly.

**Completeness:** All relevant data was recorded.

**Uniqueness:** The entries are recorded once.

**Consistency:** The data agrees with itself.

**Timeliness:** The data is kept up to date.

----
## Data is noisy

Unreliable sensors or data entry

Wrong results and computations, crashes

Duplicate data, near-duplicate data

Out of order data

Data format invalid

**Examples in inventory system?**

----
## Data changes

System objective changes over time

Software components are upgraded or replaced

Prediction models change

Quality of supplied data changes

User behavior changes

Assumptions about the environment no longer hold

**Examples in inventory system?**

----
## Users may deliberately change data

Users react to model output

Users try to game/deceive the model

**Examples in inventory system?**

----
## Accuracy vs Precision

<!-- colstart -->

Accuracy: Reported values (on average) represent real value

Precision: Repeated measurements yield the same result

Accurate, but imprecise: Average over multiple measurements

Inaccurate, but precise: ?

<!-- col -->


![Accuracy-vs-precision visualized](Accuracy_and_Precision.svg)<!-- .element: style="width:400px" -->


<!-- colend -->

<!-- references_ -->
(CC-BY-4.0 by [Arbeck](https://commons.wikimedia.org/wiki/File:Accuracy_and_Precision.svg))


----

## Accuracy and Precision in Warehouse Data?

![Shelves in a warehouse](warehouse.jpg)
<!-- .element: class="stretch" -->


----
## Data Quality and Machine Learning

More data -> better models (up to a point, diminishing effects)

Noisy data (imprecise) -> less confident models, more data needed 
  * some ML techniques are more or less robust to noise (more on robustness in a later lecture)

Inaccurate data -> misleading models, biased models
 
-> Need the "right" data

-> Invest in data quality, not just quantity


---
# Poor Data Quality has Consequences

(often delayed consequences)

----
## Example: Systematic bias in labeling

Poor data quality leads to poor models

*Not detectable in offline evaluation*

Problem in production -- now difficult to correct

![Newspaper report on canceled amazon hiring project](amazon-hiring.png)

----
## Delayed Fixes increase Repair Cost

![Cost of bug repair depending on when the bug was introduced and fixed](defectcost.jpg)


----
## Data Cascades

![Data cascades figure](datacascades.png)

Detection almost always delayed! Expensive rework.
Difficult to detect in offline evaluation.

<!-- references -->
Sambasivan, N., et al. (2021, May). “[Everyone wants to do the model work, not the data work”: Data Cascades in High-Stakes AI](https://dl.acm.org/doi/abs/10.1145/3411764.3445518). In Proc. CHI (pp. 1-15).






---

# Data Schema

Ensuring basic consistency about shape and types


----
## Dirty Data: Example

![Dirty data](dirty-data-example.jpg)
<!-- .element: class="plain" -->

*Problems with this data?*




----
## Schema Problems: Uniqueness, data format, integrity, ...

* Illegal attribute values: `bdate=30.13.70`
* Violated attribute dependencies: `age=22, bdate=12.02.70`
* Uniqueness violation: `(name=”John Smith”, SSN=”123456”), (name=”Peter Miller”, SSN=”123456”)`
* Referential integrity violation: `emp=(name=”John Smith”, deptno=127)` if department 127 not defined

<!-- references -->

Further readings: Rahm, Erhard, and Hong Hai Do. [Data cleaning: Problems and current approaches](http://dc-pubs.dbs.uni-leipzig.de/files/Rahm2000DataCleaningProblemsand.pdf). IEEE Data Eng. Bull. 23.4 (2000): 3-13.




----
## Data Schema

Define expected format of data
  * expected fields and their types
  * expected ranges for values
  * constraints among values (within and across sources)

Data can be automatically checked against schema

Protects against change; explicit interface between components



----
## Schema in Relational Databases

```sql
CREATE TABLE employees (
    emp_no      INT             NOT NULL,
    birth_date  DATE            NOT NULL,
    name        VARCHAR(30)     NOT NULL,
    PRIMARY KEY (emp_no));
CREATE TABLE departments (
    dept_no     CHAR(4)         NOT NULL,
    dept_name   VARCHAR(40)     NOT NULL,
    PRIMARY KEY (dept_no), UNIQUE  KEY (dept_name));
CREATE TABLE dept_manager (
   dept_no      CHAR(4)         NOT NULL,
   emp_no       INT             NOT NULL,
   FOREIGN KEY (emp_no)  REFERENCES employees (emp_no),
   FOREIGN KEY (dept_no) REFERENCES departments (dept_no),
   PRIMARY KEY (emp_no,dept_no)); 
```


----
## Which Problems are Schema Problems?

![Dirty data](dirty-data-example.jpg)
<!-- .element: class="plain" -->




----
## What Happens When new Data Violates Schema?

<!-- discussion -->

----
## Schema-Less Data Exchange

* CSV files
* Key-value stores (JSon, XML, Nosql databases)
* Message brokers
* REST API calls
* R/Pandas Dataframes

```
2022-10-06T01:31:18,230550,GET /rate/narc+2002=4
2022-10-06T01:31:19,332644,GET /rate/i+am+love+2009=4
```

```json
{"user_id":5,"age":26,"occupation":"scientist","gender":"M"}
```

----
## Schema Library: Apache Avro

```json
{   "type": "record",
    "namespace": "com.example",
    "name": "Customer",
    "fields": [{
            "name": "first_name",
            "type": "string",
            "doc": "First Name of Customer"
        },        
        {
            "name": "age",
            "type": "int",
            "doc": "Age at the time of registration"
        }
    ]
}
```

----
## Schema Library: Apache Avro

<div class="smallish">

<!-- colstart -->

Schema specification in JSON format

Serialization and deserialization with automated checking

Native support in Kafka

<!-- col -->

Benefits
  * Serialization in space efficient format
  * APIs for most languages (ORM-like)
  * Versioning constraints on schemas

Drawbacks
  * Reading/writing overhead
  * Binary data format, extra tools needed for reading
  * Requires external schema and maintenance
  * Learning overhead

<!-- colend -->

</div>

Notes: Further readings eg https://medium.com/@stephane.maarek/introduction-to-schemas-in-apache-kafka-with-the-confluent-schema-registry-3bf55e401321, https://www.confluent.io/blog/avro-kafka-data/, https://avro.apache.org/docs/current/

----
## Many Schema Libraries/Formats

Examples
* Avro
* XML Schema
* Protobuf
* Thrift
* Parquet
* ORC

----
## Discussion: Data Schema Constraints for Inventory System?

<div class="small">

Product Database:

| ID | Name | Weight | Description | Size | Vendor |
| - |  - |  - |  - |  - | - | 
| ... |  ... |  ... |  ... |  ... |  ... | 

Stock:

| ProductID | Location | Quantity |
| - |  - |  - |
| ... |  ... |  ... |

Sales history:

| UserID | ProductId | DateTime | Quantity | Price | 
| - |  - |  - | - |- |
| ... |  ... |  ... |... |... |

</div>

----
## Summary: Schema 

Basic structure and type definition of data

Well supported in databases and many tools

*Very low bar of data quality*









---
# Instance-Level Problems

Inconsistencies, wrong values


----
## Dirty Data: Example

![Dirty data](dirty-data-example.jpg)
<!-- .element: class="plain" -->

*Problems with the data beyond schema problems?*


----
## Instance-Level Problems


* Missing values: `phone=9999-999999`
* Misspellings: `city=Pittsburg`
* Misfielded values: `city=USA`
* Duplicate records: `name=John Smith, name=J. Smith`
* Wrong reference: `emp=(name=”John Smith”, deptno=127)` if department 127 defined but wrong

**Can we detect these?**


<!-- references -->

Further readings: Rahm, Erhard, and Hong Hai Do. [Data cleaning: Problems and current approaches](http://dc-pubs.dbs.uni-leipzig.de/files/Rahm2000DataCleaningProblemsand.pdf). IEEE Data Eng. Bull. 23.4 (2000): 3-13.


----
## Discussion: Instance-Level Problems?

![Shelves in a warehouse](warehouse.jpg)
<!-- .element: class="stretch" -->


----
## Data Cleaning Overview

Data analysis / Error detection
  * Usually focused on specific kind of problems, e.g., duplication, typos, missing values, distribution shift
  * Detection in input data vs detection in later stages (more context)

Error repair
  * Repair data vs repair rules, one at a time or holistic
  * Data transformation or mapping
  * Automated vs human guided

----
## Error Detection Examples

Illegal values: min, max, variance, deviations, cardinality

Misspelling: sorting + manual inspection, dictionary lookup

Missing values: null values, default values

Duplication: sorting, edit distance, normalization

----
## Error Detection: Example

![Dirty data](dirty-data-example.jpg)
<!-- .element: class="plain" -->

*Can we (automatically) detect instance-level problems? Which problems are domain-specific?*


----
## Example Tool: Great Expectations

```python
expect_column_values_to_be_between(
    column="passenger_count",
    min_value=1,
    max_value=6
)
```

Supports schema validation and custom instance-level checks.

<!-- references -->
https://greatexpectations.io/


----
## Example Tool: Great Expectations

![Great expectations screenshot](greatexpectations.png)
<!-- .element: class="stretch" -->


<!-- references_ -->
https://greatexpectations.io/


----
## Data Quality Rules

Invariants on data that must hold

Typically about relationships of multiple attributes or data sources, eg.
  - ZIP code and city name should correspond
  - User ID should refer to existing user
  - SSN should be unique
  - For two people in the same state, the person with the lower income should not have the higher tax rate

Classic integrity constraints in databases or conditional constraints

*Rules can be used to reject data or repair it*

----
## ML for Detecting Inconsistencies

![Data Inconsistency Examples](errors_chicago.jpg)
<!-- .element: class="plain stretch" -->

<!-- references_ -->
Image source: Theo Rekatsinas, Ihab Ilyas, and Chris Ré, “[HoloClean - Weakly Supervised Data Repairing](https://dawn.cs.stanford.edu/2017/05/12/holoclean/).” Blog, 2017.

----
## Example: HoloClean

![HoloClean](holoclean.jpg)
<!-- .element: class="stretch" -->

<div class="small">

* User provides rules as integrity constraints (e.g., "two entries with the same
name can't have different city")
* Detect violations of the rules in the data; also detect statistical outliers
* Automatically generate repair candidates (with probabilities)
</div>

<!-- references_ -->
Image source: Theo Rekatsinas, Ihab Ilyas, and Chris Ré, “[HoloClean - Weakly Supervised Data Repairing](https://dawn.cs.stanford.edu/2017/05/12/holoclean/).” Blog, 2017.

----
## Discovery of Data Quality Rules

<div class="small">

  <!-- colstart -->

Rules directly taken from external databases
  * e.g. zip code directory

Given clean data, 
  * several algorithms that find functional relationships ($X\Rightarrow Y$) among columns
  * algorithms that find conditional relationships (if $Z$ then $X\Rightarrow Y$)
  * algorithms that find denial constraints ($X$ and $Y$ cannot cooccur in a row)

<!-- col -->
Given mostly clean data (probabilistic view),
  * algorithms to find likely rules (e.g., association rule mining)
  * outlier and anomaly detection

Given labeled dirty data or user feedback,
  * supervised and active learning to learn and revise rules
  * supervised learning to learn repairs (e.g., spell checking)
<!-- colend -->
</div>

<!-- references -->

Further reading: Ilyas, Ihab F., and Xu Chu. [Data cleaning](https://dl.acm.org/doi/book/10.1145/3310205). Morgan & Claypool, 2019.

----
## Excursion: Association rule mining

<div class="smallish">

* Sale 1: Bread, Milk
* Sale 2: Bread, Diaper, Beer, Eggs
* Sale 3: Milk, Diaper, Beer, Coke
* Sale 4: Bread, Milk, Diaper, Beer
* Sale 5: Bread, Milk, Diaper, Coke

Rules
* {Diaper, Beer} -> Milk (40% support, 66% confidence)
* Milk -> {Diaper, Beer} (40% support, 50% confidence)
* {Diaper, Beer} -> Bread (40% support, 66% confidence)

*(also useful tool for exploratory data analysis)*

</div>

<!-- references -->
Further readings: Standard algorithms and many variations, see [Wikipedia](https://en.wikipedia.org/wiki/Association_rule_learning)


----
## Discussion: Data Quality Rules 

![Shelves in a warehouse](warehouse.jpg)
<!-- .element: class="stretch" -->
 













---

# Drift

----
## Monitoring for Changes

![Anomalo screenshot](anomalo.png)
<!-- .element: class="stretch" -->

<!-- references_ -->

https://www.anomalo.com/
----


## Drift & Model Decay

<div class="small">

**Concept drift** (or concept shift)
  * properties to predict change over time (e.g., what is credit card fraud)
  * model has not learned the relevant concepts
  * over time: different expected outputs for same inputs
  
**Data drift** (or covariate shift, distribution shift, or population drift)
  * characteristics of input data changes (e.g., customers with face masks)
  * input data differs from training data 
  * over time: predictions less confident, further from training data

**Upstream data changes**
  * external changes in data pipeline (e.g., format changes in weather service)
  * model interprets input data incorrectly
  * over time: abrupt changes due to faulty inputs

**How do we fix these drifts?**

</div>
Notes:
  * fix1: retrain with new training data or relabeled old training data
  * fix2: retrain with new data
  * fix3: fix pipeline, retrain entirely

----
## On Terminology

Concept and data drift are separate concepts

In practice and literature not always clearly distinguished

Colloquially encompasses all forms of model degradations and environment changes

Define term for target audience


![Random letters](../_assets/onterminology.jpg)<!-- .element: class="cornerimg" -->

----
## Breakout: Drift in the Inventory System

*What kind of drift might be expected?*

As a group, tagging members, write plausible examples in `#lecture`:

> * Concept Drift:
> * Data Drift:
> * Upstream data changes:


![Shelves in a warehouse](warehouse.jpg)
<!-- .element: class="stretch" -->





----
## Watch for Degradation in Prediction Accuracy

![Model Drift](model_drift.jpg)
<!-- .element: class="stretch" -->

<!-- references_ -->
Image source: Joel Thomas and Clemens Mewald. [Productionizing Machine Learning: From Deployment to Drift Detection](https://databricks.com/blog/2019/09/18/productionizing-machine-learning-from-deployment-to-drift-detection.html). Databricks Blog, 2019



----
## Indicators of Concept Drift

*How to detect concept drift in production?*

<!-- discussion -->

----
## Indicators of Concept Drift

Model degradations observed with telemetry

Telemetry indicates different outputs over time for similar inputs

Relabeling training data changes labels

Interpretable ML models indicate rules that no longer fit

*(many papers on this topic, typically on statistical detection)*

----
## Indicators of Data Drift

*How to detect data drift in production?*

<!-- discussion -->

----
## Indicators of Data Drift

Model degradations observed with telemetry

Distance between input distribution and training distribution increases

Average confidence of model predictions declines

Relabeling of training data retains stable labels


----
## Detecting Data Drift

* Compare distributions over time (e.g., t-test)
* Detect both sudden jumps and gradual changes
* Distributions can be manually specified or learned (see invariant detection)

<!-- colstart -->
![Two distributions](twodist.png)
<!-- col -->
![Time series with confidence intervals](timeseries.png)
<!-- colend -->


----
## Data Distribution Analysis

Plot distributions of features (histograms, density plots, kernel density estimation)
  - Identify which features drift

Define distance function between inputs and identify distance to closest training data (e.g., energy distance, see also kNN)

Anomaly detection and "out of distribution" detection

Compare distribution of output labels

----
## Data Distribution Analysis Example

https://rpubs.com/ablythe/520912


----
## Microsoft Azure Data Drift Dashboard

![Dashboard](drift-ui-expanded.png)

<!-- references -->
Image source and further readings: [Detect data drift (preview) on models deployed to Azure Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-monitor-datasets?tabs=python)


----
## Dealing with Drift

Regularly retrain model on recent data
  - Use evaluation in production to detect decaying model performance

Involve humans when increasing inconsistencies detected
  - Monitoring thresholds, automation

Monitoring, monitoring, monitoring!



----
## Breakout: Drift in the Inventory System

*What kind of monitoring for previously listed drift in Inventory scenario?*


![Shelves in a warehouse](warehouse.jpg)
<!-- .element: class="stretch" -->












---
# Data Quality is a System-Wide Concern

![](system.svg)
<!-- .element: class="plain stretch" -->

----

> "Everyone wants to do the model work, not the data work"

<!-- references -->
Sambasivan, N., Kapania, S., Highfill, H., Akrong, D., Paritosh, P., & Aroyo, L. M. (2021, May). “[Everyone wants to do the model work, not the data work”: Data Cascades in High-Stakes AI](https://dl.acm.org/doi/abs/10.1145/3411764.3445518). In Proceedings of the 2021 CHI Conference on Human Factors in Computing Systems (pp. 1-15).

----
## Data flows across components

![Transcription service example with labeling tool, user interface, database, pipeline etc](transcriptionarchitecture2.svg)
<!-- .element: class="plain stretch" -->


----
## Data Quality is a System-Wide Concern

Data flows across components, e.g., from user interface into database to crowd-sourced labeling team into ML pipeline

Documentation at the interfaces is important

Humans interacting with the system
* Entering data, labeling data
* Observed with sensors/telemetry
* Incentives, power structures, recognition

Organizational practices
* Value, attention, and resources given to data quality

----
## Data Quality Documentation

<div class="smallish">

Teams rarely document expectations of data quantity or quality

Data quality tests are rare, but some teams adopt defensive monitoring
* Local tests about assumed structure and distribution of data
* Identify drift early and reach out to producing teams

Several ideas for documenting distributions, including [Datasheets](https://dl.acm.org/doi/fullHtml/10.1145/3458723) and [Dataset Nutrition Label](https://arxiv.org/abs/1805.03677)
* Mostly focused on static datasets, describing origin, consideration, labeling procedure, and distributions; [Example](https://dl.acm.org/doi/10.1145/3458723#sec-supp)

</div>

<!-- references -->
🗎 Gebru, Timnit, et al. "[Datasheets for datasets](https://dl.acm.org/doi/fullHtml/10.1145/3458723)." Communications of the ACM 64, no. 12 (2021). <br />
🗎 Nahar, Nadia, et al. “[Collaboration Challenges in Building ML-Enabled Systems: Communication, Documentation, Engineering, and Process](https://arxiv.org/abs/2110.10234).” In Pro. ICSE, 2022.


----
## Common Data Cascades

<div class="smallish">

<!-- colstart -->
**Physical world brittleness**
* Idealized data, ignoring realities and change of real-world data
* Static data, one time learning mindset, no planning for evolution

**Inadequate domain expertise**
* Not understand. data and its context
* Involving experts only late for trouble shooting

<!-- col -->
**Conflicting reward systems**
* Missing incentives for data quality
* Not recognizing data quality importance, discard as technicality
* Missing data literacy with partners

**Poor (cross-org.) documentation**
* Conflicts at team/organization boundary
* Undetected drift

<!-- colend -->
</div>

<!-- references -->
Sambasivan, N., et al. (2021). “[Everyone wants to do the model work, not the data work”: Data Cascades in High-Stakes AI](https://dl.acm.org/doi/abs/10.1145/3411764.3445518). In Proc. Conference on Human Factors in Computing Systems.




----
## Discussion: Possible Data Cascades?

* Interacting with physical world brittleness
* Inadequate domain expertise
* Conflicting reward systems
* Poor (cross-organizational) documentation

![Shelves in a warehouse](warehouse.jpg)
<!-- .element: class="stretch" -->




----
## Ethics and Politics of Data

> Raw data is an oxymoron

<!-- discussion -->

----
## Incentives for Data Quality? Valuing Data Work?

<!-- discussion -->






<!-- 

-/--
# Quality Assurance for the Data Processing Pipelines

--/--
## Error Handling and Testing in Pipeline

Avoid silent failures!

* Write testable data acquisition and feature extraction code
* Test this code (unit test, positive and negative tests)
* Test retry mechanism for acquisition + error reporting
* Test correct detection and handling of invalid input
* Catch and report errors in feature extraction
* Test correct detection of data drift
* Test correct triggering of monitoring system
* Detect stale data, stale models

*More in a later lecture.*

 -->



---
# Bonus: Data Linter

<!-- references -->
Further readings: Nick Hynes, D. Sculley, Michael Terry. "[The Data Linter: Lightweight Automated Sanity Checking for ML Data Sets](http://learningsys.org/nips17/assets/papers/paper_19.pdf)."  NIPS Workshop on ML Systems (2017)

----
## Excursion: Static Analysis and Code Linters

*Automate routine inspection tasks*

```js
if (user.jobTitle = "manager") {
   ...
}
```

```js
function fn() {
    x = 1;
    return x;
    x = 3; // dead code
}
```

```java
PrintWriter log = null;
if (anyLogging) log = new PrintWriter(...);
if (detailedLogging) log.println("Log started");
```

----
## Static Analysis

* Analyzes possible executions of the code, without running it
* Different levels of sophistication
  * Simple heuristic and code patterns (linters)
  * Sound reasoning about all possible program executions
* Tradeoff between false positives and false negatives
* Often supporting annotations needed (e.g., `@Nullable`)
* Tools widely available, open source and commercial

----
## Static Analysis Example

![Eslint IDE integration](eslint.png)
<!-- .element: class="stretch" -->

----
## Static Analysis for Data Science Code

* Lots of research
* Style issues in Python
* Shape analysis of tensors in deep learning
* Analysis of flow of datasets to detect data leakage
* ...

<!-- references -->
Examples:
* Yang, Chenyang, et al.. "Data Leakage in Notebooks: Static Detection and Better Processes." Proc. ASE (2022).
* Lagouvardos, S. et al. (2020). Static analysis of shape in TensorFlow programs. In Proc. ECOOP.
* Wang, Jiawei, et al. "Better code, better sharing: on the need of analyzing jupyter notebooks." In Proc. ICSE-NIER. 2020.

----
## A Linter for Data?

<!-- discussion -->

----
## Data Linter at Google

<!-- colstart -->
**Miscoding**
   * Number, date, time as string
   * Enum as real
   * Tokenizable string (long strings, all unique)
   * Zip code as number

<!-- col -->
**Outliers and scaling**
   * Unnormalized feature (varies widely)
   * Tailed distributions
   * Uncommon sign

**Packaging**
   * Duplicate rows
   * Empty/missing data
<!-- colend -->
<!-- references -->
Further readings: Hynes, Nick, D. Sculley, and Michael Terry. [The data linter: Lightweight, automated sanity checking for ML data sets](http://learningsys.org/nips17/assets/papers/paper_19.pdf). NIPS MLSys Workshop. 2017.





---
# Summary

* Data from many sources, often inaccurate, imprecise, inconsistent, incomplete, ... -- many different forms of data quality problems 
* Many mechanisms for enforcing consistency and cleaning 
  * Data schema ensures format consistency
  * Data quality rules ensure invariants across data points
* Concept and data drift are key challenges -- monitor
* Data quality is a system-level concern
  * Data quality at the interface between components
  * Documentation and monitoring often poor
  * Involves organizational structures, incentives, ethics, ...

----
## Further Readings

<div class="smaller">

* Schelter, S., Lange, D., Schmidt, P., Celikel, M., Biessmann, F. and Grafberger, A., 2018. Automating large-scale data quality verification. Proceedings of the VLDB Endowment, 11(12), pp.1781-1794.
* Polyzotis, Neoklis, Martin Zinkevich, Sudip Roy, Eric Breck, and Steven Whang. "Data validation for machine learning." Proceedings of Machine Learning and Systems 1 (2019): 334-347.
* Polyzotis, Neoklis, Sudip Roy, Steven Euijong Whang, and Martin Zinkevich. 2017. “Data Management Challenges in Production Machine Learning.” In Proceedings of the 2017 ACM International Conference on Management of Data, 1723–26. ACM.
* Theo Rekatsinas, Ihab Ilyas, and Chris Ré, “HoloClean - Weakly Supervised Data Repairing.” Blog, 2017.
* Ilyas, Ihab F., and Xu Chu. Data cleaning. Morgan & Claypool, 2019.
* Moreno-Torres, Jose G., Troy Raeder, Rocío Alaiz-Rodríguez, Nitesh V. Chawla, and Francisco Herrera. "A unifying view on dataset shift in classification." Pattern recognition 45, no. 1 (2012): 521-530.
* Vogelsang, Andreas, and Markus Borg. "Requirements Engineering for Machine Learning: Perspectives from Data Scientists." In Proc. of the 6th International Workshop on Artificial Intelligence for Requirements Engineering (AIRE), 2019.
* Humbatova, Nargiz, Gunel Jahangirova, Gabriele Bavota, Vincenzo Riccio, Andrea Stocco, and Paolo Tonella. "Taxonomy of real faults in deep learning systems." In Proceedings of the ACM/IEEE 42nd International Conference on Software Engineering, pp. 1110-1121. 2020.


</div>