# OLS Diagnostics: When the Standard Error Is Lying

## Objective
I tested when the standard error from an OLS regression can be trusted, and what to do when it cannot.

## Methodology
- Simulated data where the spread of the errors grows with x, and fitted the same regression with classical and with robust (HC3) standard errors.
- Ran 400 simulated samples to check how often each 95% confidence interval actually contained the true slope, and measured each coverage rate's Monte Carlo standard error.
- Read four residual plots, each with a different problem, beside Breusch-Pagan and Jarque-Bera tests.
- Measured leverage, standardised residuals and Cook's distance, then deleted the most influential row and fitted the regression again.
- Fitted a regression on the California Housing data and compared classical and HC3 standard errors for each coefficient.
- Wrote a function, hc3_se(), that fits a regression and returns the HC3 standard error of one coefficient, and used it to compare the full data with the districts below the 5.0 ceiling.
- Found the five most influential California districts by Cook's distance and fitted the regression again without them.
- Simulated 40 firms with 25 workers each, where workers in the same firm share a shock, and compared classical, HC3 and clustered standard errors.

## Key Findings
- Heteroskedasticity did not change the estimate. Both fits gave a slope of 2.0147, but the standard error was 0.0264 classical and 0.0290 robust.
- Across 400 samples, the classical interval covered the true slope in 91.8% of them and the robust one in 93.5%, with Monte Carlo standard errors of 1.4% and 1.2%. The classical shortfall from 95% was larger than chance would explain.
- Each residual plot pointed to a different problem, and the tests did not always catch what the plots showed.
- Deleting one row out of 600 moved the slope only 0.58 of its own standard error, but the standard error fell 33%. That one row affected the standard error much more than the estimate.
- In the California Housing regression, the HC3 standard error on AveRooms was 5.02 times the classical one, so the classical standard error understated the uncertainty.
- The HC3 standard error on AveRooms was 0.0121 with all districts and 0.0082 without the 965 at the ceiling. A smaller standard error alone is not a reason to drop those districts.
- Five of the 20,640 California districts, 0.024% of the data, carried 92% of the total Cook's distance. Removing them moved the AveRooms coefficient from -0.0273 to -0.0492.
- In the firm simulation, the clustered standard error was 0.1865, compared with 0.0600 for HC3 and 0.0593 for classical, about three times larger. HC3 fixes uneven spread but not errors that are correlated within a group.
