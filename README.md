
# Table of Contents

1.  [sit: a simple suite for git](#org0dba135)
2.  [problem](#org5f9e1a1)
3.  [current solution](#org2a647f6)
4.  [wanted solution](#org6e919ee)
5.  [how to get there](#org3661b1b)
    1.  [git status part](#orgbb8271f)
    2.  [git commit part](#org69fdae9)
    3.  [git push part](#org0f4c8ea)
    4.  [](#org8ae018a)
6.  [test header](#org7f9e615)
    1.  [testsaoeth](#org92d47be)
7.  [aoeuh tnao](#orgfe16e04)
    1.  [anstoeuhsatn oe](#org0b39a1f)
8.  [aoeunt ae](#org9dfc3fd)



<a id="org0dba135"></a>

# sit: a simple suite for git


<a id="org5f9e1a1"></a>

# problem

I type too much just to commit and push in sparse git repositories in
my machine.


<a id="org2a647f6"></a>

# current solution

I have to `cd` into every git repo, which by the way I have to remember
what are they and where are they and only then `git commit` and `git
push`. This workflow is a problem because:

-   I have to remember where are all these different repos
-   Since I have these repos scattered in multiple locations in
    multiple machines, it's very error prone
-   git submodules/subtree/subrepos are way too complex for what I need


<a id="org6e919ee"></a>

# wanted solution

If I'm in the `$HOME` folder, then just `git status` right from the
`$HOME` directory only to be aware of the changes made to the
different present git repos.

Then, if I'm in the `$HOME` directory and `git commit` right from
there, I'd be committing every change to its corresponding git repo
with the same message. Very much as if I `cd` into every repo and `git
commit` right from each one manually; as already explained it's an
error prone and cumbersome way to do.

In the same way, I could `push` with one command or push from each
one, I want to have that flexibility also.


<a id="org3661b1b"></a>

# how to get there

Usually, I have to remember where are these repos located.

That can be solved using a simple array variable to store the
locations of the different git repos; the locations should always be
the same across machines and the same relative to the `$HOME`
directory.

    declare -A repositories

Then I have to add the locations of these git repos.

I could use something like "`sit add`". For the first time, it has to
be manually done. And as well, you should be able to add multiple
directories at once.

    sit-add(){
    repositories+=($1)
    }


<a id="orgbb8271f"></a>

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


<a id="org69fdae9"></a>

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


<a id="org0f4c8ea"></a>

## git push part

Since I don't have the same repos across different machines, the
pulling is not the same process as committing and pushing. So for the
moment no implementation for pushing. But if I wanted, the algorithm
should be very much like the commit and push part.


<a id="org8ae018a"></a>

## 


<a id="org7f9e615"></a>

# test header


<a id="org92d47be"></a>

## testsaoeth


<a id="orgfe16e04"></a>

# aoeuh tnao


<a id="org0b39a1f"></a>

## anstoeuhsatn oe


<a id="org9dfc3fd"></a>

# aoeunt ae

