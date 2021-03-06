## Intro

This package contains materials for the [Nice R Code 
blog](http://nicercode.github.com/), run by Rich FitzJohn and Daniel Falster. 
The site is constructed using [Octopress](http://octopress.org/). The git repo 
is private, [hosted on bitbucket](https://bitbucket.org/richfitz/nicercode). 
The site is deployed on github at 
[http://nicercode.github.com/](http://nicercode.github.com/). All edits are in 
bitbucket repo. The only thing that happens on github is to deploy. 

[Octopress documentation](http://octopress.org/docs/) 

## Excluding posts from front page

Using a small modification to the pagination plug-in [described here](arshad.github.io/blog/2012/05/10/recipe-hiding-posts-from-the-octopress-front-page/) post can be excluded from the front page by marking them draft (see _config.yaml for the list of categories to be shown or excluded on front page).

Draft posts can then be viewed at [http://nicercode.github.io/blog/categories/draft/](http://nicercode.github.io/blog/categories/draft/)

## Working with Rmd files

Rmd files should be kept in the `_drafts` directory, as they cause problems when posted in the `_posts` directory.  The function `knit_post` function can is used to publish suitable md and associated image files from the `_drafts` to over to the `_posts` directory. 

```r
source("knit_post.R")

# Setting publish = FALSE will produce files in the _drafts directory, for review 
knit_post("trial.Rmd", publish=FALSE)

# Setting publish = TRUE will publish post to _posts, figures to _images and delete corresponding files from the drafts directory

knit_post("trial.Rmd", publish=TRUE)
```

## Formatting changes to consider

- indentation of lists, works well on phones, but not on desktop
- fontsize too big?
- add about page with bios

## Formatting conventions

- dots for 

## Setting up on a new machine ##

Here are summary instructions for setting up on a new machine. For more info 
see [octopress documentation](http://octopress.org/docs/setup/).

### Clone nicercode project from bitbucket ###
`git clone git@bitbucket.org:richfitz/nicercode.git`

### Install [rbenv](http://octopress.org/docs/setup/rbenv/) ###

`git clone git://github.com/sstephenson/rbenv.git .rbenv`
`git clone git://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build`

make sure .rbenv is in path. Bash users follow std instructions at link above. 
For zshell users, make sure following lines are in .zshrc 

    path=(/Users/dfalster/bin /Users/dfalster/.rbenv/bin $path)
    export path
    eval "$(rbenv init -)" 

Then in new terminal window

    rbenv install 1.9.3-p194  #  to install newer version of ruby
    rbenv rehash
    sudo gem install bundler
    rbenv rehash    # If you use rbenv, rehash to be able to run the bundle 
command
    bundle install

### Install [pow](http://pow.cx/) ###
`curl get.pow.cx | sh`. 

pow creates a local webserver.  Give your page a local name, viewable in web 
browser on your machine,e.g. 

    cd ~/.pow
    ln -s path/to/nicercode/gitrepo nicercode

### Setup rake to work with github ###
    rake setup_github_pages 
    git@github.com:nicercode/nicercode.github.com.git



## Making a post ##
1. `rake new_post\["Trial"\]`
2. edit file produced, e.g. `edit source/_posts/2013-03-07-trial.markdown`
3. Preview post using `rake preview` #makes viewable in web-browser at 
`localhost:4000` or `nicercode.dev` (if you are using pow)
4. Other ways to preview are 
	a. `rake generate` #to build site  
	b. `rake watch` #starts process that watches for file updates and 
rebuilds. 

4. commit,push to bitbucket
5. `rake deploy` deploys to github

## Formatiing 

see the [Octopress Plugin index ](http://octopress.org/docs/plugins/) for the full list of Octopress plugins.

[Sharing code](http://octopress.org/docs/blogging/code/)
 
### Blockquotes

Use the [blockquotes package](http://octopress.org/docs/plugins/blockquote/) to format author, source, link for a quote

```
{% blockquote [author[, source]] [link] [source_link_title] %}
Quote string
{% endblockquote %}
```


### Gist code

Easily embed gists in your posts or pages using [gist Tag package](http://octopress.org/docs/plugins/gist-tag/)

```
{% gist 996818 %}
```
