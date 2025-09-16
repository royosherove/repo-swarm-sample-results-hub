---
description: Create a new report from a natural language request
---

Given the report request provided as an argument, do this:

1. Look at all files that end with *.arch.md and IGNORE any folders such as "prompts", "diagrams" etc.
2. Generate a consistent report taking into account all cursor rules in the .cursor/rules folder
3. when reporting, make sure to only use FACTS. you cannot make things up, so make sure your data is backed up with specific file locations and markers as needed 
4. double check your work to make sure you dont' have false positives or missing information
If you are not sure of something, do not state it as fact, but put it in an asterist in a special section.
5. when looking at tools or vendors, note that names can appear in multiple forms , for example llamaindex or llama-index are the same.

in the report folder create a .memory folder and place in there a REPORT_PLAN.MD file in which you will write your plan for how to execute the report.
As you execute this plan, keep updating  REPORT_PLAN.MD with what steps have been taken.
