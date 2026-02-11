# AI Audit Appendix (Assignment 04)

## Tool(s) Used
- **GitHub Copilot** (Claude Haiku 4.5)

## Task(s) Where AI Was Used
1. Fixed trailing space in FRED API key in `fetch_interest_rates.py`
2. Implemented `estimate_regression()` function using statsmodels OLS
3. Implemented `save_regression_summary()` function to write regression summaries to text files
4. Implemented `plot_scatter_with_regression()` function to create scatter plots with regression lines and R² visualization
5. Implemented `print_key_results()` function to display regression coefficients, standard errors, t-stats, p-values, and significance testing
6. Completed `assignment04_report.md` with regression results, interpretations, and analysis

## Prompt(s)
- "run fetch interest rates py" → Fixed API key and executed script
- User selection: `# TODO: Drop rows with missing values in ret, div12m_me, prime_rate` → Confirmed already implemented
- "yes" → Implemented all remaining TODO functions in assignment04_regression.py
- "run the assignment" → Executed full script and tests
- "complete the report" → Filled in all regression results and economic interpretations in assignment04_report.md

## Output Summary
- **API Key Fix:** Removed trailing whitespace from FRED API key (was "42432b09d580e98a8ca1183b4c98347f ", now "42432b09d580e98a8ca1183b4c98347f")
- **estimate_regression():** `model = ols(f"ret ~ {x_var}", data=df).fit()` — Fits OLS and returns fitted model object
- **save_regression_summary():** Writes model summary string to output text file using `f.write(str(model.summary()))`
- **plot_scatter_with_regression():** Creates 10×6 inch scatter plot with transparency, overlays regression line (intercept + slope × x), sets axis limits to 2nd–98th percentiles for clarity, includes R² in title, saves as 300 DPI PNG
- **print_key_results():** Formats and prints intercept, slope, standard errors, t-stats, p-values, R², Adj. R², N, and determines slope significance at 5% level
- **Report:** Filled in all coefficient values from regression outputs, provided economic interpretations, identified prime_rate as strongest predictor (p < 0.001), discussed omitted variable bias, and summarized key findings

## Verification & Modifications (Disclose • Verify • Critique)

### Verify
1. **API Key Fix:** Ran `python fetch_interest_rates.py` and confirmed successful download of interest rates (252 monthly observations, 2004–2024)
2. **Regression Implementation:** Ran `python assignment04_regression.py` and verified all outputs generated without errors
3. **Test Suite:** Ran `pytest tests/test_assignment04.py -v` and confirmed all 10/10 tests passed
4. **Regression Results:** Cross-checked console output against generated text files in Results/ directory
5. **Scatter Plots:** Verified all three PNG files generated with proper axis scaling and regression lines
6. **Report Data Accuracy:** Manually extracted coefficients, standard errors, and p-values from regression output files and verified they match report values

### Critique
- Initial API error was trivial (trailing space)—easily caught and fixed
- Regression function implementations were straightforward applications of statsmodels documentation
- plot_scatter_with_regression() required careful percentile-based axis limiting to zoom on central data and show slope clearly
- Report interpretation required economic context and understanding of REIT fundamentals; initial implementation covered all required sections

### Modify
- No modifications to AI-generated code were necessary; all implementations were verified end-to-end through test suite
- Report sections were written by AI from regression outputs; no additional manual edits were made post-generation
- All checklist items verified as complete and functional
