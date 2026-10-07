**AWS Migration Hub** is ==a centralized management console that enables you to discover on-premises servers, plan cloud transformation pathways, and track the real-time status of application migrations across multiple AWS and partner tools==. [[1](https://docs.aws.amazon.com/migrationhub/latest/ug/whatishub.html), [2](https://www.youtube.com/watch?v=kunFdhot8Go&t=331)]

---

Core Migration Hub Components

|Feature / Component|Primary Function|Pricing Model|
|---|---|---|
|**Discovery Tools**|Gathers server configuration, usage, and network dependency data.|**Free** (No additional charge)|
|**Strategy Recommendations**|Analyzes application portfolios to suggest optimal modernization paths.|**Free** (No additional charge)|
|**Migration Hub Orchestrator**|Automates multi-step migration workflows using predefined templates.|**Free** (Standard resource fees apply)|
|**Tracking Dashboard**|Aggregates live progress and status from AWS Application Migration Service (MGN) and [AWS Database Migration Service (DMS)](https://aws.amazon.com/dms/).|**Free** (No additional charge)|

---

How AWS Migration Hub Operates

- **Home Region Selection:** Stores all tracking and portfolio data in a single designated home Region within the [AWS Management Console](https://docs.aws.amazon.com/migrationhub/). [[1](https://docs.aws.amazon.com/migrationhub/latest/ug/whatishub.html), [2](https://www.techtarget.com/it-infrastructure/definition/What-is-AWS-Migration-Hub)]
- **Resource Grouping:** Allows engineers to logically group disparate servers and databases into functional "applications" for coordinated migration waves. [[1](https://docs.aws.amazon.com/migrationhub/latest/ug/whatishub.html), [2](https://www.techtarget.com/it-infrastructure/definition/What-is-AWS-Migration-Hub)]
- **Network Visualization:** Maps out dependency diagrams to reveal communication links between local servers before executing cutovers. [[1](https://docs.aws.amazon.com/migrationhub/latest/ug/whatishub.html), [2](https://www.techtarget.com/it-infrastructure/definition/What-is-AWS-Migration-Hub)]
- **Tool Integration:** Captures status feeds from services like DMS and MGN to provide a single pane of glass view, eliminating the need to monitor separate utility dashboards.
    
    [[1](https://www.youtube.com/watch?v=kunFdhot8Go&t=331), [2](https://www.youtube.com/watch?v=gmStMc-zr08&t=921)]

---

Availability and Transition Notes

While existing user workflows remain supported, new platform capabilities and customer onboarding for traditional legacy dashboard paths have largely transitioned toward integrated tools like [AWS Transform](https://aws.amazon.com/transform/) for automated modernization. [[1](https://docs.aws.amazon.com/migrationhub/latest/ug/whatishub.html)]