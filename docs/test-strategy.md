# Test Strategy – Construction HRMS

## 1. System purpose
This HRMS exists to ensure construction workers are paid the correct amount at the correct time. The most important business output is the final payroll/payslip, and the most important dependent user is the worker receiving that pay, followed by payroll/admin staff responsible for processing it accurately.

## 2. Core quality principle
Quality in this system is not “all pages load” or “features work in isolation.” Quality means upstream changes in employee/payroll-related data must correctly propagate to downstream calculations and outputs before payroll is processed.

## 3. Highest-risk bug pattern
The most dangerous failure pattern in this HRMS is **data propagation failure across dependent entities**.

Examples:
- Salary updated → next payslip still shows old salary
- Attendance corrected → payroll total not recalculated
- Overtime changed → salary calculation unchanged
- Employee exit marked → payroll still generated
- Onboarding completed → employee still blocked from attendance/payroll flow

## 4. Test approach
I prioritized tests around **dependency chains**, not around screens alone.

### Risk → Impact → Coverage thinking
Whenever an upstream record changes, every downstream state, rule, or payroll calculation depending on it must update correctly.

## 5. Priority coverage areas

### P0 – Must never fail
1. Salary → Payslip propagation  
2. Attendance → Payroll calculation  
3. Overtime → Payroll calculation  
4. Exit → Payroll stop/deactivation  
5. Onboarding completion → Attendance/payroll activation  

### P1 – Important dependent state transitions
6. Employee status changes affecting payroll eligibility  
7. Re-run payroll after upstream edits  
8. Prevent stale payroll values after correction flows  

## 6. Test suite structure

### Smoke tests
Purpose: confirm the system is usable enough for deeper testing.
- Login works
- Dashboard / employee module loads
- Payroll module loads
- Employee record can be opened
- Payslip or payroll page is accessible

### Regression tests
Purpose: protect business-critical propagation failures.
- `salary-propagation.spec.js`
- `attendance-payroll-link.spec.js`
- `onboarding-attendance-activation.spec.js`
- `exit-payroll-stop.spec.js`

## 7. Why this strategy is different
A generic strategy would say “test payroll, attendance, onboarding.”  
This strategy protects the specific production failure pattern shown in the assignment: **upstream HR/payroll changes failing to cascade into downstream payroll outputs.**

## 8. CI expectation
The regression suite should run on every PR. If any dependency-propagation test fails, merge should be blocked because the system may pay workers incorrectly.
