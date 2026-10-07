1. Amazon EC2: The "Control & Flexibility" Problem

Amazon EC2 solves the problem of **rigid, unscalable physical hardware**. It gives you full root access to virtual servers in the cloud, allowing you to configure them precisely like an on-premises data center, but with instant scalability.

- **Instance Types:** Solve the problem of **mismatched workloads**. By offering specialized instances (Compute Optimized, Memory Optimized, Storage Optimized), AWS ensures you don't overpay for RAM when your application actually needs raw CPU processing power.
- **Pricing Models:** Solve the problem of **wasted infrastructure spend**:
    - **On-Demand:** Solves **unpredictable or short-term workloads**. You pay by the second with zero commitment.
    - **Spot Instances:** Solves the problem of **high costs for fault-tolerant, batch workloads**. It lets you buy unused AWS compute capacity at up to a 90% discount, with the trade-off that AWS can reclaim the server with a 2-minute warning.
    - **Reserved Instances & Savings Plans:** Solve the problem of **high baseline costs for predictable traffic**. By committing to a consistent amount of compute usage for 1 or 3 years, you drastically lower your hourly rates.