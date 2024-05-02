# Bashing Git

If you are curious how to rummage through the git innards then this short one is for you! 

The current repository is based off [GitGuardian sample secrets](https://github.com/GitGuardian/sample_secrets) but with some commits on top to add the guide. ([Original README](ORIGINAL_README.md))

## Open this exercise GitPods
You can continue reading the guide in GitPods from here.

[![Start with Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/marianabocoi/secrets-git-bash)

ℹ️ If it asks you to create an account, log in with GitHub.

## Digg for secrets
You can use this [shell one-liner](https://twitter.com/TomNomNom/status/1133345832688857095) that [@TomNomNom](https://twitter.com/TomNomNom) came up with, which dumps the contents of a repository's object database, and then greps on the result.

```
{ find .git/objects/pack/ -name "*.idx"|while read i;do git show-index < "$i"|awk '{print $2}';done;find .git/objects/ -type f|grep -v '/pack/'|awk -F'/' '{print $(NF-1)$NF}'; }|while read o;do git cat-file -p $o;done|grep -E 'pattern'
```

For example, a pattern you could use is: `mongodb(\+srv)?\:(\/\/)?(\w+)?:(\w+)@`

## Remove secrets & try again
Let's see what we find if we do:
```
rm bucket_s3.py postgres_model.js 
git add .
git commit -m "removed secrets"
```

Re-run the command above.

## Bonus!
Can you make them go away completley?
