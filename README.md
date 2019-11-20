# cheats
A collection of useful commands I've come to use often. 

## GPG

### Trusting a GPG key after importing it from one machine to another

```
gpg --edit-key <KEY_ID>
gpg> trust
```

## Docker

Get a bash shell for a running container

```
docker exec -it CONTAINER_ID /bin/sh
```

## aws-vault

A great example from the aws-vault [repo](https://github.com/99designs/aws-vault) illustrating just how convenient a tool it is.

```
$ aws-vault exec home -- env | grep AWS
AWS_VAULT=home
AWS_REGION=us-east-1
AWS_ACCESS_KEY_ID=%%%
AWS_SECRET_ACCESS_KEY=%%%
AWS_SESSION_TOKEN=%%%
AWS_SECURITY_TOKEN=%%%
```

## Linux
#### Printing

##### 1. Find a network printer even if it isn't installed
``` systemctl start avahi-daemon && avahi-browse -a | grep Printer ``` 
#### Clipboard

##### 1. Copy the contents of a text file into your clipbaord
``` xclip -sel c < file.txt ```

#### GNU wget

##### 1. Downloading multiples files

``` 
# Add our URLs in to a file list. Makes a nice backup/manifest too.
(
echo www.urlfromclipboard.com/1
echo www.urlfromclipboard.com/2
echo www.urlfromclipboard.com/3
)>"shoppinglist.txt"
pause

# Point wget to our URL list
wget -i shoppinglist.txt
```

## Python & Pip
#### Pip
##### 1. Installing a pip package so that it actually installs an executable
Sometimes ```pip install``` or ```pip install -U``` doesn't cut it and you aren't 
provided with an actual executable. Run:

``` sudo pip install --prefix /usr/local packagename ```

Now if you run ``` which packagename``` you should actually see it installed
in a globally accessible place. 

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


#### Submodules

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

#### Forks

##### 7. Keeping a fork up to date

Forks are the backbone of collaboration on GitHub! If you maintain a fork of a project for long enough that you need to sync with it's upstream, repo look no further:

First, add the fork as up origin:

``` git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git ```

Then verify it worked with:

``` git remote -v ```

Then merge with:

``` git merge upstream/master```

#### Diff Strategies

##### 8. Comparing a local file to it's remote counterpart:

First make sure you have fetched the details from remote:

``` git fetch origin master ```

Then compare your two files:

``` git diff FETCH_HEAD -- yourfile.py ```
