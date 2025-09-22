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

##### 🧾 2.1 Raw Dataset Table Snapshot
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

  ##### Chain-Ladder Method	Table Snapshot

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

##### Calculated Averaged Development Factors Table Snapshot

<p align="center">
<img width="486" height="75" alt="Screenshot 2025-09-22 at 21 57 44" src="https://github.com/user-attachments/assets/3fb7dfa4-91ab-4185-841f-a45bce6e550b" />
</p>

In this case, both the simple and weighted averages are almost identical but in real-world scenarios, they often differ depending on claim volume and volatility.

#### ⛓️ Step 4: Select Development Factors (Selected LDFs) and Calculate Cumulative Development Factors (CDFs)

To project the ultimate loss for each accident year , we first need to select a single development factor for each age interval. In this project, the 3-Year Simple Average was chosen because it was nearly identical to the weighted average, and the historical data showed no significant volatility or trends.

Once selected, these factors (often called LDFs) help us understand how much claims typically grow from one development period to the next.

We then calculate the Cumulative Development Factor (CDF) for each age which tells us how much the current reported claims are expected to grow until they reach their final (ultimate) value.

📌 CDF = LDF₁ × LDF₂ × ... × LDFₙ

##### 📊 Selected Development Factors & CDF Table Snapsot
<p align="center"> <img width="479" height="46" alt="Screenshot 2025-09-22 at 22 26 56" src="https://github.com/user-attachments/assets/6641df18-3312-42e7-859c-56ce46d0da60" /> </p>


#### 📁 Key Fields in the above table:
- **Selected LDFs** show how much claims are expected to grow from one development period to the next (e.g. from month 12 to 24).
- **CDFs** show the total expected development from a specific age to the final ultimate claim value — in other words, how much more development is expected from that point onward.

####  🔍 Step 5: Results

The final step is to use the calculated factors to project the ultimate loss for the most recent accident year and determine the required reserve. This provides the key business insight for the analysis.

#### Calculation for Accident Year 2024: 

The ultimate loss and the required reserve are calculated as follows:

- Latest Reported Claims (at 12 months): $385,000
- Cumulative Development Factor (CDF): 2.35
- Projected Ultimate Loss: $385,000 × 2.35 = $905,000
- Required Reserve (IBNR): $905,000 - $385,000 = $520,000

##### 📋 Final Output Snapshot – Accident Year 2024

The table below summarises the Chain-Ladder Method output for accident year 2024, based on historical claim development patterns.

<p align="center"> <img width="584" height="166" alt="Screenshot 2025-09-23 at 08 20 10" src="https://github.com/user-attachments/assets/b23fb006-f4be-435c-8a57-8eb018488f3c" />
 </p>

#### Interpretation:

- The results show that while only $385,000 in claims have been reported for the 2024 accident year so far, the total expected cost, or Ultimate Loss, is projected to be $905,000.

- The difference, $520,000, is the required IBNR (Incurred But Not Reported) reserve. This is the amount the insurer must hold to cover the future development of known claims and the emergence of claims that have already occurred but have not yet been reported.



#### 💰 6. What This Means for the Business

While only $385,000 in claims have been reported for the 2024 accident year so far, the analysis projects that the total final cost—the Ultimate Loss—will be $905,000.
The difference of $520,000 is the IBNR (Incurred But Not Reported) reserve. This is the crucial number for the business. By setting aside this reserve, the insurer ensures it has adequate funds to cover all future payments related to 2024. 

This supports:

- Financial Stability: Guaranteeing all future claims can be paid.
- Regulatory Compliance: Meeting legally required reserve levels.
- Accurate Planning: Understanding the full financial picture of past events, not just what has been reported so far.

This forward-looking approach ensures the insurer is financially prepared for the full cost of the accident year, rather than reacting only to claims as they are reported. It is this data-driven estimate that is critical for ensuring the company's financial stability.


📂 **Project Files**

You can download the Excel file used for this project below:

🔗 [**Calculation & Data.xlsx**](https://github.com/zar-moethu/actuarial-reserving-insurance-Excel/blob/main/Calculation%20%26%20Data.xlsx)

### 🙌 Analyst's Note

- I believe every analyst’s journey is strengthened by an open mindset and a willingness to receive feedback. I welcome your thoughts, suggestions, and collaboration on this actuarial projection project.

- Feel free to download, explore, and adapt the Excel workbook or development steps for your own learning or analytical purposes  whether you're studying loss reserving techniques or applying them in practice.

📬 If you have feedback or would like to collaborate on future projects, don’t hesitate to reach out.

⚠️ **Disclaimer**: This analysis and dataset are intended for educational and demonstration purposes only not for business or  operational or financial reporting use.


