# The ManGo website

Github compatible nanoc site generated using a modified form of [these instructions](http://schmurfy.github.io/2011/05/06/create_your_github_user_page_with_nanoc.html). To get set up something like this should work:


    $ git clone git@github.com:wjessop/mango.computer.git
    $ cd mango.computer
    $ rm -rf output
    $ git clone git@github.com:wjessop/mango.computer.git output
    $ cd output
    $ git symbolic-ref HEAD refs/heads/gh-pages
    $ rm .git/index
    $ git clean -fdx

You can then run nanoc in the root dir then commit and push to master in the root, and the gh-pages branch in the output dir.
