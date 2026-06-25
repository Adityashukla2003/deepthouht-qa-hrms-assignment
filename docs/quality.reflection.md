DeepThought QA Engineer Assignment – Summary Answers

 1) What does this HRMS exist to deliver, and to whom?
  Ans- It delivers accurate, compliant payroll processing — wage calculations, tax withholdings, certified payroll reports, and union rules — to construction companies managing field workers across shifting job sites, crews, and jurisdictions.
 
 2) What is the single most dangerous bug pattern you found across your testing?
    Ans- Silent precision loss in wage/tax calculations — the system accepts bad numeric input, computes wrong amounts, and returns a 200 OK with no error. Workers get underpaid; audits fail. It's invisible until it's a lawsuit.

3) Which test in your suite are you most proud of, and why?
Ans- The overtime cascade test: a worker switches job classifications mid-week across two states. It validates that OT thresholds, prevailing wages, and tax jurisdictions all recalculate correctly at the boundary — not just in isolation. Real-world complexity, one test.

4) What did you choose NOT to automate, and why was that the right call?
   Ans- Certified payroll PDF visual validation. Automated checks can verify data fields, but whether the form looks compliant — column alignment, signature blocks, government formatting — requires human eyes. Automating it would give false confidence.

5) What's one thing in your submission that you're not fully confident about, and why you included it anyway?
Ans- My union fringe benefit test coverage. I modeled common scenarios, but union agreements vary wildly by local. I included the tests anyway because even partial coverage catches regression — and flagged them as "expand before production.

6) What changed between your first approach and your final submission?
Ans- I started testing features in isolation. Midway through I scrapped that structure and reorganized around payroll lifecycle flows — hire → hours logged → gross pay → deductions → net pay → report. Bugs at boundaries only appear when you test the chain.

7) What do you not know about quality engineering — or about construction payroll — that you would need to learn before you could truly do this job?
Ans- On QE: performance testing payroll batch jobs at scale (10k+ workers, month-end runs). On construction payroll: the full depth of Davis-Bacon Act compliance variations by state and project type. I'd need a domain expert before I could claim full coverage there.

8) If you had one more day, what would you test that you didn't get to?
Ans- Payroll batch processing under load: what happens when 500 timesheets submit simultaneously at week-end cutoff? Does the system queue correctly, maintain calculation accuracy, and produce all certified reports without data bleed between jobs?

