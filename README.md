Actuarial Reserving Analysis using the Chain-Ladder Method

🧩 1. Business Problem

An insurance company's core challenge is managing future uncertainty. They collect premiums from customers today in exchange for a promise to pay for future events (claims) like car accidents or property damage.

A key question for any insurer is: 
"How much money do we need to set aside today to cover the costs of claims that have already happened but have not yet been fully paid?"

This amount of money is known as a loss reserve.
- If it’s too large, the company holds capital inefficiently, being unable to meet future obligations.
- If the reserve is too small, the company risks insolvency, impacting profitability and investment potential.

This project demonstrates the application of a fundamental actuarial reserving method, the Chain-Ladder Method, to estimate loss reserves using historical claims development data.

📊 2. Data Source

The data used in this project is a simulated dataset representing a realistic portfolio of homeowner's insurance claims (Line of Business H3).
The raw data, which would typically be extracted from a company's database, is a detailed claims listing containing:
# 🧾 2.1 Raw Dataset Snapshot
          <p align="center">
          <img width="261" height="330" alt="Screenshot 2025-09-22 at 21 18 26" src="https://github.com/user-attachments/assets/35f50bae-a0af-4366-a97a-abbe1f9eb29e" />

# 📁 Key Fields in the Dataset:
- **Line of Business**: Homeowner's Insurance  
- **Accident Year**: Year the insured loss event occurred  
- **Development Age**: Age of the claim in months (e.g., 12, 24, 36)  
- **Claim Size**: Transaction amount reported at each development point

This raw data was aggregated to produce the Cumulative Reported Claims Triangle used in this analysis.

