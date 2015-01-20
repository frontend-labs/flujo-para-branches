```sequence
participant Master
participant Staging
Development->Development: git pull origin development
Development->type#number_summary (up to 80 characters): git checkout -b
Note right of type#number_summary (up to 80 characters): Do your work
Development->Development: git pull origin development
Development-->type#number_summary (up to 80 characters): git rebase origin development
Note right of type#number_summary (up to 80 characters): Upload to repository\n for Code Review
type#number_summary (up to 80 characters)-->Development:If Code Review was declined.\n Fix the errors.
Development->Development: git pull origin development
Development-->type#number_summary (up to 80 characters): git rebase origin development
type#number_summary (up to 80 characters)-->Staging: If Code Review was approved.\n Do Pull Request
type#number_summary (up to 80 characters)-->Staging: git merge staging
Staging->Staging: git pull origin staging
Staging-->Development: git rebase origin development
Staging-->Master: git merge staging
Master->Master:git pull origin master
Master-->Staging:git rebase origin master

```