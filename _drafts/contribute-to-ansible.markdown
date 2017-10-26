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
$ pip install -r requirements.txt
```

Ansible come with a lots of development dependencies, you can install all or just a subset
in concordance with your development purpose.

If you work on documentation all development dependencies are presents in `./docsite_requirements.txt`.
```sh
$ pip install -r ./docsite_requirements.txt
```

To working on bugfix, tests, or new features you need to install specific requirements:
```sh
$ # minimal subset of requirements to install
$ pip install -r ./test/runner/requirements/units.txt
$ pip install -r ./test/runner/requirements/integration.txt
$ pip install -r ./test/runner/requirements/coverage.txt
$ pip install -r ./test/runner/requirements/constraints.txt
$ pip install -r ./test/runner/requirements/ansible-test.txt
$ pip install -r ./test/runner/requirements/sanity.txt
```

#### c. Setup your docker environment
    c. Créer des hotes à configurer (docker)

## Step 2 - Take action!
    a. find issue on ansible
    b. apply coding best practices
    http://docs.ansible.com/ansible/latest/community.html#for-current-and-prospective-developers
    c. test
    http://docs.ansible.com/ansible/latest/dev_guide/testing.html
    d. Git : rebase, cherry-pick, squash, --amend
    e. push on your github repository

## Step 3 - Make a pull request
    a . create PR in github
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
