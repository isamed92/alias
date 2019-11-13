# -*- mode: gitconfig; -*-
# vim: set filetype=gitconfig:
##
# GitAlias.com file of many git alias items, including shortcuts, helpers, workflows, etc.
#
#
# ## Usage
#
# Typical usage for a typical user:
#
#   * Save this file as a dot file in your home directory: `~/.gitalias.txt`
#
#   * Edit your git config dot file in your home directory such as  `~/.gitconfig`
#
#   * Include the path to this file.
#
# Example file `~/.gitconfig` with an entry to include the file `~/.gitalias.txt`:
#
#     [include]
#       path = gitalias.txt
#
#
# ## Usage for older git versions
#
# If you use an older version of git that does not have git config "include" capability,
# or if you prefer more control, then you can simply copy/paste anything you like from
# this file to your own git config file.
#
#
# ## Customization
#
# If you want to use this file, and also want to change some of the items,
# then one way is to use your git config file to include this gitalias file,
# and also define your own alias items; a later alias takes precedence.
#
# Example file `~/.gitconfig` item to include the file `~/.gitalias.txt`:
#
#     [include]
#       path = ~/.gitconfig.d/gitalias.txt
#     [alias]
#       l = log --graph --oneline
#
#
# ## Links
#
#   * [GitAlias.com website](http://gitlias.com)
#   * [GitAlias GitHub](https://github.com/gitalias)
#   * [Git Basics - Git Aliases](https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases)
#   * [Git Basics - Tips and Tricks](https://git-scm.com/book/en/v1/Git-Basics-Tips-and-Tricks)
#
# ## Tracking
#
#   * Package: gitalias
#   * Version: 21.5.0
#   * Created: 2016-06-17
#   * Updated: 2019-09-04
#   * License: GPL
#   * Contact: Joel Parker Henderson (joel@joelparkerhenderson.com)
##

