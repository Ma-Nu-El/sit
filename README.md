
# Table of Contents

1.  [sit: a simple repo manager for git](#org722e6ba)
    1.  [preamble](#org52ab662)
    2.  [Kind of licensing?](#org23bba54)
2.  [problem [why bother in the first place]](#orgc99bee8)
3.  [current solution [way too inefficient]](#org151c7a3)
4.  [wanted solution [maybe too good?]](#orgfb561cf)
5.  [how to get there [middle term once again?]](#org190ccaf)
    1.  [add locations](#org4f4236c)
        1.  [verb](#orgc7ea530)
        2.  [if](#org6e7fa7d)
        3.  [fi](#orgd282985)
    2.  [display the locations](#orgd2b0713)
        1.  [if](#org7a6651c)
        2.  [fi](#orgce7ed09)
    3.  [git status part](#org338517a)
    4.  [git commit part](#org468a84f)
    5.  [git push part](#org038bb58)
    6.  [git pull part](#org3c5f646)



<a id="org722e6ba"></a>

# sit: a simple repo manager for git


<a id="org52ab662"></a>

## preamble

The source code for the Markdown and the actual executable file is the
`.org` file itself. I just *tangle* the `sit` file and *export* to
Markdown using *Orgmode's* `C-c C-e m m`.


<a id="org23bba54"></a>

## Kind of licensing?

By the way, I haven't read about licenses, but I know that I don't
want to get charged for using this stuff now or in the future, so I
guess I'd be opting for something like the GPL/MIT/BSD branch.

Please feel free to do whatever you want with this code, I just want
to type less (and remember less) in order maintain my scattered git
repositories.


<a id="orgc99bee8"></a>

# problem [why bother in the first place]

I type too much just to commit and push in different git repositories
in my machine.

Plus, it's a nice motive to learn bash.


<a id="org151c7a3"></a>

# current solution [way too inefficient]

I have to `cd` into every git repo - which by the way have to remember
its location every time for every repo -.

From here I usually do one of the two following actions:

1.  Copy the commit message and paste it on the next commit of all the
    other git repos.

1.  Push.

Maybe I haven't pushed up the different git repos and now after
committing in each repo (related or not) I want to push them up. That
involves `cd` `<insertGitRepoLocation>` and then `git push` and repeat
again for every repo.

This workflow is a problem because:

-   I have to remember where are all these different repos

Note that the number of repos is highly variable, so getting used to
remember some locations is not an option since you could easily forget
that particular little test repo you needed to commit/push. I have
forgotten those. It's annoying.

-   Since I have these repos scattered in multiple directories in
    multiple machines, it's very error prone
-   git submodules/subtree/subrepos are way too complex for what I need


<a id="orgfb561cf"></a>

# wanted solution [maybe too good?]

If I'm in the `$HOME` folder, then just `git status` right from the
`$HOME` directory only to be aware of the changes made to the
different present git repos.

I'd be committing every change to its corresponding git repo with the
same message. Very much as if I `cd` into every repo and `git
commit` right from each one manually; as already explained it's an
error prone and cumbersome way to do.

In the same way, I could `push` with one command or push from each
one, I want to have that flexibility also.


<a id="org190ccaf"></a>

# how to get there [middle term once again?]

Usually, I have to remember where are these repos located.

That can be solved using a simple array variable to store the
locations of the different git repos; the locations should always be
the same across machines and the same relative to the `$HOME`
directory.

Something like 

    declare -A repositories


<a id="org4f4236c"></a>

## DONE add locations


<a id="orgc7ea530"></a>

### verb

I could use something like "`sit add`". For the first time, it has to
be manually done. And as well, you should be able to add multiple
directories at once.


<a id="org6e7fa7d"></a>

### if

    if [ $1 == 'add' ]
    then

    REPO_NAME=$2
    REPO_DIR=$3
    echo $REPO_NAME>>repoNam.txt
    echo $REPO_DIR>>repoDir.txt


<a id="orgd282985"></a>

### fi

    fi


<a id="orgd2b0713"></a>

## display the locations


<a id="org7a6651c"></a>

### if

    if [ $1 == 'ls' ]
    then

    echo "repo nicknames"
    cat repoNam.txt
    echo ""
    echo "repo locations"
    cat repoDir.txt
    echo ""


<a id="orgce7ed09"></a>

### fi

    fi


<a id="org338517a"></a>

## git status part

Next thing is to collect the output of `git status` performed in every
single repo and display that collected info in just one message. The
info of that message should contain the repo location followed by the
actual output of that `git status` command performed in that repo. And
repeat for every repo location.

    yourRepo1/
    - changes not staged for commit
    - blah blah balh
    
    yourRepo1/
    - changes not staged for commit
    - blah blah balh


<a id="org468a84f"></a>

## git commit part

Here's when you need more flexibility. There are usually two
scenarios:

-   you want to commit everything at once, sharing the commit message.
-   you've made changes related to different things and you need
    different commit messages.

For the first option, the algorithm to commit should be the same as
the `git status` algorithm, except that now you have to input a commit
message shared for every repo.

For the second option, you just `cd` into every repo and `commit`
using your appropriate message, just as we've always done.


<a id="org038bb58"></a>

## git push part

Same idea for the commit part.


<a id="org3c5f646"></a>

## git pull part

Since I don't have the same repos across different machines, the
pulling is not the same process as committing and pushing. So for the
moment no implementation for pulling. But if I wanted, the algorithm
should be very much like the commit and push part.

