# Nigeria Malaria Dashboard (2000–2023)

This project is a complete Power BI dashboard that analyzes malaria incidence in Nigeria between 2000 and 2023 using official data from the World Health Organization (WHO). The purpose is to turn raw data into a visual, story-driven dashboard that supports advocacy, monitoring, and better public health decisions.

## Objective
To analyze, visualize, and communicate trends in malaria incidence in Nigeria using real-world data and build a professional Power BI dashboard as part of a public health data portfolio.

## Region Extraction
The original dataset was global. I filtered it to focus only on Nigeria using the column `GEO_NAME_SHORT` with this logic:
```
GEO_NAME_SHORT = "Nigeria"
```
This allowed for a focused national-level analysis without the distraction of multiple country data.

## DAX Calculated Columns (New Columns Created)
To make the dashboard deeper and more meaningful, I created the following new columns in Power BI using DAX:

**1. Year-over-Year (YoY) % Change**
This compares the malaria rate of each year to the previous one.

```powerbi
YoY_Change = 
VAR CurrentYear = [DIM_TIME]
VAR CurrentRate = [RATE_PER_1000_N]
VAR PreviousRate = 
    CALCULATE(
        MAX([RATE_PER_1000_N]),
        FILTER(
            'Nigeria_Malaria_Incidence',
            [DIM_TIME] = CurrentYear - 1
        )
    )
RETURN
    IF(
        ISBLANK(PreviousRate) || PreviousRate = 0,
        BLANK(),
        DIVIDE(CurrentRate - PreviousRate, PreviousRate)
    )
```

**2. Decade**
This groups each year into 2000s, 2010s, and 2020s.

```powerbi
Decade = INT([DIM_TIME] / 10) * 10
```

**3. Estimate Gap**
This shows the difference between WHO’s upper and lower estimate for each year.

```powerbi
Estimate_Gap = [RATE_PER_1000_NU] - [RATE_PER_1000_NL]
```

## 📊 Visuals in the Dashboard
- **KPI Cards** for Highest, Lowest, and Average malaria rates
- **Line Chart** to show overall trend of malaria from 2000 to 2023
- **Area Chart** showing WHO’s estimate range (upper vs lower)
- **Column Chart** to show Year-over-Year % Change
- **Bar Chart by Decade** showing malaria trends across the 2000s, 2010s, and 2020s
- **Estimate Gap Chart** showing how confident WHO was each year

## 📈 Key Insights
- Nigeria’s malaria incidence rate has decreased overall, from over 400 per 1,000 in the early 2000s to below 310 in the 2020s.
- The highest rates were recorded between 2003 and 2005.
- Some years (like 2012 and 2020) saw malaria rates rise again.
- The 2020s showed the best overall average, suggesting improved malaria control.
- WHO estimates had high uncertainty in years like 2004 and 2005, shown by a wide estimate gap.

## 💡 Recommendations
1. Expand malaria prevention campaigns in high-risk and rural areas.
2. Improve health data systems to reduce gaps in malaria estimate accuracy.
3. Use historical spikes to plan better seasonal interventions.
4. Increase public education on mosquito net use and early treatment.
5. Invest in vaccine access and ongoing research to reduce long-term burden.

6.  ## 📊 Dashboard Preview  
![Nigeria Malaria Analysis Dashboard](https://github.com/Bees-png/Nigeria-malaria-analysis/blob/main/Malaria%20dashboard.jpg)  


##  Dataset Information
- **Source:** [WHO Global Health Observatory (GHO)](https://www.who.int/data/gho)
- **Fields used:** 
  - `DIM_TIME` = Year
  - `GEO_NAME_SHORT` = Country
  - `RATE_PER_1000_N` = Main malaria rate
  - `RATE_PER_1000_NL` = WHO lower estimate
  - `RATE_PER_1000_NU` = WHO upper estimate
- Filter applied: Nigeria only

## 🛠️ Tools Used
- **Power BI Desktop** – for dashboard creation and DAX calculations
- **Excel** – for quick initial data filtering
- **GitHub** – for hosting the project and documentation
- **WHO Portal** – as the primary data source
- **Canva (optional)** – to convert PDF dashboard into JPG for preview

##  Files in this Repository
- ` MALARIA ANALYSIS IN NIGERIA.pbix` – PowerBI file (fully editable)
- `442CEA8_ALL_LATEST.csv` – Filtered dataset for Nigeria
- `malaria dashboard.jpg` – Image preview for GitHub and LinkedIn

## Author
**Blessing Ofili**  
Public Health Advocate & Healthcare Data Analyst  
Nigeria  
🔗 LinkedIn: [https://linkedin.com/in/ofili-blessing-2b993a272](https://linkedin.com/in/ofili-blessing-2b993a272)

---
 If this dashboard was useful or inspiring, feel free to  give it a star, or reach out to collaborate. Together we can use data to power better health outcomes in Nigeria and beyond.

