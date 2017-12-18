---
layout: post
title:  "How to contribute to ansible project"
date:   2016-12-6 12:55:28 +0100
categories: ansible contribute version git fork bug report
---
## Introduction

Since we find Ansible awesome, we wanted to share our experience of contributing to it. In this article we will explain, step by step, how to contribute to Ansible, and more globally to a lot of open-source projects.  For those who don't quite know what Ansible is, we will start with a refresher; we will then move on to setting up your environment, developing on it, performing your first pull-request and, finally, we'll finish with tips on how to get your request accepted.

We will use throughout the article two of our contributions as examples. The [first issue](https://github.com/ansible/ansible/issues/29886) was on the `oom_killer`option of the `docker_container` module; the [second one](https://issue-link.com) was on <Insert issue here, but maybe not a fix since we already have one>.

## Goals

The main goal of this article is to make you into a good Ansible contributor; however this guide can be used on a lot of other projects too, and especially in regards to the speed at which your pull-requests are merge!

Before we start, we would like to emphasize once more that, like most open-source projects, Ansible is always in need of help from the community to make it better. Everyone is welcome to take part, and the more the merrier! On this note, let's begin!

## Prerequisites

in order to contribute to Ansible, you'll need a few things to get started.

* **python** : Ansible is written in Python so, to ensure compatibility, you'll need different versions. We recommend using *python 2.7* and *python 3.5*.

* **pipenv**: To improve the development lifecycle, we will use [pipenv](https://github.com/kennethreitz/pipenv); however, you are welcome to use other tools such as `virtualenv` and `pip` instead if you are more used to them.

* **GitHub**: Since the project is hosted on GitHub, you'll need to have an account. You can create one for free [here](https://github.com/).

* **git**: GitHub being based on `git`, you'll need to have it installed on your computer. If you are new to git, you can find more information on the [official website](https://git-scm.com/).

* **docker**: Finally, you'll need to install [docker](https://www.docker.com/) in order to create a fully isolated environment setup on which you can run your playbooks. As a matter of fact, some of Ansible's unit and integration tests are partly built on docker.

* **motivation**: Working on an open-source project such as Ansible can be a really fun and rewarding experience. Always remember that it's because of people who, like you, have the motivation to give some of their time for free that the open-source community continues to thrive.

## So what's Ansible?
    
Most of you reading the articles will probably be familiar with Ansible, but a little recap never hurts.

Ansible is a simple IT automation Engine. It is designed to easily configure as many servers as possible with little effort; this makes it the perfect devOps partner for automation, such as CI/CD processes. Ansible also has a wide variety of plugins which enable it to manage about anything in machines such as servers, network devices, storage bays... It's easy to learn, does not need anything installed, and its configuration and playbooks are written in YAML, which is a highly readable data format. The only thing Ansible requires to work is to have python and an SSH server installed on the managed servers, and even then, it can also manage Windows servers with PowerShell, though we will only be using Linux use cases here. Ansible force lies in its capability to easily configure a maximum of devices and the guarantee that the configuration will be constitent with all targets regardless of their initial state. What is its secret? The re-enterability < I don't know what that word means > of Ansible modules! 

---


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

Congrats ! You should be ready now to create your first pull request (PR) on [ansible project](https://github.com/ansible/ansible).

    a . Create a pull request on ansible github project.
You now have pushed your new branch into your fork. The next step is now to create the PR. to do this, let's go to the ansible github
 project page : [https://github.com/ansible/ansible](https://github.com/ansible/ansible). 
You should see a button 'Compare & pull request' on the top of the page :
![Compare & pull request](../_img/contribute-to-ansible/create_merge_request.png)

You simply have to click it (of course) and you'll be able to check if you're not trying to PR unwanted commits or have a look to 
your code to visually check that everything seems ok. You have to double check at this step that you are asking a merge to devel branch.

Once it looks goot for you, click "Create pull request" and, congrats, your request is proposed to ansible community !
Few seconds after created it, the CI will run all the relevant tests againts your new MR while a bot will take care of it and add severals labels regarding your code.
If the CI is correct and pass all the tests, the bot will ping some relevant mainteners to review your PR. For example, if your are trying to fix an issue on a module, 
the bot will ping the module's authors and mainteners. The goal from this point is to obtain two shipit (or LGTM) to have your PR merged, we will treat this in step 4.

    b. understand ansibullbot labels


## step 4 - What's happens next?

Now you have submitted your pull request to the official ansible project,
you may be confronted to two possible cases.

- First, after a code review maintainers can ask you to apply changes in your code.
- Secondly, your changes looks good and you gets two shipit.

Now we want to explain how to deals with these use cases.

#### a. How to integrate modifications to the PR

After a code review maintainers can ask you to apply somes changes in your
developments.

If you wants your work being merged, you have to apply these review comments, it's a sine qua non condition.

So in your local environment apply these changes on the branch related to your pull request.

When you have fix the review comments, you can push your modifications into your fork:

```sh
$ git push origin <your-branch-name>
```

Then, your changes are automaticaly integrated to the already existing pull request. You have just to notify
the comments author to review your changes.

```
@reviewer_name changes applied!
```

If your changes are accepted the reviewer can approuve these by sending a shipit to your pull request.

#### b. Obtain 2 shipit

To get your changes merged in the official project you need to obtains at least 2 `shipit`.

Shipit is a keyword recognized by the ansibulbot.

If your modifications are on a community module the ansibulbot can automaticaly merge your changes
with the official repository source code, else, if your changes are on a core module,
your modifications are merged by a core maintainer and can be rejected by him if something went wrong.

The community is very active, code review and shipit can happen faster than you think.

We recommand you to check periodicaly the status of your merge request.
If your pull request doesn't move forward you can ask module maintainers for a review.

Do not stay inactive and be proactive about your work!

## Conclusion

Ansible is an indispensable tool, used by DevOps, system engineers, and a lot of
teams and projects all around the world. Have deep knownledge on this technology
is a great assets to your career, specialy for DevOps/system jobs.
In addition to that contributing to ansible helps this product to be more efficient
and great!

With this article we have introduced to you on how to become contributors and make 
ansible more understandable.

We hope you liked our article, and do not hesitate to contact us to discuss with us.

## About the authors

#### [Sébastien Boyron (dj4ngo)](https://github.com/dj4ngo)

Lead System engineer at [Squad](https://www.squad.fr/en/)

#### [Hervé Beraud (4383)](https://github.com/4383)

Hervé Beraud have contributed to the ansible project it was also contributor 
on Alpine Linux and somes others projects and stuffs. He's a python addict, and 
DevOps enthusiastic. Also he's specialized on CI/CD workflow, methods,
and best practices on openstack tripleO technologies and he use ansible everyday at works.

He's currenty Lead DevOps Engineer and Python expert at [Squad](https://www.squad.fr/en/).
