```sequence
master->master: git branch staging origin/master
master-->staging: git checkout staging
staging->staging: git push -u origin staging
staging->staging: git branch development origin/staging
staging-->development: git checkout development
development->development: git push -u origin development
development->development: git pull
development->development: git branch [type]_[issue_number]_summary origin/development
development-->[type]_[issue_number]_summary: git checkout [type]_[issue_number]_summary
Note right of [type]_[issue_number]_summary: Do your work
[type]_[issue_number]_summary-->development: git checkout development
development->development: git pull
development-->[type]_[issue_number]_summary: git checkout [type]_[issue_number]_summary
[type]_[issue_number]_summary->[type]_[issue_number]_summary: git rebase -i origin/development
[type]_[issue_number]_summary->[type]_[issue_number]_summary: git push -u origin [type]_[issue_number]_summary
Note right of [type]_[issue_number]_summary: Ready for Code Review
Note left of [type]_[issue_number]_summary: If Code Review was  declined.\n Fix the errors.
[type]_[issue_number]_summary-->development: git checkout development
development->development: git pull
development-->[type]_[issue_number]_summary: git checkout [type]_[issue_number]_summary
[type]_[issue_number]_summary->[type]_[issue_number]_summary: git rebase -i origin/development
[type]_[issue_number]_summary->[type]_[issue_number]_summary: git push origin +[type]_[issue_number]_summary
Note left of [type]_[issue_number]_summary: If Code Review was approved.\n Do Pull Request
[type]_[issue_number]_summary-->development: git checkout development
development->development: git merge [type]_[issue_number]_summary
development-->staging:git checkout staging
staging->staging: git pull
staging->staging: git merge development
staging->staging: git push origin staging
Note left of staging: Test Cases from QA
staging-->master: git checkout master
master->master: git pull
master->master: git merge staging
master->master: git push origin master
master-->staging: git checkout staging
staging->staging: git pull
staging->staging: git rebase -i origin/master
staging->staging: git push origin +staging
staging-->development: git checkout development
development->development: git pull
development->development: git rebase -i origin/staging
development->development: git push origin +development
```

Image caption
-------

> **git branch [new_branch] [parent_branch]:** Create new branch based on parent branch.
> **git push -u [branch]: ** Push your changes and set up the stream between the local and the remote branch.
> **git pull: ** Combination of *git fetch*, which connects to the remote repository and fetches new commits, and *git merge* (or *git rebase*) which incorporates the new commits into your local branch. 
> **git rebase -i [parent_branch]:** Update your current branch based on the parent branch, so the commits from the parent branch are placed first that the commits from the current branch. The ‘-i’ option enables the the [interactive mode](http://git-scm.com/docs/git-rebase#_interactive_mode) .
> **git push origin +[branch]:** Force update to the remote branch with the local branch.