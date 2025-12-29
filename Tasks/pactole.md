# Pactole - Define All Input Data

**Priority:** Q1
**Size:** #L
**Started:** 2025-12-29
**Project:** Pactole (Personal Finance)
**Source:** /Users/gael/Sources/pactole

---

## Phase 1: Revenue Definition
- [x] Define salary structure (base, bonuses, etc.) ✅ 2025-12-29
- [x] Define path to pay slips ✅ 2025-12-29
- [x] Define other income sources (if any) ✅ 2025-12-29

## Phase 2: Expense Categories
- [x] Define expense categories (housing, food, transport, etc.) ✅ 2025-12-29
- [x] Define recurring vs variable expenses ✅ 2025-12-29
- [x] Analyze bank statements to populate actual data ✅ 2025-12-29
- [ ] Define payment methods tracking
- [ ] Refine "other" category (155 uncategorized transactions)

## Phase 3: Bank Accounts
- [x] List all bank accounts ✅ 2025-12-29
- [x] Define account structure (checking, savings, etc.) ✅ 2025-12-29
- [x] Record current balances (solde) ✅ 2025-12-29
- [x] Define account relationships ✅ 2025-12-29

## Phase 4: Projections
- [x] Define provisional bonus structure ✅ 2025-12-29
- [ ] Define expected annual increases
- [ ] Define known future expenses

## Phase 5: Data Sources & Paths
- [x] Path to pay slips ✅ 2025-12-29
- [ ] Bank statement import format
- [x] Other data sources ✅ 2025-12-29

---

## Notes

### 2025-12-29: Phase 1 Complete
**Revenue structure defined:**
- Monthly: Net salary, car allowance, rental income
- Annual: LTCI, MIC, retention plan, dividends

**Files created:**
- `pactole/models/revenue.py` - RevenueType, Frequency enums + RevenueSource dataclass
- `tests/test_revenue.py` - Unit tests
- `data/revenue_config.yaml` - Configuration template (needs actual values)

**Pay slips path:** `/Users/gael/Documents/Perso/Harman/pay_slip`
- Pattern: `YYYY_MM_martinet_gael_*.pdf`

### 2025-12-29: Phase 3 & 4 (partial) Complete
**Accounts defined:**
- Personal: Credit Mutuel (perso + joint), Trade Republic, Revolut perso
- Company (Capacitor): Revolut business, CIC
- Investments: Gold ETF, Apple stock, GBP money market funds
- Retirement: Natixis PEE, Generali La Retraite
- Loans: House (-204,604 EUR), Pool (-108,837 EUR)

**Bonus structure documented:**
- MIC: 20% target, CY24 = 18,520 EUR
- LTCI 2024: $34k target (vests 2025-2027)
- LTCI 2025: $36k target (vests 2026-2028)
- Retention: 4 x 62,100 EUR (Dec 2024-2026)

**Files created:**
- `pactole/models/account.py` - Account, Investment, Loan models
- `tests/test_account.py` - 5 unit tests
- `data/financial_config.yaml` - Complete financial data

### 2025-12-29: Phase 2 (partial) Complete
**Expense model created with 16 categories:**
Housing, Utilities, Insurance, Transport, Food, Health, Education, Entertainment, Subscriptions, Taxes, Clothing, Gifts, Travel, Children, Pets, Professional, Other

**Files created:**
- `pactole/models/expense.py` - Expense, RecurringExpense, MonthlyBudget models
- `tests/test_expense.py` - 6 unit tests

### 2025-12-29: Bank Statement Analysis Complete
**Parsers created for:**
- Credit Mutuel (French CSV, `;` delimiter)
- CIC Pro (French CSV, `;` delimiter)
- Revolut Business (UTF-8 CSV)

**Files created:**
- `pactole/services/bank_parser.py` - Transaction parser with auto-detection
- `pactole/services/categorizer.py` - Auto-categorization with pattern matching
- `tests/test_bank_parser.py` - 12 tests

**2025 Expense Summary (531 transactions):**
| Category | Amount | Monthly Avg |
|----------|--------|-------------|
| Housing (loans + DIY) | 45,528 EUR | 3,794 |
| Other (uncategorized) | 41,891 EUR | 3,491 |
| Utilities | 13,966 EUR | 1,164 |
| Taxes | 10,661 EUR | 888 |
| Subscriptions | 6,509 EUR | 542 |
| Food | 5,640 EUR | 470 |
| Insurance | 3,477 EUR | 290 |
| Transport | 1,656 EUR | 138 |
| **TOTAL** | **~130,036 EUR** | **~10,836** |

**Next steps:**
- Refine categorization rules for "other" category
- Add bank statement import format documentation

