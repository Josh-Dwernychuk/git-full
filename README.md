# git-full
Shell script to add, commit, and push to current branch in one command

# Setup
Find out where your git executables are stored:
```
echo $(git --exec-path)/
# /usr/libexec/git-core/
```

Create git-full file in executables directory:
```
vim /usr/libexec/git-core/git-full
```

Insert git-full sh script into file:
```
#!/bin/sh

source "$(git --exec-path)/git-sh-setup"

USAGE="COMMITS"
function _full() {
    for ((i = 1; i < $#; i++))
    do
    git add ${!i}
    done
    git commit -m "${!i}"
    branch=$(git branch | sed -n -e 's/^\* \(.*\)/\1/p')
    git push origin $branch
}
_full "$@"
```

Change file permissions:
```
chmod +x /usr/libexec/git-core/git-full
```

# Usage
```
git full . "commit message"
git full filename.py "commit message"
git full filename1.py filename2.py "Commit message"
```
