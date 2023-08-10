---
title: Automating Linux Installation Using Ansible - Part One - Code Creation
date: 2023-08-10
categories: [Automation, Ansible]
tags: [ansible, automation, os install, linux, project-write up]     # TAG names should always be lowercase
---

# Introduction
This is the next in the series about how I set up my Windows/Linux dual-booted machine.

To download and install the software needed for the Linux side of this project a piece of automation software called Ansible was used. 

This blog post will talk on the basics of Ansible and give an explanation of the code used.


## What is Ansible?
For some background, Ansible is an automation tool that can help automate installation, configuration, provisioning and more for most manual IT processes.

It is useful when you need to make environments with the same setup every time, for example when setting up multiple computers on a domain, or when you're using virtual machines.

With the basic setup being automated you can fine-tune what happens every time and no steps are skipped, resulting in fewer errors, and can improve the overall security of your system.

# Explain what you'll need to do beforehand
*If you're used to Ansible and know how to use it then you can skip ahead past this section*

If you've never used Ansible before then there are a couple of requirements before you can start.

The first is having an account for an online code repository where you can store your code in and sync to a piece of software called Git, in this instance Github was the one chosen, while the repositories (Often called repos for short) that were used to assist in this project are hosted on GitLab.

You will also need to have some sort of coding environment set up to follow along as well, this is a setup that allows you to make your code.

## Git
Git is a piece of software used for version controlling your code, this makes it easy to save your work as well as for dealing with any errors that come up.

