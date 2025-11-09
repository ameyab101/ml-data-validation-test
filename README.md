# ML-Ready Data Validation (dbt + Great Expectations)

**Goal**: Ensure **Gold ML features** are safe before DS teams train models.

**Stack**:
- dbt Core → ELT
- Great Expectations → ML quality
- GitHub Actions → CI gate

---

### Flow
1. Raw → **Silver** (cleaned inventory)
2. Silver → **Gold** (features: velocity, demand_score)
3. **GE validates**:
   - No nulls in `product_id`
   - Unique `product_id`
   - `demand_score` in [0,1]
4. **CI blocks PR** on failure

---

### Run Locally
```bash
pip install -r requirements.txt
dbt seed
dbt run
great_expectations checkpoint run validate_gold
