# Bug Analysis – Most Dangerous Failure Pattern

## Bug pattern
Data propagation failure across dependent entities.

## Example incident
A salary value is edited for an employee, but the next generated payslip still uses the old salary.

## Why this is dangerous
This is not just one salary bug. It reveals a broader class of failure:
- an upstream entity changes
- dependent calculations or downstream states do not refresh
- payroll reflects stale data

## Where the same pattern can reappear
- Salary → payslip amount
- Attendance → payable days / payroll total
- Overtime → extra earnings
- Onboarding completion → payroll eligibility
- Exit date/status → payroll stop
- Employee status → payroll inclusion/exclusion rules

## Root cause hypothesis
The system likely has hidden dependencies between entities, but those dependencies are not reliably enforced or tested. A developer can update one module without realizing another module depends on it.

## Business consequence
If this pattern reaches production:
- workers may be underpaid or overpaid
- payroll staff may manually correct errors
- disputes and trust loss increase
- repeated payroll rework delays salary processing
- new developers become dangerous because dependency knowledge lives only in senior engineers’ heads

## QA response
The fix is not “test the one bug.”  
The fix is to build a regression suite around the entire dependency chain and block merges when propagation failures appear.
