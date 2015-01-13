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

## Generating the site, viewing changes locally

1. In the root of the site run `nanoc` to generate the current site. It generates to the "output" dir.
2. Run `guard` in the root directory to spin up a web server on localhost (changes to content will be visible by refreshing the page).

## Pushing the site live

cd to the output dir, commit the changes and push to github.

## Guide to setting up a meeting

1. Create the meetup page in the site (pages/). Use an existing page as a template.
2. Generate the site to the output dir and push live
3. Tweet about it using the @mango_users twitter account. See @wjessop if you need the creds.
4. Anounce to the mailing list. Details on the site.
