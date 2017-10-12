# How to contribute on Ansible project

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

    A la recherche de volontaires,
    montée en compétence sur le sujet
    pouvoir corriger d'éventuels bugs
    rajouter des modules ou plugins

## Step 1 - Prepare environment
    a. Récupérer les sources
        . Forker le projet
        . checkouter en local
        . configurer l'upstream (avec comment update le fork)
        . se placer sur la bonne branche

    b. Créer un environnement python (pyvenv)
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
    a. How to integrate modifications to the PR
    b. obtain 2 shipit

    Git
    Github

## Conclusion
