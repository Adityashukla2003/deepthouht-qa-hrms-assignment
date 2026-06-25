# Risk Matrix – Construction HRMS

| Risk / Failure Pattern | Business Impact | Who Gets Hurt | Test Coverage |
|---|---|---|---|
| Salary update does not reflect in next payslip | Worker paid wrong amount | Worker, payroll admin | salary-propagation.spec.js |
| Attendance correction does not recalculate payroll | Underpayment / overpayment | Worker, payroll admin | attendance-payroll-link.spec.js |
| Overtime not included in salary calculation | Worker loses earned pay | Worker | attendance-payroll-link.spec.js / overtime coverage |
| Employee exit does not stop payroll | Wrong payroll payout after exit | Company payroll team, finance | exit-payroll-stop.spec.js |
| Onboarding completion does not activate payroll eligibility | New worker excluded from payroll | New worker, site admin | onboarding-attendance-activation.spec.js |
| Status change does not update downstream rules | Incorrect payroll inclusion/exclusion | Worker, payroll admin | targeted regression checks |
| Dependency knowledge exists only in one senior developer’s head | New code breaks hidden flows | Whole team, workers indirectly | regression suite + CI |
