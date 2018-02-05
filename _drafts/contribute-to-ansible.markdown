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

Ansible has several competitors like [Chef](https://www.chef.io/chef/), [Puppet](https://puppet.com/), [Saltstack](https://saltstack.com/), [Fabric](https://fabric.io) and other; we chose it because of its ease of use and agentless-ness. It is coded entirely in python, which is a language we appreciate and, on top of that, we use it everyday at work and are very satisfied with it. 

*"Now, that sounds great buy where's the catch?"* you may wonder. Ansible is open-source, with a growing community and very easy to use, so you'll probably gain time in the long run by investing in learning how to use it; it is also completely free (you can have some support on some modules for prefessional use cases).


#### Back to the basics :

Before we begin, let's define a few technical terms:
  - Ansible is executed on a host server called the `controller`
  - Ansible manages servers/devices called `managed nodes`.
For a more comprehensive glossary, you can check out the [full official one](http://docs.ansible.com/ansible/latest/glossary.html).

Ansible uses an [inventory](http://docs.ansible.com/ansible/latest/intro_inventory.html), which defined information about the accessed nodes in one or more YAML files. It is used to make SSH connections to manage the nodes. You can choose to either use password or key authentication and are able to elevate your privileges on the managed node with su, sudo, or [similar tools](http://docs.ansible.com/ansible/latest/become.html). You can even use an SSH bastion by added ssh args variables or an already configured `ssh_config` file. This should allow you to connect in almost any situation.

To specify the operations to perform on the managed nodes, you will need to write a playbook, once again in YAML fomat. You can find extensive documentation on writing playbooks [here](http://docs.ansible.com/ansible/latest/playbooks.html). To avoid duplicating roles and allow for more flexibility, we stronly recommend that you use [playbook roles](http://docs.ansible.com/ansible/latest/playbooks_roles.html); wel also suggest that you take a moment to read the [best practices](http://docs.ansible.com/ansible/latest/playbooks_best_practices.html) on how to organize your Ansible directory.

If you still want more information, you can check out [how Ansible works](https://www.ansible.com/how-ansible-works), or have a look at the [official website](https://www.ansible.com/) to find more resources, such as the well-written and up-to-date [official documentation](http://docs.ansible.com/ansible/latest/index.html). This should give you a much better idea of what Ansible is and how you can use it to make your daily work easier.

## Why contribute?

Ansible is being used more and more in industry, so there are a lot of issues being opened. The issues can be a feature request, a bug report or even simply a question to the maintenance team. Contributors are still needed to improve the quality and stability of the project even now. 

The project is open-source and maintained by RedHat, so there are two kinds of contributors:
- the majority of contributors are volunteers and use their free time to work on Ansible
- the rest are member are the core team, and they are considered as *commiters*.

You can contribute by enhancing the documentation, migrating code, fixing issues or even adding features. All contributions are welcome! Not only will contributing improve your skills on Ansible, but also your ability to work in big teams, spread all over the world; moreover, your commits can be used in interviews as examples of your work. If you are not familiar with git yet, keep in mind that learning to use it well can be extremely useful as it is in use in most big companies today; if your company is not using it, it is also an opportunity to show you rproactivity and push them to start using it.

Working on this project allowed us to learn how to use it in depth. We discovered new use cases, new modules and other things by diving deep inside the code.

To contribute, keep in mind that you'll need to follow [guidelines](http://docs.ansible.com/ansible/latest/community.html#contributing-code-features-or-bugfixes), which are put in place to help developers follow a similar programming style and keep the code uniform and easy to read. if you have any questions, you can ask the community, which will be a good way to meet new people with similar interests.

Before getting started, we highly recommend to read the [official development documentation](http://docs.ansible.com/ansible/dev_guide/testing.html), guides on [how to develop modules](http://docs.ansible.com/ansible/dev_guide/developing_modules.html) and [how to test your work](http://docs.ansible.com/ansible/dev_guide/testing.html) alongside the main guidelines.

Once you know more about how to develop on Ansible, you'll want to find issues, either from the [issue list](https://github.com/ansible/ansible/issues) on the project page, or through the [topics list](https://github.com/ansible/ansible/projects). Once you know what you're going to work on, you'll have to [fork](https://help.github.com/articles/about-forks/) the project and, once you think you're done with the programming part, you'll have to create a [pull request](https://help.github.com/articles/using-pull-requests). Those concepts are important because they come back time and time again when working on very large scale project.

Finally, if you want to contact the community, you can use the following:
- [IRC channels](http://docs.ansible.com/ansible/latest/community.html#irc-channel)
- [IRC meetings](http://docs.ansible.com/ansible/latest/community.html#irc-meetings)
- [mailing list](http://docs.ansible.com/ansible/latest/community.html#mailing-list-information)

And now, it's time to get contributin'!



## Step 1 - Preparing environment

#### a. Forking the project

To start working on the project, you'll need to fork it. To do so, go to the [ansible official GitHub page](https://github.com/ansible/ansible) and click on the fork button.

![Fork ansible]({{ "/assets/contribute-to-ansible/fork-ansible.png" | absolute_url }})

A few moments later, your fork should appear in your github account.

![Now ansible was forked]({{ "/assets/contribute-to-ansible/forked.png" | absolute_url }})

#### b. Setting up your git environment

You can now setup your local environment. First, you'll need to set up your git workspace. To do so, and if possible, open your git shell. If you are on Linux or MacOS, simply open a terminal; on Windows, you'll have to start an executable.

```sh
$ # setup your identity
$ git config --global user.name "<your name>"
$ git config --global user.email "<your-email@example.com>"
$ # setup pushing method
$ git config --global push.default current
```

Now, clone the fork on your computer and get on the right branch. To make things easier, you may consider having a folder where you clone all your git projects.

```sh
$ git clone https://github.com/<your-github-account>/ansible
$ cd ansible
$ git checkout devel
```


To make sure you stay up-to-date, you'll want to configure your clone to be able to receive updates from the project. Keep in mind that, from now on, we may refer to the remote or your fork as `origin`, and the remote of the official project as `upstream`.

```sh
$ git remote add upstream https://github.com/ansible/ansible
$ # check remotes
$ git remote -v
origin  https://github.com/<your-github-username>/ansible (fetch)
origin  https://github.com/<your-github-username>/ansible (push)
upstream        https://github.com/ansible/ansible (fetch)
upstream        https://github.com/ansible/ansible (push)
```

Now that the upstream is set up, if you ever need to synchronize your clone with the upstream, you'll just have to do the following:

```sh
$ git fetch upstream
...
$ git merge upstream/devel
```

Don't forget after a synchronisation to update your fork!

```sh
$ git push origin devel
```

There you go! The project is now ready to be worked on on your computer!

#### c. Setup your python environment

Since Ansible is written in python, you'll need to setup a python working environment. Though we will use `pipenv`, you are welcome to use any python environment manager you are most confortable with.

First, setup the environment itself:

```sh
$ pipenv --python 3.5 # replace python version for python 2.7
$ pipenv shell
$ # your now in your python virtual environment
```

Now source, source the ansible context:
```sh
$ source hacking/env-setup
```

Install base dependencies:
```sh
$ pipenv install -r requirements.txt
```

Ansible comes with a lot of development dependencies, you can install all of them or just a subset depending on what you're working on. For instance, if you're working on the documentation, all development dependencies are present in `./docsite_requirements.txt`.

```sh
$ pipenv install -r ./docsite_requirements.txt
```
On the other hand, if you're working on bugfixes, tests or new features, you'll need to install specific dependencies:
```sh
$ # minimal subset of requirements to install
$ pipenv install -r ./test/runner/requirements/units.txt
$ pipenv install -r ./test/runner/requirements/integration.txt
$ pipenv install -r ./test/runner/requirements/coverage.txt
$ pipenv install -r ./test/runner/requirements/constraints.txt
$ pipenv install -r ./test/runner/requirements/ansible-test.txt
$ pipenv install -r ./test/runner/requirements/sanity.txt
```

Your python environment is now fully setup and ready for work; all that is left to prepare is docker.

#### d. Setup your docker environment
    d. Créer des hotes à configurer (docker)

## Step 2 - Getting to work!

#### a. Find issues on ansible

Now that your environment is fully operational, it's time to get to work! First, you'll need to find a subject to work on. Ansible has an [issue tracker](https://github.com/ansible/ansible/issues), so you'll want to go there to find something to work on. If you are new to Ansible and Python, we recommend that you begin with bugfixes as it's easier a problem to resolve than outright writing new features. Thankfully, the issue tracker comes with labels which allow you to filter easier problems, with the `easyfix` label, for instance.

So! [go to the issues tracker and search jobs](https://github.com/ansible/ansible/issues)!

![Ansible issues tracker]({{ "/assets/contribute-to-ansible/ansible-issues-tracker.png" | absolute_url }})

The labels also allow you to select certain subjects or types of issue you might prefer to work on. Here's an example :

You want to work on the Docker features of Ansible. You can use labels to find existing issues for bugs or features on that subject. Simply apply the filter to your search and you'll get all the features related to Docker on Ansible.

![Ansible filter issues by labels]({{ "/assets/contribute-to-ansible/ansible-filter-by-labels.png" | absolute_url }})

We strongly advice that you play around with the filter system to get acquainted with it; the more you're interested in an issue, the easeir it'll be to get it resolved!


#### b. Working on your issue

You did it! You finally have an environment to work on, and an issue to resolve! You can finally get yours hands dirty.

Since your environment is already set up, the process to start your work will be pretty straightforward. You first need to get the code you're going to work on. In the Ansible project, the default git branch is `devel`, which corresponds to the latest version of the product. Ansible requires that you work on this branch to create new local feature branches; the backports, which is the porting a feature from the `devel` branch to other branches, is done by the core team. 

Say you want to fix a bug on the docker module; the workflow will look like this:
```sh
$ git checkout devel
$ git checkout -b fix-docker-module
```

You are now on your new branche, `fix-docker-module`. You can directly begin to try and resolve your bug.

Note that patches should always be done using the `devel` branch, since backporting is done afterwards. For more information, you can read the
[official ansible contributing guide](http://docs.ansible.com/ansible/latest/community.html#contributing-code-features-or-bugfixes).


#### c. Coding in style

Because it is maintained by a lot of people, Ansible needs development guidelines to ensure project quality, stability and maintainability. The Ansible aesthetic encourages simple, readable code with consistent, conservatively extending, backwards-compatible improvements. When contributing, please observe the following guidelines:

- All code developed for Ansible needs to support both Python2-2.6 and higher, and Python3-3.5 and higher,
- Indentation should be done with 4 spaces; no tabs allowed,
- The Ansible team does not enforce an 80-column limit, but you should keep it under 160 columns,
- The Ansible team does not accept `style only` pull requests, unless the code is nearly unreadable,
- Ansible is not strictly compliant with [PEP8](https://www.python.org/dev/peps/pep-0008/), but it does not hurt to follow them.

For more information about coding guidelines, feel free to visit their [dedicated page](http://docs.ansible.com/ansible/latest/community.html#for-current-and-prospective-developers).

#### d. Testing your work

Ansible comes in *battery included*, which means that it comes with a lot of features, including some that are very useful during development. Among those features, you'll find a full test suite that helps you make sure you did not introduce bugs or broke things while contributing. It is necessary that you write those tests, and you are ecouraged to add some if they lack, before creating a pull request. Note that adding tests does not need a specific issue for that, so feel free to add it directly in your commit ; it can only help make sure Ansibl stays stable down the line.

The tests are automatically launched during the Continuous Integration (CI) step of the upstream projectn, therefore it's strongly recommended that you run them beforehand on your local environment to make sure it will pass so that it does not get rejected by the CI Bot (ansibulbot) or the maintainers.

There are 4 types of tests:
- [compilation testing](http://docs.ansible.com/ansible/latest/dev_guide/testing_compile.html): tests the Python code against a variety of Python versions.
- [unit testing](http://docs.ansible.com/ansible/latest/dev_guide/testing_units.html): tests directly against individual parts of the code base.
- [sanity testing](http://docs.ansible.com/ansible/latest/dev_guide/testing_sanity.html): tests the code against Ansible's coding standards and requirements.
- [integration testing](http://docs.ansible.com/ansible/latest/dev_guide/testing_integration.html): functional tests of modules and Ansible core functionality.

In this guide we will only focus on sanity and unit testing since the other types are not usually run for basic contributions; if you tackle more important issues however, you will be required to run all tests. 

Unit testing test features to determine whether their function as such; if the tests fail, the you can easily figure out where the problem comes from and fix it. On the other hand, sanity check on the other hand only makes sure that your code follows the development guidelines described earlier in the article. 

Once you're done working, to run the tests all you need to do is use the ` ansible-test` command:

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
Further information on testing can be found in the [official documentation](http://docs.ansible.com/ansible/latest/dev_guide/testing.html).

Testing will prevent regression in your implementation, but the quality of the Ansible project is also due to the fact that the contributors take care to paintina  proper Version Control History.



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
