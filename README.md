# How to contribute to StatLab Articles

These instructions are intended for University of Virginia StatLab fellows and UVa Library Research Data Services staff. 

## Getting started

- Make sure you are using the latest version of RStudio. (If you already have RStudio installed, go to Help...Check for Updates)
- Make sure you are using the latest version of R. Go to [https://cloud.r-project.org/](https://cloud.r-project.org/) to see the version of the latest release. Then open RStudio and enter `version` in the console and hit Enter. If the latest release is newer than your version, then download and install the latest version of R. 
- install the blogdown package from CRAN or GitHub. Depending on how often you use R this may or may not install a lot of additional packages which blogdown depends on. This can take a minute or two.

```
# install from CRAN
install.packages("blogdown")
# Or, install from GitHub
if (!requireNamespace("devtools")) install.packages("devtools")
devtools::install_github("rstudio/blogdown")
```

- (Optional) Check for package updates. This is recommended if you installed R/RStudio a long time ago but haven't used it in a while. Go to Tools...Check for Package Updates... A list of available updates will be generated (if any). Unless you are neck deep in a project that absolutely requires using specific versions of packages, I would update all packages. Click Select All and then Install Updates. Again this may take a while if you have a lot of old packages.



- Since blogdown is based on the static site generator Hugo (https://gohugo.io), you also need to install Hugo. There is a helper function in blogdown to download and install it automatically on major operating systems (Windows, macOS, and Linux),
`blogdown::install_hugo()`. The install shouldn't take more than a few seconds. To upgrade or reinstall Hugo, you can use `blogdown::update_hugo()`. To check if you have Hugo installed: `blogdown::hugo_version()`


## Fork and Clone the repositories

There are two repositories for StatLab Articles: **blog** and **uvastatlab.github.io**. The **blog** repo contains the source code for _generating_ the web site. The  **uvastatlab.github.io** repo contains the actual web site. 

- Fork both repositories by clicking the Fork button on GitHub; both repos will be copied to your GitHub account
- Clone the forked repos to your computer:
    * Let's start with the 'blog' repo. Click the green 'Clone or download' button in your forked version of the 'blog' repo
	* highlight and copy the URL (eg: https://github.com/your_github_user_name/blog.git OR git@github:your_github_user_name/blog.git, if you're set up with SSH)
	* Open Git Bash on your computer and navigate to where you want to clone the repo. This is basically downloading the files to your computer. (Google "how to use cd command line unix" if not sure how to change directories at the command line.
	* Enter `git clone https://github.com/your_github_user_name/blog.git` or `git clone git@github:your_github_user_name/blog.git` at the prompt and hit Enter. You should see a message like "Cloning into 'blog'...
	* Repeat the steps above for the uvastatlab.github.io repo
- cd into new repos and add a Git remote that points back to the original repository (the one you FORKED):
    * `git remote add upstream https://github.com/uvastatlab/blog.git`
    * `git remote add upstream https://github.com/uvastatlab/uvastatlab.github.io.git`


	
## Start and work on a new bog post

- Before starting make sure your fork is in sync with original repo
    * `git pull upstream master`
    * `git push origin master`


- Before starting work on your blog post, create a new branch in both repos!
    * `git checkout -b new_branch_name `
	

- Open RStudio, File...Open Project... and open the "blog" project file in the blog repo
- Click Addins in the tool bar and click New Post. The first time you do this you may be asked to Install Required Packages. Go ahead and click Yes. You should only have to do this one time.
- Complete the fields. **Make sure you select R Markdown (.Rmd) as the format!** Click Done. This starts a new Rmd file with a header. 
- Start working on your blog post using R Markdown. 
- To preview your work, run `blogdown::serve_site()` at the command line. You should only need to do this once! Thereafter clicking Ctrl + S or Cmd + S should render a preview in the Viewer window. **DO NOT CLICK THE KNIT BUTTON!**
- Keep working on your blog post until you're ready to publish


## Submit new post to GitHub

- Do the following in both repos
   *  `git add .`
   * `git commit -m "descriptive comment"`
   * `git push origin new_branch_name`
   * Do in both repos

- Open a pull request to the uvastatlab repos. Again have to do in BOTH repos.
   * Go to your forked version of repo in GitHub
   * Click the 'Compare & pull request' button. Hopefully you'll see a green message that says "Able to merge"
   * Click the 'Create pull request' button
   * Do in both repos

Clay or Michele will either Merge your pull request or reply with comments or changes. 

In the event we reply with changes, implement the changes and resubmit the pull request:
- go to Rmd file and make changes
- go to Git Bash
    * `git add .`
	* `git commit -m "made requested changes"`
	* `git push origin new_branch_name`
	* Do in both repos
    * There is no need to open another pull request! Your changes will appear to Michele and Clay.

- Once your pull request has been accepted (ie, your blog post is published), you need to do the following in BOTH repos:
	* Fetch from upstream repo: `git fetch upstream` (may need to wait for GitHub to catch up)
    * Check out your fork's local master branch: `git checkout master`
    * merge changes from upstream/master into the local master branch: `git merge upstream/master`
    * delete the branch you created (because the changes are already in the master branch): `git branch -d new_branch_name`
    * update the master branch in your forked repository: `git push origin master`
    * push the deletion of your branch to your GitHub repository: `git push --delete origin new_branch_name`

TIP: use your up arrow keys to recall commands. 	
	
- Clay/Michele: how to locally review changes:
   * See https://help.github.com/en/articles/checking-out-pull-requests-locally
   * Go to RStudio, open 'blog' project and run blogdown::serve_site()
   * Review changes
   * Either request changes or merge pull request
   * Probably best to conduct review and pull requests in the 'blog' repo

- Once pull request is accepted and new branch merged, Clay and Michele:
    * In your local 'blog' repo:
        * `git checkout master` 
        * `git pull origin master` 

    * In your local 'uvastatlab.gitghub.io' repo:
        * `git reset --hard`
        * `git clean -dfx`
        * `git pull origin master`



## How to add images not generated by R Markdown

Place image under `blog/static/img`   
Example: `blog/static/img/fig1.png`   
In Rmd file enter: `![](/img/fig1.png)`   


## How to add data sets to site
Store in `/static/data`   
Example: `blog/static/data/demo.csv`   
Example: `blog/static/data/demo.Rds`   

In Rmd file add: `demo <- read.csv("../../static/data/demo.csv")`
In Rmd file add: `demo <- readRDS("../../static/data/demo.Rds")`

Clay and Michele can also upload data to https://static.lib.virginia.edu/statlab/materials/ 

## How to include LaTeX

For R Markdown posts, you can use $math$ for inline math expressions, and $$math$$ for display-style expressions.

## Please include the following footer in your blog post

````
For questions or clarifications regarding this article, contact the UVa 
Library StatLab: [statlab@virginia.edu](mailto:statlab@virginia.edu) 

_Your Name_   
_Statistical Research Consultant_  
_University of Virginia Library_  

```{r}
sessionInfo()
```

````

## Rmd file names

The file name of the Rmd file will be prefaced with whatever date you set in the dialog to create a new post. You can later change the date in the metadata header, and that will get reflected in the site's navigation when the site is rebuilt. However the Rmd file name will continue to have the original date unless you update it manually. It's probably fine to just leave the file name as is. The date of publication of a StatLab article isn't terribly important. All that matters is the metadata date is what you want it to be. 

It's important to note that the tile of your post will also be used to create the name of the Rmd file. Again, you can update the title in the metatdata header but it will not update the file name. **It's a good idea to settle on a blog post title before you actually create the post.**

If the date and title radically change and it bothers you, you can just delete the post and start over. Go to `blog/content/post/` and delete your Rmd file and associated HTML file. **Please be careful! Don't delete the wrong post!** Obviously our site is version controlled and you can restore a deleted file, but it's easier to not have to mess with it. 


## Tags and categories

Try to use existing tags, but feel free to create your own. Use all lower-case (eg, mixed effect modeling, logistic regression, neural networks, etc), except when using acronyms (eg, AIC, ANOVA, OLS, etc)
