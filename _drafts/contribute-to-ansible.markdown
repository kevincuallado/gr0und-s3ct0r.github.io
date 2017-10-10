# How to contribute to the ansible project

## Introduction

Because we find Ansible, just awsome, we would like to share our experience about contributing to it. 
We will see, step-by-step, how to contribute to Ansible and generally on a lot of open-source projects. 
We so will begin it by refreshing you on what is Ansible. 
Next we will see four steps, how to set-up your environment, how to develop on it, how to perform your first pull-request and then we will se the best process to have your request accepted. 

## Goals

The goal of this article is, of course, how to become an Ansible contributor, but not only, we will help you to speed up your pull-request merge! 

Ansible is needing help, and of course everyone are welcome! Let's begin!

## Prerequisites
Contribute to ansible needs some prerequisites.

Ansible is written in python so you need to install different versions to ensure compatibility:
- python 2.7
- python 3.5

For improve development lifecycle we strongly encourage you to use [pipenv](https://github.com/kennethreitz/pipenv).
Instead, you can use mainstream tools like `virtualenv` and `pip`.

Ansible project is hosted on github so [you require a github account](https://github.com/) for deal with it.

Github is based on the `git` version control system, so you need to install it.

Ansible tests and integration have parts based on docker.
You'll need to install [docker](https://www.docker.com/) to have a fully isolated development setup to play your playbooks against it.
For information this is an very interesting part of contributions on ansible.

## What's Ansible?
    Principe de fonctionnement
    petit exemple d'installation d'un paquet (liens vers le site officiel de ansible)
    Différencier serveur de client (machine hote ou cible) retrouve rles vrais termes ansible

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
