By Roberto Echieverria Sosa & Yue Hu 

## Introduction

Power outages leave millions of Americans in the dark each year, disrupting communities and critical infrastructure nationwide. To better understand the patterns and causes of these events, this project analyzes and visualizes major power outages across the United States. The U.S. Department of Energy defines a major outage as one affecting at least 50,000 customers or causing an unplanned firm load loss of 300 megawatts or more. Using a dataset compiled by Purdue University’s LASCI Lab, this analysis incorporates outage severity, geographic and temporal data, climate conditions, land-use features, electricity consumption patterns, and economic characteristics of affected states.

The primary research question driving this project is:
**What factors most significantly influence the duration of a power outage?**

Outage duration is a critical response variable, as prolonged outages are
associated with increased economic costs, reduced service reliability,
and heightened regulatory scrutiny. Identifying the key drivers of outage
duration can provide insight into system vulnerabilities and inform
strategies for improving grid resilience and operational efficiency.

## Dataset Summary

<p>The dataset consists of <strong>1,534 rows</strong>, each representing a distinct outage event. The following columns are particularly relevant to our analysis:</p>
<table>
  <thead>
    <tr>
      <th>Column Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'YEAR'</code></td>
      <td>Year an outage occurred</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'MONTH'</code></td>
      <td>Month an outage occurred</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'U.S._STATE'</code></td>
      <td>State where the outage occurred</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'NERC.REGION'</code></td>
      <td>North American Electric Reliability Corporation (NERC) region involved</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'CLIMATE.REGION'</code></td>
      <td>U.S. climate region (National Centers for Environmental Information, 9 regions)</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'ANOMALY.LEVEL'</code></td>
      <td>Oceanic El Niño/La Niña (ONI) index by season</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'OUTAGE.START.DATE'</code></td>
      <td>Day of the year when the outage started</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'OUTAGE.START.TIME'</code></td>
      <td>Time of day when the outage started</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'OUTAGE.RESTORATION.DATE'</code></td>
      <td>Day of the year when power was fully restored</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'OUTAGE.RESTORATION.TIME'</code></td>
      <td>Time of day when power was fully restored</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'CAUSE.CATEGORY'</code></td>
      <td>Category of event causing the major outage</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'OUTAGE.DURATION'</code></td>
      <td>Duration of the outage (minutes)</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'DEMAND.LOSS.MW'</code></td>
      <td>Peak demand lost during the outage (MW)</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'CUSTOMERS.AFFECTED'</code></td>
      <td>Number of customers affected</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'TOTAL.PRICE'</code></td>
      <td>Average monthly electricity price (cents per kWh)</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'TOTAL.SALES'</code></td>
      <td>Total electricity consumption (MWh)</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'TOTAL.CUSTOMERS'</code></td>
      <td>Annual total number of customers served</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'POPPCT_URBAN'</code></td>
      <td>Percentage of state population living in urban areas (%)</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'POPDEN_URBAN'</code></td>
      <td>Urban population density (persons per square mile)</td>
    </tr>
    <tr>
      <td><code class="language-plaintext highlighter-rouge">'AREAPCT_URBAN'</code></td>
      <td>Percentage of state land area classified as urban (%)</td>
    </tr>
  </tbody>
</table>

These features enables us to investigate climate-specific trends in outage severity and duration