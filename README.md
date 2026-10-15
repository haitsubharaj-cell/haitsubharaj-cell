<p align="center">
  <img src="assets/banner.svg" alt="Subharaj Hait — Data Architect, Solution Architect, Data Engineer" width="100%"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Experience-10%20yrs%20BI%20%26%20Data-0B1B33?style=for-the-badge" alt="10 years BI and data"/>
  <img src="https://img.shields.io/badge/Status-Open%20to%20Architect%20Roles-2F5D8F?style=for-the-badge" alt="Open to architect roles"/>
  <img src="https://img.shields.io/badge/Joining-Immediate-5BA4E6?style=for-the-badge" alt="Immediate joiner"/>
  <img src="https://img.shields.io/badge/Location-Kolkata%20%7C%20Bengaluru%20%7C%20Pune%20%7C%20Remote-1C3D66?style=for-the-badge" alt="Locations"/>
  <a href="https://www.linkedin.com/in/subharaj-hait-9b24373a0"><img src="https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"/></a>
</p>

---

## 👋 About me

I design data platforms that business people actually use. Over **10 years in Business Intelligence**, I've moved from building reports to owning the whole path the data travels — **source systems → ingestion → medallion layers → governed semantic model → executive dashboard**.

My edge is that I started on the **business side** (commerce and industrial accounts) and spent a decade inside **master data management** and enterprise reporting. I model data the way finance, HR and sales teams think about it, then engineer it so it stays correct at scale.

- 🏗️ **Most recently:** Technical Architect, Hexaware Technologies (Bengaluru)
- 🗂️ **A decade at:** Sabyasachi Calcutta LLP — master data + Power BI reporting
- 🎯 **Looking for:** Data Architect · Solution / Technical Architect · Data Engineer · Power BI Architect
- 🏆 Recognised by **LearnTube.ai among the Top 1000 Professionals in India** (2026)

---

## 🧭 Where I fit

<p align="center">
  <img src="assets/role-fit.svg" alt="Role-fit map across Data Architect, Solution Architect, Data Engineer and Power BI Architect" width="100%"/>
</p>

---

## 🏛️ Reference architecture I design and deliver

The blueprint behind most of my work — a governed, layered platform where every number on a dashboard can be traced back to its source.

```mermaid
flowchart LR
    subgraph SRC["📥 Sources"]
        A1[ERP / SAP<br/>SuccessFactors]
        A2[CRM · Sales<br/>invoices]
        A3[Flat files<br/>CSV · JSON · Excel]
        A4[MDM hub<br/>Prospecta]
    end

    subgraph ING["⚙️ Ingest & orchestrate"]
        B1[Azure Data Factory]
        B2[Fabric Dataflows Gen2]
        B3[Python ETL jobs]
    end

    subgraph LAKE["🪙 Medallion lakehouse · Fabric / Snowflake"]
        C1[(Bronze<br/>raw, as-landed)]
        C2[(Silver<br/>cleaned, conformed,<br/>SCD 1/2)]
        C3[(Gold<br/>star schemas ·<br/>Data Vault marts)]
    end

    subgraph SERVE["📊 Serve"]
        D1[Semantic model<br/>DAX · TMDL · Direct Lake]
        D2[Power BI<br/>executive dashboards]
        D3[Self-service<br/>analytics]
    end

    GOV{{🛡️ Governance · data quality rules · master-data golden records}}

    SRC ==> ING ==> C1
    C1 --> C2 --> C3 --> D1 --> D2 & D3
    A4 -. golden records .-> C2
    GOV -.-> LAKE
    GOV -.-> D1

    classDef src fill:#163259,stroke:#5BA4E6,color:#fff
    classDef ing fill:#1C3D66,stroke:#7FB6EA,color:#fff
    classDef bronze fill:#8C6A43,stroke:#5c4329,color:#fff
    classDef silver fill:#8C97A6,stroke:#5e6874,color:#0B1B33
    classDef gold fill:#C9A646,stroke:#8f7425,color:#0B1B33
    classDef serve fill:#2F5D8F,stroke:#9CC9F0,color:#fff
    classDef gov fill:#0B1B33,stroke:#C9A646,color:#fff
    class A1,A2,A3,A4 src
    class B1,B2,B3 ing
    class C1 bronze
    class C2 silver
    class C3 gold
    class D1,D2,D3 serve
    class GOV gov
```

**Design principles I hold to**

