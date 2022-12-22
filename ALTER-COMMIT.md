# How to alter commits

Sometimes it might so happen that you make a muck out of your code, a small mistake here or there. Sometimes you just want your commit history to look nice and readable for anyone else. Sometimes it could be that the project requires you to do commits in certain way. Git has the tools necessary to do all that and more. In this document you can get a crash course about how to alter those commits and work to make your commit history a bit more orderly.

A great tool for that is the `git rebase` command. It is a very powerful tool, and while this means that you can do some nice things, you can also do something very bad with it if you are not careful or knowledgeable. Of course I only recommend using it when you are the only working on your own branch and nobody else is working. Otherwise it needs to be a team-wide agreement or good understanding and good habits how to deal with that.

Let's start with the cases:

### CASE 1 - merging two most recent commits together
You are working on some code, commit it all and then you notice you made some mistake. You can fix it, write a git commit that says "fix mistake" and then you're done. However this is a bad commit. At least the message is definitely. While you can write a smarter commit, sometimes an ever better solution is to merge those two commits and avoid others seeing this additional commit completely. It is done by rebasing it into a previous.

It can be done by writing `git rebase -i HEAD~2`. The `-i` stands for interactive mode. `HEAD~2` takes two most recent commits. Change the number to whatever you wish and you will see however many commits you want to edit.

Then you will see commits with a `pick` prefix and their ids and commit messages. The bottom one is the newest. so if you wish to merge it into the previous one simply delete the `pick` prefix and change it with `f` or `fixup` keyword. This will merge the two commits together and only the second newest will be visible in history. The code will also be merged into one so your code will definitely not go away.
Obviously you want to have this in remote repository, so then you need to push it. Simply writing `git push` will refuse you. Rebase also changes the commit itself since after these two commits were merged it sort of creates a new one in its place. So the commit you merged is gone, and the commit you merged into is replaced with a new one that contains your combined code. In that case you need to **force** your code into the remote repository. You can write `git push --force` and it would work. However it is dangerous to do that because if someone else also worked on that branch and committed in that time you will delete someone's code accidentally. When you're forcefully pushing always use option `--force-with-lease`. This tries to first detect if there were any changes to remote repository and if there were then it will refuse you and will tell you to pull the changes first. A safeguard, so always use it when pushing forcefully. Only use `--force` when you are really really sure of what you are doing.

After these commands the result will be that there is no longer a commit that fixes a single line where you made a simple mistake on a commit minutes earlier, but the fixed code will remain.

### CASE 2 - merging two commits which are not directly adjacent

Let's say in commit 1 there was a text where you made some mistake, a typo for example. Then you made a separate commit that deals with some other problem. Then you notice your mistake in commit 1 and you want to fix it graciously without almost unnecessary commit remaining in history. In that case you create a commit that fixes your typo.

Then, write `git rebase -i HEAD~3`. The 3 in this case means 3 most recent commits.
So now you want to merge the 3rd and 1st commits. In this case move the 3rd commit one line up above commit #2. Then on that freshly moved 3rd commit (which is now in row 2) change the keyword from `pick` to `f` and save the rebase changes. This will then merge those two commits and it will look as if you never made a typo in the first commit in the first place.
Then of course remember to `git push --force-with-lease`.
I only recommend this on branches, staged for pull requests where you are working alone. Otherwise, as mentioned before, you need good understanding with teammates or team-wide agreement.

### CASE 3 removing unnecessary code and commit

You created a commit in your PR, but after some time you decide that this code is completely unnecessary and there is no point in keeping it. You can either create a new commit where you manually remove those changes. You can create a `revert` commit where it reverts these changes. Or you can drop the commit with the git rebase. In order to drop the last commit simply write `git rebase -i HEAD~1` then change the keyword from `pick` to `d` and save the rebase changes. Push via `git push --force-with-lease` and voilà - commit and code is gone.
You can drop any commit you like, i.e. 4th last commit. However I would strongly recommend to exercise as much caution as possible, because your code might still remain if the files you dropped were later worked on in another commit. This will case your code to stay OR conflicts appear.

### CASE 4 - merging two most recent commits via git reset

Same as in CASE 1, you might want to merge those two commits but you want to avoid using git rebase. In this case you can use git reset.

Begin by checking how many recent commits you want to merge into one. In this case I want to have two of them merged into one.
Write `git log` to get the commit id that you want to get back to. For example if you want to merge two commits then copy the 3rd most recent commit ID.
Write `git reset --soft <3rd-newest-commit-id>`. This will remove those two commits but retain their code that is taged for commit as if you began your work anew and already written the necessary code. Now you can make a new commit with whatever message you like. Then make the push with `git push --force-with-lease` and you're set.

### CASE 5 - squashing commits

Sometimes you might want to merge two commits since you want to avoid the commit clutter but retain their messages. In that case do evverything as in CASE 1 but write `s` prefix instead of `pick` or `f`. This will squash the commits into one but will retain their messages separated by an empty line.
