# Salomon Marquez Site
This repository contains guidelines to produce and contribute to the Salomon Marquez portfolio. It includes documentation samples such as how-to guides, architecture guides, APIs, and proposals. This documentation process follows a [docs-like-code](https://contentmarketinginstitute.com/2015/04/intelligent-content-application-economy/) approach where everyone can contribute to it under defined guidelines. As a result, the documentation is produced and deployed in a static site. Visit the following link to consult the site: https://sblaizerwize.github.io/

## Table of Contents
- [Introduction](#introduction)
  - [Prerequisites](#prerequisites)
  - [Getting Started](#getting-started)
- [Creating New Content](#creating-new-content)  
- [Linting](#linting)
- [Contribution](#contribution)
  - [Coding Conventions](#coding-conventions)
  - [Review Process](#review-process)

---
## Introduction
This site uses GitHub Pages as hosting provider. The documentation strategy integrates CI/CD tools to generate and update content using Hugo as static site generator. The following table details the content of the repository. 

| **Directory** | **Description** |
| ------ | ------ |
| archetypes | Includes content files with preconfigured front matter fields. |
| content | Includes all pages related to the project's documentation. |
| resources | Caches files to speed up site generation. |
| static | Includes static content such as images, audios, videos of the site. |
| styles | Includes VALE linter tools and rules that comply with the Wizeline Style Guide. |
| themes | Includes the style guide template of the DocOps site based on the [Hugo Book Theme](https://themes.gohugo.io/hugo-book/). |
| .gitlab-ci.yml | Specifies the configuration of the CI/CD tools. |
| .vale.ini | Specifies the configuration of VALE linter. |
| README | Includes guidelines and instructions of this repository. |
| config.toml | Specifies the configuration of the static site generator. |

---
### Prerequisites
To upload new content to this repository, you must install on your system the following:

- Install [Visual Studio Code](https://code.visualstudio.com/download)
- Install [Hugo](https://gohugo.io/getting-started/installing/).
If your are installing Hugo on Windows OS, follow the instructions on this [video](https://www.youtube.com/watch?v=G7umPCU-8xc). Then, reboot you computer to apply all changes done in your windows environment variables. 
- Install [Vale](https://errata-ai.gitbook.io/vale/) 

[⇧ back to top](#table-of-contents)

---
### Getting Started
Before producing new or updating existing content for the documentation site, you need to get familiar with the **/content** folder. This directory contains the **docs** and **menu** folders. 

The **docs** folder contains all the documentation of the site. The structure of this folder complies with that of the table of contents (TOC) located at the left menu of the site. The next schema shows the structure of the **docs** folder: 

```
.
├── docs
│   ├── apis
│   ├── architecture
│   ├── howto
│   └── season2020
└── menu
```

On the other hand, the **menu** folder contains a `_index.md` file that provides the skeleton of the TOC. This file links the TOC with their respective page content located in the **docs** folder. 

---
## Creating New Content 
To create new content for the documentation site, follow the next steps. 

**Generate Content**
To generate new content. 

1. Clone this repository. 
2. Navigate into the **content/docs** folder.
3. Create a new subdirectory and name it according to its content. 
- In the subdirectory, create a new `_index.md` file.
- In the `_index.md` file include the following header:
```
---
title: <section-title>
type: docs
weight: 1
---
```
- In the body of the `_index.md` file, write down your new content in markdown format.
4. Save all changes.  

**Link Content**
To link newly generated content. 

1. Navigate to the **content/menu** folder. 
2. Create a new link to the content that you generated in the [Creating New Content](#creating-new-content) section:
```
  - [<Menu-Title>]({{< relref "/docs/<subfolder>" >}})
```
3. Save all changes. 

**Validate Content**
To validate newly generated content. 

1. Navigate into the main folder of the project from your terminal.
2. Run the following code:
```
hugo serve
```
3. Open a new  window or tab in a browser. The Hugo web server is available at http://localhost:1313/DocOps/. 

**Check Style and Typos**
To check format issues and typos of your documentation, run vale from your terminal:

```
vale content/docs/subdirectory/_index.md 
```

**Note**: Vale linter is only available for reviewing text in English.

[⇧ back to top](#table-of-contents)

---
## Linting
Vale is a linter that allows you to check syntaxis, typos, and grammatical rules in English before making a PR. To upload new documentation to the site, you must run Vale linter. Use this tool to create clear, consistent, and concise documentation. 

[⇧ back to top](#table-of-contents)

---
## Contribution
Consult the following coding conventions and reviewing guidelines to contribute to the site. 

---
### Coding Conventions
To create a new branch follow the next code convention.
New branch: `docs/<task-to-be-done>`
Example: `docs/update-readme`

To create a pull request follow the next code conventions:
- `feat: task done`  
Indicates a new feature for the user, not for a built script.
- `fix: task done`  
Indicates a bug fix for the user, not for a built script.
- `docs: task done`  
Indicates changes to the documentation. 
- `style: task done`  
Indicates style changes such as formatting, and fixing missing semicolons. It does not indicate a production code change.
- `refactor: task done`  
Specifies a refactoring of production code, eg. renaming a variable.
- `test: task done`  
Includes missing tests, refactoring tests, etc. It does not indicate a production code change.
- `chore: task done`  
Indicates an updating of grunt tasks for example. It does not indicate a production code change.

Example: `docs: added glossary term` 

[⇧ back to top](#table-of-contents)

---
### Reviewing Process
To simplify the reviewing process, respond the following questions that best describe your PR. Then, include your answers in your Merge Request (MR) message. 

- What does this PR do?
- Where should the reviewer start?
- How should this be manually tested?
- Any background context you want to provide?
- Screenshots (if appropriate)
- Questions

[⇧ back to top](#table-of-contents)

