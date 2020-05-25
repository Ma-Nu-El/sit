
# Table of Contents

1.  [sit: a simple repo manager for git](#org0e82d48)
2.  [problem](#orgefe8de7)
3.  [current solution](#orgd34d49b)
4.  [wanted solution](#orgcaed530)
5.  [how to get there](#orge23d6cd)
    1.  [git status part](#org7bb8512)
    2.  [git commit part](#orgd4c7ab8)
    3.  [git push part](#org206b087)
    4.  [git pull part](#org4a7faed)



<a id="org0e82d48"></a>

# sit: a simple repo manager for git

The source code for the Markdown and the actual executable file is the
`.org` file itself. I just *tangle* the `sit` file and *export* to
Markdown using *Orgmode's* `C-c C-e m m`.


<a id="orgefe8de7"></a>

# problem

I type too much just to commit and push in different git repositories
in my machine.


<a id="orgd34d49b"></a>

# current solution

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


<a id="orgcaed530"></a>

# wanted solution

If I'm in the `$HOME` folder, then just `git status` right from the
`$HOME` directory only to be aware of the changes made to the
different present git repos.

I'd be committing every change to its corresponding git repo with the
same message. Very much as if I `cd` into every repo and `git
commit` right from each one manually; as already explained it's an
error prone and cumbersome way to do.

In the same way, I could `push` with one command or push from each
one, I want to have that flexibility also.


<a id="orge23d6cd"></a>

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


<a id="org7bb8512"></a>

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


<a id="orgd4c7ab8"></a>

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


<a id="org206b087"></a>

## git push part

Same idea for the commit part.


<a id="org4a7faed"></a>

## git pull part

Since I don't have the same repos across different machines, the
pulling is not the same process as committing and pushing. So for the
moment no implementation for pushing. But if I wanted, the algorithm
should be very much like the commit and push part.

