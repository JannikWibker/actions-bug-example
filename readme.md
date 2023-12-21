# Bug in github actions

Trying to access the `before` property of the push event does not work if the branch that the commits are getting pushed to has not existed on the remote prior.

The expected value of `github.event.before` would be a valid sha(*), but it is `0000000000000000000000000000000000000000` (40x `0`). 

(*): Assume n commits get pushed at once, then the expected value would be the first parent of the first of these commits (if it exists, it is unclear what should happen if the first pushed commit is the initial commit; `null` seems like an appropriate value)

Compare the action runs of the main branch with that of the `bug-showcase` branch.