| Principle | What it looks like in practice |
|---|---|
| **Model for the business question** | Star schemas with conformed dimensions; grain decided with stakeholders before a single table is built |
| **History is a feature** | SCD Type 2 on dimensions that drive reporting (customer, product, employee) so past numbers never silently change |
| **One version of the truth** | Master data golden records feed the Silver layer — duplicates are fixed upstream, not patched in DAX |
| **Assumptions are swappable** | Business assumptions live in their own tables (e.g. cost rates), so finance can replace them without touching the model |
| **Built to be maintained** | Semantic models in TMDL / `.pbip` for source control, measure libraries organised by domain |

---

## 🚀 Featured work

### 1 · Sunrise Beverages — sales & profitability analytics (Power BI + Microsoft Fabric)

> Technical case study for a Senior Data Analyst (Power BI & Fabric) role: **15,000 invoice lines, 2024 – 2026**, turned into a decision-ready model and a 14-page business summary.

<sub>Model shape (simplified):</sub>

```mermaid
erDiagram
    FACT_SALES }o--|| DIM_DATE : "invoice date"
    FACT_SALES }o--|| DIM_PRODUCT : "sku"
    FACT_SALES }o--|| DIM_CUSTOMER : "customer"
    FACT_SALES }o--|| DIM_REGION : "territory"
    DIM_PRODUCT }o--|| ASSUMED_COST_RATES : "pack type"

    FACT_SALES {
        int invoice_line_id PK
        date invoice_date FK
        string sku FK
        string customer_id FK
        decimal volume_hl
        decimal net_revenue
    }
    ASSUMED_COST_RATES {
        string pack_type PK
        decimal cost_per_hl
    }
```

| Aspect | Detail |
|---|---|
| **Challenge** | Source data had **no cost column**, yet the business needed profitability |
| **Architecture decision** | Introduced an `AssumedCostRates` table (cost per HL by pack type) — profit is calculated transparently and finance can swap in standard costs later with zero model changes |
| **Delivered** | Star-schema model in Power Query / **TMDL**, **51 DAX measures**, **5 report pages**, `.pbix` + `.pbip` project, 14-page business summary |
| **Stack** | `Power BI` `DAX` `Power Query M` `TMDL` `Microsoft Fabric` |

---

### 2 · Enterprise master data management & HR data governance

> A decade of keeping enterprise master data clean, governed and reporting-ready at Sabyasachi Calcutta LLP.

```mermaid
flowchart LR
    S[Source records<br/>SAP · HR · vendor files] --> M[Match &<br/>de-duplicate]
    M --> V{Validation<br/>rules}
    V -- pass --> G[(Golden record<br/>Prospecta MDM)]
    V -- fail --> R[Data steward<br/>review queue]
    R --> M
    G --> D[Downstream BI &<br/>payroll / compliance reports]
    classDef n fill:#163259,stroke:#5BA4E6,color:#fff
    classDef g fill:#C9A646,stroke:#8f7425,color:#0B1B33
    class S,M,R,D n
    class G g
    class V n
```

- Maintained master data on **Prospecta** as the single source for downstream reporting
- Managed **employee (HR) master data** with **SAP HCM / SuccessFactors Employee Central**, supporting **payroll, PF, ESI and labour-law compliance** reporting
- Built **Power BI** reporting and **Python / SQL** automation on top of governed master data

**Stack:** `Prospecta` `SAP SuccessFactors` `SQL` `Python` `Power BI`

---

### 3 · Interactive sales performance dashboards (HTML / JavaScript + Plotly.js)

> Web-native executive dashboards — proof that I can deliver insight outside the Power BI canvas too.

- **CSV / JSON ingestion** with a data-cleaning pipeline in the browser
- Advanced visuals: **choropleth maps, donut charts, spline-area trends, grouped bars**
- Responsive layouts with **dark and light themes**, iterated against detailed design specs

**Stack:** `JavaScript` `Plotly.js` `HTML` `CSS`

---

### 4 · Enterprise Power BI dashboard blueprints

> Full specification-to-build packages for large dashboards, including a **FIBO Sports Products** sales dashboard and a **Vande Bharat Express** operations dashboard.

```mermaid
flowchart LR
    R[Requirements &<br/>KPI catalogue] --> M[Data model<br/>design] --> P[Power Query M<br/>transform scripts] --> D[DAX measure<br/>library] --> U[Report UX &<br/>page specs] --> RM[Phased<br/>roadmap]
    classDef n fill:#1C3D66,stroke:#9CC9F0,color:#fff
    class R,M,P,D,U,RM n
```

