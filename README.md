# Week 1 - AWS and Linux

- [Week 1 - AWS and Linux](#week-1---aws-and-linux)
  - [Tools Used](#tools-used)
  - [General](#general)
  - [All about Cloud](#all-about-cloud)
  - [SSH folder and .pem](#ssh-folder-and-pem)
  - [Using AWS](#using-aws)
  - [Using Linux](#using-linux)
  - [Other](#other)

## Tools Used
For this tutorial the following technologies are used:

Virtual Machine related:
* AWS EC2: Creating & Configuring Virtual Machine instance
* Git BASH: Navigating local machine, VM Connection
* BASH: Executing commands in Linux inside VM
* .pem file: Private key for SSH
  
Documentation:
* Microsoft Visual Code: Documentation
* Markdown All in One plugin: Git-MarkDown Style Docmentation 

VM Main Tools:
* Nginx: Web-server
* Maven: Build and run web-server
* Apache2: Reverse Proxying
* MySQL-Server: Database-server

Misc Tools:
* Chat GPT: Naive information gathering, BASH assistance, troubleshooting
* Google Bard: Surface-level information gathering

## General
Tips:
* **NEVER** push any credentials to GitHub, this includes .pem files and .ssh folders - doing so could mean being picked by Amazons vulnerability scanning as well as potential for misuse, incurring danger or financial ramifications
* Use a mix of ```pwd && git status``` in Window's Home Directory and .ssh folder to determine whether the folder is a git repository (which it should not be)
* Be aware of how you configure a VM - these may incur additional costs
* Be wary of Linux's ```rm -rf <targetfile>``` command - this is a force remove and can potentially allow the removal of important files or potentially the whole system when used incorrectly
* Be wary of Linux's ```pkill -9 <pid>``` command - this brute force kill should be minimised and it can potentially cause processes to be orphaned and turned into zombie processes.
* Be careful when copying and pasting commands in a terminal - there is no undo feature and it is a potential attack vector for malicious parties to inject code.
* When using AI, be wary of out-of-date information and potential danger from lack of context.
* When using VMs for automated server running, allow time for commands to be executed - a combination of commands could potentially take up to ~5 minutes.

Commands:
* Ctrl + Shift + P -> Command Menu
* Ctrl + Shift + V -> Preview Markdown
* Git - Shift + Insert -> Paste
* Command Menu -> Create Table of Contents

## All about Cloud
* [Learn Core Cloud Concepts](WhatIsCloud)
* [Learn Basic of AWS](AWS)
* Cloud Architecture

## SSH folder and .pem
* [Learn how to store .pem](StoringSSH)

## Using AWS
* [Learn how to create a VM](CreatingAVM)
* [Starting, Stopping & Terminating VMs](StartStopVM)
* [Connecting to a VM](ConnectingToVM)
* Removing AMIs

## Using Linux
* [Navigation and Basics](Linux)
* [BASH Scripting and Processes](Linux2)
* [File ownership & management](FileOwnership&Management)
* [File transfer & Automating Java App Deployment](Linux3)
* [Reverse Proxying](ReverseProxySetup/README.md)
* [Two-Tier Deployment](TwoTierDeployment/README.md)

## Other
* [Quickstart BASH Scripts](QuickstartBash/README.md)
* Blockers & Troubleshooting