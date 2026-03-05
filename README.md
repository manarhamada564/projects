
## Staging (`models/staging/`)
- Rename columns
- Type casting
- Simple transformations
- Standardization
- No joins
- Materialized as **views**

> Clean starting point. Acts as a gatekeeper layer.

## Intermediate (`models/intermediate/`)
- Joins between staging models
- Business logic
- Aggregations
- Reusable transformations
- Use CTEs for clarity
- Usually materialized as **views**

> Organize business logic clearly. Optimize for readability.

---

## Marts (`models/marts/`)
- Final business-ready tables
- Denormalized
- Aggregated
- Dashboard-friendly
- Materialized as **tables**

> Optimized for analytics consumption.

---

## Structure
```bash
models/
staging/
intermediate/
marts/
seeds/
macros/
tests/
```

---

## Naming Conventions

Follow dbt Labs style guidelines.

| Layer | Prefix Example |
|--------|----------------|
| Staging | `stg_orders` |
| Intermediate | `int_customer_metrics` |
| Dimension | `dim_customers` |
| Fact | `fct_orders` |

✅ Use clear, business-meaningful names  
❌ Avoid vague names like `final_table`

---

## Important Commands

### Initialize Project

```bash
dbt init dbt_project
```
Verify connection & configuration:
```bash
dbt debug
```
Install dependencies (if using packages.yml):
```bash
dbt deps
```
### Seeds (Load CSV Files)
Load CSV files from seeds/ into database:
```bash
dbt seed
```
Force reload (drop & recreate tables):
```bash
dbt seed --full-refresh
```

### Run Models
Run all models:
```bash
dbt run
```
Run specific model:
```bash
dbt run -m model_name
```
Run multiple models:
```bash
dbt run -m model_a model_b
```
Run by directory:
```bash
dbt run -m staging.*
dbt run -m intermediate.*
dbt run -m marts.*
```
Run model + downstream dependencies:
```bash
dbt run -m model_name+
```
Run upstream dependencies:
```bash
dbt run -m +model_name
```
Run upstream + downstream:
```bash
dbt run -m +model_name+
```

### Testing
Run all tests:
```bash
dbt test
```
Test specific model:
```bash
dbt test -m model_name
```
### Build (Run + Test Together)
Run models and tests:
```bash
dbt build
```

### Run specific model with tests:
```bash
dbt build -m model_name
```
### Documentation
Generate docs:
```bash
dbt docs generate
```
```bash
Serve docs locally:
```bash
dbt docs serve
```
### Clean Project
Remove compiled artefacts:
```bash
dbt clean
```
Recommended Daily Workflow
```bash
dbt debug
dbt seed
dbt run -m model_name
dbt test
dbt build
