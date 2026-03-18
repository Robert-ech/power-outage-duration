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

<p>The dataset consists of <strong>1,534 rows</strong>, each representing a distinct outage event and followed by 56 columns each representing an outage feature. The following columns are relevant to our analysis:</p>
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

## Data Cleaning & Exploratory Data Analysis

### Column Selection
The original 56 column dataset was filtered down to the 20 columns listed below, retaining only those relevant to outage duration prediction. The way we processed the columns was by running random forest on the features to calculate correlation to outage time and keeping the most relavant ones. We also kept features needed to test our predictions.

- **Temporal and geographic data:**  
  <code class="language-plaintext highlighter-rouge">'YEAR'</code>,
  <code class="language-plaintext highlighter-rouge">'MONTH'</code>,
  <code class="language-plaintext highlighter-rouge">'U.S._STATE'</code>,
  <code class="language-plaintext highlighter-rouge">'NERC.REGION'</code>,
  <code class="language-plaintext highlighter-rouge">'CLIMATE.REGION'</code>

- **Outage characteristics:**  
  <code class="language-plaintext highlighter-rouge">'CAUSE.CATEGORY'</code>,
  <code class="language-plaintext highlighter-rouge">'OUTAGE.DURATION'</code>,
  <code class="language-plaintext highlighter-rouge">'DEMAND.LOSS.MW'</code>,
  <code class="language-plaintext highlighter-rouge">'CUSTOMERS.AFFECTED'</code>

- **Climate:**  
  <code class="language-plaintext highlighter-rouge">'ANOMALY.LEVEL'</code>

- **Economic indicators:**  
  <code class="language-plaintext highlighter-rouge">'TOTAL.PRICE'</code>,
  <code class="language-plaintext highlighter-rouge">'TOTAL.SALES'</code>,
  <code class="language-plaintext highlighter-rouge">'TOTAL.CUSTOMERS'</code>

- **Urban demographics:**  
  <code class="language-plaintext highlighter-rouge">'POPPCT_URBAN'</code>,
  <code class="language-plaintext highlighter-rouge">'POPDEN_URBAN'</code>,
  <code class="language-plaintext highlighter-rouge">'AREAPCT_URBAN'</code>

- **Timestamps:**  
  <code class="language-plaintext highlighter-rouge">'OUTAGE.START.DATE'</code>,
  <code class="language-plaintext highlighter-rouge">'OUTAGE.START.TIME'</code>,
  <code class="language-plaintext highlighter-rouge">'OUTAGE.RESTORATION.DATE'</code>,
  <code class="language-plaintext highlighter-rouge">'OUTAGE.RESTORATION.TIME'</code>
---

### Datetime Combination
The two separate columns: 
<td><code class="language-plaintext highlighter-rouge">'OUTAGE.START.DATE'</code></td>   
<td><code class="language-plaintext highlighter-rouge">'OUTAGE.START.TIME'</code></td>  

We combined these columns into a single timestamp object to reduce redundancy. Ensuring outage start and end times were in their own unique column.

<td><code class="language-plaintext highlighter-rouge">'OUTAGE.START'</code></td>

The same process was applied to restoration time, creating:

<td><code class="language-plaintext highlighter-rouge">'OUTAGE.RESTORATION'</code></td>

The original four date/time columns were then removed.

---

### Zero to NaN Replacement

Zero values were replaced with NaN. A value of 0 in these fields likely indicates missing data rather than a true zero. For example a recorded major outage cannot realistically have zero duration or affect zero customers.

For the following columns:

<td><code class="language-plaintext highlighter-rouge">'OUTAGE.DURATION'</code></td>
<td><code class="language-plaintext highlighter-rouge">'CUSTOMERS.AFFECTED'</code></td>
<td><code class="language-plaintext highlighter-rouge">'DEMAND.LOSS.MW'</code></td>

### Exploratory Data Analysis

<iframe
  src="assets/urban_vs_outage.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Assessment of Missingness

### Finding MNAR
We found <code class="language-plaintext highlighter-rouge">'DEMAND.LOSS.MW'</code> by roughly observing columns with many missing values. We initially tried <code class="language-plaintext highlighter-rouge">'CUSTOMERS.AFFECTED'</code> but the number of NANs was too small. Then we found the percent of <code class="language-plaintext highlighter-rouge">'DEMAND.LOSS.MW'</code> that is missing values, ~46%, so we decided to dig deeper.

### MNAR Assessment
We believe <code class="language-plaintext highlighter-rouge">'DEMAND.LOSS.MW'</code> is likely MNAR. When a power outage causes very small or negligible demand loss, utility companies may not bother recording the value. This means the data is missing because the actual demand loss was too low to warrant reporting. Since the missingness depends on the unobserved value itself, this is MNAR. To potentially make it MAR, we could look up utility reporting thresholds or company specific logging policies. If we knew, for example, that certain utilities only report demand loss above a specific MW cutoff, then the missingness would be explained by the utility's reporting rules (an observed variable) rather than the value itself.

### Missingness Dependency
We analyzed the missingness of <code class="language-plaintext highlighter-rouge">'DEMAND.LOSS.MW'</code> (46%) by running permutation tests against two other columns. We found the following relationships to <code class="language-plaintext highlighter-rouge">'DEMAND.LOSS.MW'</code>:

Dependent on — <code class="language-plaintext highlighter-rouge">'CAUSE.CATEGORY'</code>: We used Total Variation Distance as our test statistic since <code class="language-plaintext highlighter-rouge">'CAUSE.CATEGORY'</code> is categorical. After 1000 permutations, we obtained a p-value of 0.0, meaning none of the shuffled TVDs matched or exceeded the observed TVD of ~0.179. We reject the null hypothesis. The missingness of <code class="language-plaintext highlighter-rouge">'DEMAND.LOSS.MW'</code> depends on <code class="language-plaintext highlighter-rouge">'CAUSE.CATEGORY'</code>. This makes sense because different outage causes, such as severe weather storms vs. intentional attacks, likely have different reporting standards for demand loss.

<iframe
  src="assets/missingness_cause.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Not dependent on — <code class="language-plaintext highlighter-rouge">'MONTH'</code>: We used the absolute difference in group means as our test statistic. After 1000 permutations, we obtained a p-value of 0.235, well above our 0.05 significance level. We fail to reject the null — the missingness of <code class="language-plaintext highlighter-rouge">'DEMAND.LOSS.MW'</code> does not depend on <code class="language-plaintext highlighter-rouge">'MONTH'</code>. This is reasonable since there is no strong reason for reporting completeness to vary by time of year.

<iframe
  src="assets/missingness_month.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>



