**Marketing Analytics Capstone Project \- StratusLink Communications Digital Media Campaign** 

**StratusLink Communications Digital Media Campaign**  
Analyzing cross-channel campaign performance to inform location, audience, creative, and inventory strategy for a national telecommunications client

**1\. Project Overview**:

Marketing campaign data offers a direct window into how efficiently ad spend is translating into performance — where budget is working hardest, which audiences and creatives are converting, and which inventory sources deliver the most value. As a capstone project for the COOP Careers Data Analyst Fellowship, I worked in a team of three to analyze the digital media campaign performance of our client, StratusLink Communications, a national telecommunications provider offering mobile, broadband, TV/streaming, and enterprise services to over 80 million customers. In this scenario, our team acted as a marketing agency responsible for consolidating and analyzing the client’s campaign reporting across their programmatic display (banner) buys, activated through multiple ad exchanges to publishers. Evaluated campaign effectiveness using provided performance data segmented into four core analysis areas: spatial, audience, creative, and inventory and viewability. Benchmarked results against client-defined KPI goals and supporting performance/branding metrics to surface insights and recommendations to drive more effective campaign strategy and decision-making.

**2\. Objective**

Our objective was to analyze StratusLink's digital media campaign performance to identify what was driving (and limiting) efficiency across location, audience, creative, and inventory/viewability dimensions, and to deliver data-driven recommendations to strengthen overall campaign effectiveness. This meant benchmarking performance against the client's primary and secondary KPI goals for each initiative — audience ($250 CPA / 0.015% CTR), desktop conversion ($350 CPA / 0.015% CTR), smartphone conversion ($400 CPA / 0.015% CTR), and viewability (60% viewability / $80 vCPM) — and using those benchmarks to surface actionable insights the client could use to maximize ROI and customer acquisition. 

**3\. Dataset:**

