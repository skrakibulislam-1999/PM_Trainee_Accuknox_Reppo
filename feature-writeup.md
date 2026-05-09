# Feature Write-Up
## Accuknox — Alert Triage Workflow

---

## What Problem Am I Trying to Solve?

Imagine you are a security engineer and an alert just fired.
Something is wrong in your cloud account. Could be serious.
Could be nothing. You do not know yet.

So you open the alert.

And it tells you almost nothing useful.

You spend the next 20 minutes jumping between tabs, 
Googling the policy name, trying to figure out who else 
on the team knows about this, and wondering if someone 
already started working on it.

Meanwhile the actual problem — let us say a public S3 
bucket with sensitive files — is still sitting there, 
wide open.

That gap between "alert fired" and "engineer knows 
what to do and is doing it" is what this design is 
trying to close.

---

## The Features I Proposed and Why

---

### Feature 1 — Show the Fix Inside the Alert
Priority: Most Important

This one is simple. When an engineer opens an alert, 
the page should tell them what to do. Not in a vague 
"review your settings" kind of way. In a clear, 
numbered, step-by-step way.

Step 1 — do this.
Step 2 — do this next.
Step 3 — check this thing.

That is it. No Googling. No switching tabs. 
No figuring it out from scratch.

I think this single feature saves more time than 
anything else in this design. It is the first thing 
that should be built.

---

### Feature 2 — Let Someone Claim the Alert
Priority: Most Important

Here is something that happens more than people 
want to admit. An alert comes in. Everyone on the 
team sees it. Nobody touches it because they all 
assumed someone else was handling it.

An hour later it is still open.

This feature fixes that with one button. 
"Assign to me" or "Assign to teammate." 
One click. Now everyone can see who is on it.

Simple idea. Big difference in practice.

---

### Feature 3 — Keep a Running Log of What Happened
Priority: Most Important

Every time something happens with an alert — it fires, 
someone gets notified, someone claims it, someone 
resolves it — that action gets added to a timeline 
automatically.

The engineer does not have to write any of this.
It just happens in the background.

Why does this matter? Two reasons.

First, the whole team can see what is going on 
without having to ask. Second, a lot of companies 
are legally required to show a record of how security 
incidents were handled. This timeline creates that 
record without any extra work.

---

### Feature 4 — Make Engineers Leave a Note When They Close an Alert
Priority: Most Important

Before an engineer can mark an alert as resolved, 
they have to write a short note about what they did.

I know that sounds annoying. But it is only 
about 20 seconds of work and it is genuinely useful.

The next time a similar alert comes in, someone 
on the team can look back and see exactly what 
worked last time. And if there is ever a security 
audit, there is a clear record of every resolution.

So I made this required. You cannot close the alert 
without it. The design enforces it so nobody skips it.

---

### Feature 5 — Show Related Alerts on the Same Page
Priority: Nice to Have — can come later

Security problems usually do not happen alone.

If there is an exposed S3 bucket and an open port 
on the same AWS account, those two things are 
probably connected somehow.

This feature shows other active alerts that are 
linked to the same resource or the same account, 
right there on the alert detail page.

It is not urgent. The core workflow works fine 
without it. But once everything else is running 
well, this makes engineers smarter about finding 
root causes instead of just closing alerts one by one.

---

## What Gets Built First and Why

I kept this really simple.

Features 1 to 4 all need to ship together because 
they cover the complete journey — from the moment 
an alert fires to the moment it is properly closed. 
If any one of them is missing, the workflow has 
a gap in it.

Feature 5 is a good next step but it is not 
required for the basic experience to work.

| Feature | Build it when? | One-line reason |
|---|---|---|
| Fix steps inside the alert | First release | Biggest time saver |
| Assign ownership | First release | Stops alerts from being ignored |
| Activity timeline | First release | Team visibility and audit trail |
| Required resolution note | First release | Compliance and team learning |
| Related alerts panel | Second release | Nice to have, not urgent |

---

## How Would I Know if This Actually Worked?

These are the things I would check after launch to 
see if the design made a real difference.

| What I Would Measure | What It Tells Me | Goal |
|---|---|---|
| How long before an engineer takes action on an alert | Are they getting started faster? | 40% faster |
| How long from alert open to alert resolved | Is the whole process quicker? | 30% faster |
| HIGH alerts with no owner after 30 minutes | Are critical things getting picked up? | Zero |
| Alerts closed with a resolution note | Is the audit trail complete? | 100% always |
| Did engineers find it easier to use? | Is the design actually helpful? | 4 out of 5 rating |

---

## Extra Ideas Worth Talking to the Dev Team About

These are not part of the main design but I think 
they are worth a conversation early on.

**Slack notifications**
Most engineers live in Slack all day, not in a 
security dashboard. If the platform could ping 
the right person when an alert is assigned or 
its status changes, that would save a lot of 
"did you see that alert?" messages.

**One-click fixes for common problems**
Some remediations are the same every single time. 
Restricting a public S3 bucket, for example, is 
always the same steps. Could the platform just 
do it automatically with a single confirm button? 
That would be a huge time saver for common issues.

**Show the logs inside the alert**
The remediation steps tell engineers to check 
CloudTrail logs. But that means opening the AWS 
Console in a completely separate tab. If the 
relevant logs could just appear inside the alert 
detail page, that is one less place engineers 
have to go.

**What happens when the same problem comes back?**
If an engineer resolves an alert but the same 
misconfiguration shows up again three days later, 
does the system create a brand new alert or 
bring back the old one? This needs a clear answer 
early because it affects how engineers track 
problems that keep recurring.

---

Submitted by
SK RAKIBUL ISLAM
skrakibulislam291999@gmail.com
