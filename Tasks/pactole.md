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
- [x] Define payment methods tracking ✅ 2025-12-30
- [x] Refine "other" category (reduced from 203 to 96 transactions) ✅ 2025-12-30

## Phase 3: Bank Accounts
- [x] List all bank accounts ✅ 2025-12-29
- [x] Define account structure (checking, savings, etc.) ✅ 2025-12-29
- [x] Record current balances (solde) ✅ 2025-12-29
- [x] Define account relationships ✅ 2025-12-29

## Phase 4: Projections
- [x] Define provisional bonus structure ✅ 2025-12-29
- [x] Define expected annual increases ✅ 2025-12-30
- [x] Define known future expenses ✅ 2025-12-30

## Phase 5: Data Sources & Paths
- [x] Path to pay slips ✅ 2025-12-29
- [x] Bank statement import format ✅ 2025-12-30
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
- ~~Refine categorization rules for "other" category~~ ✅
- Add bank statement import format documentation

### 2025-12-30: Phase 2 Complete
**Categorization refined:**
- Added 50+ new patterns covering restaurants, hotels, subscriptions, gifts, pets
- Separated business (Capacitor) expenses from personal (is_business_expense flag)
- Internal transfers properly excluded (credit card statements, account transfers)
- Reduced uncategorized from 203 (70k EUR) → 96 (9.2k EUR)

**Updated expense summary (personal only):**
| Category | Amount | Monthly Avg |
|----------|--------|-------------|
| Housing | 62,777 EUR | 5,231 |
| Utilities | 15,544 EUR | 1,295 |
| Subscriptions | 12,346 EUR | 1,029 |
| Taxes | 10,970 EUR | 914 |
| Other (bank fees, electronics) | 9,251 EUR | 771 |
| Food | 8,582 EUR | 715 |
| Insurance | 6,158 EUR | 513 |
| Professional | 4,483 EUR | 374 |
| Transport | 1,914 EUR | 159 |
| Gifts | 1,601 EUR | 133 |
| Travel | 1,207 EUR | 101 |
| Entertainment | 891 EUR | 74 |
| Clothing | 478 EUR | 40 |
| Pets | 204 EUR | 17 |
| Health | 186 EUR | 16 |
| **TOTAL** | **136,591 EUR** | **11,383** |

**Business expenses (Capacitor):** 21,209 EUR
**Internal transfers (excluded):** 283,364 EUR

**Payment methods tracking added:**
- PaymentMethod enum: CARD, DIRECT_DEBIT, TRANSFER, CHECK, CASH, INTERNAL, OTHER
- Automatic detection from transaction description
- 13 unit tests for payment method detection

**Files modified:**
- `pactole/services/categorizer.py` - Expanded rules, added CategorizedTransactions
- `pactole/services/bank_parser.py` - Added PaymentMethod enum and detection
- `tests/test_bank_parser.py` - Added 13 payment method tests
- `scripts/analyze_other.py` - Enhanced analysis with payment methods

### 2025-12-30: Phase 4 Complete
**Projections added to financial_config.yaml:**

**Annual increase assumptions:**
- Salary: 3.8% per year
- Expense inflation: 2.5% per year (general)

**Bonus projections (based on last 2 years):**
- MIC: ~18,500 EUR/year (March)
- LTCI: Time-vested portions ($7.9k-$16.3k/year depending on year)
- Retention: 3 x 62,100 EUR remaining (Dec 2025, Dec 2026 x2)

**Known future expenses:**
| Expense | Amount | Date | Priority |
|---------|--------|------|----------|
| House windows | 20,000 EUR | Feb 2026 | High |
| House painting | 10,000 EUR | Apr 2026 | Medium |
| Kitchen renovation | 15,000 EUR | S2 2026/S1 2027 | Medium (flexible) |
| **TOTAL** | **45,000 EUR** | | |

**5-year salary projection:**
| Year | Gross Monthly | Annual Gross |
|------|---------------|--------------|
| 2025 | 10,948 EUR | 131,371 EUR |
| 2026 | 11,364 EUR | 136,363 EUR |
| 2027 | 11,796 EUR | 141,553 EUR |
| 2028 | 12,244 EUR | 146,932 EUR |
| 2029 | 12,710 EUR | 152,516 EUR |
| 2030 | 13,193 EUR | 158,312 EUR |

### 2025-12-30: Phase 5 Complete - TASK COMPLETE
**Bank statement import format documented:**
- Created `docs/bank_statement_formats.md`
- Documented 3 bank formats: Credit Mutuel, CIC, Revolut Business
- Includes: column mappings, encoding, export instructions, file naming conventions
- Auto-detection rules documented

**All input data now defined:**
- Phase 1: Revenue (salary, bonuses, rental)
- Phase 2: Expenses (16 categories, payment methods)
- Phase 3: Accounts (personal, business, investments, loans)
- Phase 4: Projections (salary increases, future expenses)
- Phase 5: Data sources (paths, import formats)

