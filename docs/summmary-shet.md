# Part 3 – Summary Sheet Answers

## 1) What does this HRMS exist to deliver, and to whom?
This HRMS exists to deliver one outcome: a worker gets paid the correct amount at the correct time. The person who depends on it most is the worker whose pay reflects their salary, attendance, overtime, onboarding, and exit status.

## 2) What is the single most dangerous bug pattern you found across your testing? Why is it dangerous?
The most dangerous pattern is data propagation failure, where an upstream change like salary, attendance, overtime, or exit status does not update downstream payroll calculations. It is dangerous because the same hidden dependency bug can silently cause underpayment, overpayment, or payroll for the wrong employee across multiple workflows.

## 3) Which test in your suite are you most proud of, and why? What specific production failure would it prevent? Who would it protect?
The salary-to-payslip propagation regression test is the one I value most because it protects the exact production failure described in the assignment while also representing a broader dependency pattern. It would prevent a worker’s updated salary from failing to appear in the next payslip and directly protects both the worker and the payroll/admin team.

## 4) What did you choose NOT to automate, and why was that the right call?
I did not spend time automating low-risk cosmetic or layout checks because they do not threaten the business outcome this system exists to protect. In this assignment, automation time is better spent on dependency-chain failures that can cause workers to be paid incorrectly.

## 5) What's one thing in your submission that you're not fully confident about, and why you included it anyway?
I am not fully confident that I identified every hidden dependency in the HRMS because I do not have full production domain context or access to the real internal rules. I included the broader dependency-chain regression approach anyway because it is the safest way to reduce the chance of repeating the same class of payroll failures.

## 6) What changed between your first approach and your final submission? What did you rewrite, and why?
My first approach was more generic and category-based, covering payroll, attendance, onboarding, and standard QA areas separately. I rewrote it to focus on the actual business failure pattern—upstream data changes not propagating to downstream payroll outputs—because that is the real risk the assignment is asking me to protect.

## 7) What do you not know about quality engineering — or about construction payroll — that you would need to learn before you could truly do this job?
I would need to learn the exact payroll rules for construction workers, especially how attendance, overtime, site-based shifts, and employment status affect final pay. I would also need to learn the real dependency map between employee, attendance, onboarding, exit, and payroll entities in this HRMS so I can design coverage around actual production risk instead of assumptions.

## 8) If you had one more day, what would you test that you didn't get to? Why is it important, and who would it protect?
With one more day, I would test payroll recalculation after multiple upstream changes happen together—for example salary edit + attendance correction + overtime update before payroll generation. That matters because real payroll failures often come from interaction between changes, and it would protect workers, payroll admins, and finance from compound calculation errors.