For more detail on how to use Git and Github as well as how to set them up then please check out [this tutorial](https://www.freecodecamp.org/news/introduction-to-git-and-github/).

## Coding Environment
The coding environment that was used for this project was Visual Studio Code, it was used due to it being comfortable and versatile to use.


For more detail on how to set up a coding environment in general, please check out [this tutorial to set up VSCode](https://code.visualstudio.com/Docs/setup/setup-overview).

After it has been set up, download Ansible onto it [following this guide](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).


# Ansible Code Breakdown
This section will cover the code that was created for the project and give explantions along the way.

The code that was created for this project can be found [at this repository](https://github.com/Asuna-Cross/laptop-config).

## Basic Structure
The first two files made were `playbook.yml` and `ansible.cfg`.

### ansible.cfg
This file was required due to the project using collections and roles. For projects that don't use either of these then this file can be skipped.

```ini
[defaults]
# Installs collections into [current dir]/ansible_collections/namespace/collection_name
collections_paths = ./

# Installs roles into [current dir]/roles/namespace.rolename
roles_path = ./roles
```

The purpose of this file is to set the default paths in the repository that any collections and roles downloaded will be placed into.

For a more advanced breakdown of the ansible.cfg file and what it is capable of [the docs for it can be found here](https://docs.ansible.com/archive/ansible/2.4/intro_configuration.html).

### Tasks
Ansible works by splitting everything up into "tasks", it is what it says on the tin. It is a task for Ansible to do.

The following is an example of a task (From the tasks in [this role](https://gitlab.com/johnroberts/ansiblerole-gui-tools/-/blob/master/tasks/main.yml?ref_type=heads))

```yaml
- name: Install Audacity
  become: true
  ansible.builtin.package:
    state: present
    pkg: audacity
  when: install_audacity
```

The name is the name that is displayed when the role is being performed, and the "when" indicates how to reference it to make it happen, the "when" is not always needed, however due to how this project is set up as variables, this is needed.

`become: true` references the need to needing to have admin permissions to do the task.

`ansible.builtin.package` this is a module from Ansible it looks up for the package manager and installs the package that is asked for.

So in the above example, the task is to go to the package manager of the system that it is on and look to see if audacity is there and install it.

*Note: .package is a more generalised form of package manager, if the system being setup uses apt packages then the command can be switched to `ansible.builtin.apt`, however this is more specalised compared to `ansible.builtin.package`.*

### playbook.yml
The tasks are gathered up and together they form the playbook. This is the file that is ran and holds all of the instructions over what Ansible is to run.

For more detailed information about Ansible playbooks, [this is an introduction from Ansible themselves](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_intro.html).

### Roles
Roles are a collection of tasks that can be toggled on and off through variables in the playbook. These are used when a set of tasks can be reused for multiple projects and can reduce programming time when it comes to building multiple sets of systems that have common ground.

This project uses two external roles, [gui-tools](https://gitlab.com/johnroberts/ansiblerole-gui-tools.git) which is responsible for installing all tools that have a graphical user interface (GUI) and [cli-tools](https://gitlab.com/johnroberts/ansiblerole-cli-tools.git), which is responsible for installing all tools that operate on the command line.

## Download the role requirements
To begin with the roles, two folders called `roles` and `ansible_collections` were created. Inside these there were two files, `.gitignore` and `requirements.yml`.

### .gitignore
This file tells Git to ignore files and folders when it tracks. In this case it was told the following for both of the folders.

```
#Ignore Everything
/*
#Apart from these two, we need these
!.gitignore
!requirements.yml
```

As can be seen with the comments, the `/*` indicated for git to ignore tracking everything in that folder.

The `!` gives an exception and tells git to include the files after them.

### requirements.yml
This file contains where to find and download the required roles and collections for the project to work. In this case the code looks like the following.

**For the ansible-collections**
```yaml
---
collections:
  - name: community.general
```
This points towards a collection on [Ansible's website](https://docs.ansible.com/collections.html).

**For the roles**
```yaml
---
- src: https://gitlab.com/johnroberts/ansiblerole-gui-tools.git
  scm: git
  version: master
  name: gui-tools

- src: https://gitlab.com/johnroberts/ansiblerole-cli-tools.git
  scm: git
  version: master
  name: cli-tools
```

What this is doing is going to the links provided and pulling down both of these roles with the names given to them in the folder. The version is choosing which branch to pick from as well so there is more control here.

As this project uses the most recent versions, the "master" branch was used.

*Note: In some places the Master branch is being phased out and replaced by the "main" branch, be sure to check the branch before downloading*

### Downloading the requirements
To download the required roles and collections after the files above have been set up, open up a terminal in the coding environment. Make sure that the terminal is in the folder that holds the main repository for this project then type the following commands.
```bash
ansible-galaxy role install -r roles/requirements.yml
ansible-galaxy collection install -r ansible_collections/requirements.yml
```
These will reference back to both of the requirements files and from there download all the files onto the computer that the command was executed on.

## Using the Roles Variables
After the roles are set up and downloaded the main playbook.yml can be modified.

An example of how this is done is as follows
```yaml
---
- name: Mass Install
  hosts: all
  roles:
    - gui-tools
  vars:
    - install_bitwarden: true
```

Similar to the tasks above, except there are a few changes.

`hosts: all` makes reference to which users that these changes should be made to, in this case it is pointing towards every user as this is a laptop installation.

`roles` this is in reference to the roles downloaded above, it is named with the name picked for the roles when stating that they were required.

`vars` this is for the variables that can be toggled on and off, in both of the roles used in this project there is a master list with all of the variables that can be changed in the "defaults" folder. Referencing that list, the roles to be turned on were copied into the main playbook and turned to true.

*Note: There was one change that had to be done, for some of the software the exact version of Linux had to be mentioned, however due to Mint not following the same names as Ubuntu there had to be changes to say which release it was based off of*

# Ending Notes
With all of this saved and completed it is time to put this onto the laptop and run it, that will be covered in the next blog post.

As for this, it was fun getting to know Ansible and all of the things that it is capable of, it's a tool I can see myself using quite a lot and I'm grateful for being given the chance to learn.

If you wish to see a repo that handles Ansible in both a machine set up like the use this one is for, or in conjunction with something such as Vagrant, check out [this VM base box](https://gitlab.com/johnroberts/vm-base) from the same creator who made both of the roles used in this project.
