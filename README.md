# cheats
A collection of useful commands I've come to use often. 

## Linux
#### Printing

##### 1. Find a network printer even if it isn't installed
``` systemctl start avahi-daemon && avahi-browse -a | grep Printer ``` 
#### Clipboard

##### 1. Copy the contents of a text file into your clipbaord
``` xclip -sel c < file.txt ```


## Git
#### Working with Branches
##### 1. Take an outdated branch and force it to be up to date with a new one

(For when you don't care about any of the changes in the out of date branch and don't 
want to delete a branch just for the sake of recreating an up to date branch of the same name.)

``` git push origin --force newbranch:outofdatebranch ```

##### 2. Create a branch locally _and_ remotely 
``` git fetch && checkout -b branch && git push origin branch ```

##### 3. Remove a branch locally _and_ remotely 

```git branch -d branch && git push origin -d branch ```


#### Other

##### 4. Completely reset a local repo without having to reclone 

```git fetch origin && git reset --hard origin/master && git clean -f -d ```

Optionally, checkout (an equally squeaky-clean version of) the branch you were trying to work on before the Gods had forsaken you:

``` git checkout mybranch && git pull && git clean -f -d```

##### 5. Add a submodule to your repository
After doing this you'll always want to clone your repository recursively using ``` git clone -r``` in order to 
clone your submodules as well. 

``` 
    git submodule add https://github.com/chaconinc/DbConnector
    git submodule init
    git submodule update
```

##### 6. Syncing submodules if you forgot to clone recursively

Sometimes you forget to use the `--recursive` flag while cloning, or you didn't think the repo had submodules. You can setup the submodules without recloning 

``` 
    git submodule init
    git submodule update
```

