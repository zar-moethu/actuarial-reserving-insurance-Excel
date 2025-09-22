## Actuarial Reserving Analysis using the Chain-Ladder Method

### 🧩 1. Business Problem

An insurance company's core challenge is managing future uncertainty. They collect premiums from customers today in exchange for a promise to pay for future events (claims) like car accidents or property damage.

A key question for any insurer is: 
"How much money do we need to set aside today to cover the costs of claims that have already happened but have not yet been fully paid?"

This amount of money is known as a loss reserve.
- If it’s too large, the company holds capital inefficiently, being unable to meet future obligations.
- If the reserve is too small, the company risks insolvency, impacting profitability and investment potential.

This project demonstrates the application of a fundamental actuarial reserving method, the Chain-Ladder Method, to estimate loss reserves using historical claims development data.

### 📊 2. Data Source

The data used in this project is a simulated dataset representing a realistic portfolio of homeowner's insurance claims (Line of Business H3).
The raw data, which would typically be extracted from a company's database, is a detailed claims listing containing:

#### 🧾 2.1 Raw Dataset Snapshot
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

  #### Chain-Ladder Method	Snapshot

<p align="center">
<img width="502" height="155" alt="image" src="https://github.com/user-attachments/assets/24c96d27-dff9-4454-bc98-793b9572573d" />
</p>

### 📈 Step 2: Calculate Age-to-Age Development Factors

### 📈 Step 2: Calculate Age-to-Age Development Factors

Age-to-age development factors were calculated to understand **how much the total claims for a given accident year increased between two points in time**.

The formula used is: Development Factor = Claims at later age / Claims at earlier age

#### 📊 Development Factors Snapshot

<p align="center">
  <img width="502" height="145" alt="image" src="https://github.com/user-attachments/assets/11299c52-0a30-4ef2-b168-b45a6689f2b6" />
</p>

As shown in the above snapshot, development factors are calculated for each accident year and each development period by dividing the claims reported at the later age by the claims reported at the earlier age.

For example, a development factor of **1.91** means that the claims increased by approximately **90%** between month 12 and month 24.






- Data Aggregation: The raw claims data was organized into a cumulative development triangle, showing how the total losses for each accident year have grown over time.
- Calculate Development Factors: Age-to-age loss development factors (LDFs) were calculated to measure the historical growth pattern from one development period to the next.
- Select Average Factors: A 3-Year Weighted Average was used to select the most appropriate LDFs for projection. This gives more weight to recent years with higher claim volumes, providing a stable and responsive estimate.
- Project Ultimate Losses: The selected LDFs were used to project the current cumulative claims for incomplete accident years to their estimated final, or "ultimate," value.
- Calculate IBNR Reserves: The final reserve was calculated by subtracting the latest reported claims from the projected ultimate loss. This reserve is also known as the IBNR (Incurred But Not Reported) reserve.



