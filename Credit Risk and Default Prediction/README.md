# Credit Risk and Default Prediction

## Introduction

Credit risk refers to the likelihood that a borrower will fail to repay a loan. Rather than simply asking *if* a borrower will default, this project focuses on *when* repayment happens. Using survival analysis techniques, I explored the timing of loan repayment across different types of borrowers using real-world data.

This project applies the **Kaplan-Meier estimator** to estimate survival functions — or, in this context, the duration over which a loan remains unpaid. It also includes subgroup comparisons and median repayment durations to interpret behavioral differences across borrower groups.

The analysis draws from two datasets:
- A **telecommunications churn dataset** from [Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
- A **German credit risk dataset** from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/144/statlog+german+credit+data)

---

## Data

- **Telco Churn**: Customer subscription and churn data from a telecommunications company.
- **German Credit Risk**: Financial and demographic data on loan applicants, including repayment status.
- **Key Fields**: `duration` (loan length in months), `full_repaid` (1 if repaid, 0 if not), `credit_history`, and `telephone` ownership.

---

## Conceptual Background

Survival analysis is used to study the time until an event occurs. Here, the "event" is loan repayment or customer churn. The **Kaplan-Meier estimator** models the probability of surviving past a given time — in this case, the probability a loan is still unpaid at a given point in time.

We also interpret group-based differences to uncover patterns, such as whether borrowers with a certain credit history repay sooner, or whether phone ownership correlates with slower repayment behavior.

---

## Data Preparation and Baseline Survival Curves

Both datasets were cleaned and processed for use in survival analysis:
- Non-numeric fields were converted to binary or categorical formats.
- Missing or malformed values (e.g., in `TotalCharges`) were handled appropriately.
- The `duration` and `event` columns were extracted for modeling.

Kaplan-Meier curves were then created for:
- Telco customer churn
- Overall loan repayment behavior

These baseline curves helped establish general repayment patterns before subgroup analysis.

---

## Exploring Key Features and Group Differences

To better understand how borrower characteristics impact repayment, we compared survival curves across subgroups.

### Credit History

- **existing_credit_paid**: These borrowers have a history of successfully repaying previous loans. Their median repayment duration is **24 months**, indicating consistent, moderate repayment behavior. Lenders may view this group as relatively low risk with predictable outcomes.

- **critical_account**: Borrowers in this category have existing overdue loans or problematic credit records. Their loans typically end in **18 months**, which seems fast, but is likely due to **early default or charge-off** rather than full repayment. This group represents higher credit risk, with repayment disruptions occurring earlier in the loan lifecycle.

- **delay_in_paying**: This group has a record of past delays in making payments. Surprisingly, they exhibit the **longest median duration of 27 months** — suggesting that although repayment is slower, these borrowers often **eventually fulfill their obligations**. Their behavior may reflect negotiated or extended payment plans.

### Telephone Ownership

- **Has phone**: Borrowers with a phone take **24 months** on average to repay. Access to a phone may facilitate **ongoing communication with lenders**, allowing for **rescheduling or restructuring** of payments. This can result in longer, more flexible repayment timelines, though not necessarily higher default risk.

- **No phone**: This group repays faster, with a median of **21 months**. Without direct lines of communication, these borrowers may face **stricter repayment conditions** or may be less likely to negotiate deferrals — which could incentivize quicker repayment. Their behavior may also reflect **greater urgency or financial discipline** under constraint.

---

## Survival Time Insights and Summary

To quantify repayment behavior, we calculated **median survival times** for each group. These values represent the point at which half the borrowers in a group have completed repayment.

| Feature             | Group                      | Median Duration (Months) | Interpretation                                      |
|---------------------|----------------------------|---------------------------|-----------------------------------------------------|
| Credit History       | Existing Credit Paid       | 24                        | Steady repayment behavior                           |
|                      | Critical Account           | 18                        | Earlier repayment or higher early default risk      |
|                      | Delay in Paying            | 27                        | Longest timeline, but eventual repayment            |
| Telephone Ownership  | Has Telephone              | 24                        | Slower repayment, possibly due to negotiation       |
|                      | No Telephone               | 21                        | Faster repayment, possibly fewer financial levers   |

These median durations provide context beyond the visual survival curves and reinforce the observed behavioral differences between subgroups.

---

## Final Insights

This project demonstrated how survival analysis can uncover not just whether borrowers repay loans, but **how long** they take to do so. By comparing subgroups like credit history and phone ownership, we gained insight into behavioral patterns that may inform lending decisions.

Visual tools like Kaplan-Meier curves, paired with summary statistics like median survival time, offer a powerful way to interpret repayment dynamics over time.