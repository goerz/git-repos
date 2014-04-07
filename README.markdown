# git-repos

[http://github.com/goerz/git-repos](http://github.com/goerz/git-repos)

Author: [Michael Goerz](http://michaelgoerz.net)

This code is licensed under the [GPL](http://www.gnu.org/licenses/gpl.html)

The purpose of the `git repos` script is to give you an overview of all the git
repositories on your hard drive. Specifically, it will show you which
repositories have local modifications, are out of sync with their remote,
unmerged branches, or stashes. The output is colored to highlight such
potential problems.

Since it can take a while to traverse your entire disk searching for git
repositories, the script prefers to read a list of all available repositories
from a file, `~/.gitrepos` by default. You may build this list by using the
`--build-repolist` option. Alternatively, you could run cron jobs that do
something like the following:

    /usr/bin/find $HOME -type d -name .git | /usr/bin/sed 's/\/\.git$//' > $HOME/.gitrepos

Note that `git-repos` will not look for bare repositories.

## Install ##

Store the script anywhere in your `$PATH`

## Dependencies ##

* The script depends only on the [git][1] executable, which must be in your
  PATH. It has been tested against git version 1.8.3.4, but it should also work
  with moderately older and all newer versions. If it doesn't, let me know.

[1]: http://git-scm.com/

## Usage ##

    Usage: git-repos [OPTIONS] [PATH]

    Show a summary for each repo listed in the file REPOLIST.  If the PATH
    argument is given, only print those repos out of REPOLIST that are subfolders
    of PATH. If the REPOLIST file does not exists, find all repos that are
    subfolders of PATH.

    Options:
    -h, --help            show this help message and exit
    --no-color            Do not use color in output
    --fetch               Perform a fetch on each repository
    --status              Run 'git status' on unclean repositories
    --all                 Report about all found git repos. By default, only
                            repos that are not clean, have stashes, local unmerged
                            branches, or are out of sync, are reported
    --remote              Disregard all repos that do not have least one remote
                            defined
    --local               Disregard all repos that have any remote defined
    --repolist=REPOLIST   Textfile that contains the path of all your git
                            repositories Defaults to /Volumes/HOME/goerz/.gitrepos
    --build-repolist      Overwrite the REPOLIST (see --repolist option) with a
                            list of all git repos that are subfolders of PATH.
                            Exit after the repolist has been written. This might
                            take a long time.
    --verbosity=VERBOSITY
                            In combination with --build-repolist, print progress
                            information. VERBOSITY > 0 causes all found repos to
                            be printed to screen as they are found. VERBOSITY > 1
                            causes all traversed directories to be printed to
                            screen.
    --append              In combination with --build-repolist, append to
                            REPOLIST instead of overwriting it.