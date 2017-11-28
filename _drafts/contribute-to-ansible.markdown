---
layout: post
title:  "How to contribute to ansible project"
date:   2016-12-6 12:55:28 +0100
categories: ansible contribute version git fork bug report
---
## Introduction

Because we find Ansible, just awsome, we would like to share our experience about contributing on it. 
We will see, step-by-step, how to contribute on Ansible and generally on a lot of open-source projects. 
We so will begin it by refreshing you on what is Ansible. 
Next we will see four steps, how to set-up your environment, how to develop on it, how to perform your first pull-request and then we will se the best process to have your request accepted. 
We will follow two of our contributions as example during all this article. The first one was an issue on oom_killer option of docker_container module [#29886](https://github.com/ansible/ansible/issues/29886), the second one was ....TODO: 4383: choose the one you wanna explain, maybe it could be a good idea to don't choose a fix ... 

## Goals

The goal of this article is, of course, how to become an Ansible contributor, but not only, we will help you to speed up your pull-request merge! 

Ansible is needing help, and of course everyone are welcome! Let's begin!

## Prerequisites
Contribute on Ansible implies some prerequisites.

Ansible is written in python so you'll need different versions to ensure compatibility:
- python 2.7
- python 3.5

To improve development lifecycle we will use [pipenv](https://github.com/kennethreitz/pipenv).
Instead, you can use mainstream tools like `virtualenv` and `pip`.

Ansible project is hosted on github so [you require a github account](https://github.com/) for deal with it.

Github is based on the `git` version control system, so you'll need it.

You'll need also [docker](https://www.docker.com/) to have a fully isolated development setup to play your playbooks against.
Ansible unit and integration tests have parts also based on docker.
For your information, this is a very interesting part to contribute on Ansible.

## What's Ansible?
    
If you are reading this article, you should propably be already familiar with Ansible... So if you're not reading it, we'll explain it quickly ...

Ansible is a simple IT automation engine. It is designed to easily configure several servers. It's a really good devOps partner to automate quickly and easily a CI/CD for example. Ansible have a lot of plugins which are used to manage almost everything in a server, network device, storage bay.... It is easy-to-use; all the configuration ans playbooks are simple yaml files and it doesn't need any agent on managed nodes. Ansible requires only an SSH connection and python installed on the manages server. In fact, that's not really true since Ansibe can manage windows nodes using the powershell distant connexion. It is fair to say that we will cover only the Linux use cases in this article. Ansible force lie in the capability to easily configure a lot of devices and guaranty that the configuration is consistent in all targets regardless the initial state. How is it done ? The concept behind an Ansible module is to be re-enterable!

Ansible have severals competitors like, [Chef](https://www.chef.io/chef/), [Puppet](https://puppet.com/), [Saltstack](https://saltstack.com/), [Fabric](https://fabric.io) or others. Why did we choose Ansible? As we said previously, it is easy to use, and don't need agent. It is fully coded in python which is a language we appreciate and, on top of that, we are using it professionnaly every days and are really happy with it, of course. 

OK, that sounds great, but what's the price? Ansible is an open-source project which have a growing community and it is really easy to use, so it won't costs many times (it will even save so much !) and it's fully free (you can have some support on some modules for profesionnal purposes regarding your use cases).



#### Let's see main principles :

We will just define few glossary terms before:
There are two kinds of machines used during an Ansible deployment:
  - Ansible is executed on a server host called `controller`
  - The servers/devices managed by Ansible are called `managed nodes`
Complete glossary is available [here](http://docs.ansible.com/ansible/latest/glossary.html) if you need it.

Ansible uses an [inventory](http://docs.ansible.com/ansible/latest/intro_inventory.html)  which defines all managed nodes access in a simple (or multiples) YAML file. Ansible is using SSH to manage nodes. It can deal with a password or key authentication and is able to elevate privileges using su, sudo [or several others](http://docs.ansible.com/ansible/latest/become.html). You can even use an SSH bastion by simply using ssh args variables or your `ssh_config` file. This can address almost cases.

To define what to perform on managed nodes you must creates playbook. This is still YAML files. You can find some documentation about playbooks [here](http://docs.ansible.com/ansible/latest/playbooks.html). To avoid having code duplication and win some flexibility I strongly recommend you to use [playbooks roles](http://docs.ansible.com/ansible/latest/playbooks_roles.html).

We recommend to follow the [best practices](http://docs.ansible.com/ansible/latest/playbooks_best_practices.html) to organize your Ansible directory layout


Get more informations on [how it works](https://www.ansible.com/how-ansible-works) or more generaly on [Ansible official site](https://www.ansible.com/) 
The [Ansible documentation](http://docs.ansible.com/ansible/latest/index.html) is really up-to-date, well organised and contained a lots of example. It will be a great help for you. 

    

## Why contribute?

Ansible usage have grew up rapidly and many issues are continously opened.

An issue can be a feature request, a bug reporting, or even simply a question to the maintainance team.
Rather than considering, ansible need contributors to continue to improve its quality and stability every days..

Ansible is an opensource project maintained by the redhat company, so he have to kind of contributors:
- the biggest parts of contributors are volunteers and works on ansible on free times.
- the rest of the contributors are considered as commiters, they are members of the core team.

You can contribute by adding parts of documentation, migrate code, fix issues or even adding features.
So all contributions are welcomes!

Contributing helps you to improve your skill about ansible but also improve your
skills on large distribued development team all around the world.

You would become more efficient with git usages, concepts, and a lot of stuffs very useful in the real life.

Working on this project allowed us to discover it in depth. We discovered new uses, new modules, and a lot of nice things.

Contributing follow guidelines. These guidelines help developers to learn how to develop on ansible.
The community can help you to introduce yourself inside contribution project.

Ansible project is hosted on [github](https://github.com/ansible/ansible) you can fork this project and start to work on.

The contribution guidelines was describe in the [contribution code](http://docs.ansible.com/ansible/latest/community.html#contributing-code-features-or-bugfixes).

For submit your work you must deal with [github pull request](https://help.github.com/articles/using-pull-requests).

You can also read [how to developing modules](http://docs.ansible.com/ansible/dev_guide/developing_modules.html), and [how to testing your work](http://docs.ansible.com/ansible/dev_guide/testing.html)  in the [official documentation](http://docs.ansible.com/ansible/latest/dev_guide/).

If you need help many communication channel are available for that:
- [IRC channels](http://docs.ansible.com/ansible/latest/community.html#irc-channel)
- [IRC meetings](http://docs.ansible.com/ansible/latest/community.html#irc-meetings)
- [mailing list](http://docs.ansible.com/ansible/latest/community.html#mailing-list-information)

You can [find several issues on the github project page](https://github.com/ansible/ansible/issues), select your subject and workon for starting contributing.
Hovewer you can [follow topics projects](https://github.com/ansible/ansible/projects) for summarize issues by themes.

Now it's time to start contributing!

## Step 1 - Prepare environment

#### a. Setup your fork

First, go to the [ansible github official page](https://github.com/ansible/ansible) and click on the fork button.

![Fork ansible]({{ "/assets/contribute-to-ansible/fork-ansible.png" | absolute_url }})

Wait a few moments and now your fork appear in your github account.

![Now ansible was forked]({{ "/assets/contribute-to-ansible/forked.png" | absolute_url }})

Now prepare your local environment.

```sh
$ # setup your identity
$ git config --global user.name "<your name>"
$ git config --global user.email "<your-email@example.com>"
$ # setup pushing method
$ git config --global push.default current
```

Clone your fork localy and place yourself to the right branch:

```sh
$ git clone https://github.com/<your-github-account>/ansible
$ cd ansible
$ git checkout devel
```

Configure your clone for fetching upstream updates:

```sh
$ git remote add upstream https://github.com/ansible/ansible
$ # check remotes
$ git remote -v
origin  https://github.com/<your-github-username>/ansible (fetch)
origin  https://github.com/<your-github-username>/ansible (push)
upstream        https://github.com/ansible/ansible (fetch)
upstream        https://github.com/ansible/ansible (push)
```

Synchronize your local clone with upstream:
```sh
$ git fetch upstream
...
$ git merge upstream/devel
```

Update your forked repository
```sh
$ git push origin devel
```

#### b. Setup your python environment

Ansible is written in python so you need to setup a python develop environment.

Setup a new python virtual environment:

```sh
$ pipenv --python 3.5 # replace python version for python 2.7
$ pipenv shell
$ # your now in your python virtual environment
```

Now source ansible development context:
```sh
$ source hacking/env-setup
```

Install base dependencies:
```sh
$ pipenv install -r requirements.txt
```

Ansible come with a lots of development dependencies, you can install all or just a subset
in concordance with your development purpose.

If you work on documentation all development dependencies are presents in `./docsite_requirements.txt`.
```sh
$ pipenv install -r ./docsite_requirements.txt
```

To working on bugfix, tests, or new features you need to install specific requirements:
```sh
$ # minimal subset of requirements to install
$ pipenv install -r ./test/runner/requirements/units.txt
$ pipenv install -r ./test/runner/requirements/integration.txt
$ pipenv install -r ./test/runner/requirements/coverage.txt
$ pipenv install -r ./test/runner/requirements/constraints.txt
$ pipenv install -r ./test/runner/requirements/ansible-test.txt
$ pipenv install -r ./test/runner/requirements/sanity.txt
```

#### c. Setup your docker environment
    c. Créer des hotes à configurer (docker)

## Step 2 - Take action!

#### a. Find issues on ansible
Now it's time to take actions! Now you'll be able to see what's going on under the hood of Ansible.
First you need helps to find a subject to work on. Ansible gets an
an issues tracker which will helps you can find ideas or ways of work.
If your are neeby with ansible or python I recommand to you
to prefer bugfix because it can be more easily at start than directly start to write a new feature.
You can filter issues with labels and choose an easy fix by using the `easyfix` label.

So! [go to the issues tracker and search jobs](https://github.com/ansible/ansible/issues)!

![Ansible issues tracker]({{ "/assets/contribute-to-ansible/ansible-issues-tracker.png" | absolute_url }})

If you want to work on specific subjects or on specific kinds of
issues you can apply filters on your research. Parts of filters are based on labels so you can use it to find your happiness.

Example:

Considere you want to works on the docker features of ansible, for fixing a bug or implement a new feature,
you research for appropriated label and find the existing label docker. So apply this filter to your research
and reach only the issues in connection with docker subject.

![Ansible filter issues by labels]({{ "/assets/contribute-to-ansible/ansible-filter-by-labels.png" | absolute_url }})

Also you can filter for kind of issues (fix or feature) and refine your research.

#### b. Start to work

Well! You have your developmenent environment, you know basicly how to work on ansible, how about actually starting to work?

On the ansible project the default git branch is devel, devel correspond to the latest version of this product.
Ansible ask to you to work on the `devel` branch by creating a new local feature branch based on this.
Backports between versions of ansible as managed by the core team.

Considere you want to fix a bug on docker module so the workflow looks like this:

```sh
$ git checkout devel
$ git checkout -b fix-docker-module
```

You are now on your new branch `fix-docker-module`. You can start to work on and to try to resolve your bug.

Patches should always be made against the `devel` branch.

For more informations you can read the
[official ansible contributing guide](http://docs.ansible.com/ansible/latest/community.html#contributing-code-features-or-bugfixes).

Now you have start to work you must be careful about coding rules best practices.

#### c. Apply coding rules best practices

Ansible is maintained by lot of people so this project need to impose somes 
development guidelines for to ensure project quality, stability, and maintainability.

Ansible’s aesthetic encourages simple, readable code and consistent,
conservatively extending, backwards-compatible improvements.
When contributing code to Ansible, please observe the following guidelines:

- Code developed for Ansible needs to support Python2-2.6 or higher and Python3-3.5 or higher.
- Use a 4-space indent, not tabs.
- Ansible team do not enforce 80 column lines; up to 160 columns are acceptable.
- Ansible team do not accept ‘style only’ pull requests unless the code is nearly unreadable.
- Ansible are not strictly compliant with [PEP8](https://www.python.org/dev/peps/pep-0008/).See [PEP8](https://www.python.org/dev/peps/pep-0008/) for more information.

Ansible are not strictly compliant with PEP8 but we still want to encourage you to respect this standard.

More informations about coding rules are availables [here](http://docs.ansible.com/ansible/latest/community.html#for-current-and-prospective-developers).

#### d. Test your works

Ansible was battery included, this mean that ansible come with a lot of included features,
and offers to you a many functionalities very useful during your developments.
Ansible comes with a full suite of tests that avoiding to introduce bugs or breaking some functionalities. You so have to pass these tests and should write or improve existing if you find a lack on somes. You do not need an issue for that, feel free to contribute on it, it will be a great improvement.

Before submit your works to the official project you must pass all these tests in your local environment.

These test are automticaly launch during continuous integration (CI) steps of the upstream project.

When your works was submitted to the ansible team CI execute tests automaticaly.
If something went wrong your work it automaticaly rejected by the CI robot (ansibulbot) or by maintainers.

We can define 4 major kinds of tests:
- [compile](http://docs.ansible.com/ansible/latest/dev_guide/testing_compile.html): test python code against a variety of Python versions.
- [unit](http://docs.ansible.com/ansible/latest/dev_guide/testing_units.html): tests directly against individual parts of the code base.
- [sanity](http://docs.ansible.com/ansible/latest/dev_guide/testing_sanity.html): the primary purpose of these tests is to enforce Ansible coding standards and requirements.
- [integration](http://docs.ansible.com/ansible/latest/dev_guide/testing_integration.html): functional tests of modules and Ansible core functionality.

Now we want to focus only sanity and unit tests. These tests are commons tests for any ansible contributors.
Others test (compile and integration) are less used for basic contributions.

Unit tests are tested functionalities to determine whether they are fit for use. If something went wrong
you can rapidely determine where the problem occur and fix it immediately.

Sanity check syntax and coding rules. With it you can ensure that you have applied all the best practices in use on this project.

Well! Now we want to explain to you how to deal with tests.

At step 1 we already have setup your development environment so you already have all tools for launch tests.

All testing modules was available via the `ansible-test` command.

You can use them like this:

```sh
$ # sanity tests
$ ansible-test sanity # pass all sanity checks
...
$ ansible-test sanity --test pep8 # or define a specific test to run
...
$ # unit tests
$ ansible-test unit --tox apt # for testing the apt ansible module
$ ansible-test unit --tox --python 3.5 # for using unit test with specific version of python
```

For more general informations about ansible tests you can [read the official documentation](http://docs.ansible.com/ansible/latest/dev_guide/testing.html)

Testing help you to prevent regression on your implementations,
but the quality of the ansible project is also due to the fact that the contributors
take care to maintain an proper version control history.

#### e. Maintain a properly and semantic git history

Before submitting your work to the ansible team you must ensure yourself to have an proper git history.

What's an proper git history? This is a semantical history that help code reviewing and project maintainability.

Example, considere you have worked on new feature implementation, so you have made a lot of commits. Somes commits was semanticaly valid, but others
can be caused by mistakes in your development. For example fixing a bug introduced during previous commit on the same feature.

These commits can make code review hard and annoying.

After all, the fix commit is just a repair of your own implementation, the upstream project does not need to know your fix...

You can squash the fixing commit in the main commit where your core implementation comes to life.

So considere these 2 commits, 1 for the main implementation, 1 for the fix, and squash them together:

```sh
$ git log
commit af15df42cd4af5f545952d00da5451fe75ae672f
Author: Hervé Beraud <herveberaud.pro@gmail.com>
Date:   Thu Oct 26 16:32:18 2017 +0200

    fix a problem on my own code

commit be49777a8b859c1c67b82fad0a0c79fa1510d5af
Author: Hervé Beraud <herveberaud.pro@gmail.com>
Date:   Thu Oct 26 14:30:01 2017 +0200

    implement a new feature
```

You can see your 2 commits on your history, now squash them together:

```sh
$ # now squash your history
$ git rebase -i HEAD~2
pick be49777a implement a new feature
pick af15df42 fix an problem on my own code
```

Now you can tell git what to do with each commit. Let’s keep the commit `be49777a`,
the one were we added our feature. 
We’ll squash the following commit into the first one -
leaving us with one clean commit with features X in it.
You can rewrite the commit message or keep it intact.

```sh
pick be49777a implement a new feature
squash af15df42 fix an problem on my own code
```

Now you have a proper and semantic git history

```sh
$ git log
commit be49777a8b859c1c67b82fad0a0c79fa1510d5af
Author: Hervé Beraud <herveberaud.pro@gmail.com>
Date:   Thu Oct 26 14:30:01 2017 +0200

    implement a new feature
```

Other subject, you can also rewrite your commits message by using the --amend git option.
This option allow to you to rewrite bad message or make it more semantic.

Ansible maintainers will appreciate that and you will be grateful.

Now you have make a really good job, let's push your works on your fork together!

#### f. Push your works on your github repository

At this point, you've done your development, you've tested it and get a properly history,
we think you can push your modifications to your own fork.

This is a really simple action, just one command to tip on your keyboard:

```sh
$ git push origin <your-branch-name>
```

If you already have pushed modifications to your fork and that you want to
rewrite history before submitting your new pull request you can force to
push your modifications by using the option `--force` to the `git push` command:

```sh
$ git push --force origin <your-branch-name>
```

Keep in mind to never delete your development branch before it is fully integrated to the upstream project.

Now you can start to submit your pull request to the official project.

## Step 3 - Make a pull request
    a . create PR in github
    b. understand ansibullbot labels

## step 4 - What's happens next?
    a. How to integrate modifications to the PR
    b. obtain 2 shipit

    Git
    Github

## Conclusion
