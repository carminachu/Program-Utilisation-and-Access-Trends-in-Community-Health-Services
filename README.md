# Program Utilisation and Access Trends in Community Health Services

## Project Background

**Community Child & Family Health Services**, a fictional Victorian not-for-profit organisation supporting families with children aged 0–5, is modernising its operations through the implementation of a new **Client Information Management System (CIMS)** to improve data quality, service reporting, and organisational performance. Operating within the community health and social services sector, **CCFHS** delivers residential programs, telehealth support, group sessions, and community outreach, all of which are governed by strict state and federal reporting obligations. 

This project analyses program utilization across multiple datasets to support alignment of services and operational planning within healthcare teams, ensuring more responsive and effective support for patient needs.

**Insights and recommendations are provided on the following key areas:**

- Program service growth (Year-over-Year: 2023→2024): High-level analysis of service delivery trends to inform workforce planning, resource allocation, and operational decision-making.
- Service type importance (RPP, Day Stay, Telehealth, In-Home, Workshop, Mental Health Support): Assessment of the relative importance and utilization of each service type to support data-driven prioritisation and service design decisions.
- Client Demographic Contribution (Age and Gender):  Analysis of key demographic segments driving program utilization to guide targeted service planning, engagement strategies, and capacity planning.
- Equity Indicators and Risk Factors: Evaluation of utilization patterns across equity and risk groups (e.g. CALD, NDIS, Indigenous status, DV risk, SEIFA) to identify potential access gaps and opportunities for targeted outreach and equitable service delivery.
- Average Wait Time (Days): Review of wait time trends across services to assess access, operational efficiency, and consistency of service delivery over time.

## 🔗 Project Resources

