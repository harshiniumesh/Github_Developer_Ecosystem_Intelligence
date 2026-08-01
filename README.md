# 📊 GitHub Developer Ecosystem Intelligence Power BI Dashboard

An interactive, multi-page Power BI dashboard providing end-to-end intelligence on open-source developer activity, repository health, community engagement, and tech stack adoption trends.

---

## 📑 Dashboard Architecture & Screenshots

### Page 1: Executive Overview & Ecosystem Pulse
*High-level strategic view of global open-source repository performance and developer reach.*

![Page 1 - Executive Overview](assets/1.png)

* **Key Metrics:** Total Active Repositories, Cumulative Stars, Merged PRs, Active Contributors.
* **Core Visuals:** Interactive World Map (Developer Density), Monthly Commit Trendlines, and Global Event Distribution.

---

### Page 2: Developer Engagement & Community Dynamics
*Operational insights focused on developer workflows, PR turnaround times, and issue tracking.*

![Page 2 - Community Dynamics](assets/2.png)

* **Key Metrics:** Median PR Resolution Time, Time-to-First-Review, Issue Close Rate.
* **Core Visuals:** PR Lead Time Funnel, Contributor Cohort Matrix (New vs. Returning Maintainers).

---

### Page 3: Tech Stack & Repository Insights
*Comparative analysis of programming language trends, framework adoption, and growth velocity.*

![Page 3 - Tech Stack Insights](assets/3.png)

* **Key Metrics:** Top Languages by Repo Share, Fork-to-Star Ratios, Growth Momentum.
* **Core Visuals:** Language Market Share Matrix, Repository Velocity Scatter Plot (Stars vs. Forks).

---

## 🛠️ Data Architecture & DAX Modeling

The dashboard relies on a normalized **Star Schema** centered around GitHub event facts:

* **Fact Tables:** `Fact_Commits`, `Fact_PullRequests`, `Fact_Issues`
* **Dimension Tables:** `Dim_Developer`, `Dim_Repository`, `Dim_Date`, `Dim_Language`

### Key DAX Measures

#### 1. Average PR Cycle Time (Hours)
```dax
Avg_PR_Cycle_Time_Hours = 
AVERAGEX(
    FILTER('Fact_PullRequests', 'Fact_PullRequests'[State] = "Closed"),
    DATEDIFF('Fact_PullRequests'[created_at], 'Fact_PullRequests'[merged_at], HOUR)
)
