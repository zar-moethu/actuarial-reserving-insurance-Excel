## Actuarial Reserving Analysis using the Chain-Ladder Method

### 🧩 1. Business Problem

An insurance company's core challenge is managing future uncertainty. They collect premiums from customers today in exchange for a promise to pay for future events (claims) like car accidents or property damage.

A key question for any insurer is: 
"How much money do we need to set aside today to cover the costs of claims that have already happened but have not yet been fully paid?"

This amount of money is known as a loss reserve.
- If it’s too large, the company holds capital inefficiently, being unable to meet future obligations.
- If the reserve is too small, the company risks insolvency, impacting profitability and investment potential.
  
This project demonstrates the application of a fundamental actuarial reserving method, the Chain-Ladder Method, to estimate the required loss reserve for a portfolio of claims using historical claims development data.

### 📊 2. Data Source

The data used in this project is a simulated dataset representing a realistic portfolio of homeowner's insurance claims (Line of Business H3).
The raw data, which would typically be extracted from a company's database, is a detailed claims listing containing:

#### 🧾 2.1 Raw Dataset Table Snapshot
<p align="center">
 <img width="261" height="330" alt="Screenshot 2025-09-22 at 21 18 26" src="https://github.com/user-attachments/assets/35f50bae-a0af-4366-a97a-abbe1f9eb29e" />
</p>


#### 📁 Key Fields in the Dataset:
- **Line of Business**: Homeowner's Insurance
- **Accident Year**: Year the insured loss event occurred  
- **Development Age**: Age of the claim in months (e.g., 12, 24, 36)  
- **Claim Size**: Transaction amount reported at each development point

This raw data was aggregated to produce the Cumulative Reported Claims Triangle used in this analysis.

### ⚙️ 3. Methodology

The Chain-Ladder Method was used to project the ultimate losses. This is a standard industry technique that uses historical data to predict future development. The process involved several key steps:

#### 📐 Step 1: Construct the Cumulative Reported Claims Triangle

- The raw claim-level data is **aggregated** by:
  - Accident Year (row)
  - Development Age (column)
  - Each cell shows the **cumulative reported claims** as of that development month.

  #### Chain-Ladder Method	Table Snapshot

<p align="center">
<img width="502" height="155" alt="image" src="https://github.com/user-attachments/assets/24c96d27-dff9-4454-bc98-793b9572573d" />
</p>

#### 📈 Step 2: Calculate Age-to-Age Development Factors


Age-to-age development factors were calculated to understand **how much the total claims for a given accident year increased between two points in time**.

The formula used is: Development Factor = Claims at later age / Claims at earlier age

#### Development Factors Table Snapshot

<p align="center">
  <img width="502" height="145" alt="image" src="https://github.com/user-attachments/assets/11299c52-0a30-4ef2-b168-b45a6689f2b6" />
</p>

As shown in the above snapshot, development factors are calculated for each accident year and each development period by dividing the claims reported at the later age by the claims reported at the earlier age.

For example, a development factor of **1.91** means that the claims increased by approximately **90%** between month 12 and month 24.

#### 📊 Step 3: Calculate Averaged Development Factors

To smooth out volatility across accident years and prepare stable estimates for projecting future claims, we calculate two types of averages:

**3-Year Simple Average**
The arithmetic mean of the most recent three development factors for each period (e.g. 12–24, 24–36, etc.).

**3-Year Weighted Average**
Averages that give more weight to years with larger claim volumes, which can produce more stable and responsive estimates.

#### ✅ Calculated Averaged Development Factors Table Snapshot

<p align="center">
<img width="486" height="75" alt="Screenshot 2025-09-22 at 21 57 44" src="https://github.com/user-attachments/assets/3fb7dfa4-91ab-4185-841f-a45bce6e550b" />
</p>

In this case, both the simple and weighted averages are almost identical but in real-world scenarios, they often differ depending on claim volume and volatility.

#### ⛓️ Step 4: Select Development Factors (Selected LDFs) and Calculate Cumulative Development Factors (CDFs)

