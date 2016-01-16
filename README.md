# Advanced git concepts

The not-so-every day workflow

### Merging
#### Scenario 1: You have need to add a new category of films, but that is not due to be released yet. Your team has decided that the work is going to be done on a branch, until the feature is ready to be released

Checkout a new brach called scifi  
Create a folder called scifi inside the movies folder  
Create a file blade_runner.txt in the scifi folder  
Make changes to the file and commit them  
Push the branch to the remote repository  

```console
  git checkout -b scifi
  git add .
  git commit -m "Add Blade Runner to scifi films"
  git push -u origin scifi:scifi
  git log --pretty=oneline --decorate
```

#### The feature is nearly done, but there is some urgent work that needs to be done on master and you need to push a hotfix

Checkout master  
Add film_noir/the_maltese_falcon.txt  
Push the change to master  

```console
  git checkout master
  git add .
  git pull
  git push
  git log --pretty=oneline --decorate
```

#### Let's finish the feature and merge it back to master

checkout the scifi branch  
Make a change in the blade_runner.txt file and push it to the remote  

```console
  git checkout scifi
  git add .
  git commit -m <Short meaningful message>
  git push
```

#### Merging

```console
  git checkout master
  git merge scifi
  git log --pretty=oneline
  git push
```

### Rebasing
#### Scenario 1, take 2: You have need to add a new category of films, but that is not due to be released yet. Your team has decided that the work is going to be done on a branch, until the feature is ready to be released

Create a branch called thriller  
Add thriller/spectre.txt to the branch  
Push the branch to the remote repository  

```console
  git checkout -b thriller
  git add .
  git commit -m "Add Spectre to thriller films"
  git push -u origin thriller:thriller
  git log --pretty=oneline --decorate
```

#### The feature is nearly done, but there is some urgent work that needs to be done on master and you need to push a hotfix

Checkout master  
Make a change to film_noir/maltese_falcon.txt  
Push to the remote  

```console
  git checkout master
  git add .
  git pull
  git push
  git log --pretty=oneline --decorate
```

#### Let's finish the feature and merge it back to master

```console
  git checkout thriller  
  git rebase master
  git checkout master
  git merge thriller
  git log --pretty=oneline --decorate --all --graph
```
