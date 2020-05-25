
# Table of Contents

1.  [sit: a simple suite for git](#org9bd8e8f)
        1.  [problem](#org3e284b3)
        2.  [current solution](#orge97cd26)
        3.  [wanted solution](#orgfe6f891)
        4.  [how to get there](#orgc17880b)
        5.  [test header](#orgddaef54)
        6.  [aoeuh tnao](#org9e1c742)
        7.  [aoeunt ae](#org7166132)



<a id="org9bd8e8f"></a>

# sit: a simple suite for git


<a id="org3e284b3"></a>

### problem

I type too much just to commit and push in sparse git repositories in
my machine.


<a id="orge97cd26"></a>

### current solution

I have to `cd` into every git repo, which by the way I have to remember
what are they and where are they and only then `git commit` and `git
push`. This workflow is a problem because:

-   I have to remember where are all these different repos
-   Since I have these repos scattered in multiple locations in
    multiple machines, it's very error prone
-   git submodules/subtree/subrepos are way too complex for what I need


<a id="orgfe6f891"></a>

### wanted solution

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


<a id="orgc17880b"></a>

### how to get there

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

1.  git status part

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

2.  git commit part

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

3.  git push part

    Since I don't have the same repos across different machines, the
    pulling is not the same process as committing and pushing. So for the
    moment no implementation for pushing. But if I wanted, the algorithm
    should be very much like the commit and push part.

4.  


<a id="orgddaef54"></a>

### test header

1.  testsaoeth


<a id="org9e1c742"></a>

### aoeuh tnao

1.  anstoeuhsatn oe


<a id="org7166132"></a>

### aoeunt ae

