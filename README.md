# gitcheats
A collection of useful Git commands I've come to use often. 


## Working with Branches
### 1. Take an outdated branch and force it to be up to date with a new one

(For when you don't care about any of the changes in the out of date branch and don't 
want to delete a branch just for the sake of recreating an up to date branch of the same name.)

``` git push origin --force origin newbranch:outofdatebranch ```

### 2. Create a branch locally _and_ remotely 
``` git fetch && checkout -b branch && git push origin branch ```

### 3. Remove a branch locally _and_ remotely 

```git fetch origin && git reset --hard origin/master && git clean -f -d ```

Optionally, checkout the branch you were working on:
``` git checkout mybranch && git pull && git clean -f -d```

## Other

### 4. Completely reset a local repo without having to reclone 

```git branch -d branch && git push origin -d branch ```

### 5. Add a submodule to your repository
After doing this you'll always want to clone your repository recursively using ``` git clone -r``` in order to 
clone your submodules as well. 

``` git submodule add https://github.com/chaconinc/DbConnector
    git submodule init
    git submodule update
```