*Source*: [Digital Marketing Campaign Data](https://www.kaggle.com/datasets/jihyunlee81/digital-marketing-campaign-data) (Provided by COOP Careers as part of the Data Analyst Fellowship capstone project) 

*Size/Scope*: The dataset contained 13 columns and 727 rows.

The dataset included core performance and cost metrics — impressions, clicks, total conversions, gross cost, and viewability — alongside dimensional fields describing how and where each ad was delivered, such as location (state, city, latitude/longitude), audience segment, creative size and messaging, device, device make, App/URL, and exchange.

**4\. Methodology**

**Process Overview:** Campaign performance was evaluated against the client’s key benchmarks (CPA, CTR, vCPM, and viewability), and supplemented with performance/branding metrics (CVR, CPC, and CPM). Audience segments were consolidated into strategic consumer groups to make performance easier to interpret and act on. Performance was then analyzed across four areas — location, audience, creative, and inventory/viewability — to identify high- and low-performing areas, benchmark results against campaign goals, and translate findings into optimization recommendations.

**Analysis Type & Techniques:**  
 Exploratory Data Analysis (EDA) and data visualization, covering:

* **Audience analysis** — consolidating raw audience segments into engineered, strategic consumer groups and building personas  
* **Spatial analysis** — evaluating location performance by state  
* **Creative analysis** — evaluating creative size performance by device, location (top 5 states identified in spatial analysis), and messaging *(shared with team)*  
* **Inventory and Viewability analysis** — ranking ad exchanges and publishers (App/URL) using a weighted score model based on key benchmarks *(my focus)*

**Data Considerations & Caveats:**  
While working with the dataset, we noted several limitations that shaped how we interpreted the results:

* **Audience Segment**: Made formatting adjustments in the audience segment column by replacing “ Â»” with “ \>”.  
* **Location:** 13 data ranges were excluded from the dataset due to location entries with cross-state listings. To assess the significance of excluded entries, cross-checked discrepancies before and after the exclusion. There was little impact, implying a low risk of removal.  
* **Device:** “Apple PC” and “Windows PC” devices were combined into a single device group, “Desktop”.  
* **Calculation:** Because some clicks had 0 entries, CVR and CPC were invalid. So, when CVR and CPC were used, rows with invalid entries were removed during analysis.

**Tools Used:** Excel (data cleaning & preparation), Tableau (visualization), SQL (data analysis)

**5\. My Role**

As an Inventory Analyst, I led the inventory and viewability analysis, developing a weighted scoring model to analytically rank exchanges and publishers across multiple performance variables. Since exchanges and publishers rarely lead on every metric at once, this model combines the campaign's four core benchmarks — CPA, CTR, vCPM, and viewability — into a single composite score, allowing for a fair comparison across otherwise inconsistent performers.

**Primary Model:**

Score \=   
$[0.25(\frac{25th\ Percentile\ of\ CPA}{Actual\ CPA})+0.25(\frac{Actual\ CTR}{75th\ Percentile\ of\ CTR})+0.25(\frac{Target\ vCPM}{Actual\ vCPM})+0.25(\frac{Actual\ Viewability}{Target\ Viewability})]\times \frac{LOG(Actual\ Impressions)}{LOG(Max\ Impressions)}$

*Model Breakdown:*

* Each metric was given an equal weight of 25% in the score  
* “Target \[Metric\]”: the KPI goal for that metric  
* “Actual \[Metric\]”: the calculated value from the dataset for that metric  
* Normalized everything by converting all metrics into “higher score \= better performance”  
* CTR has a target goal of 0.015%, but only 6 of the 727 rows had 0% CTR. Excluding the 0% CTR, the minimum CTR was 0.03% (double the target goal). Therefore, using the top 25% of the metric helps balance it, preventing CTRs from dominating the score.  
* Specifically, the top 25% because it represents “good performance” without being distorted by outliers.  
* The LOG at the end helps balance the skewness of total impressions, preventing large players from dominating.

To add further depth beyond the primary model, I also developed two supplementary models isolating performance and branding metrics separately:

**Performance Score**: weighted CPA, CVR, CPC, and CPM (25% each), similarly adjusted for impression volume — used to evaluate cost-efficiency and conversion behavior independent of brand-level metrics.

Performance Score \= $[0.25(\frac{25th\ Percentile\ of\ CPA}{Actual\ CPA})+0.25(\frac{25th\ Percentile\ of\ CPC}{Actual\ CPC})+0.25(\frac{Actual\ CVR}{75th\ Percentile\ of\ CVR})+0.25(\frac{25th\ Percentile\ of\ \ CPM}{Actual\ CPM})]\times \frac{LOG(Actual\ Impressions)}{LOG(Max\ Impressions)}$

**Branding Score**: weighted viewability and CTR (50% each) against their respective benchmarks, adjusted for impression volume — used to isolate brand visibility and engagement performance.

Branding Score \= $[0.5(\frac{Actual\ Viewability}{Target\ Viewability})+0.5(\frac{Actual\ CTR}{75th\ Percentile\ of\ CTR})]\times \frac{LOG(Actual\ Impressions)}{LOG(Max\ Impressions)}$

To validate the models, I manually reviewed the underlying data and cross-checked results against charts to confirm the rankings matched what the raw data showed, rather than relying on the composite score alone.

I also collaborated with the team on the Creative analysis, evaluating creative size performance across devices, locations, and messaging. Additionally, I supported the broader team by answering questions and reviewing work across the Audience and Spatial analyses to help ensure accuracy and consistency across the project.

**6\. Key Findings**

**Audience**

* All engineered audience segments exceeded the campaign's CTR benchmark (0.015%), but only *Financially Motivated* audiences met the CPA goal of $250, delivering the most cost-efficient conversions.  
* *Technology Enthusiasts* showed the strongest balance of engagement and conversion performance; *Travel & Experiences* showed growth potential through more targeted messaging; *Entertainment and Automotive* Consumers underperformed relative to acquisition goals.  
* Three audience personas were developed: *Family Planner* (value-driven households seeking affordability), *Tech Professional* (digitally engaged, connectivity/performance-focused), and *Connected Traveler* (experience-oriented, values flexibility and premium services).

**Spatial**

* Indiana, Kentucky, and Ohio were the most cost-effective states, with CPAs well below the campaign average of $327. South Carolina and Louisiana had the highest CPAs, with Michigan and Alabama also performing below average.  
* Alabama, Arkansas, and Michigan had the highest CTRs (strongest engagement), though Arkansas's result should be treated cautiously due to low data volume. Illinois, Indiana, and Kentucky had the lowest CTRs despite performing well on CPA/CVR.  
* Ohio, Arkansas, and Mississippi had the highest viewability rates, while Kentucky, Michigan, and Georgia had the lowest; Arkansas remains a low-volume outlier.

**Creative**

* All creative formats underperformed against the 60% viewability benchmark. Ignoring that benchmark, 320x50 delivered the strongest results ($311 CPA, $62 vCPM, 59% viewability), while 300x50 lagged across all metrics.  
* *By state (top 5 states)*: 320x50 was the most cost-efficient format across top states but lacked viewability; 300x250 delivered consistent performance and served as the core format. 300x50 underperformed with high CPAs, particularly in New York and Illinois.  
* *By device*: desktop met its CPA goal, with Windows outperforming; on mobile, nearly all formats hit the CPA target except 300x50, with 320x50 leading. No format met the 60% viewability goal on either device.  
* *By message*: two messages failed to meet the viewability goal, suggesting weaker engagement or placement issues, while "10% Discount – Ends 6/1" (320x50) performed best with the lowest CPA.

**Inventory & Viewability** 

* Ad Exchanges were ranked using a weighted score model; Taboola, OpenX, Xandr \- Monetize SSP, Yahoo Exchange, and Smart RTB+ emerged as the top-performing platforms, indicating cost-effective results, high visibility, and strong brand awareness.  
* The top 5 publishers by weighted score were msn.com (broad, mainstream reach), mail.yahoo.com (older audience, well-suited to promotions), streetinsider.com (finance-focused, investor/business audience), outlook.live.com (professional, B2B-oriented audience), and screenrant.com (younger, entertainment-focused audience).

**7\. Visuals**

**8\. Conclusion / Recommendations**

Overall, the analysis revealed a clear gap between engagement and acquisition efficiency across the campaign—most segments, formats, and locations drove strong click-through activity but fell short of the client's CPA and viewability goals, pointing to specific, actionable optimization opportunities.

*Audience*: Increase investment in Financially Motivated and Travel & Experiences audiences, test tailored messaging for Technology Enthusiasts, refine targeting for Entertainment and Automotive Consumers, and reallocate spend from underperforming segments.

*Spatial*: Prioritize budget allocation toward high-performing states like Indiana, Kentucky, and Ohio, where CPAs are below average and efficiency is strongest; reduce or limit spend in high-CPA states such as South Carolina, Louisiana, Michigan, and Alabama.

*Creative*: Reallocate budget toward the high-performing 320x50 format, which delivered the best results across devices, locations, and messaging. Prioritize premium inventory placements to address the widespread shortfall against the 60% viewability goal.

*Inventory*: Pursue direct-buy deals with the top 5 publishers (msn.com, mail.yahoo.com, streetinsider.com, outlook.live.com, screenrant.com) at recommended rates. Gradually increase budget on high-performing exchanges (Taboola, OpenX, Xandr, Yahoo Exchange, Smart RTB+), and consider removing underperforming exchanges to improve profit margin.

**9\. Links**

[Marketing Analysis Dashboard](https://public.tableau.com/app/profile/gracejihyunlee/viz/CapstoneProject-Marketing_17799722882720/Dashboard2) (In Progress)

[Marketing Analysis Presentation](https://drive.google.com/file/d/1p0HcPBS30crFwp05ONmk3XNf8FHypg5e/view?usp=sharing)

[Marketing Analysis One-pager](https://drive.google.com/file/d/17G9IzozWA07fhFVooaPFYZWCHhAKrrx4/view?usp=sharing) 


  

