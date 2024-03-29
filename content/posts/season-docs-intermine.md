+++
title = "Intermine Documentation Project"
description = ""
tags = [
    "open source",
    "season of docs",
]
date = "2020-07-09"
categories = [
    "proposal",
]
menu = "main"
+++

This is a sample document that illustrates how I audited, developed, and presented a proposal for the Intermine project for the Google Season of Docs 2020 edition

# **Welcome to the InterMine Documentation Site**
InterMine is an open source data warehouse build specifically for the integration and analysis of complex biological data. In this site you can find documentation and tutorials to get you up to speed with our brand new platform [**BlueGenes**](http://bluegenes.apps.intermine.org/).

---
{{< columns >}} <!-- begin columns block -->
## **Quick Start**
Learn in 5 min BlueGenes


<---> <!-- magic sparator, between columns -->

## **How-To Guides**
Know BlueGenes Features

<---> <!-- magic sparator, between columns -->

## **Tutorials**
Learn a task in BlueGenes
{{< /columns >}}

---

## **Sample Video Tutorial**

{{< youtube Qm-JRmCbBuA >}}

{{< hint info >}}
**Want to Learn More?**  
Visit our YouTube channel and have access to all our tutorials. 
{{< /hint >}}

---
# **InterMine User Training Docs | Proposal**
## **Overview**
*Provide a brief overview of the project. What problem are you going to solve and how are you going to solve it?*

"InterMine is an open source biological data warehouse, designed to help biologists analyse and query data". Currently, the InterMine platform is undergoing a migration process to a new one named BlueGenes. This new modern interface requires the creation of documentation to encourage new and existing end-users to use it. Based on an audit of the InterMine docs and existing resources, there are several opportunity areas for the new documentation of BlueGenes in terms of accessibility, organization, consistency, and updating. 

The aim of this proposal is to fulfill the documentation requirements of BlueGenes, focusing on a non-technical and semi-technical audience, by following a DocOps strategy. DocOps is a methodology that treats documentation as code fostering a collaborative ecosystem to produce high-quality, centralized, and updated documentation.

The BlueGenes documentation will be delivered in a static site powered by Hugo using GitHub Pages as hosting provider. A central repository will store all documentation related to the site such as how-to guides, tutorials, and media resources. The resources will combine text, screenshots, and videos creating a seamless learning experience for the end-users. Click on this link, to consult an example of a documentation site and a video tutorial for BlueGenes.  

The proposal includes the following sections:
- Statement of the problem. Includes an audit of the current InterMine documentation.
- Implementation plan. Describes the documentation strategy for InterMine.
- Timeline and Milestones. Details the step-by-step process for the implementation plan.
- Deliverables. Lists the documents that can be created. 
- Supporting information. Includes background of the Technical Writer and references that support the proposal.  

---
## **Statement of the Problem**
*State clearly what the problem is. Please use the project requirements as a guide, but do not copy and paste.*

This section describes the current state of the InterMine documentation. The following table lists the opportunity areas after auditing the different sources of documentation.

| **Opportunity Area**      | **Description** |
| ----------- | ----------- |
| Up-to-date docs     | Since the creation of the documentation repository in 2014, scattered efforts for adding and/or updating content have been recorded. Particularly, the content for the tutorials section, which was created in 2016, has not been updated since then. The brand new BlueGenes platform requires updated documentation to increase its usage.        |
| Well-ordered docs   | End-users find it difficult to access relevant information of the InterMine's main features because the documentation is hosted in two different sites. Whereas the [InterMine Documentation site](https://flymine.readthedocs.io/en/latest/) consists of tutorials and exercises, the [InterMine HomePage](http://intermine.org/tutorials) allocates tutorials in a video format along with other useful resources in Python. Documentation must exist in a single site having its own repository.        |
| Consistent content   | The content of tutorials and exercises is composed of different resources such as text, screenshots, and videos. However, not all this content complies with the same template. InterMine documentation site can offer end-users a seamless learning experience. This can be achieved by making the learning resources consistent.         |
| Collaborative docs   | Four people contribute to the InterMine documentation Rachel Lyne, Joshua Heimbach, Calvin Job Puram, and Yo Yehudi (maintainer). However, there are no clear and specific guidelines of how the community of InterMine users can contribute to documentation (a how-to guide to contribute). Besides, the tone, voice, and style of InterMine documentation is not defined. A style guide can foster community interaction with the documentation site to upload, renew, and fix content in a systematic way.        |
| Platform compatibility   | The [InterMine HomePage](http://intermine.org/tutorials) uses Hugo as a static generator whereas the [InterMine Documentation site](https://flymine.readthedocs.io/en/latest/) uses Sphinx. Both sites must use the same infrastructure to ease the creation, collaboration, and maintenance of the InterMine documentation site.        |
| Resources compatibility   | Media resources are hosted on different locations such as YouTube and TechSmith screencast. Besides, the duration and format of the videos is not consistent. Some videos use tag description while others use a voice-over description format. By defining the infrastructure, specific guidelines, and a style guide, all resources can be consistent and user-friendly.        |

---
 ## **Implementation Plan**
*Try to be concise, but do explain your plan thoroughly.*

The implementation plan for this project consists of four stages:

1. **Agreements Stage**
2. **Working Stage**
    - Setting up Infrastructure
    - Documenting the main features of BlueGenes
    - Documenting the main Biology-related topics
    - Documenting Tutorials that cover the main tasks that can be done with BlueGenes.
3. **Closing Stage**
    - Documenting a Product Overview of BlueGenes 
    - Documenting InterMine's Contributors Guide (optional)
4. **Final Stage**
    - Creating Project's Report
    - Completing Mentor's Assessments

**Agreements Stage**\
This stage refines the main goals, tasks, and deliverables of this proposal taking into account the documentation risks. I will start reviewing the opportunity areas for the InterMine documentation with the team. My interest is to foster a very close collaboration with the team and members of the community and identify all sources of information to document. Together, we will settle down the foundations of the project's infrastructure to build and create the docs. 

**Working Stage**\
This stage focuses on setting up the infrastructure of the documentation site and documenting the main features of BlueGenes. I will explore and use the BlueGenes platform by myself with the fresh eyes of an end-user. This will give me the freedom to start documenting the main  features that are already on the production stage. Fig. 1 shows the documentation lifecycle that I will follow.

![DocumentationLifecycle]({{< resource url="/season2020/doc-lifecycle.png" >}})
***Fig. 1 Documentation Lifecycle for InterMine.***\
&nbsp;

**Closing Stage**\
This stage focuses on the creation of a product overview of BlueGenes. Having created all the content of the site, I will produce a getting started section where end-users can get up to speed with the tools that BlueGenes offers. This can be a five-minute tutorial section. As a final deliverable, I will give a demo session to the InterMine's community showing the documentation generated in the static site. If time allows, this stage includes the creation of a How-to guide for contributors. 

**Final Stage**\
This stage includes all paperwork related to the project´s closure. 

---
## **Timeline: Milestones**
*Cover September to December 2020 milestones.*

This section describes the milestones for the project based on the implementation plan. 

**Community bonding	(August 17, 2020 - September 13, 2020)**\
During this stage of the project, I suggest the following activities:
- Get to know InterMine's mentors to foster team collaboration.
- Refine goals, tasks, and deliverables of this proposal. 
- Run an investigation period to define:
    - InterMine's documentation infrastructure
    - Style and tone for the documentation
    - Media style and format


**Doc development (September 14, 2020 - November 30, 2020)**\
The following table describes the milestones and timeline for this proposal. 

{{< rawhtml >}}
<table>
  <tr>
   <td rowspan="2" colspan="3" ><strong>Deliverables and Tasks</strong> 
   </td>
  </tr>
  <tr>
  </tr>
  <tr>
   <td colspan="3" ><strong>1. Setting up documentation infrastructure</strong> [1 week]
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td colspan="2" >Static site infrastructure
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td colspan="2" >Hosting infrastructure for static content such as videos
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td colspan="2" >CI/CD tools (if required)
   </td>
  </tr>
  <tr>
   <td colspan="3" ><strong>2. Documenting BlueGenes main features</strong> [4 weeks]
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td colspan="2" >How-to guide for MyMind Account
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td colspan="2" >How-to guides for searching tools
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>
   </td>
   <td>Keyword Search
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>
   </td>
   <td>Template Search
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>
   </td>
   <td>Query Builder
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>
   </td>
   <td>Region Search 
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>
   </td>
   <td>List Search 
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td colspan="2" >How-to guides for viewing data tools
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>
   </td>
   <td>Report Pages
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>
   </td>
   <td>List Analysis Pages 
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>
   </td>
   <td>Result Tables
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>
   </td>
   <td>Region Search Results
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>
   </td>
   <td>List Analysis Pages
   </td>
  </tr>
  <tr>
   <td colspan="3" ><strong>3. Documenting How-to guides for Biology-related content</strong> [4 weeks]
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td colspan="2" >Gene Ontology
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td colspan="2" >Expression Data
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td colspan="2" >Pathways
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td colspan="2" >Regulatory Data
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td colspan="2" >Orthologues
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td colspan="2" >Interactions
   </td>
  </tr>
  <tr>
   <td colspan="3" ><strong>4. Documenting Tutorials</strong> [3 weeks]
   </td>
  </tr>
  <tr>
   <td colspan="3" ><strong>5. Documenting BlueGene’s Product Overview</strong> [1 week]
   </td>
  </tr>
  <tr>
   <td colspan="3" ><strong>6. Documenting a How-to guide to contribute to InterMine’s documentation (optional)</strong> [1 week]
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td colspan="2" >Define a Style Guide
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td colspan="2" >Create README for the main repository
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td colspan="2" >Integrate VALE as a tool to validate documentation’s style and tone
   </td>
  </tr>
  <tr>
   <td colspan="3" ><strong>7. Work on Final Report</strong> [1 week]
   </td>
  </tr>
  <tr>
   <td colspan="3" ><strong>8. Complete Mentor’s evaluations</strong> [1 week]
   </td>
  </tr>
</table>
{{< /rawhtml >}}

---
## **Deliverables**
*Indicate which deliverables are required and which are optional. Include presentation of your project on the InterMine community call as a deliverable.*

This section lists some of the deliverables included for this proposal. 
- A static site powered by Hugo and hosted in GitHub Pages.
- How-to guides for the main features of BlueGenes.
- How-to guides for the main Biology-related topics.  
- Tutorials that cover the main tasks that can be done with BlueGenes.
- A Product Overview of BlueGenes.
- A how-to guide to contribute to InterMine's documentation (optional).
- A Style Guide for InterMine's documentation (optional).
- VALE as a tool to check the fundamentals of the style guide (optional).

---
 ## **Documentation Risks**
**Assumptions**\
The technical writer assumes the following:
- At least one stakeholder from InterMine must review and approve all deliverable documents.
- Documentation is delivered in a static site generator. 

**Dependencies and Risks**\
The InterMine documentation has the following dependencies and risks:
- Documentation delivery estimates are subject to change based on the scope of the project. 
- Late changes of the scope and requirements can prevent timely delivery of high-quality documentation. 
- Late feedback for documentation in the reviewing process can affect the high-quality and timely delivery of the documentation. 



