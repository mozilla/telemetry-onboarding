# Contributing to Firefox Data Platform projects

This is a tutorial on how to work with the various Firefox Data Platform projects.

## Github Workflow @ Fx Data Platform

The Firefox Data Platform team makes extensive use of Git, and particularly Github for many projects. This document describes the ideal approach to working with repositories on Github.

### Creating a new repo

Feel free to create the repo under your own account for initial development or skunkworks projects.

Once a project approaches “production quality”, it should be moved to one of the official Mozilla github organizations: either “mozilla” or “mozilla-services”. This move can be requested in #github on IRC, and when you request the move, you should also request that the “telemetry” group own the repo after it has been moved. If you find you’re not in the “telemetry” group, you should request to be added.

### Branches and PRs

Create a new branch to work on a new feature. Try to keep the work focused on a single logical change or feature. Ideally there should be a bug filed in bugzilla for the task.

To submit changes, make a personal fork of the repository, push your branch there, and open a pull request.
Keeping development branches on forks keeps the upstream repository cleaner and lessens the chance of accidentally
pushing changes to master prematurely.
Pushing branches upstream should be reserved for cases where your changes need to be tested or built
by the CI pipeline.

#### Atomic commits

Each commit should make a single standalone change if possible, so that the resulting branch contains a series of logical steps to make the full change or implement the feature. The list of commits in a patch should tell the story of how the patch evolved but every single commit should ideally pass a test suite run.

##### Why should we care about atomic commits?

To follow the `atomic commits` workflow requires a time investment from the patch author, but that time will be vastly regained in the review process. The idea is that a reviewer’s time is very valuable, even only because there are usually more contributors than reviewers. Once the patch author gets used to the atomic commit workflow, not much effort will be required to organise the commits and that will result in a win-win.

Another good point in favor of the atomic commits workflow is that it works well for history archeology. Cherry-picking and bisection are almost useless when you have either meaningless or giant commits.

##### Organizing your commits

In order to properly organise your work, there are several git subcommand that may be of help:

`git commit --amend` modifies the last commit in the current branch (including the commit message)

`git rebase -i <commit id/sha>^` interactively change your past commits. This is one of the best ways to rearrange your commits. It lets you reorder, delete, amend, combine, and reword your commit history.

`git commit --fixup <commit id/sha>` create a new ‘fixup’ commit for a previous commit. The new commit can be then rebased

Bonus points if you use `git commit --fixup` in combination with `git rebase -i <commit id/sha>^ --autosquash` to automatically rearrange your fixup commits in the right place.

#### Commit message

There are several guides online that talk about this topic. The tl;dr is to keep it informative and succinct. First line no more than 50 chars long and eventually a blank line and an extended description.

On many projects there are conventions in use, like prefixing the message with the issue/bug number or use an imperative form for verbs. The best thing to do here is to check the project history and follow the same conventions. For new projects you can ask your mentor/peers on what’s best to do.

Here is an article on [How to Write a good Git Commit Message](http://chris.beams.io/posts/git-commit/).

### Reviews

Code should not be merged into an official mozilla github project without being reviewed by one of your peers. If you don’t know who to ask for review, check the history of the project or files. If it is a brand new repository, ask someone on your team.

Typically the person reviewing the change will merge the branch once all feedback has been addressed. If they do not have permission to merge, they will comment with “r+” or similar, at which point the author can merge the change.

For any complex review, or really any review at all, the reviewable.io tool is invaluable. Please try to use this if possible. Major advantages include the ability to keep track of changes even if the commits are rebased or modified, tracking of whether individual comments have been addressed or not, and batching up of feedback (so the conversation generates a single notification per iteration instead of a notification per comment).

#### Code review checklist

TODO

### New webdev projects

#### Django (with Sugardough)

If you need to start a new project that involves web development a good starting point is [Sugardough](https://github.com/mozilla/sugardough), a [Django](https://www.djangoproject.com/) project template made by some [awesome people](https://github.com/mozilla/sugardough/graphs/contributors) in the Mozilla webdev community. It comes with lots of goodies and sane defaults: readthedocs, travis, converalls, docker-compose, etc. See [the project readme](https://github.com/mozilla/sugardough#sugardough) for a more extensive list of features.

#### Django Rest Framework

If your project requires a restful api, please do yourself a favor and consider using [Django Rest Framework](http://www.django-rest-framework.org/). It integrates well with the Django ORM, although it's not a requirement, and the Django authentication system. It's fully configurable and it comes with standard-compliant defaults.
It also provides a documentation site for your api where users can test it directly.

Both Django and Django Rest Framework have been used by the Mozilla webdev community for years and their value has been even recognised with a [MOSS grant](https://wiki.mozilla.org/MOSS)