[alias]

  ##
  # One letter alias for our most frequent commands.
  #
  # Guidelines: these aliases do not use options, because we want
  # these aliases to be easy to compose and use in many ways.
  ##

  a = add
  b = branch
  c = commit
  d = diff
  f = fetch
  g = grep
  l = log
  m = merge
  o = checkout
  p = pull
  r = remote
  s = status
  w = whatchanged

  ##
  # Short aliases for our frequent commands.
  #
  # Guidelines:
  #
  #  * Generally speaking, the alias should be in the same
  #    order as the command name followed by its options.
  #
  #    * Right: fb = foo --bar
  #    * Wrong: bf = foo --bar
  ##

  ### add ###

  # add all
  aa = add --all

  # add by patch - looks at each change, and asks if we want to put it in the repo.
  ap = add --patch

  # add just the files that are updated.
  au = add --update

  ### branch ###

  # branch - edit the description
  be = branch --edit-description

  # branch and only list branches whose tips are reachable from the specified commit (HEAD if not specified).
  bm = branch --merged

  # branch and only list branches whose tips are not reachable from the specified commit (HEAD if not specified).
  bnm = branch --no-merged

  ### commit ###

  # commit - amend the tip of the current branch rather than creating a new commit.
  ca = commit --amend

  # commit - amend the tip of the current branch, and edit the message.
  cam = commit --amend --message

  # commit - amend the tip of the current branch, and do not edit the message.
  cane = commit --amend --no-edit

  # commit interactive
  ci = commit --interactive

  # commit with a message
  cm = commit --message

  ### checkout ###

  # checkout - update the working tree to match a branch or paths. [same as "o" for "out"]
  co = checkout

  ### cherry-pick ###

  # cherry-pick - apply the changes introduced by some existing commits; useful for moving small chunks of code between branches.
  cp = cherry-pick

  # cherry-pick - abort the picking process
  cpa = cherry-pick --abort

  # cherry-pick - continue the picking process
  cpc = cherry-pick --continue

  # cherry-pick without making a commit, and when when recording the commit, append a line that says "(cherry picked from commit ...)"
  cp-nx = cherry-pick --no-commit -x

  ### diff ###

  # diff - show changes not yet staged
  dc = diff --cached

  # diff - show changes about to be commited
  ds = diff --staged

  # diff - show changes but by word, not line
  dw = diff --word-diff

  # diff deep - show changes with our preferred options. Also aliased as `diff-deep`.
  dd = diff --check --dirstat --find-copies --find-renames --histogram --color

  ### clean ###

  # clean everything to be pristine
  cleanest = clean -ffdx

  ### grep ###

  # grep i.e. search for text
  g = grep

  # grep - show line number
  gl = grep --line-number

  # grep group - search with our preferred options. Also aliased as `grep-group`.
  gg = grep --break --heading --line-number --color

  ### log ###

  # log with a text-based graphical representation of the commit history.
  lg = log --graph

  # log with one line per item.
  lo = log --oneline

  # log with patch generation.
  lp = log --patch

  # log with first parent, useful for team branch that only accepts pull requests
  lfp = log --first-parent

  # log with items appearing in topological order, i.e. descendant commits are shown before their parents.
  lt = log --topo-order

  # log like - we like this summarization our key performance indicators. Also aliased as `log-like`.
  ll = log --graph --topo-order --date=short --abbrev-commit --decorate --all --boundary --pretty=format:'%Cgreen%ad %Cred%h%Creset -%C(yellow)%d%Creset %s %Cblue[%cn]%Creset %Cblue%G?%Creset'

  # log like long  - we like this summarization our key performance indicators. Also aliased as `log-like-long`.
  lll = log --graph --topo-order --date=iso8601-strict --no-abbrev-commit --abbrev=40 --decorate --all --boundary --pretty=format:'%Cgreen%ad %Cred%h%Creset -%C(yellow)%d%Creset %s %Cblue[%cn <%ce>]%Creset %Cblue%G?%Creset'

  ## ls-files ##

  # ls-files - show information about files in the index and the working tree; like Unix "ls" command.
  ls = ls-files

  # ls-ignored -  list files that git has ignored.
  ls-ignored = ls-files --others --i --exclude-standard

  ### merge ###

  # merge but without autocommit, and with a commit even if the merge resolved as a fast-forward.
  me = merge --no-commit --no-ff

  ### pull ###

  # pull if a merge can be resolved as a fast-forward, otherwise fail.
  pf = pull --ff-only

  # pull with rebase - to provide a cleaner, linear, bisectable history.
  #
  # To automatically do "pull --rebase" everywhere:
  #
  #     git config --global pull.rebase true
  #
  # To automatically do "pull --rebase" for any branch based on master:
  #
  #    git config branch.master.rebase true
  #
  # To automatically do "pull --rebase" for any newly-created branches:
  #
  #     git config --global branch.autosetuprebase always
  #
  # To integrate changes between branches, you can merge or rebase.
  #
  # When we use "git pull", git does a fetch then a merge.
  # If we've made changes locally and someone else has pushed changes
  # to our git host then git will automatically merge these together
  # and create a merge commit that looks like this in the history:
  #
  #    12345678 - Merge branch 'foo' of bar into master
  #
  # When we use "git pull --rebase", git does a fetch then a rebase.
  # A rebase resets the HEAD of your local branch to be the same as
  # the remote HEAD, then replays your local commits back into repo.
  # This means you don't get any noisy merge messages in your history.
  # This gives us a linear history, and also helps with git bisect.
  #
  pr = pull --rebase

  # pp - pull with rebase preserve of merge commits
  #
  # See https://stackoverflow.com/questions/21364636/git-pull-rebase-preserve-merges
  #
  # You should only rebase if you know (in a sort of general sense)
  # what you are doing, and if you do know what you are doing, then you
  # would probably prefer a merge-preserving rebase as a general rule.
  #
  # Although by the time you've decided that rebasing is a good idea,
  # you will probably find that a history that has its own embedded
  # branch-and-merge-points is not necessarily the correct "final
  # rewritten history".
  #
  # That is, if it's appropriate to do a rebase at all, it's at least fairly
  # likely that the history to be rebased is itself linear, so that the
  # preserve-vs-flatten question is moot anyway.
  #
  # See https://stackoverflow.com/questions/38269092/is-it-possible-to-put-preserve-merges-in-the-gitconfig
  #
  # While preserving merges is probably generally superior, in at least a 
  # few ways, to discarding them when rebasing, the fact is that rebase 
  # cannot preserve them. The only thing it can do, once some commits 
  # have been copied to new commits, is re-perform them. This can have new
  # and/or different merge conflicts, vs the last time the merge was done. 
  # You should also pay close attention to the restrictions on merge 
  # preservation in the git rebase documentation.
  #
  # Without getting into a lot of detail, it always seems to me that most
  # commit graph subsets that "should be" rebased, rarely have any 
  # internal merges. If such a graph subset has a single final merge, you
  # can simply strip away that merge (with git reset) before rebasing, 
  # and re-do that single merge manually at the end. (In fact, git rebase 
  # normally drops merge commits entirely, so you don't have to run the git
  # reset itself in some cases. The one where you do have to run it is when
  # the merge is into the branch onto which you intend to rebase. This is 
  # where git pull actually does the right thing when it uses 
  # `git rebase -p`, except that it fails to check for, and warn about, 
  # internal merges, which are sort of warning signs that rebasing might 
  # not be a good idea.
  #
  pp = pull --rebase=preserve

  ### rebase ###

  # rebase - forward-port local commits to the updated upstream head.
  rb = rebase

  # rebase abort - cancel the rebasing process
  rba = rebase --abort

  # rebase - continue the rebasing process after resolving a conflict manually and updating the index with the resolution.
  rbc = rebase --continue

  # rebase - restart the rebasing process by skipping the current patch.
  rbs = rebase --skip

  # rbi - rebase interactive on our unpushed commits.
  #
  # Before we push our local changes, we may want to do some cleanup,
  # to improve our commit messages or squash related commits together.
  #
  # Let's say I've pushed two commits that are related to a new feature and
  # I have another where I made a spelling mistake in the commit message.
  # When I run "git rbi" I get dropped into my editor with this:
  #
  #     pick 7f06d36 foo
  #     pick ad544d0 goo
  #     pick de3083a hoo
  #
  # Let's say I want to squash the "foo" and "goo" commits together,
  # and also change "hoo" to say "whatever". To do these, I change "pick"
  # to say "s" for squash; this tells git to squash the two together;
  # I also edit "hoo" to rename it to "whatever". I make the file look like:
  #
  #     pick 7f06d36 foo
  #     s ad544d0 goo
  #     r de3083a whatever
  #
  # This gives me two new commit messages to edit, which I update.
  # Now when I push the remote repo host receives two commits
  #
  #     3400455 - foo
  #     5dae0a0 - whatever
  #
  rbi = rebase --interactive @{upstream}

  # See https://blog.filippo.io/git-fixup-amending-an-older-commit/
  # This is a slightly modified version
  fixup = "!f() { TARGET=$(git rev-parse \"$1\"); git commit --fixup=$TARGET && GIT_EDITOR=true git rebase --interactive --autosquash $TARGET~; }; f"

  ### reflog ###

  # reflog - reference log that manages when tips of branches are updated.
  rl = reflog

  ### remote ###

  # remote - manage set of tracked repositories [same as "r"].
  rr = remote

  # remote show - gives some information about the remote <name>.
  rrs = remote show

  # remote update - fetch updates for a named set of remotes in the repository as defined by remotes.
  rru = remote update

  # remote prune - deletes all stale remote-tracking branches under <name>.
  rrp = remote prune

  incoming = !git remote update --prune; git log ..@{upstream}
  outgoing = log @{upstream}..

  # Push to all remotes
  push-to-all-remotes = !git remote | xargs -I% -n1 git push %

  ### revert ###

  # revert - undo the changes from some existing commits
  rv = revert

  # revert without autocommit; useful when you're reverting more than one commits' effect to your index in a row.
  rvnc = revert --no-commit

  ### show-branch ###

  # show-branch - print a list of branches and their commits.
  sb = show-branch

  ### submodule ###

  # submodule - enables foreign repositories to be embedded within a dedicated subdirectory of the source tree.
  sm = submodule

  # submodule init
  smi = submodule init

  # submodule add
  sma = submodule add

  # submodule sync
  sms = submodule sync

  # submodule update
  smu = submodule update

  # submodule update with initialize
  smui = submodule update --init

  # submodule update with initialize and recursive; this is useful to bring a submodule fully up to date.
  smuir = submodule update --init --recursive

  ### status ###

  # status with short format instead of full details
  ss = status --short

  # status with short format and showing branch and tracking info.
  ssb = status --short --branch

  ### ALIAS MANAGEMENT ###

  # Show our defined alias list
  aliases = "!git config --get-regexp '^alias\\.' | cut -c 7- | sed 's/ / = /'"

  add-alias = "!f() { [ $# = 3 ] && git config $1 alias.\"$2\" \"$3\" && return 0 || echo \"Usage: git add-(local|global)-alias <new alias> <original command>\" >&2 && return 1; }; f"
  add-global-alias = "!git add-alias --global"
  add-local-alias = "!git add-alias --local"

  # Rename an alias
  rename-alias = "!f() { [ $# = 3 ] && [ $2 != $3 ] && [ ! -z \"$(git config $1 --get alias.$2)\" ] && [ -z \"$(git config $1 --get alias.$3)\" ] && git config $1 alias.$3 \"$(git config $1 --get alias.$2)\" && git config $1 --unset alias.$2 && return 0 || echo \"Usage: git rename-(local|global)-alias <alias existing name> <new alias name>\nThe alias you are going to rename must exist and new name must not exist.\" >&2 && return 1; };f"
  rename-global-alias = "!git rename-alias --global"
  rename-local-alias = "!git rename-alias --local"

  # Last tag in the current branch
  lasttag = describe --tags --abbrev=0

  # Latest annotated tag in all branches
  lasttagged = !git describe --tags `git rev-list --tags --max-count=1`

  # From https://gist.github.com/492227
  head = log -n1
  heads = !"git log origin/master.. --format='%Cred%h%Creset;%C(yellow)%an%Creset;%H;%Cblue%f%Creset' | git name-rev --stdin --always --name-only | column -t -s';'"
  lost = !"git fsck | awk '/dangling commit/ {print $3}' | git show --format='SHA1: %C(yellow)%h%Creset %f' --stdin | awk '/SHA1/ {sub(\"SHA1: \", \"\"); print}'"

  ### diff-* ###

  diff-all = !"for name in $(git diff --name-only $1); do git difftool $1 $name & done"
  diff-changes = diff --name-status -r
  diff-stat = diff --stat --ignore-space-change -r
  diff-staged = diff --cached

  # Diff using our preferred options. A.k.a. `dd`.
  diff-deep = diff --check --dirstat --find-copies --find-renames --histogram --color

  ### grep-* ###

  # Find text in any commit ever.
  grep-all = !"f() { git rev-list --all | xargs git grep \"$@\"; }; f"

  # Find text and group the output lines. A.k.a. `gg`.
  grep-group = grep --break --heading --line-number --color

  # grep with ack-like formatting
  grep-ack = \
    -c color.grep.linenumber=\"bold yellow\" \
    -c color.grep.filename=\"bold green\" \
    -c color.grep.match=\"reverse yellow\" \
    grep --break --heading --line-number

  ### init ###

  # initalize a repo and immediate add an empty commit, which makes rebase easier.
  init-empty = !"f() { git init && git commit --allow-empty --allow-empty-message --message ''; }; f"

  ### merge-* ###

  # Given a merge commit, find the span of commits that exist(ed).
  # Not so useful in itself, but used by other aliases.
  # Thanks to Rob Miller for the merge-span-* aliaes.
  merge-span = !"f() { echo $(git log -1 $2 --merges --pretty=format:%P | cut -d' ' -f1)$1$(git log -1 $2 --merges --pretty=format:%P | cut -d' ' -f2); }; f"

  # Find the commits that were introduced by a merge
  merge-span-log = "!git log `git merge-span .. $1`"

  # Show the changes that were introduced by a merge
  merge-span-diff = !"git diff `git merge-span ... $1`"

  # Show the changes that were introduced by a merge, in your difftool
  merge-span-difftool = !"git difftool `git merge-span ... $1`"

  # Interactively rebase all the commits on the current branch
  rebase-branch = !"git rebase --interactive `git merge-base master HEAD`"

  # Sort by date for branches; can be useful for spring cleaning
  refs-by-date = for-each-ref --sort=-committerdate --format='%(committerdate:short) %(refname:short)'

  # Find all objects that aren't referenced by any other object (orphans).
  # To help an orphan, we create a new branch with the orphan's commit hash,
  # then merge it into our current branch:
  #
  #    git branch foo <commit>
  #    git merge foo
  #
  orphans = fsck --full

  # List all blobs by size in bytes.
  # By [CodeGnome](http://www.codegnome.com/)
  rev-list-all-objects-sort-by-size = !"git rev-list --all --objects  | awk '{print $1}'| git cat-file --batch-check | fgrep blob | sort -k3nr"


  ### LOG ALIASES ###

  # Show log of changes, most recent first
  log-changes = log --oneline --reverse

  # Show log of new commits after you fetched, with stats, excluding merges
  log-fresh = log ORIG_HEAD.. --stat --no-merges

  # Show log in our preferred format for our key performance indicators. A.k.a. `ll`.
  log-like = log --graph --topo-order --date=short --abbrev-commit --decorate --all --boundary --pretty=format:'%Cgreen%ad %Cred%h%Creset -%C(yellow)%d%Creset %s %Cblue[%cn]%Creset %Cblue%G?%Creset'

  # Show log in our preferred format for our key performance indicators, with long items. A.k.a. `lll`.
  log-like-long = log --graph --topo-order --date=iso8601-strict --no-abbrev-commit --decorate --all --boundary --pretty=format:'%Cgreen%ad %Cred%h%Creset -%C(yellow)%d%Creset %s %Cblue[%cn <%ce>]%Creset %Cblue%G?%Creset'

  # Show log with dates in our local timezone
  log-local = log --date=local

  # Show the log for my own commits by my own user email
  log-my = !git log --author $(git config user.email)

  # Show log as a graph
  log-graph = log --graph --all --oneline --decorate

  # Show the date of the earliest commit, in strict ISO 8601 format
  log-first-date = !"git log --date-order --format=%cI | tail -1"

  # Show the date of the latest commit, in strict ISO 8601 format
  log-latest-date = log -1 --date-order --format=%cI

  # Show the log of the recent hour, day, week, month, year
  log-hour  = log --since "1 hour ago"
  log-day   = log --since "1 day ago"
  log-week  = log --since "1 week ago"
  log-month = log --since "1 month ago"
  log-year  = log --since "1 year ago"

  # Show the log of my own recent hour, day, week, month, year
  log-my-hour  = log --author $(git config user.email) --since "1 hour ago"
  log-my-day   = log --author $(git config user.email) --since "1 day ago"
  log-my-week  = log --author $(git config user.email) --since "1 week ago"
  log-my-month = log --author $(git config user.email) --since "1 month ago"
  log-my-year  = log --author $(git config user.email) --since "1 year ago"

  # Show a specific format string and its number of log entries
  log-of-format-and-count = "!f() { format=\"$1\"; shift; git log $@ --format=oneline --format="$format" | awk '{a[$0]++}END{for(i in a){print i, a[i], int((a[i]/NR)*100) \"%\"}}' | sort; }; f"
  log-of-count-and-format = "!f() { format=\"$1\"; shift; git log $@ --format=oneline --format="$format" | awk '{a[$0]++}END{for(i in a){print a[i], int((a[i]/NR)*100) \"%\", i}}' | sort -nr; }; f"

  # Show the number of log entries by a specific format string and date format string
  log-of-format-and-count-with-date = "!f() { format=\"$1\"; shift; date_format=\"$1\"; shift; git log $@ --format=oneline --format=\"$format\" --date=format:\"$date_format\" | awk '{a[$0]++}END{for(i in a){print i, a[i], int((a[i]/NR)*100) \"%\"}}' | sort -r; }; f"
  log-of-count-and-format-with-date = "!f() { format=\"$1\"; shift; date_format=\"$1\"; shift; git log $@ --format=oneline --format=\"$format\" --date=format:\"$date_format\" | awk '{a[$0]++}END{for(i in a){print a[i], int((a[i]/NR)*100) \"%\", i}}' | sort -nr; }; f"

  # Show the number of log items by email
  log-of-email-and-count         = "!f() { git log-of-format-and-count \"%aE\" $@; }; f"
  log-of-count-and-email         = "!f() { git log-of-count-and-format \"%aE\" $@; }; f"

  # Show the number of log items by hour
  log-of-hour-and-count          = "!f() { git log-of-format-and-count-with-date \"%ad\" \"%Y-%m-%dT%H\" $@ ; }; f"
  log-of-count-and-hour          = "!f() { git log-of-count-and-format-with-date \"%ad\" \"%Y-%m-%dT%H\" $@ ; }; f"

  # Show the number of log items by day
  log-of-day-and-count           = "!f() { git log-of-format-and-count-with-date \"%ad\" \"%Y-%m-%d\" $@ ; }; f"
  log-of-count-and-day           = "!f() { git log-of-count-and-format-with-date \"%ad\" \"%Y-%m-%d\" $@ ; }; f"

  # Show the number of log items by week
  log-of-week-and-count          = "!f() { git log-of-format-and-count-with-date \"%ad\" \"%Y#%V\" $@; }; f"
  log-of-count-and-week          = "!f() { git log-of-count-and-format-with-date \"%ad\" \"%Y#%V\" $@; }; f"

  # Show the number of log items by month
  log-of-month-and-count         = "!f() { git log-of-format-and-count-with-date \"%ad\" \"%Y-%m\" $@ ; }; f"
  log-of-count-and-month         = "!f() { git log-of-count-and-format-with-date \"%ad\" \"%Y-%m\" $@ ; }; f"

  # Show the number of log items by year
  log-of-year-and-count          = "!f() { git log-of-format-and-count-with-date \"%ad\" \"%Y\" $@ ; }; f"
  log-of-count-and-year          = "!f() { git log-of-count-and-format-with-date \"%ad\" \"%Y\" $@ ; }; f"

  # Show the number of log items by hour of day
  log-of-hour-of-day-and-count   = "!f() { git log-of-format-and-count-with-date \"%ad\" \"%H\" $@; }; f"
  log-of-count-and-hour-of-day   = "!f() { git log-of-count-and-format-with-date \"%ad\" \"%H\" $@; }; f"

  # Show the number of log items by day of week
  log-of-day-of-week-and-count   = "!f() { git log-of-format-and-count-with-date \"%ad\" \"%u\" $@; }; f"
  log-of-count-and-day-of-week   = "!f() { git log-of-count-and-format-with-date \"%ad\" \"%u\" $@; }; f"

  # Show the number of log items by week of year
  log-of-week-of-year-and-count  = "!f() { git log-of-format-and-count-with-date \"%ad\" \"%V\" $@; }; f"
  log-of-count-and-week-of-year  = "!f() { git log-of-count-and-format-with-date \"%ad\" \"%V\" $@; }; f"

  # TODO
  log-refs = log --all --graph --decorate --oneline --simplify-by-decoration --no-merges
  log-timeline = log --format='%h %an %ar - %s'
  log-local = log --oneline origin..HEAD
  log-fetched = log --oneline HEAD..origin/master

  # chart: show a summary chart of activity per author.
  #
  # Example:
  #
  #     $ git chart
  #     ..X..........X...2..12 alice@example.com
  #     ....2..2..13.......... bob@example.com
  #     2.....1....11......... carol@example.com
  #     ..1............1..1... david@example.com
  #     ....1.......1.3.3.22.2 eve@example.com
  #
  # The chart rows are the authors.
  # TODO: sort the rows meaningfully,
  # such as alphabetically, or by count.
  #
  # The chart columns are the days.
  # The chart column prints one character per day.
  #
  #   * For 1-9 commits, show the number.
  #   * For 10 or more commits, show "X" as a visual indicator.
  #   * For no commits, show "." as a visual placeholder.
  #
  # The chart timeline adjusts the date range automatically:
  #
  #   * The timeline starts with the date of the earliest commit.
  #   * The timeline stops with the date of the latest commit.
  #   * The intent is to show the most relevant information.
  #
  chart = "!f() { \
    git log --format=oneline --format=\"%aE %at\" --since=\"48 days ago\" $@ | \
    awk ' \
    function time_to_slot(t) { return strftime(\"%Y-%m-%d\", t, true) } \
    function count_to_char(i) { return (i > 0) ? ((i < 10) ? i : \"X\") : \".\" } \
    BEGIN { \
      time_min = systime(); time_max = 0; \
      SECONDS_PER_DAY=86400; \
    } \
    { \
      item = $1; \
      time = 0 + $2; \
      if (time > time_max){ time_max = time } else if (time < time_min){ time_min = time }; \
      slot = time_to_slot(time); \
      items[item]++; \
      slots[slot]++; \
      views[item, slot]++; \
    } \
    END{ \
      printf(\"Chart time range %s to %s.\\n\", time_to_slot(time_min), time_to_slot(time_max)); \
      time_max_add = time_max += SECONDS_PER_DAY; \
      for(item in items){ \
        row = \"\"; \
        for(time = time_min; time < time_max_add; time += SECONDS_PER_DAY) { \
          slot = time_to_slot(time); \
          count = views[item, slot]; \
          row = row count_to_char(count); \
        } \
        print row, item; \
      } \
    }'; \
  }; f"

  # churn: show log of files that have many changes
  #
  #   * Written by (Corey Haines)[http://coreyhaines.com/]
  #   * Scriptified by Gary Bernhardt
  #   * Obtained from https://github.com/garybernhardt/dotfiles/blob/master/bin/git-churn
  #   * Edited for GitAlias.com repo by Joel Parker Henderson
  #   * Comments by Mislav http://mislav.uniqpath.com/2014/02/hidden-documentation/
  #
  # Show churn for whole repo:
  #
  #   $ git churn
  #
  # Show churn for specific directories:
  #
  #   $ git churn app lib
  #
  # Show churn for a time range:
  #
  #   $ git churn --since='1 month ago'
  #
  # These are all standard arguments to `git log`.
  #
  # It's possible to get valuable insight from history of a project not only
  # by viewing individual commits, but by analyzing sets of changes as a whole.
  # For instance, `git churn` compiles stats about which files change the most.
  #
  # For example, to see where work on an app was focused on in the past month:
  #
  #     $ git churn --since='1 month ago' app/ | tail
  #
  # This can also highlight potential problems with technical debt in a project.
  # A specific file changing too often is generally a red flag, since it probably
  # means the file either needed to be frequently fixed for bugs, or the file
  # holds too much responsibility and should be split into smaller units.
  #
  # Similar methods of history analysis can be employed to see which people were
  # responsible recently for development of a certain part of the codebase.
  #
  # For instance, to see who contributed most to the API part of an application:
  #
  #    $ git log --format='%an' --since='1 month ago' app/controllers/api/ | \
  #      sort | uniq -c | sort -rn | head
  #
  #    109 Alice Anderson
  #    13 Bob Brown
  #    7 Carol Clark
  #
  churn = !"f() { git log --all --find-copies --find-renames --name-only --format='format:' \"$@\" | awk 'NF{a[$0]++}END{for(i in a){print a[i], i}}' | sort -rn;};f"


  # summary: print a helpful summary of some typical metrics
  summary = "!f() { \
    printf \"Summary of this branch...\n\"; \
    printf \"%s\n\" $(git rev-parse --abbrev-ref HEAD); \
    printf \"%s first commit timestamp\n\" $(git log --date-order --format=%cI | tail -1); \
    printf \"%s latest commit timestamp\n\" $(git log -1 --date-order --format=%cI); \
    printf \"%d commit count\n\" $(git rev-list --count HEAD); \
    printf \"%d date count\n\" $(git log --format=oneline --format=\"%ad\" --date=format:\"%Y-%m-%d\" | awk '{a[$0]=1}END{for(i in a){n++;} print n}'); \
    printf \"%d tag count\n\" $(git tag | wc -l); \
    printf \"%d author count\n\" $(git log --format=oneline --format=\"%aE\" | awk '{a[$0]=1}END{for(i in a){n++;} print n}'); \
    printf \"%d committer count\n\" $(git log --format=oneline --format=\"%cE\" | awk '{a[$0]=1}END{for(i in a){n++;} print n}'); \
    printf \"%d local branch count\n\" $(git branch | grep -v \" -> \" | wc -l); \
    printf \"%d remote branch count\n\" $(git branch -r | grep -v \" -> \" | wc -l); \
    printf \"\nSummary of this directory...\n\"; \
    printf \"%s\n\" $(pwd); \
    printf \"%d file count via git ls-files\n\" $(git ls-files | wc -l); \
    printf \"%d file count via find command\n\" $(find . | wc -l); \
    printf \"%d disk usage\n\" $(du -s | awk '{print $1}'); \
    printf \"\nMost-active authors, with commit count and %%...\n\"; git log-of-count-and-email | head -7; \
    printf \"\nMost-active dates, with commit count and %%...\n\"; git log-of-count-and-day | head -7; \
    printf \"\nMost-active files, with churn count\n\"; git churn | head -7; \
  }; f"

  ### LOOKUP ALIASES ###

  # whois: given a string for an author, try to figure out full name and email:
  whois = "!sh -c 'git log --regexp-ignore-case -1 --pretty=\"format:%an <%ae>\n\" --author=\"$1\"' -"

  # Given any git object, try to show it briefly
  whatis = show --no-patch --pretty='tformat:%h (%s, %ad)' --date=short

  # Show who contributed with summarized changes
  who = shortlog --summary --

  # Show who contributed, in descending order by number of commits
  whorank = shortlog --summary --numbered --no-merges

  # List all issues mentioned in commit messages between range of commits
  #
  # Replace `\\\"ISSUE-[0-9]\\+\\\"` regular expression with one matching your issue tracking system.
  # For Jira it should be as simple as putting your project name in place of `ISSUE`.
  #
  # Best used with tags:
  #  $ git issues v1.0..v1.1
  #
  # But will work with any valid commit range:
  #  $ git issues master..HEAD

  issues = !sh -c \"git log $1 --oneline | grep -o \\\"ISSUE-[0-9]\\+\\\" | sort -u\"

  # Show the commit's parents
  commit-parents = !"f(){ git cat-file -p \"${*:-HEAD}\" | sed -n '/0/,/^ *$/{/^parent /p}'; };f"

  # Is the commit a merge commit? If yes exit 0, else exit 1
  commit-is-merge = !"f(){ [ -n \"$(git commit-parents \"$*\" | sed '0,/^parent /d')\" ];};f"

  # Show the commit's keyword-marked lines.
  #
  # Show each line in the commit message that starts with zero or more blanks,
  # then a keyword (alphanum and dash characters), then a colon.
  #
  # Example commit:
  #
  #     commit ce505d161fccdbc8d4bf12047846de7433ad6d04
  #     Author: Joel Parker Henderson <joel@joelparkerhenderson.com>
  #     Date:   Tue May 28 11:53:47 2019 -0700
  #
  #         Add feature foo
  #
  #         This commit is to add feature foo.
  #
  #         Time: 5 hours
  #         Cost: 600 USD
  #
  # Command:
  #
  #     $ git commit-message-key-lines ce505d161fccdbc8d4bf12047846de7433ad6d04
  #     Commit: ce505d161fccdbc8d4bf12047846de7433ad6d04
  #     Author: Joel Parker Henderson <joel@joelparkerhenderson.com>
  #     Date: Tue May 28 11:53:47 2019 -0700
  #     Time: 5 hours
  #     Cost: 600 USD
  #
  # Normalize the output:
  #
  #   * Start the output with "Commit: <commit>"
  #
  #   * Omit leading blanks
  #
  #   * After the colon, use one space (not tab, not multiple spaces, etc.)
  #
  # Known issues:
  #
  #   * TODO: improve the keyword matcher so it requires the keyword to end
  #     in an alphanum (not a dash), and also so the dash is a separator i.e.
  #     the matcher does not accept a dash followed by another dash.
  #
  commit-message-key-lines = "!f(){ echo \"Commit: $1\"; git log \"$1\" --format=fuller | grep \"^[[:blank:]]*[[:alnum:]][-[:alnum:]]*:\" | sed \"s/^[[:blank:]]*//; s/:[[:blank:]]*/: /\"; }; f"


  ### WORKFLOW ALIASES ###

  # Clone a git repository including all submodules
  cloner = clone --recursive

  # Stash aliases for push & pop
  #
  # Note that if you are using an older version of git, before 2.16.0,
  # then you can use the older "stash save" instead of the newer "stash push".
  save = stash push
  pop = stash pop

  # Stash snapshot - from http://blog.apiaxle.com/post/handy-git-tips-to-stop-you-getting-fired/
  # Take a snapshot of your current working tree without removing changes.
  # This is handy for refactoring where you can't quite fit what you've done
  # into a commit but daren't stray too far from now without a backup.
  #
  # Running this:
  #
  #    $ git snapshot
  #
  # Creates this stash:
  #
  #    stash@{0}: On feature/handy-git-tricks: snapshot: Mon Apr 8 12:39:06 BST 2013
  #
  # And seemingly no changes to your working tree.
  #
  snapshot = !git stash push "snapshot: $(date)" && git stash apply "stash@{0}"

  # When you're a little worried that the world is coming to an end
  panic = !tar cvf ../panic.tar *

  # Create an archive file of everything in the repo
  archive = !"f() { top=$(rev-parse --show-toplevel); cd $top; tar cvf $top.tar $top ; }; f"

  # Do everything we can to synchronize all changes for the current branch.
  #
  #  * git get: fetch and prune, pull and rebase, then update submodules
  #  * git put: commit all items, then push
  #
  # TODO: handle tags, delete superfluous branches, and add error handing.
  #
  get = !git fetch --prune && git pull --rebase=preserve && git submodule update --init --recursive
  put = !git commit --all && git push

  # Do everything we can to make the local repo like the master branch.
  #
  # TODO: handle tags, and delete superfluous branches, and add error handling.
  #
  mastery = !git checkout master && git fetch origin --prune && git reset --hard origin/master

  # Ignore all untracked files by appending them to .gitignore:
  ignore = "!git status | grep -P \"^\\t\" | grep -vF .gitignore | sed \"s/^\\t//\" >> .gitignore"

  # Do a push/pull for just one branch
  push1 = "!git push origin $(git branch-name)"
  pull1 = "!git pull origin $(git branch-name)"

  # Track and untrack, with default parameters, and with printing the command
  track = "!f(){ branch=$(git rev-parse --abbrev-ref HEAD); cmd=\"git branch $branch -u ${1:-origin}/${2:-$branch}\"; echo $cmd; $cmd; }; f"
  untrack = "!f(){ branch=$(git rev-parse --abbrev-ref HEAD); cmd=\"git branch --unset-upstream ${1:-$branch}\"; echo $cmd; $cmd; }; f"

  # Track all remote branches that aren't already being tracked;
  # this is a bit hacky because of the parsing, and we welcome
  # better code that works using more-specific git commands.
  track-all-remote-branches = !"f() { git branch -r | grep -v ' -> ' | sed 's/^ \\+origin\\///' ; }; f"

  ##
  # Reset & Undo
  ##

  # Reset and undo aliases are ways to move backwards on the commit chain.
  # We find that novices prefer the wording "undo"; experts prefer "reset".
  reset-commit       = reset --soft HEAD~1
  reset-commit-hard  = reset --hard HEAD~1
  reset-commit-clean = !git reset --hard HEAD~1 && git clean -fd
  reset-to-pristine  = !git reset --hard && git clean -ffdx
  reset-to-upstream  = !git reset --hard $(git upstream-name)

  # Undo is simply a synonym for "reset" because "undo" can help novices.
  undo-commit        = reset --soft HEAD~1
  undo-commit-hard   = reset --hard HEAD~1
  undo-commit-clean  = !git reset --hard HEAD~1 && git clean -fd
  undo-to-pristine   = !git reset --hard && git clean -ffdx
  undo-to-upstream   = !git reset --hard $(git upstream-name)

  # Nicknames
  uncommit = reset --soft HEAD~1
  unadd = reset HEAD
  unstage = reset HEAD

  # Discard changes in a (list of) file(s) in working tree
  discard = checkout --

  # Clean and discard changes and untracked files in working tree
  cleanout = !git clean -df && git checkout -- .

  # Expunge a file everywhere; this command is typically for a serious problem,
  # such as accidentally committing a file of sensitive data, such as passwords.
  # After you use command, you will likely need to force push everything.
  # See https://help.github.com/articles/removing-sensitive-data-from-a-repository/
  expunge = !"f() { git filter-branch --force --index-filter \"git rm --cached --ignore-unmatch $1\" --prune-empty --tag-name-filter cat -- --all }; f"

  # Edit all files of the given type
  edit-cached   = !"f() { git ls-files --cached          | sort -u ; }; `git var GIT_EDITOR` `f`"
  edit-deleted  = !"f() { git ls-files --deleted         | sort -u ; }; `git var GIT_EDITOR` `f`"
  edit-others   = !"f() { git ls-files --others          | sort -u ; }; `git var GIT_EDITOR` `f`"
  edit-ignored  = !"f() { git ls-files --ignored         | sort -u ; }; `git var GIT_EDITOR` `f`"
  edit-killed   = !"f() { git ls-files --killed          | sort -u ; }; `git var GIT_EDITOR` `f`"
  edit-modified = !"f() { git ls-files --modified        | sort -u ; }; `git var GIT_EDITOR` `f`"
  edit-stage    = !"f() { git ls-files --stage | cut -f2 | sort -u ; }; `git var GIT_EDITOR` `f`"

  # Editing and adding conflicted files: when we get many merge conflicts
  # and want to quickly solve them using an editor, then add the  files.
  edit-unmerged = !"f() { git ls-files --unmerged | cut -f2 | sort -u ; }; `git var GIT_EDITOR` `f`"
  add-unmerged  = !"f() { git ls-files --unmerged | cut -f2 | sort -u ; }; git add `f`"

  # Ours & Theirs - easy merging when you know which files you want
  #
  # Sometimes during a merge you want to take a file from one side wholesale.
  #
  # The following aliases expose the ours and theirs commands which let you
  # pick a file(s) from the current branch or the merged branch respectively.
  #
  #   * ours: checkout our version of a file and add it
  #   * theirs: checkout their version of a file and add it
  #
  # N.b. the function is there as hack to get $@ doing
  # what you would expect it to as a shell user.
  #
  ours   = !"f() { git checkout --ours   $@ && git add $@; }; f"
  theirs = !"f() { git checkout --theirs $@ && git add $@; }; f"

  # Work In Progress: from https://gist.github.com/492227 and VonC on stackoverflow.
  # This enables a quick way to add all new and modified files to the index,
  # while cleaning the index from the files removed from the working tree;
  # this cleaning will facilitate a rebase, because there won't be any conflict
  # due to an "unclean" working directory (not in sync with the index).
  # The unwip will restore the deleted files to the working tree.
  wip = !"git add --all; git ls-files --deleted -z | xargs -0 git rm; git commit --message=wip"
  unwip = !"git log -n 1 | grep -q -c wip && git reset HEAD~1"

  # Assume
  #
  # Sometimes we want to change a file in a repo, but never check in your edits.
  # We can't use .gitignore because the file is tracked. We use update-index.
  #
  # If you interact with big corporate projects, such as projects in Subversion,
  # then you might run into the need to ignore certain files which are under
  # Subversion control, yet you need to modify them but not commit.
  # The assume-unchanged flag comes to the rescue.
  #
  # Suppose we want to edit passwords.txt and for god's sake never check it in:
  #
  #     $ git status
  #     modified passwords.txt
  #     modified foo.txt
  #
  #     $ git assume passwords.txt
  #     $ git status
  #     modified foo.txt
  #
  #     $ git assumed
  #     passwords.txt
  #
  #     $ git unassume passwords.txt
  #     $ git status
  #     modified passwords.txt
  #     modified foo.txt
  #
  # Thanks to http://durdn.com/blog/2012/11/22/must-have-git-aliases-advanced-examples/
  # Thanks to http://blog.apiaxle.com/post/handy-git-tips-to-stop-you-getting-fired/

  assume   = update-index --assume-unchanged
  unassume = update-index --no-assume-unchanged
  assume-all = "!git st -s | awk {'print $2'} | xargs git assume"
  unassume-all = "!git assumed | xargs git update-index --no-assume-unchanged"
  assumed  = !"git ls-files -v | grep ^h | cut -c 3-"

  # Delete all branches that have already been merged into the master branch.
  master-cleanse = !git master-cleanse-local; git master-cleanse-remote

  # Delete all local branches that have been merged into the local master branch.
  master-cleanse-local = "!git checkout master && git branch --merged | xargs git branch --delete"

  # Delete all remote branches that have been merged into the remote master branch.
  master-cleanse-remote = !"git branch --remotes --merged origin/master | sed 's# *origin/##' | grep -v '^master$' xargs -I% git push origin :% 2>&1 | grep --colour=never 'deleted'"

  # Publish the current branch by pushing it to the remote "origin",
  # and setting the current branch to track the upstream branch.
  publish = !"git push --set-upstream origin $(git branch-name)"

  # Unpublish the current branch by deleting the
  # remote version of the current branch.
  unpublish = !"git push origin :$(git branch-name)"

  # Delete a branch name, then create the same branch name based on master -
  # useful if you have, for example, a development branch and master branch
  # and they go out of sync, and you want to nuke the development branch.
  #
  # Calls the `publish` and `unpublish` aliases.
  #
  reincarnate = !"f() { [[ -n $@ ]] && git checkout \"$@\" && git unpublish && git checkout master && git branch -D \"$@\" && git checkout -b \"$@\" && git publish; }; f"

  # Friendly wording is easier to remember.
  # Thanks to http://gggritso.com/human-git-aliases
  branches = branch -a
  tags = tag -n1 --list
  stashes = stash list


  ### SHELL SCRIPTING ALIASES ###

  # Get the top level directory name
  top-name = rev-parse --show-toplevel

  # Get the current branch name
  branch-name = rev-parse --abbrev-ref HEAD

  # Get the upstream branch name
  upstream-name = !git for-each-ref --format='%(upstream:short)' $(git symbolic-ref -q HEAD)

  # Execute shell scripts. Git always runs scripts in the top directory.
  # For example "git exec pwd" will always show you the top directory.
  exec = ! exec


  ### MAINTENANCE ALIASES ###

  # pruner: prune everything that is unreachable now.
  #
  # This command takes a long time to run, perhaps even overnight.
  #
  # This is useful for removing unreachable objects from all places.
  #
  # By [CodeGnome](http://www.codegnome.com/)
  #
  pruner = !"git prune --expire=now; git reflog expire --expire-unreachable=now --rewrite --all"

  # repacker: repack a repo the way Linus recommends.
  #
  # This command takes a long time to run, perhaps even overnight.
  #
  # It does the equivalent of "git gc --aggressive"
  # but done *properly*,  which is to do something like:
  #
  #     git repack -a -d --depth=250 --window=250
  #
  # The depth setting is about how deep the delta chains can be;
  # make them longer for old history - it's worth the space overhead.
  #
  # The window setting is about how big an object window we want
  # each delta candidate to scan.
  #
  # And here, you might well want to add the "-f" flag (which is
  # the "drop all old deltas", since you now are actually trying
  # to make sure that this one actually finds good candidates.
  #
  # And then it's going to take forever and a day (ie a "do it overnight"
  # thing). But the end result is that everybody downstream from that
  # repository will get much better packs, without having to spend any effort
  # on it themselves.
  #
  # http://metalinguist.wordpress.com/2007/12/06/the-woes-of-git-gc-aggressive-and-how-git-deltas-work/
  #
  # We also add the --window-memory limit of 1 gig, which helps protect
  # us from a window that has very large objects such as binary blobs.
  #
  repacker = repack -a -d -f --depth=300 --window=300 --window-memory=1g

  # Do everything we can to optimize the repository.
  #
  # This command takes a long time to run, perhaps even overnight.
  #
  # Currently, this command simply calls `git pruner` and `git repacker`.
  # There's a step that may be unnecessarying, calling `git prune-pack`.
  #
  optimize = !git pruner; git repacker; git prune-packed


  ### ADVANCED ALIASES ###

  # Search for a given string in all patches and print commit messages.
  # Posted by Mikko Rantalainen on StackOverflow.
  #
  # Example: search for any commit that adds or removes string "foobar"
  #     git searchcommits foobar
  #
  # Example: search commits for string "foobar" in directory src/lib
  #     git searchcommits foobar src/lib
  #
  # Example: search commits for "foobar", print full diff of commit with 1 line context
  #     git searchcommits foobar --pickaxe-all -U1 src/lib
  searchcommits = !"f() { query=\"$1\"; shift; git log -S\"$query\" \"$@\"; }; f \"$@\""

  # A 'debug' alias to help debugging builtins: when debugging builtins,
  # we use gdb to analyze the runtime state. However, we have to disable
  # the pager, and often we have to call the program with arguments.
  # If the program to debug is a builtin, we use this alias.
  debug = !GIT_PAGER= gdb --args git

  # Getting the diff of only one function: when we want to see just the
  # differences of one function in one file in two different commits,
  # we create two temp files which contain only the function, then diff.
  # Use this alias this way: git funcdiff <old-rev> <new-rev> <path> <function>
  # diff-func = !sh -c "git show \"\$1:\$3\" | sed -n \"/^[^ \t].*\$4(/,/^}/p\" > .tmp1 && git show \"\$2:\$3\" | sed -n \"/^[^ \t].*\$4(/,/^}/p\" > .tmp2 && git diff --no-index .tmp1 .tmp2" -

  # Calling "interdiff" between commits: if upstream applied a
  # slightly modified patch, and we want to see the modifications,
  # we use the program interdiff of the patchutils package.
  intercommit = !sh -c 'git show "$1" > .git/commit1 && git show "$2" > .git/commit2 && interdiff .git/commit[12] | less -FRS' -

  # Prune all your stale remote branches: there's no way to tell
  # git remote update to prune stale branches, and git remote prune
  # does not understand --all. So here is a shell command to do it.
  prune-all = !git remote | xargs -n 1 git remote prune

  # Thanks to cody cutrer
  cherry-pick-merge = !"sh -c 'git cherry-pick --no-commit --mainline 1 $0 && \
    git log -1 --pretty=%P $0 | cut -b 42- > .git/MERGE_HEAD && \
    git commit --verbose'"

  # Thanks to jtolds on stackoverflow
  remote-ref = !"sh -c ' \
    local_ref=$(git symbolic-ref HEAD); \
    local_name=${local_ref##refs/heads/}; \
    remote=$(git config branch.\"#local_name\".remote || echo origin); \
    remote_ref=$(git config branch.\"$local_name\".merge); \
    remote_name=${remote_ref##refs/heads/}; \
    echo remotes/$remote/$remote_name'"

  # Thanks to jtolds on stackoverflow
  rebase-recent = !git rebase --interactive $(git remote-ref)

  # Use graphviz for display.
  # This produces output that can be displayed using dotty, for example:
  #   $ git graphviz HEAD~100..HEAD~60 | dotty /dev/stdin
  #   $ git graphviz --first-parent master | dotty /dev/stdin
  graphviz = !"f() { echo 'digraph git {' ; git log --pretty='format:  %h -> { %p }' \"$@\" | sed 's/[0-9a-f][0-9a-f]*/\"&\"/g' ; echo '}'; }; f"

  # Serve the local directory by starting a git server daemon, so others can pull/push from my machine
  serve = "-c daemon.receivepack=true daemon --base-path=. --export-all --reuseaddr --verbose"

  ##########################################################################

  ##
  # Git alias settings suitable for topic branches.
  #
  # These aliases are simple starting points for a simple topic flow.
  # Lots of people have lots of ideas about how to do various git flows.
  #
  # Some people like to use a topic branch for a new feature, or a
  # hotfix patch, or refactoring work, or some spike research, etc.
  #
  # Our simple workflow:
  #
  #     $ git topic-start foo
  #     ... do work ...
  #     $ git topic-stop
  #
  # If you want more control, then you can use these building blocks:
  #
  #     $ git topic-create foo
  #     $ git topic-delete
  #
  # If you want to pull and push while you're working, then use these:
  #
  #     $ git topic-pull
  #     $ git topic-push
  #
  # If you want to manage your branch while you're working, then use these:
  #
  #     $ git topic-sync
  #     $ git topic-rename
  #
  # Ideas for your own alias customizations:
  #
  #   * Notify your team, such as by sending an email, posting to chat, etc.
  #   * Trigger testing of the new topic branch to ensure all tests succeed.
  #   * Update the project management software.
  #
  # Customize these aliases as you like for your own workflow.
  ##

  ##
  # Provide the name of the topic base branch, such as "master".
  #
  # When we create a new topic branch, we base it on the topic base branch.
  # Many projects use the default "master" branch; some projects use custom
  # branches, such as "trunk", "develop", "integrate", "release", etc.
  #
  # Customize this alias as you like for your own workflow.
  ##

  topic-base-branch-name = "!f(){ \
    printf \"master\n\"; \
  };f"

  ### START & STOP ###

  ##
  # Start a topic branch.
  #
  # Example:
  #
  #     git topic-start foo
  #
  # We use this alias to begin work on a new feature,
  # new task, new fix, new refactor, new optimization, etc.
  #
  # This implementation does these steps:
  #
  #   1. Create the topic branch.
  #   2. Push the topic branch.
  #
  # Customize this alias as you like for your own workflow.
  ##

  topic-start = "!f(){ \
    topic_branch=\"$1\"; \
    git topic-create \"$topic_branch\"; \
    git topic-push; \
  };f"

  ##
  # Stop a topic branch; this must be the current branch.
  #
  # Example:
  #
  #     git topic-stop
  #
  # We use this alias to complete work on a new feature,
  # new task, new fix, new refactor, new optimization, etc.
  #
  # This implementation does these:
  #
  #   1. Push the topic branch.
  #   2. Delete the topic branch.
  #
  # Customize this alias as you like for your own workflow.
  ##

  topic-stop = "!f(){ \
    git topic-push; \
    git topic-delete; \
  };f"

  ### CREATE & DELETE ###

  ##
  # Create a topic branch.
  #
  # Example:
  #
  #     git topic-create foo
  #
  # This implementation does these steps:
  #
  #   1. Update the base branch locally.
  #   2. Create a new branch with your topic name, based on the base branch.
  #
  # Customize this alias as you like for your own workflow.
  ##

  topic-create = "!f(){ \
    topic_branch=\"$1\"; \
    base_branch=$(git topic-base-branch-name); \
    git checkout \"$base_branch\"; git pull; \
    git checkout -b \"$topic_branch\" \"$base_branch\"; \
  };f"

  ##
  # Delete a topic branch; this must be the current branch.
  #
  # Example:
  #
  #     git topic-delete
  #
  # This implementation does these:
  #
  #   1. Delete the topic branch locally.
  #   2. Delete the topic branch remotely.
  #
  # Customize this for your own workflow preferences.
  #
  # If you use a sharing site such a GitHub, and use typical settings,
  # then this implementation deletes your branch for the site.
  #
  # Many teams choose to delete topic branches when they are finished,
  # to keep the repositories clean and with a smaller number of branches.
  #
  # If git says "unable to push to unqualified destination" then it means
  # that the remote branch doesn't exist, so git is unable to delete it.
  # That's fine; it means someone else has already deleted the branch.
  # To synchronize your branch list, use "git fetch --prune".
  #
  # Customize this alias as you like for your own workflow.
  ##

  topic-delete = "!f(){ \
    topic_branch=$(git branch-name); \
    base_branch=$(git topic-base-branch-name); \
    if [ \"$topic_branch\" = \"$base_branch\" ]; then \
      printf \"You are trying to delete your git topic branch,\n\"; \
      printf \"but you are on the base branch: $topic_base_branch.\n\"; \
      printf \"Please checkout the topic branch that you want,\n\"; \
      printf \"then retry the git topic delete command.\n\"; \
    else \
      git checkout \"$base_branch\"; \
      git branch --delete \"$topic_branch\"; \
      git push origin \":$topic_branch\"; \
    fi; \
  };f"


  ### PULL & PUSH ###

  ##
  # Update the current topic branch by pulling changes.
  #
  # Example:
  #
  #     git topic-pull
  #
  # This implementation does these:
  #
  #   1. Pull the topic branch from the origin.
  #
  # If you use any kind of testing framework, or test driven development,
  # then it can be wise to test your topic immediately after running this,
  # to ensure that any available updates are successfully integrated.
  #
  # Customize this alias as you like for your own workflow.
  #
  #   * E.g. some teams prefer to use `pull --rebase`.
  ##

  topic-pull = "!f(){ \
    git pull; \
  };f"

  ##
  # Update the current topic branch by pushing changes.
  #
  # Example:
  #
  #     git topic-push
  #
  # This implementation does these:
  #
  #   1. Push the topic branch to the origin.
  #   2. Set the upstream tracking.
  #
  # Customize this for your own workflow preferences.
  #
  # If you use a sharing site such a GitHub, and use typical settings,
  # then this implementation makes your branch visible to collaborators.
  #
  # Many teams share branches before they are fully ready, to help
  # the team provide feedback on the work-in-progress.
  #
  # Customize this alias as you like for your own workflow.
  ##

  topic-push = "!f(){ \
    topic_branch=$(git branch-name); \
    git push --set-upstream origin \"$topic_branch\"; \
  };f"

  ### MANAGE TOPIC BRANCHES ###

  ##
  # Update the current topic branch with up-to-date base branch
  # by either rebasing or merging.
  #
  # Example:
  #
  #     git topic-rebase-base
  #
  # This implementation does these:
  #
  #   1. Run checkout base_branch.
  #   2. Pull base_branch
  #   3. Run checkout topic_branch.
  #   4. Merge/Rebase base_branch.
  #
  # Customize this alias as you like for your own workflow.
  ##

  topic-rebase-base = "!f(){ \
    topic_branch=$(git branch-name); \
    base_branch=$(git topic-base-branch-name); \
    git checkout \"$base_branch\"; git pull; \
    git checkout \"$topic_branch\"; git rebase \"$base_branch\"; \
  };f"

  topic-merge-base = "!f(){ \
    topic_branch=$(git branch-name); \
    base_branch=$(git topic-base-branch-name); \
    git checkout \"$base_branch\"; git pull; \
    git checkout \"$topic_branch\"; git merge \"$base_branch\"; \
  };f"

  ##
  # Update the current topic branch by synchronizing changes.
  #
  # Example:
  #
  #     git topic-sync
  #
  # This implementation does these:
  #
  #   1. Run topic-pull.
  #   2. Run topic-push.
  #
  # Customize this alias as you like for your own workflow.
  ##

  topic-sync = "!f(){ \
    git topic-pull; \
    git topic-push; \
  };f"

  ##
  # Move/rename the current topic branch.
  #
  # Example:
  #
  #     git topic-move hello
  #
  # This implementation does these:
  #
  #   1. Move/rename the local branch.
  #   2. Move/rename the remote branch by pushing to origin.
  #
  # Customize this alias as you like for your own workflow.
  ##

  topic-move = "!f(){ \
    new_branch=\"$1\"; \
    old_branch=$(git branch-name); \
    git branch --move \"$old_branch\" \"$new_branch\"; \
    git push origin \":$old_branch\" \"$new_branch\"; \
  };f"


  ##########################################################################

  ##
  # Git aliases suitable for particular software integrations and tooling,
  # such as other version control system e.g. CVS, Subversion, etc.
  ##

  ### CVS ALIAS ###

  cvs-i = cvsimport -k -a
  cvs-e = cvsexportcommit -u -p

  ### GitK ###

  # show conflicting merge in gitk:
  gitk-conflict = !gitk --left-right HEAD...MERGE_HEAD

  # show full history in gitk (including "deleted" branches and stashes)
  gitk-history-all = !gitk --all $( git fsck | awk '/dangling commit/ {print $3}' )

  ### Ruby on Rails ###

  # Do everything we can to synchronize all changes for a Ruby On Rails app.
  # We like using rebase (instead of merge), bundle for gems, and rake db:migrate
  rails-get = !"git pull --rebase; git submodule update --init --recursive; bundle check || bundle install; bundle exec rake db:migrate; bundle exec rake db:test:prepare"

  ### Subversion ###

  svn-b = svn branch
  svn-m = merge --squash
  svn-c = svn dcommit
  svn-cp = !GIT_EDITOR='sed -i /^git-svn-id:/d' git cherry-pick --edit

  ##########################################################################

  ##
  # Git aliases to correct common typing mistakes, which git built-in autocorrection
  # does not handle
  ##

  ### Use with shell alias `gitp = git` ###

  ull = pull
  ush = push