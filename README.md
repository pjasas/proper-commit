# proper-commit
Your guide to etiquette of branching and committing

Branch naming guidelines:
1. If working on a particular JIRA task then branch name MUST begin with the JIRA task number followed by underscore (`_`) and a short description. Example: `AMM-1111_a_short_description`.
3. If working on some code that has no task then branch name MUST NOT contain any JIRA task prefix and SHOULD simply begin with a description of the thing you're working on. Example: `short_description_of_my_code`.
2. If working on a bugfix task that goes to master ASAP, then branch name works the same as is usual with JIRA task except it MUST begin with `hotfix/`. Example: `hotfix/AMM-1111_short_description_of_that_fix`.
4. if working on a immediate bugfix that has to go to master ASAP that has no JIRA task then branch name MUST begin with `hotfix/` and then it can be followed by a short description. Example: `hotfix/short_description_of_bugfix`.
