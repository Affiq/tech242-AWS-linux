# Week 1 - AWS and Linux

- [Week 1 - AWS and Linux](#week-1---aws-and-linux)
  - [Tools Used](#tools-used)
  - [General](#general)
  - [All about Cloud](#all-about-cloud)
  - [SSH folder and .pem](#ssh-folder-and-pem)
  - [Using AWS](#using-aws)
  - [Using Linux](#using-linux)

## Tools Used
For this tutorial the following technologies are used:
* Microsoft Visual Code: Documentation
* Markdown All in One plugin: Git-MarkDown Style Docmentation 
* AWS EC2: Creating & Configuring Virtual Machine instance
* Git BASH: Navigating local machine, VM Connection
* BASH: Executing commands in Linux inside VM
* Chat GPT: Surface-level information gathering
* Google Bard: Surface-level information gathering

## General
Tips:
* **NEVER** push any credentials to GitHub, this includes .pem files and .ssh folders - doing so could mean being picked by Amazons vulnerability scanning as well as potential for misuse, incurring danger or financial ramifications
* Be aware of how you configure a VM - these may incur additional costs
* Be wary of Linux's ```rm -rf <targetfile>``` command - this is a force remove and can potentially allow the removal of important files or potentially the whole system when used incorrectly
* Be wary of Linux's ```pkill -9 <pid>``` command - this brute force kill should be minimised and it can potentially cause processes to be orphaned and turned into zombie processes.
* Be careful when copying and pasting commands in a terminal - there is no undo feature and it is a potential attack vector for malicious parties to inject code.

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
* Starting and Stopping Virtual Machines
* Connecting to a Virtual Machine
* Changes in Local IP Address

## Using Linux
* [Linux navigation commands](Linux)
* [Linux process commands](Linux2)
* [File ownership & management](FileOwnership&Management)
