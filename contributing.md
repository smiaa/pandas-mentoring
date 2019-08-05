<br>

### Terms
  * Upstream: the repository from the ```original_author```
  * Origin: the forked repository under your ```account```
<br>

### 1. Fork a ```project``` to your GitHub ```account```
### 2. Clone the ```project``` to your local environment
```
    git clone git@github.com:account/project.git
    cd project
```
### 3. Set up the origin and upstream of the your local ```project```
```  
   #  Add the "upstream" to your cloned repository
    git remote add upstream git@github.com:original_author/project.git

   # Add the "origin" to your cloned repository
    git remote add origin git@github.com:account/project.git
```

### 4. Synchronize with updates from the upstream
```
   # 1) Go to the "master" branch of your fork ("origin")
    git checkout master

   # 2) Fetch the commits from the "upstream"
    git fetch upstream

   # 3) If you have local changes, stash the changes of your "master" branch
    git stash

   # 4) Merge the changes from the "master" branch of the "upstream" into your the "master" branch of your "origin"
    git merge upstream/master

   # 5) Resolve merge conflicts if any and commit your merge
    git commit -m "Merged from upstream"

   # 6) Push the changes to your fork ("origin")
    git push

   # 7) Get back your stashed changes (if any)
    git stash pop
```
### 5. Do your work in a ```new-branch``` of your origin
```
   # 1) Add a new branch from your origin/master branch
   git branch new-branch origin/master
   git checkout new-branch

   # 2) Make a commit of your work (e.g. you added your name in the README.md)
   git add README.md
   git commit -m 'add my name'

   # 3) If you had multiple commits, but you want to select a specific commit(e.g. commit id: bbb909f) for a pull request
   git cherry-pick bbb909f

   # 4) Push to your new-branch
   git push origin new-branch
```

### 6. Send a pull request on GitHub
 * Go to the ```new-branch``` of your forked ```project```
 * Click ```Compare & pull request```
 * Leave a comment
   * If you are solving an issue (e.g. ```#17```), add ```Closes #17``` in the comment, the issue will automatically be closed when the pull request is merged.


### Reference
* [GitHub forking](https://gist.github.com/Chaser324/ce0505fbed06b947d962)  
* [Git cherry-pick](https://git-scm.com/docs/git-cherry-pick)
