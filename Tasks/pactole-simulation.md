# Pactole - Financial Simulation & Retirement Planning

**Priority:** Q2
**Size:** #L
**Started:** 2025-12-30
**Project:** Pactole (Personal Finance)
**Source:** /Users/gael/Sources/pactole

---

## Context

**Goal:** Build a financial simulation tool to optimize investment strategy and plan retirement.

**Key parameters:**
- Current age: 55 (in Feb 2025)
- Target retirement: 65 (~10 years)
- Planning horizons: 5, 10, 15, 20 years
- Scenarios: With/without Capacitor company
- **Household**: Include wife's income & retirement
- **Estate**: Real estate valuation, succession planning

**Philosophy:** Complex simulations, simple software (KISS)

---

## Phase 0: Complete Input Data ✅
- [x] Add wife's salary and income data
- [x] Add wife's retirement estimate (relevé de carrière)
- [x] Estimate primary residence value
- [x] Estimate other real estate (if any) → none besides primary
- [x] Document children (for succession planning)

## Phase 1: Projection Engine ✅
- [x] Load financial config (YAML → Python objects)
- [x] Monthly cash flow calculator (household income - expenses)
- [x] Multi-year projection (compound growth, inflation)
- [x] Handle one-time future expenses
- [x] Handle loan payoff dates (house 2036, pool 2034)

## Phase 2: Investment Modeling ✅
- [x] Define investment return assumptions (conservative/moderate/aggressive)
- [x] Model French investment vehicles (PEA, Assurance-vie, PER, CTO)
- [x] Model investment account growth over time
- [x] Model retirement account contributions & growth (PEE, Generali)
- [x] Currency handling (EUR, USD, GBP)
- [x] French tax modeling (PFU vs barème, social charges)

## Phase 3: Scenario System ✅
- [x] Define scenario data structure (`models/scenario.py`)
- [x] BusinessEntity model for holding companies (Capacitor)
- [x] ScenarioRunner service for projections
- [x] Capacitor scenarios: A (keep+rent), B (keep-no rent), C (liquidate)
- [x] ScenarioComparator for side-by-side comparison
- [x] CLI command: `pactole scenarios`
- [x] PEE/PER contributions modeling (4,610€/year until 2036)
- [x] Rental income pulled from config (1,000€/month)
- [x] Comprehensive test suite (28 tests)

**Current findings (15 years, 2025-2039):**
| Scenario | Total Net Worth |
|----------|-----------------|
| A: Keep + Rent | 1,205k€ |
| B: Keep - No Rent | **1,559k€** ← Winner |
| C: Liquidate | 1,233k€ |

**TODO:** Verify Capacitor monthly expenses (currently A=1000€/m, B=550€/m)

## Phase 4: Retirement Calculator ✅
- [x] Input current French pension estimate (relevé de carrière)
- [x] RetirementCalculator service (`services/retirement.py`)
- [x] Retirement milestones for household (primary + spouse)
- [x] Income timeline projection (salary → pension transition)
- [x] Retirement income needs (configurable % of current expenses)
- [x] Gap analysis (pension + other income vs target)
- [x] Required capital calculation ("the number" using 4% rule)
- [x] CLI command: `pactole retirement`
- [x] Comprehensive test suite (9 tests)

**Retirement findings (based on real config):**
| Person | Retirement | Age | Monthly Net Pension |
|--------|------------|-----|---------------------|
| Sabine | Nov 2027 | 63 | 2,669€ |
| Gael | Jan 2036 | 66 | 3,888€ |

**Gap analysis (at 75% expense ratio):**
- Target: 8,800€/month (75% of 11,733€ current expenses)
- Combined pension: 6,557€/month + rental 1,000€/month
- Coverage: 167.9% → **Surplus expected** (no capital withdrawal needed)

## Phase 5: Estate & Succession Planning
- [ ] Total net worth calculation (financial + real estate - loans)
- [ ] French succession tax rules (abattements, barème)
- [ ] Donation strategies (donation-partage, démembrement)
- [ ] Assurance-vie succession advantages
- [ ] Simulate wealth transfer scenarios to children

## Phase 6: Reports & Visualization
- [ ] CLI summary report (`pactole report`)
- [ ] Projection tables (`pactole project`)
- [ ] Charts: Net worth over time (household)
- [ ] Charts: Cash flow projection
- [ ] Charts: Scenario comparison
- [ ] Charts: Estate value over time
- [ ] Export: CSV, PDF

