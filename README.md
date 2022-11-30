# proper-commit
Your guide to etiquette of branching and committing

Branch naming guidelines:
1. If working on a particular JIRA task then branch name MUST begin with the JIRA task number followed by underscore (`_`) and a short description. Example: `AMM-1111_a_short_description`.
3. If working on some code that has no task then branch name MUST NOT contain any JIRA task prefix and SHOULD simply begin with a description of the thing you're working on. Example: `short_description_of_my_code`.
2. If working on a bugfix task that goes to master ASAP, then branch name works the same as is usual with JIRA task except it MUST begin with `hotfix/`. Example: `hotfix/AMM-1111_short_description_of_that_fix`.
4. if working on a immediate bugfix that has to go to master ASAP that has no JIRA task then branch name MUST begin with `hotfix/` and then it can be followed by a short description. Example: `hotfix/short_description_of_bugfix`.

Commit message guidelines:
1. Commit message should be structured as follows:
```
<task number>: <description>

[optional body]
```
2. If working on a JIRA task (bugfix or not), then commit message MUST begin with task number and a semicolon, for example `AMM-1111:`.
3. If working on a code that has no JIRA task then commit message SHOULD begin with the short description of the code.
4. Commit description MUST be written in imperative mood (Expressing a command; authoritatively or absolutely directive).
5. Commit description SHOULD be no more than 60 characters long. Longer descriptions might be cut off by repositories and such.
6. Commit description SHOULD only deal with one topic.
7. A longer commit body MAY be provided after the short description, providing additional contextual information about the code changes. The body MUST begin one blank line after the description.
8. A commit body is free-form (imperative mood is not used here) and MAY consist of any number of newline separated paragraphs.
9. If commit body consists of lines where code parts are explained then each line SHOULD be prefixed with an asterisk and a space `*<space>` in order to a provide neat bulleted list.
10. Commit body lines SHOULD try to be maximum 72 characters long (including prefix)

Example of a commit:

```
AMM-1111: create UserDocument entity

* Also added phpDoc parameters for related User entity
* Fixed test names for User model tests
* Moved asserts up by several lines for "<filename>" test in <filename> because currently they are not asserted since an expected exception in line 94 stops code execution beforehand.
```
