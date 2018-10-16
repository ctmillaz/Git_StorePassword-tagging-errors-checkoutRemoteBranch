# StoreGitPassword-tagging-errors-checkoutRemoteBranch

# How to make git cache your password on GitHub

### Set git to use the credential memory cache
`$git config --global credential.helper cache`

### Set the cache to timeout after 1 hour (setting is in seconds)
`$git config --global credential.helper 'cache --timeout=3600'`

----------------------------------------------------------------------
### Also, I’m not using a STIG image, so I need to switch over to one to see how things work in a more restrictive environment.

### On my non-STIG CentOS image, I was able to cache my git credentials with just this one command:
`git config --local credential.helper cache`

### This creates an encrypted(?) folder under your home folder:
### $ ls -ad ~/.git-*

### drwx------. 2 miller <nameOfUser> <date> /your/homeDirectory/.git-credential-cache


### After setting that configuration value, you’re prompted for username/password the first time you log in, but not thereafter.


### Another credential caching mechanism outside of GIT is netrc. It worked for me, but STIG rules prohibit the use of netrc. STIG might also prohibit GIT’s credential-helper, too.


### One of the error messages you encountered below is Bad owner or permissions on /your/homeDirectory/.ssh/config. This can usually be solved using these commands:
`chmod 600   ~/.ssh/config`
`chown $USER ~/.ssh/config`

### The config file needs tight permissions to keep others out, and SSH makes sure permissions are set before it works. But that doesn’t mean SSH will necessarily work after fixing this one issue.

-----------------------------------------------------------------------------------------------------------------------------------
# Tagging

### Checking out a tag is like checking out a specific commit that was labeled.
### Make sure all tags exist locally
 
```
git fetch --all --tags --prune
```

### Checkout tag by running
```
git checkout tags/<tag_name> -b <branch_name>
```
### Instead of origin use the tags/ prefix

### list all the tags
```
git tag
```

### list all tags with the given pattern example: v-
```
git tag --list 'v-*'
```

### creating a normal tag
```
git tag
```

### Annotating a tag
```
git tag -a
```

### Delete a tag
```
git tag -d <tag name>

```
----------------------------------------------------------------------------------------------------------------------------
# Errors

### Problem:     fatal: index file smaller than expected

### Solution:    rm .git/index
	         git add .

### Problem: 	error: unable to resolve reference HEAD: No such file or directory
		fatal: cannot lock HEAD ref

### Solution:	Reclone git repo and copy source and compiler config
### Alternative Solution: 
```
cat .git/HEAD
```
```
rm <directory_listed_command>
```



---------------------------------------------------------------------------------------------------------------------------------


### How to create a local branch from a remote branch or remote-ready:
### Example: $ git checkout --track origin/newsletter
### Leave out the remotes portion and just use origin/<branch>
`$ git checkout --track origin/<branch>`

### You wil still need to do a git push to the remote branch for coworkers to see it.
