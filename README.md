# cheats
A collection of useful commands I've come to use often. 

### SSH

- Regenerating a public key from a private key
```bash
chmod 400 ~/.ssh/id_rsa # If you haven't done so already
ssh-keygen -y -f ~/.ssh/id_rsa > ~/.ssh/id_rsa.pub
```

### Hugo
- Getting up and running from a new machine
```bash
git clone git@github.com:ranguli/blog.joshmurphy.ca
cd blog.joshmurphy.ca
hugo server -D
```

### GPG

- Trusting a GPG key after importing it from one machine to another
```
gpg --edit-key <KEY_ID>
gpg> trust
```

### Docker

- Get a bash shell for a running container
```
docker exec -it CONTAINER_ID /bin/sh
```

### aws-vault

- A great example from the aws-vault [repo](https://github.com/99designs/aws-vault) illustrating just how convenient a tool it is.
```
$ aws-vault exec home -- env | grep AWS
AWS_VAULT=home
AWS_REGION=us-east-1
AWS_ACCESS_KEY_ID=%%%
AWS_SECRET_ACCESS_KEY=%%%
AWS_SESSION_TOKEN=%%%
AWS_SECURITY_TOKEN=%%%
```

### Linux
- Find a network printer even if it isn't installed
```
systemctl start avahi-daemon && avahi-browse -a | grep Printer
```

- Copy the contents of a text file into your clipbaord
```
xclip -sel c < file.txt
```

### wget

- Downloading multiples files
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

## Git

- Take an outdated branch and force it to be up to date with a new one (for when you don't care about any of the changes in the out of date branch and don't want to delete a branch just for the sake of recreating an up to date branch of the same name.)

```
git push origin --force newbranch:outofdatebranch
```

- Create a branch locally _and_ remotely 
```
git fetch && checkout -b branch && git push origin branch
```

- Remove a branch locally _and_ remotely 
```
git branch -d branch && git push origin -d branch
```

- Completely reset a local repo without having to reclone 
```
git fetch origin && git reset --hard origin/master && git clean -f -d
git checkout mybranch && git pull && git clean -f -d # Optionally checkout a clean version of the branch
```

Add a submodule to your repository

- After doing this you'll always want to clone your repository recursively using ``` git clone -r``` in order to 
clone your submodules as well. 
``` 
git submodule add https://github.com/chaconinc/DbConnector
git submodule init
git submodule update
```

- Syncing submodules if you forgot to clone recursively (by using `--recursive`). You can setup the submodules without recloning 
``` 
git submodule init
git submodule update
```

- Keeping a fork up to date
```
# First add the fork as upstream
git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
git remote -v # Verify it worked
git merge upstream/master # Then merge it
```

- Comparing a local file to it's remote counterpart:
```
git fetch origin master # Make sure you have fetched the details from remote
git diff FETCH_HEAD -- yourfile.py # Compare your two files
```