## Phase 7: CLI Polish
- [ ] Clean command-line interface
- [ ] Configuration validation
- [ ] Error handling & helpful messages
- [ ] Documentation

---

## Technical Approach

**Libraries:**
- `pydantic` or `dataclasses` for models
- `pyyaml` for config loading
- `matplotlib` for charts
- `rich` for terminal output (optional)

**Architecture:**
```
pactole/
├── models/          # Data models (existing)
├── services/
│   ├── loader.py    # Load config → objects
│   ├── projector.py # Projection engine
│   ├── simulator.py # Scenario simulation
│   └── retirement.py # Retirement calculations
├── reports/
│   ├── summary.py   # Text reports
│   └── charts.py    # Visualizations
└── cli/
    └── main.py      # CLI commands
```

---

## French Tax & Investment Considerations

### Tax System (to model)
- **Income tax**: Progressive brackets (0%, 11%, 30%, 41%, 45%)
- **Social charges**: CSG/CRDS on investment income (~17.2%)
- **Flat tax (PFU)**: 30% option on capital gains/dividends
- **Quotient familial**: Family situation impact

### Investment Vehicles (French-specific)

#### Personal Investments
| Vehicle | Tax Advantage | Limits/Notes |
|---------|---------------|--------------|
| **PEA** | After 5 years: only 17.2% social charges (no income tax) | 150k€ max, EU stocks only |
| **PEA-PME** | Same as PEA | +75k€, SME stocks |
| **Assurance-vie** | After 8 years: 4,600€/9,200€ annual abattement + 7.5% tax (or PFU 12.8%) | No limit, flexible, succession |
| **PER** | Contributions deductible from income tax, taxed at withdrawal | Locked until retirement |
| **CTO** | PFU 30% (or barème + 17.2%) | No limit, full flexibility |

#### Business/Employer Plans
| Vehicle | Tax Advantage | Notes |
|---------|---------------|-------|
| **PEE** | Tax-free gains after 5 years (only 17.2% social) | Employer contribution up to 3x employee |
| **PERCO/PERCOL** | Same as PEE, retirement-locked | Can transfer to PER |
| **Madelin** | Deductible contributions (TNS only) | For self-employed, locked |
| **Article 83** | Employer contributions exempt | Company retirement plan |

#### Business Income (Capacitor)
| Regime | Rate | Notes |
|--------|------|-------|
| **IS (Corp tax)** | 15% up to 42.5k€, 25% above | Small business rate |
| **Flat tax (dividends)** | 30% PFU (12.8% IR + 17.2% social) | Or opt for barème |
| **Salary vs dividends** | Trade-off | Social charges vs flat tax |

#### Key Tax Optimization Strategies
- **PEA max**: Fill 150k€ PEA before CTO
- **Assurance-vie 8 years**: Open early, use abattement annually
- **PER timing**: Deduct when high income, withdraw when lower (retirement)
- **Dividend timing**: Control Capacitor dividend based on other income
- **Abattement 40%**: If opting barème instead of PFU for dividends

### Retirement Income (French system)
- **Régime général**: Base pension (CNAV)
- **AGIRC-ARRCO**: Complementary pension (cadre)
- **Input needed**: Current estimate from relevé de carrière (info-retraite.fr)

---

## Notes

### Capacitor Scenarios (to be detailed)
- **Keep**: Continue rental income, business expenses
- **Close/Sell**: One-time cash event, no ongoing income/expenses
- Impact on taxes, social charges, retirement contributions

### Investment Return Assumptions
| Profile | Annual Return | Notes |
|---------|---------------|-------|
| Conservative | 3-4% | Bonds, money market |
| Moderate | 5-6% | Balanced portfolio |
| Aggressive | 7-8% | Equity-heavy |

### French Succession Rules (2025)
- **Abattement par enfant**: 100,000 € (renews every 15 years)
- **Abattement conjoint**: Exonération totale
- **Assurance-vie**: 152,500 € abattement per beneficiary (before 70)
- **Donation-partage**: Anticipate succession with tax advantages
- **Démembrement**: Separate usufruit/nue-propriété

### Real Estate Valuation
- Primary residence: To be estimated
- Method: Compare with local market (notaires, DVF data)
- Consider: 30% abattement on primary residence for IFI

### Key Milestones
- Pool loan ends: Sept 2034
- House loan ends: July 2036
- Retirement target: ~2035 (age 65)

