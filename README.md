 DeepThought QA Engineer Assignment – Construction HRMS

 Overview
This repository contains my submission for the DeepThought QA Engineer assignment. The system under test is a Construction HRMS where quality is defined by one business outcome: workers must be paid the correct amount at the correct time.

My testing strategy is built around the highest-risk production failure pattern shown in the assignment: **upstream HR/payroll data changes not propagating correctly to downstream calculations and outputs**. Instead of treating the salary-change bug as a one-off issue, I designed the suite to protect the broader dependency chain across employee data, attendance, overtime, onboarding, exit, and payroll generation.

Business Understanding
This HRMS does not exist to merely store employee records or generate payslips. Its core job is to ensure that payroll reflects the current reality of the worker’s employment, attendance, and compensation state.

The most important output is the **final payslip / payroll amount**, and the user most dependent on it is the **worker who is expecting correct payment on time**, along with payroll/admin staff responsible for processing payroll accurately.


## Key Risk Identified
The most dangerous bug pattern in this system is **data propagation failure across dependent entities**.

Example:
- Salary updated → payslip still uses old salary
- Attendance updated → payroll total not recalculated
- Exit marked → payroll continues after employee left
- Onboarding completed → attendance/payroll eligibility not activated

This is dangerous because the same failure pattern can silently appear in multiple places, causing underpayment, overpayment, payroll disputes, and loss of trust in the system.

 Test Strategy
My test strategy focuses on the dependency chain rather than isolated screens.

 Core principle
Whenever an upstream entity changes, every downstream calculation or state that depends on it must reflect that change correctly.

 Priority regression areas
1. Salary → Payslip propagation
2. Attendance → Payroll calculation
3. Overtime → Payroll calculation
4. Onboarding → Attendance / payroll eligibility activation
5. Exit → Payroll stop / deactivation
6. Employee status changes → dependent payroll/attendance behavior

 Test Suite Structure

 Smoke tests
Basic confidence checks that the system is usable:
- Login works
- Payroll core flow loads
- Key payroll page is accessible

 Regression tests
Focused protection for high-impact business failures:
- salary-propagation.spec.js
- attendance-payroll-link.spec.js
- onboarding-attendance-activation.spec.js
- exit-payroll-stop.spec.js


 Example Regression Coverage

 1. Salary propagation
**Goal:** Verify that editing an employee’s salary is reflected in the next payslip calculation.

 2. Attendance to payroll linkage
**Goal:** Verify that changes in attendance affect payroll totals correctly.

 3. Onboarding activation
**Goal:** Verify that onboarding completion enables downstream attendance/payroll participation.

 4. Exit payroll stop
**Goal:** Verify that exited employees do not continue receiving payroll.


 Why this suite matters
This suite is designed to prevent the class of production incidents described in the assignment, not just one individual bug. It protects the business output that matters most: **accurate payroll for real workers**.


 CI
The regression suite is intended to run on every pull request. If a dependency-propagation test fails, the merge should be blocked until the issue is resolved.


 Repo Contents
- `docs/test-strategy.md` → detailed QA strategy
- `docs/bug-analysis.md` → root cause analysis of failure pattern
- `docs/risk-matrix.md` → risk → impact → coverage mapping
- `docs/summary-sheet.md` → answers for Part 3 summary questions
- `tests/` → automated smoke + regression coverage
- `.github/workflows/ci.yml` → CI pipeline



## Final Position
My approach is intentionally centered on business impact rather than generic QA categories. The highest-value work in this HRMS is protecting the data-dependency chain that determines whether a worker is paid correctly and on time.