- **Data Quality Check**: The SQL queries used to inspect and clean the data for this analysis can be found here [[link](https://docs.google.com/spreadsheets/d/1TnQysry7-BT1Gp438DsQV8-yNDu4toQbPGkzGbxSLuE/edit?usp=sharing)].
- **Looker Studio Report**: An interactive Looker Studio report to explore sales trends can be found here [[link](https://lookerstudio.google.com/reporting/650d7b66-7918-4d10-b463-5d4222c2aab1)].
  
# **Data Structure & Initial Checks**

The dataset (2023-2025) is designed as a **relational model** to replicate a real-world Client Information Management System (CIMS) environment, supporting operational, compliance, and outcome reporting. It contains five interconnected tables:

- **`clients` (12,000 rows):** Demographics, risk factors, and equity indicators for each unique client.
- **`services` (50,000 rows):** Each service episode delivered, linked to a client via `client_id`. Includes program type, clinician, referral source, wait times, and attendance status.
- **`outcomes` (~35,000 rows):** Pre- and post-program outcome measures for attended services, including K10, EPDS, and parenting confidence scores. Linked to `services` via `service_id`.
- **`data_quality` (50,000 rows):** Simulated validation checks and completeness flags for each service record, supporting governance and CIMS migration analysis.
- **`sla_performance` (50,000 rows):** Service-level agreement and compliance metrics, including wait-time compliance, attendance compliance, and timeliness of data entry.

<img width="851" height="557" alt="image" src="https://github.com/user-attachments/assets/668ddb2d-1001-484e-acaa-05ff2b133692" />


⚠️ **Important Notes:**

- This analysis focuses on the 2023–2024 period to ensure a balanced year-over-year comparison. A star schema was used to design the data model, with the Services table serving as the fact table and the remaining five tables structured as dimension tables.
- This analysis leverages the `clients` and `services` datasets to generate actionable insights and data-driven visualisations. Additional datasets will be integrated in future analyses to deepen insights and support more comprehensive program utilisation decision-making.

Prior to beginning the analysis, a variety of checks were conducted for quality control and familiarization with the datasets can be found [here](https://docs.google.com/spreadsheets/d/1TnQysry7-BT1Gp438DsQV8-yNDu4toQbPGkzGbxSLuE/view). It also includes data dictionary.

# **📈 Executive Summary**

**Overview of Findings**

**Service attended volumes grew modestly by +1.1% from 2023 to 2024**, reflecting stable demand. While monthly results follow an expected seasonal pattern, **Nov 2024 stands out with a 5.8% decline** compared to Nov 2023. This warrants further investigation to identify underlying drivers.

<img width="365" height="264" alt="image" src="https://github.com/user-attachments/assets/b060879b-805f-49e3-92fd-18f91bcb68e0" />
<img width="1008" height="316" alt="image" src="https://github.com/user-attachments/assets/27afb8f9-75f7-46b8-9ec6-5967e8c887a4" />


**Service Delivery Trend**

- **Majority of the services were attended**, with attendance rate ranging between **~76% to 78%**. However, **Did Not Attend (DNA) and Cancelled appointment together accounts for nearly one quarter of total service utilisation**, highlighting opportunities to improve utilisation.

<img width="718" height="287" alt="image" src="https://github.com/user-attachments/assets/1a8d6b8f-e683-4b53-bcb0-e2cbb204cdcc" />


- **Reductions in Did Not Attend (DNA) and Cancelled appointments (-0.14 and -0.11 p.p. respectively)** suggest improved attendance outcomes in 2024.
<img width="597" height="95" alt="image" src="https://github.com/user-attachments/assets/63f81d2d-453a-4dce-b202-d5ef8a47265a" />

- Monthly trend analysis shows that **Did Not Attend (DNA) appointments increased year-over-year from Jun to Dec**, with the exception of November. **Cancelled appointments also showed year-over-year increases in Jan, June, Aug - Sep, and December**. This pattern highlights the second half of the year as a key period of elevated non-attendance risk.

<img width="698" height="303" alt="image" src="https://github.com/user-attachments/assets/ea100870-4e98-4294-b2da-4af83ef80748" />

<img width="701" height="279" alt="image" src="https://github.com/user-attachments/assets/a4c3bae6-8351-4ed4-9159-ab882a4c7653" />

- **Average wait times remained stable at ~12 days** across all services from 2023 to 2024, indicating consistent access and operational efficiency.

<img width="812" height="712" alt="image" src="https://github.com/user-attachments/assets/5ff13045-557f-432a-b45e-1b5ad68cf541" />


**Client Demographic**

- The **25–34 age group represented the highest utilization of services**, highlighting them as the primary user base across offerings. Similarly, **females accounted for the largest share** of service utilization overall.

<img width="756" height="346" alt="image" src="https://github.com/user-attachments/assets/c538fd17-2224-405a-abd7-23c990c5d544" />


- Analysis of service utilization by Equity Indicators and Risk Factors in 2024 shows the following contributions from each group:
    - CALD: **Non-CALD background accounted for ~83% of utilization**.
    - NDIS: **Non-NDIS category represented ~97% of utilization**.
    - Domestic Violence (DV) Risk: **Non-DV risk category contributed ~90%**.
    - Indigenous Status: **Non-Indigenous background accounted for ~96%**.
    - SEIFA: **Mid socioeconomic group represented ~50% of utilization**.

**Deep dive analysis**

- **November 2024 Decline**
    
    The November 2024 decline in attended services was largely attributable to a **17.5% drop in In-Home services**, with additional declines observed in **Workshops and Telehealth**. Seasonal factors and evolving service delivery preferences may have contributed to this trend.

<img width="542" height="324" alt="image" src="https://github.com/user-attachments/assets/7d058318-1f3e-439b-8d34-251d442e77cc" />

**Recommendation:** 

- **Reassess the allocation of resource**s between in-home, telehealth, and workshop services to match post-pandemic patient preferences.
- **Explore opportunities to promote hybrid models** that integrate in-person, telehealth, and targeted in-home care for high-need clients.
- I**mplement seasonal planning** to anticipate and mitigate end-of-year slowdowns.

---

**Drop in Telehealth in 2024**

**Telehealth accounted for the largest attended service volume**, ranging from ~21% to 25%, but experienced a **notable year-end decline of 13.4% in 2024** compared to the previous period. Overall, **Telehealth dropped by 15% for the year**, despite ongoing demand. These trends likely reflect post-pandemic normalization, with patients increasingly returning to in-person or hybrid care, combined with typical seasonal slowdown.

<img width="827" height="400" alt="image" src="https://github.com/user-attachments/assets/4d5199d1-ae66-4dab-b7ce-f481d31ccc06" />
<img width="781" height="297" alt="image" src="https://github.com/user-attachments/assets/bf32f325-ad35-46ea-92b9-7677b11db0b9" />


**Recommendation**

- **Refocusing Telehealth on high-value use cases** (e.g. follow-ups, low-complexity care, rural access, after-hours services) where it delivers the strongest access and efficiency gains.
- **Aligning workforce and capacity planning** to seasonal demand patterns, reducing over-allocation during predictable year-end slowdowns.
- **Strengthening hybrid care pathways**, enabling flexible transitions between Telehealth and in-person care based on clinical appropriateness and patient preference.
- **Monitoring patient outcomes and utilisation by modality**, ensuring Telehealth continues to deliver comparable or superior outcomes rather than purely service volume.

---

**Mental Health Support experience growth**

**Mental Health Support services saw the largest growth** among all service types, increasing by **7.8% in 2024**. This increase may indicate growing demand for mental health support, potentially reflecting **higher prevalence or recognition of mental health issues** in the community. It could also reflect **improved access or awareness of mental health services**, or expanded program capacity.

<img width="720" height="384" alt="image" src="https://github.com/user-attachments/assets/ef744145-0154-4cb1-89bd-f79e5969db85" />


**Recommendation**

- **Consider expanding capacity for mental health programs** to meet increasing demand.
- **Invest in workforce training and recruitment** for mental health professionals.
- **Strengthen outreach and awareness campaigns** to ensure communities can access mental health support efficiently.

---

**Ages 25–34 Drive Telehealth Utilisation as the Most Digitally Engaged Cohort**

**Telehealth attended service** accounted for approximately **17% of service utilizatio**n among the **25–34 age group** and was the **leading channel for accessing Mental Health Support**, representing **~3% of total services**.

<img width="648" height="200" alt="image" src="https://github.com/user-attachments/assets/888773a0-c69f-402e-ab7f-783db7595b66" />


This reflects the 25–34 age group’s comfort and familiarity with technology-enabled healthcare, alongside a higher prevalence or awareness of mental health issues within this demographic.

- **Prioritise Telehealth for youth-focused mental health pathways**, particularly for early intervention, follow-ups, and continuity of care.
- **Tailor service design and communication** to digitally native cohorts to sustain engagement and reduce barriers to access.
- **Protect and allocate Telehealth capacity** for mental health services where demand, accessibility, and patient preference clearly align.
- **Track outcomes and engagement by age and modality**, ensuring Telehealth delivers equitable outcomes while supporting service efficiency.

---

**Mental Health Support for 45+age group shows the largest increase**

- The 45+ age group experienced the largest increase by ~49% in Mental Health Support utilization in 2024.
<img width="1101" height="596" alt="image" src="https://github.com/user-attachments/assets/02d1e502-c5d2-4360-88a6-8bc14af79f28" />

**Recommendations:**

- **Highlights an opportunity to expand targeted mental health programs** and outreach for the 45+ demographic.

---

**Female Dominated Utilisation; Male Mental Health Demand Rising**

- Among the gender demographic, **Telehealth accounted for approximately 27%** of overall service utilization and around **4% specifically for Mental Health Support services** in females.
<img width="650" height="187" alt="image" src="https://github.com/user-attachments/assets/57814cfd-09a2-45ed-9433-9e940427d444" />

- Despite males accounting for a relatively small share of total service utilisation (~11%) in 2024, demand for **Mental Health Support among males increased by ~20%**. **Growth in the ‘Other’ category (~43%)** is subject to confirmation pending data validation.

<img width="1336" height="157" alt="image" src="https://github.com/user-attachments/assets/43f1932b-876d-40c2-961a-3bafe98e8415" />


**Recommendations:**

- **Expand targeted outreach and engagement** for males to ensure Mental Health Support services continue to meet growing demand.
- **Develop tailored communication campaigns** that address stigma and promote awareness of available mental health services for men.
- **Monitor utilization trends** in both male and female demographics to inform resource allocation and program planning.

---

**Majority of service utilisation from general population**

- The majority of service utilization comes from the general population rather than high-risk or priority equity groups.

<img width="962" height="595" alt="image" src="https://github.com/user-attachments/assets/b6302279-d543-49e9-9122-17dd449eed4c" />


Recommendations:

- This highlights potential gaps in engagement or access for priority populations (CALD, NDIS, Indigenous, high DV risk), **signaling an opportunity for targeted outreach and support programs**.

**⚠️ Assumptions and Caveats:**

Throughout the analysis, multiple assumptions were made to manage challenges with the data. These assumptions and caveats are noted below:

- Trends identified in this analysis are based on data recorded in CIMS and reflect documented service activity only.
- The analysis utilised `services` and `client` tables exclusively.
- Further insights could be generated by incorporating additional tables, which is recommended for future reporting sprint.
- The analysis is limited to the 2023–2024 reporting period
