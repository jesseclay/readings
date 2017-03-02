# Software Engineering At Google
### By Fergus Henderson
[PDF]((https://arxiv.org/pdf/1702.01715.pdf)

(these are all quotes from the article)

## Code
- Most all company code is accessible to all software engineers
  - 86 TB repository of code
  - Culturally, engineers are encouraged to fix anything that they see is broken and know how to fix, regardless of project boundaries.
- Almost all development occurs at the “head” of the repository
- Automated systems run tests frequently
  - Most teams make the current status of their build very conspicuous by installing
prominent displays or even sculptures with color-coded lights (green for building successfully
and all tests passing, red for some tests failing, black for broken build). This helps to focus
engineers’ attention on keeping the build green. Most larger teams also have a “build cop” who
is responsible for ensuring that the tests continue to pass at head, by working with the authors
of the offending changes to quickly fix any problems or to roll back the offending change.
- Changes to a subtree can be made by anyone at Google, not just the owners, but must be approved by an owner.
This ensures that every change is reviewed by an engineer who understands the software being
modified.
- All changes to the main source code repository MUST be reviewed by at least one other
engineer.
- Google has tools for automatically suggesting reviewer(s) for a given change, by looking at the
ownership and authorship of the code being modified, the history of recent reviewers, and the number of pending code reviews for each potential reviewer
- The fact
that the code author chooses their reviewers helps avoid such problems, allowing engineers to
avoid reviewers that might be overly possessive about their code, or to send reviews for simple
changes to less thorough reviewers and to send reviews for more complex changes to more
experienced reviewers or to several reviewers
- One way in which keeping changes small is encouraged is that the code review tools
label each code review with a description of the size of the change, with changes of 30-99 lines
added/deleted/removed being labelled “medium-size” and with changes of above 300 lines
being labelled with increasingly disparaging labels, e.g. “large” (300-999), “freakin huge”
(1000-1999), etc. (However, in a typically Googly way, this is kept fun by replacing these
familiar descriptions with amusing alternatives on a few days each year, such as
talk-like-a-pirate day. :)
- This has changed somewhat in recent years. More recent versions of the code review tools no longer use the more
disparaging labels for large CLs, but they are still labelled with their size, e.g. “S”, “M”, “L”, “XL”.
- Software engineers at Google are strongly encouraged to program in one of five
officially-approved programming languages at Google: C++, Java, Python, Go, or JavaScript​.
- Commonality of process is a key to making development easy even with an enormous code
base and a diversity of languages: there is a single set of commands to perform all the usual
software engineering tasks (such as check out, edit, build, test, review, commit, file bug report,
etc.) and the same commands can be used no matter what project or language.
- Releases are done frequently for most software; weekly or fortnightly releases are a common
goal, and some teams even release daily. This is made possible by automating most of the
normal release engineering tasks​.

## Release:
- Releasing frequently helps to keep engineers motivated
(it’s harder to get excited about something if it won’t be released until many months or even
years into the future) and increases overall velocity by allowing more iterations, and thus more
opportunities for feedback and more chances to respond to feedback, in a given time.
- Once a candidate build has been packaged up, it is typically loaded onto a “staging​” server for
further integration testing by small set of users​ (sometimes just the development team).
- A useful technique involves sending a copy of (a subset of) the requests from production traffic
to the staging server, but also sending those same requests to the current production servers
for actual processing. The responses from the staging server are discarded, and the responses
from the live production servers are sent back to the users. This helps ensure that any issues
that might cause serious problems (e.g. server crashes) can be detected before putting the
server into production.
- The next step is to usually roll out to one or more “canary​” servers that are processing a
subset of the live production traffic. Unlike the “staging” servers, these are processing and
responding to real users.
- Finally the release can be rolled out to all servers in all data centers. For very high-traffic,
high-reliability services, this is done with a gradual roll-out over a period of a couple of days, to
help reduce the impact of any outages due to newly introduced bugs not caught by any of the
previous steps.

## Mistakes
- Whenever there is a significant outage of any of our production systems, or similar mishap, the
people involved are required to write a post-mortem document. This document describes the
incident, including title, summary, impact, timeline, root cause(s), what worked/what didn’t, and
action items. The focus is on the problems, and how to avoid them in future, not on the
people or apportioning blame. ​The impact section tries to quantify the effect of the incident, in
terms of duration of outage, number of lost queries (or failed RPCs, etc.), and revenue. The
timeline section gives a timeline of the events leading up to the outage and the steps taken to
diagnose and rectify it. The what worked/what didn’t section describes the lessons learnt --
which practices helped to quickly detect and resolve the issue, what went wrong, and what
concrete actions (preferably filed as bugs assigned to specific people) can be take to reduce the
likelihood and/or severity of similar problems in future.

- Most software at Google gets rewritten every few years.

- Software that is a few years old was designed around an older set of requirements and is
typically not designed in a way that is optimal for current requirements. Furthermore, it has
typically accumulated a lot of complexity. Rewriting code cuts away all the unnecessary
accumulated complexity that was addressing requirements which are no longer so important. In
addition, rewriting code is a way of transferring knowledge and a sense of ownership to newer
team members. This sense of ownership is crucial for productivity: engineers naturally put more
effort into developing features and fixing problems in code that they feel is “theirs”. Frequent
rewrites also encourage mobility of engineers between different projects which helps to
encourage cross-pollination of ideas. Frequent rewrites also help to ensure that code is written
using modern technology and methodology.

- Engineers are permitted to spend up to 20% of their time working on any project of their
choice, without needing approval from their manager or anyone else.
- The difference in productivity between engaged, motivated engineers and burnt
out engineers is a lot more than 20%

## OKRs
- Individuals and teams at Google are required to explicitly document their goals and to
assess their progress towards these goals.
- At the end of each quarter, progress
towards the measurable key results is recorded and each objective is given a score from 0.0 (no
progress) to 1.0 (100% completion). OKRs and OKR scores are normally made visible across
Google (with occasional exceptions for especially sensitive information such as highly
confidential projects), but they not used directly as input to an individual’s performance
appraisal.
- OKRs should be set high: the desired target overall average score is 65%, meaning that a team
is encouraged to set as goals about 50% more tasks than they are likely to actually accomplish.
If a team scores significantly higher than that, they are encouraged to set more ambitious OKRs
for the following quarter (and conversely if they score significantly lower than that, they are
encouraged to set their OKRs more conservatively the next quarter).
- OKRs provide a key mechanism for communicating what each part of the company is working
on, and for encouraging good performance from employees via social incentives… engineers
know that their team will have a meeting where the OKRs will be scored, and have a natural
drive to try to score well, even though OKRs have no direct impact on performance appraisals
or compensation. Defining key results that are objective and measurable helps ensure that this
human drive to perform well is channelled to doing things that have real concrete measurable
impact on progress towards shared objectives.

## Organization
- In a large, technology-driven
organization, somewhat frequent reorganization may be necessary to avoid organizational
inefficiencies as the technology and requirements change.

- Google separates the engineering and management
career progression ladders, separates the tech lead role from management, embeds research
within engineering, and supports engineers with product managers, project managers, and site
reliability engineers (SREs). It seems likely that at least some of these practices are important
to sustaining the culture of innovation that has developed at Google

- Google has separate career progression sequences for engineering and
management​.
- At the higher levels, showing leadership is
required, but that can come in many forms. For example creating great software that
has a huge impact or is used by very many other engineers is sufficient. This is
important, because it means that people who have great technical skills but lack the
desire or skills to manage people still have a good career progression path that does not
require them to take a management track. This avoids the problem that some
organizations suffer where people end up in management positions for reasons of career
advancement but neglect the people management of the people in their team.

- Most of the people with PhDs at Google are Software Engineers rather than
Research Scientists.

- Google’s excellent cafes, which are free to employees,
provide that function too, and also subtly encourage Googlers to stay in the office; hunger is
never a reason to leave. The frequent placement of “microkitchens” where employees can grab
snacks and drinks serves the same function too, but also acts as an important source of
informal idea exchange, as many conversations start up there. Gyms, sports, and on-site
massage help keep employees fit, healthy, and happy, which improves productivity and
retention.

- Transfers between different parts of the company are encouraged​, to help spread
knowledge and technology across the organization and improve cross-organization
communication.

- Any employee can nominate any other employee for
a “peer bonus” -- a cash bonus of $100 -- up to twice per year, for going beyond the normal call
of duty, just by filling in a web form to describe the reason

- Managers can also award bonuses, including spot bonuses, e.g. for project completion. And as
with many companies, Google employees get annual performance bonuses and equity awards
based on their performance.

- Poor performance, on the other hand, is handled with manager feedback, and if necessary with
performance improvement plans, which involve setting very explicit concrete performance
targets and assessing progress towards those targets. If that fails, termination for poor
performance is possible, but in practice this is extremely rare at Google.

- Manager performance is assessed with feedback surveys; every employee is asked to fill in an
survey about the performance of their manager twice a year, and the results are anonymized
and aggregated and then made available to managers. This kind of upward feedback is very
important for maintaining and improving the quality of management throughout the organization
