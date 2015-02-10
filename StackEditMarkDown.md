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