To project the ultimate loss for each accident year , we first need to select a single development factor for each age interval. In this project, the 3-Year Simple Average was chosen because it was nearly identical to the weighted average, and the historical data showed no significant volatility or trends.

Once selected, these factors (often called LDFs) help us understand how much claims typically grow from one development period to the next.

We then calculate the Cumulative Development Factor (CDF) for each age which tells us how much the current reported claims are expected to grow until they reach their final (ultimate) value.

📌 CDF = LDF₁ × LDF₂ × ... × LDFₙ

#### 📊 Selected Development Factors & CDF Table Snapsot
<p align="center"> <img width="479" height="46" alt="Screenshot 2025-09-22 at 22 26 56" src="https://github.com/user-attachments/assets/6641df18-3312-42e7-859c-56ce46d0da60" /> </p>


#### 📁 Key Fields in the above table:
- **Selected LDFs** show how much claims are expected to grow from one development period to the next (e.g. from month 12 to 24).
- **CDFs** show the total expected development from a specific age to the final ultimate claim value — in other words, how much more development is expected from that point onward.

### 💰 Step 5: Project Ultimate Losses

In this project, we calculate the ultimate loss for accident year 2024. This is done by taking the most recent cumulative reported claim amount and multiplying it by the corresponding Cumulative Development Factor (CDF).

The ultimate loss represents the total expected cost of all claims from 2024, including both the claims already reported and those that may have occurred but are not yet reported. So far, only $385,000 of claims have been reported (after 12 months), but additional claims are expected to emerge over time.

**Formula:**  
📌 *Ultimate Loss = Latest Reported Claims × CDF*


#### 📊 Calculation for Accident Year 2024:

- **Latest Reported Claims (at 12 months)** = \$385,000  
- **CDF (from 12 months to ultimate)** = 2.35  
- **Projected Ultimate Loss** = \$385,000 × 2.35 = **\$905,000**

This means the Ultimate Loss column  shows the total expected cost of all claims for 2024 - **\$905,000**

### 🧾 Calculate IBNR (Incurred But Not Reported)

Once we have the ultimate loss estimate, we can calculate the IBNR reserve, the portion of incurred losses that have occurred but are not yet reported.

**Formula:**  
📌 *IBNR = Ultimate Loss − Latest Reported Claims*

#### 🧮 IBNR Reserve for 2024:

- **IBNR** = \$905,000 − \$385,000 = **\$520,000**

This means the insurer should hold **\$520,000** in reserve for claims from accident year 2024 that have occurred but have not yet been reported.

#### 📋 Final Output Snapshot – Accident Year 2024 (shown in red)

<p align="center"> <img width="612" height="170" alt="Chain-Ladder Final Output for 2024" src="https://github.com/user-attachments/assets/51cb45a1-a09f-46cc-878d-405931a4771a" /> </p>


 ### 🧠 Step 6: What Does This Mean for the Business?

As of 12 months into accident year 2024, only $385,000 in claims have been reported. However, based on historical development patterns, the total ultimate loss is projected to be $905,000. This includes:

- Reported claims: $385,000
- Claims that have occurred but not yet been reported (IBNR): $520,000

This projection means the insurer should expect additional claims to be reported over time that relate to events that have already occurred in 2024.

By recognising the IBNR, the insurer can ensure sufficient reserves are held to meet future obligations  even if those claims have not yet been reported. This supports sound financial planning, regulatory compliance, and a more accurate picture of the insurer’s total liabilities.




📂 **Project Files**

- *Power BI Dashboard File* (Then, Click on View Raw):  
  [WeatherDashboard.pbix](https://github.com/zar-moethu/weather-AQI-dashboard-nz-powerbi/blob/main/WeatherReport%20(VF).pbix)
- *Dashboard Overview (PDF Preview)*:  
  [Dashboard Overview (PDF)](https://github.com/zar-moethu/weather-AQI-dashboard-nz-powerbi/blob/main/Dashboard%20Overview.pdf)

  ⚠️ **Disclaimer:**



