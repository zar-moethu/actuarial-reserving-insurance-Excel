Actuarial Loss Reserving Analysis using the Chain-Ladder Method

1. Business Problem
An insurance company's core challenge is managing future uncertainty. They collect premiums from customers today in exchange for a promise to pay for future events (claims) like car accidents or property damage.
A key question for any insurer is: "How much money do we need to set aside today to cover the costs of claims that have already happened but have not yet been fully paid?"
This pool of money is known as a loss reserve. If the reserve is too small, the company could become insolvent. If it's too large, the company is holding capital inefficiently. This project demonstrates the fundamental actuarial method used to estimate this reserve.



2. Data Source
The data used in this project is a simulated dataset representing a realistic portfolio of homeowner's insurance claims (Line of Business H3).
The raw data, which would typically be extracted from a company's database, is a detailed claims listing containing:

          <img width="268" height="332" alt="Screenshot 2025-09-22 at 21 01 59" src="https://github.com/user-attachments/assets/7ade11ce-f892-44b8-bd16-b346636b54e7" />

- Development Age: The age of the claim in months.
- Accident Year: The year the claim event occurred.
- Claim Size: The value of the transaction.

This raw data was aggregated to produce the Cumulative Reported Claims Triangle used in this analysis.

