# Network-Anomaly-Detection-Using-Clustering-methods
### The task is to build network intrusion detection system to detect anomalies and attacks in the Network.

This study applies unsupervised clustering to the KDD Cup ’99 network‑traffic subset to detect anomalous (attack) flows without using labelled data at inference time. After data cleaning and exploratory analysis, a K‑Means model with K = 3 achieved a 79.9 % attack‑detection rate at a 0.6 % false‑alarm rate, outperforming multiple DBSCAN configurations. Visual and statistical analyses identify byte counts and host/service request rates as primary discriminators.

### Methodology
**K‑Means Baseline**

Silhouette scan (K = 2–6) suggested K = 2 (0.2445) ≈ K = 3 (0.2443).
Chose K = 3 to allow a dedicated attack cluster.
Used init='k‑means++', n_init='auto', max_iter=300.

![Screenshot 2025-05-29 at 12 57 22 pm](https://github.com/user-attachments/assets/89a4f8c0-93b3-48d6-a940-28632736ec99)

![Screenshot 2025-05-29 at 12 57 45 pm](https://github.com/user-attachments/assets/f74a26da-0cfc-40df-be09-9cc32c97e851)

**Density‑Based Scan (DBSCAN)**

Two grids explored: eps ∈ {0.3,0.5,0.7} & wider eps ∈ {1.0,1.5,2.0} with min_samples ∈ {5,10,15} on a 20 k sample.
Best detection = 8 % (eps = 1.0, ms = 10); false alarms 11 %.

**Discussion**

The K‑Means model meets the assessment’s twin goals: high detection (≈ 80 %) and low false‑alarm burden (< 1 %). DBSCAN struggled in the 122‑D Euclidean space—a common effect of the curse of dimensionality—producing either excessive noise or poor recall. Principal‑component or auto‑encoder compression could improve density‑based methods in future work.

Feature analysis suggests that attacks in this subset generate much larger byte counts and aggressive host/service request rates. These insights can inform threshold‑based alarms or feature engineering for any follow‑up supervised models.

![Screenshot 2025-05-29 at 12 58 50 pm](https://github.com/user-attachments/assets/cd95ac1f-a0ff-422a-848d-c41143c26709)

![Screenshot 2025-05-29 at 12 59 31 pm](https://github.com/user-attachments/assets/99cb77fb-c8ce-48ad-862f-74da957c5f59)

**Limitations**

20 % of attacks remain hidden inside normal clusters—primarily low‑volume or stealthy probes.

No temporal features were used; session‑based aggregation may expose additional patterns.

Results are validated on the same historical dataset; live deployment would need drift monitoring.

**Conclusion**

Unsupervised K‑Means clustering, with minimal tuning, successfully isolates the majority of malicious traffic in the KDD Cup ’99 subset while keeping false alerts under one percent. Byte‑count and host‑request features are the most indicative of anomalous behaviour. Future extensions should explore dimensionality reduction for density‑based methods and incorporation of temporal windows for evolving attack signatures.

