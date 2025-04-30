---
layout: post
title: Code Review Guidelines
---
I was recently reading something about code review, and I got some gems from online. Thought of writing my notes and also add those links here for future reference.


# 🎯 Code Review Guidelines/thoughts to follow

It is better you go through the reference material at the end of this post. But I will put here what I learnt about reviews and what I would look for. 

## Terms

- **CL: Change List**: A self contained change that has been submitted to VCS (see the term definition below), and is made available for reviewers to review. In different companies, these are called PR, Change, Diff, Patch etc.

- **VCS: Version Control System**. A locally  hosted or cloud hosted code repository. Bitbucket, Github are all good examples of a cloud hosted VCS

- **LGTM: Looks Good To Me.** A comment which is prefixed with LGTM is approved by the reviewer and can go to Production as is. In different companies, this has different meanings. For eg. in Meta, this doesn't mean ready to deploy or ready to go to Prod yet. Also, depends on who/what capacity the reviewer is. 

- **Nit: Nit-Picking.** Something that is not urgent or important to fix, but to remind the developer to take care of it next time. Again, this means different things in different companies


### Code Review Guidelines & Motivations

Below checklist is in random order of my learning. Use the references below for a perfect read

- Code should be well designed, easy to read and understand
- Check if the code meets all or some parts of the requirements. Depends on if it is a full-commit or a partial commit of a big change
- Check for any logic errors, missing best practices or incorrect behavior
- Check for missing Test Cases, Edge Cases, Security Scan reports, Vulnerability Scan Reports, Code Style report and any AI based code review comments (eg. Github Copilot)
- Review 200 to 400 lines of code in one sitting. More than that will cause fatigue
- Always have the ticket/task in front of you for the code you are reviewing for
- 

### Code Level Deep Dive Review I used to do
- Alert when loop inside a loop is coded, Expensive operations inside a loop, multiple method calls in loop, multiple exceptions coming out of a loop etc.
- Unnecessary Exception throwing or handling
- Multiple logging statements (may have been put at the time of coding/debugging). Opposite of this is also to be checked - inefficient logging. There should be at least two lines of logs - whats coming in, and what goes out of a method. 
- Excessive allocations of objects. In java, see how many "new" are being called
- inefficient string concatenations. Overloaded + operator is dangerous in String operation, especially in a loop
- Code duplication. Check those SonarQube reports


## References from Internet (not in any order)
- https://google.github.io/eng-practices/review/reviewer/
- https://google.github.io/eng-practices/
- https://gist.github.com/thcipriani/8dbce9b755c1d74617de34a153c2ecae
- https://www.reddit.com/r/learnprogramming/comments/n84xru/how_do_you_do_an_actual_code_review/

Fully written by Easo Thomas, 0% helped by AI tools. Reference links are a result of Google Search.