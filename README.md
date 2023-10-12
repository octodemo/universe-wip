<h1 align="center">Harnessing AI: Next Level Strategies for Advanced Security</h1>
<h5 align="center">@s-samadi</h3>
<h5 align="center">@abhi-dutta</h3>

<p align="center">
  <a href="#introduction">Introduction</a> •
  <a href="#prerequisites">Prerequisites</a> •
  <a href="#monagallery">Mona Gallery</a> •  
  <a href="#learning-objectives">Learning Objectives</a> •
  <a href="#workshop-guide">Workshop Guide</a> •
  <a href="#learning-resources">Learning Resources</a>
</p>



### Introduction

This repository template contains the source code for the `Mona Gallery` vulnerable application and also step by step guidance on all the exercises that we are going to walk through in todays workshop.

### Prerequisites

Please make sure that you have all the prerequisites in place before we start of the wokshop

1) The mona-gallery repo is imported as a new repository under the [githubuniverseworkshops](https://github.com/githubuniverseworkshops) that you have been given access to
2) Make sure that you have created a codespace from the repository that you just imported (the codespace should have been automatically created )
3) Make sure that you have the GitHub Copilot, GitHub Copilot Chat & GitHub Copilot Lab plugins are pre installed intalled in the Visual Studio Code IDE in your codespace
4) Configure the plugin to grant you access to GitHub copilot through the [githubuniverseworkshops](https://github.com/githubuniverseworkshops) Org that you have been granted access to


### Monagallery

The Mona Gallery is a an intentional vulnerable application which consists of few most common vulnerable types (sql injection, csrf, deserialization, etc.). The application code is written in a multitude of technology (Go, Python, TypeScript, Java). The reference architecture of the application is shown below. We will use this application to run through the different workshop use cases like secret scanning, CodeQL analysis, dependency scans. We will see how GitHub Copilot can be used along with the different App Sec offerings from GitHub under it's Advanced Security offering to assist developers and security architects in faster iidentification and remediation of vulnerabilities

![image](https://github.com/octodemo/universe-wip/assets/79184790/34600cdc-5dde-4dc4-9a68-8e31709c1ec0)

### Learning Objectives

In this workshop you would learn:
  - How to use GitHub Copilot to get clean code
  - How to use GitHub Copilot to write regular expressions which will be used in GitHub Advanced Security Decret Scanning feature to identify secrets
  - Use GitHub Copilot to get remediation guidance on how to fix application security vulnerability in your code
  - Use GitHub Copilot to do threat modelling for security architects to get more contextual information about the application
  - How AI is used to auto fix reediation recommendation for codeql vulnerabilities in a Pull Request
  - How GitHub Copilot will be used learn about Application Security and the different types of vulnerabilities in app sec world

### Workshop Guide

Steps to start:

1. Use `githubuniverseworkshops/mona-gallery` repository as a template to create a new GitHub repo under `githubuniverseworkshops` org where you have been granted access to
2. The follow along lab exercies are listed [here](/Exercise.md) 

### Learning Resources

  - [GitHub Advanced Security Learning Path - Microsoft Learn](https://learn.microsoft.com/en-us/collections/rqymc6yw8q5rey)
  - [Docs - GitHub Advanced Security](https://docs.github.com/en/enterprise-cloud@latest/get-started/learning-about-github/about-github-advanced-security)
  - [GitHub Copilot Learning Path - Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/introduction-to-github-copilot/)
  - [Docs - GitHub Copilot](https://docs.github.com/en/copilot)
