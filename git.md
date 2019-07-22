# Git
### Ignore files

Remove existing files from the repo

```
find . -name .DS_Store -print0 | xargs -0 git rm -f --ignore-unmatch
```

Ignore future files

```
touch .gitignore
echo .DS_Store >> .gitignore
```

### Make forked repo private

```
git clone --bare https://github.com/shiyinw/public-repo.git
cd public-repo.git
git push --mirror https://github.com/shiyinw/private-repo.git
cd ..
rm -rf public-repo.git
```

### Delete > 100M commits

Round back to the last commit

```
git rm --cached giant_file
git commit --amend -CHEAD
git push
```

Filter this file in all the commits

```
git filter-branch —-tree-filter 'rm -rf CTRP' HEAD
```

Reset the whole repo

```
git reset HEAD~1 --soft
git reset --hard HEAD
```

### LFS

Git Large File Storage

```
git lfs install
git lfs track "*.psd"
git add .gitattributes
```

### Change commit emails

```
git filter-branch --env-filter '
CORRECT_NAME="shiyinw"
CORRECT_EMAIL="wangsysusan@gmail.com"
export GIT_COMMITTER_NAME="$CORRECT_NAME"
export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
export GIT_AUTHOR_NAME="$CORRECT_NAME"
export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
' --tag-name-filter cat -- --branches --tags
git push --force --tags origin HEAD:master
```

### Install packages from git

```
pip3 install git+git://github.com/fchollet/keras.git --upgrade --no-deps
```

### Sync forked repo from original repo

```
git clone git@github.com:YOUR-USERNAME/YOUR-FORKED-REPO.git
git remote add upstream git://github.com/ORIGINAL-DEV-USERNAME/REPO-YOU-FORKED-FROM.git
git fetch upstream
git pull upstream master
```

