---
title: Automating Linux Setup Using Ansible - Part Two - Installation
date: 2023-10-17
categories: [Automation, Ansible]
tags: [ansible, automation, os install, linux, project-write up]     # TAG names should always be lowercase
---

# Introduction
This is a continuation of the previous post regarding how to set up a machine using Ansible.

# Ansible
## First Steps
The first steps to getting the Ansible playbook running are to download git and Ansible onto the target machine.

## Clone Repo
After Ansible is installed it's time to install Git. To do this use the command `apt install git`, this will go out to the apt collection and automatically find and install git.

Due to the repo used being private at the time github had to be authenticated before it could work. See [the github docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
) for futher instructions on how to authenticate using SSH keys.

## Download and Install Ansible Collections
Once the repo has been downloaded it is time to run the same commands as the ones ran to re-download the ansible collections from the last blog post.

For simplicity, here they are again.

```bash
#Install ansible roles + collections
ansible-galaxy install -r roles/requirements.yml
ansible-galaxy collection install -r ansible_collections/requirements.yml
```

## Run the Command to Install
From here run the command

```bash
ansible-playbook -K --connection=local --inventory 127.0.0.1, --limit 127.0.0.1 playbook-localhost.yml
```

### What It's Doing

The following is an explanation of the command above and what each section is used for

- `ansible-playbook` is calling the command that is about to be ran.

- the `-K` is alerting the code that it is required to become root and thus will prompt for the root user password to be entered.

- `--connection=local` indicates that ansible is going to be executing these tasks on the host machine rather than a remote one.

- `--inventory` Ansible allows multiple machines to be provisioned at the same time by using an inventory, this is a list of all machines that the playbook will run on. In this case it's being defined on the command line and is only for this one project, however it can be used as a standalone file, more information on this can be found [in the ansible documents](https://docs.ansible.com/ansible/latest/inventory_guide/index.html).

- Using the IP location of `127.0.0.1` is stating that this is to be ran on the machine that the command originates from. This is commonly known as the "loopback IP"

- `playbook-localhost.yml` is the name of the playbook that's to be used for this installation.

# Conclusion
Overall Ansible cut down a lot of my time when it came to downloading and installing things for my laptop. There wasn't too many hiccups, apart from there being some things that I wasn't able to automate and had to do by hand.

These things that I couldn't change were setting up my internet browser and my keyboard settings. However asides from that I feel like I've just scratched at the surface of what Ansible is capable of and look forward to seeing what else I'm able to do with it.