**Stack:** `Power BI` `DAX` `Power Query M` `Data modeling`

---

## 🧰 Tech stack

**Data platforms & engineering**

![Microsoft Fabric](https://img.shields.io/badge/Microsoft%20Fabric-0B1B33?style=flat-square&logo=microsoft&logoColor=white)
![Snowflake](https://img.shields.io/badge/Snowflake-29B5E8?style=flat-square&logo=snowflake&logoColor=white)
![Azure Data Factory](https://img.shields.io/badge/Azure%20Data%20Factory-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)
![Azure Synapse](https://img.shields.io/badge/Azure%20Synapse-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)
![Apache Spark](https://img.shields.io/badge/Spark%20SQL-E25A1C?style=flat-square&logo=apachespark&logoColor=white)

**Languages**

![SQL](https://img.shields.io/badge/SQL-9%20yrs-2F5D8F?style=flat-square&logo=postgresql&logoColor=white)
![Python](https://img.shields.io/badge/Python-9%2B%20yrs-3776AB?style=flat-square&logo=python&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-Advanced-F2C811?style=flat-square&logo=powerbi&logoColor=black)
![Power Query M](https://img.shields.io/badge/Power%20Query%20M-1C3D66?style=flat-square&logo=powerbi&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)

**BI, modeling & governance**

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=flat-square&logo=powerbi&logoColor=black)
![Tabular Editor](https://img.shields.io/badge/Tabular%20Editor-1C3D66?style=flat-square)
![DAX Studio](https://img.shields.io/badge/DAX%20Studio-1C3D66?style=flat-square)
![Plotly](https://img.shields.io/badge/Plotly.js-3F4F75?style=flat-square&logo=plotly&logoColor=white)
![Prospecta MDM](https://img.shields.io/badge/Prospecta-MDM-0B1B33?style=flat-square)
![SAP SuccessFactors](https://img.shields.io/badge/SAP-SuccessFactors-0FAAFF?style=flat-square&logo=sap&logoColor=white)

**Architecture & design tools**

![Visio](https://img.shields.io/badge/Visio-3955A3?style=flat-square&logo=microsoftvisio&logoColor=white)
![draw.io](https://img.shields.io/badge/draw.io-F08705?style=flat-square&logo=diagramsdotnet&logoColor=white)
![Lucidchart](https://img.shields.io/badge/Lucidchart-F96B13?style=flat-square)
![Figma](https://img.shields.io/badge/Figma-F24E1E?style=flat-square&logo=figma&logoColor=white)

**Modeling patterns I apply in real projects:** Star schema · **Data Vault 2.0** · **SCD Type 1 / 2** · **Medallion (Bronze / Silver / Gold)** · Direct Lake

---

## 📈 Career journey

<p align="center">
  <img src="assets/career-timeline.svg" alt="Career timeline from commerce and accounts to technical architect" width="100%"/>
</p>

---

## 🔭 Currently levelling up

```mermaid
mindmap
  root((Architect<br/>track))
    Microsoft Fabric
      Lakehouse
      Dataflows Gen2
      Direct Lake mode
    Azure
      Data Factory
      Synapse
    Modeling
      Advanced DAX
      Star schema at scale
      Data Vault 2.0
    Leadership
      Solution design docs
      Architecture decision records
```

---

## 🤝 Let's talk

I'm an **immediate joiner**, open to roles in **Bengaluru, Pune, remote**, and international opportunities (**UAE, Saudi Arabia, UK/Europe, US/Canada, Australia, Singapore**).

<p align="left">
  <a href="https://github.com/haitsubharaj-cell"><img src="https://img.shields.io/badge/GitHub-haitsubharaj--cell-0B1B33?style=for-the-badge&logo=github&logoColor=white" alt="GitHub"/></a>
  <a href="https://www.linkedin.com/in/subharaj-hait-9b24373a0"><img src="https://img.shields.io/badge/LinkedIn-Subharaj%20Hait-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"/></a>
  <!-- Add your email badge here:
  <a href="mailto:YOUR-EMAIL"><img src="https://img.shields.io/badge/Email-Get%20in%20touch-2F5D8F?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"/></a>
  -->
</p>

<sub>Languages: English · Hindi · Bengali</sub>
