+++
title = "Sympy Documentation Project"
description = ""
tags = [
    "open source",
    "season of docs",
]
date = "2021-05-13"
categories = [
    "proposal",
]
menu = "main"
+++

This is a sample document that illustrates how I audited, developed, and presented a proposal for the Sympy project for the Google Season of Docs 2021 edition

# **SymPy Proposal for Season of Docs 2021**
I want to express my interest in participating in the project named **Documentation Organization - SymPy** that is taking part in the Google Season of Docs 2021. Currently, I am looking for opportunities to contribute and sum up efforts to the open-source software (OSS) community. I think we can be a good fit because of the following reasons. 

A few months ago, I worked with a development team of 15 engineers to define a documentation strategy. This strategy followed a docs-like-code approach where the engineers had specific guidelines to contribute to documentation fostering organization and consistency. Please refer to this [architecture guide](https://sblaizerwize.github.io/docs/architecture/) as a sample document created from this strategy. Besides, in this project, I gained experience working with static websites powered by Hugo. 

As part of my daily role, I am familiar with gathering information from subject matter experts (SMEs) ranging from end-users and stakeholders to developers, data engineers, and solution architects. This experience will be valuable when collecting information from users of the SymPy site to find areas of improvement. 

My proposal consists of five main stages. I provide my estimates in terms of effort (strong, medium, small). Once I have a better understanding of the content, credentials, and dependencies, we can all together establish a timeframe. 

1. **Audit all sources of SimPy documentation (strong)**
2. **Set an organization strategy for documentation (medium)**
In this stage, I will assess [Diátaxis](https://diataxis.fr/) as a documentation system to organize SimPy content into four categories: How-To guides, Tutorials, References, and Explanations. Alternatively, I will evaluate a tagging system used in [mkdocs](https://github.com/jldiaz/mkdocs-plugin-tags) that shows more scalability, particularly when searching documents that can fit into two or more categories. It is important that the proposed organization system is flexible to include new content such as the user guides.
3. **Classify documents based on the chosen organization strategy (strong)**
In this stage, I will organize content into categories complying with the organization strategy. 
4. **Improve the SymPy site user experience (strong)**
In this stage, I will perform a survey introducing questions that can help us understand how end-users navigate, access, and consult the different types of documents of the SymPy site. Then, I will perform analytics to gather insights from the collected data and apply those recommendations to improve the SymPy site. To avoid content disruption of the original SymPy site, I recommend working on a development branch until deploying the last version. If time allows, I will explore if Sphinx can include Google Analytics to track the usability of the SimPy site.
5. **Test Sympy site (medium)**
In this stage, I will perform a final round of tests to assess the final version of the SymPy site. I recommend conducting another survey six months after the last release of the site to collect and compare valuable insights about its usability.  

I am looking forward to contributing to SymPy. Please refer to my resume and portfolio for a more detailed description of my technical writing experience.

**Salomon Marquez**

[Portfolio](https://sblaizerwize.github.io/) | [LinkedIn](https://www.linkedin.com/in/sblaizer/) | [GitHub](https://github.com/sblaizerwize) | [Scholar](https://scholar.google.com.mx/citations?hl=en&user=A91CjSIAAAAJ&view_op=list_works&sortby=pubdate)


---
## **1. What ideas do you have for improving the SymPy documentation organization? and What sorts of challenges do you anticipate for this project and how will you work to overcome them?**

My proposal consists of five main stages. I provide my estimates in terms of effort (strong, medium, small). Once I have a better understanding of the content, credentials, and dependencies, we can all together establish a timeframe. 

1. **Set an organization strategy for documentation (medium effort)**
    * **Ideas**
        - Define the model to organize SymPy documentation. 
        - Create a documentation catalog.
    * **Challenges**
        - Discuss with mentors the best approach to organize information and define the guidelines so that the SymPy community can contribute to the documentation following this approach.
    * **Proposed solutions**
        - Analyze use cases of existing documentation following the [Diátaxis](https://diataxis.fr/) organization system. For example, [Numpy](https://numpy.org/devdocs/) and [Edo](https://edo.readthedocs.io/en/latest/).
        - Compare the [Diátaxis](https://diataxis.fr/) system against other strategies that use a [documentation catalog](https://cloud.google.com/data-catalog/docs#docs).

2. **Audit all sources of SymPy documentation (strong effort)**
    * **Ideas**
        - Audit the four primary sources of information: [SymPy Website](https://sympy.org/), [SymPy Documentation](https://docs.sympy.org/), [SymPy Source Code](https://github.com/sympy/sympy), [SymPy Wiki](https://github.com/sympy/sympy/wiki).
    * **Challenges**
        - Analyze SymPy documentation that includes over 243 .rst files and 576 Wiki pages.
    * **Proposed solutions**
        - Allocate more time to accomplish this stage of the project.

3. **Classify documents based on the chosen organization strategy (medium effort)**

    * **Ideas**
        - Tag documents based on the organization model.
        - Evaluate a tagging system used in [mkdocs](https://github.com/jldiaz/mkdocs-plugin-tags) that shows more scalability, particularly when organizing documents that can fit into two or more categories.
    * **Challenges**
        - Test if Sphinx is compatible with a file tagging system. 
    * **Proposed solutions**
        - Instead of tags, organize the information using folders in the [SymPy doc directory](https://github.com/sympy/sympy/tree/master/doc).  
        - Work on a proof of concept in the Test environment of the SymPy site to implement the file tagging system.

4. **Improve the SymPy site user experience (strong effort)**
    * **Ideas**
        - Perform a survey that can help us understand how end-users interact with the SymPy site.
        - Gather valuable insights from collected data.
        - Update the SymPy site to include the new documentation categories and apply the collected feedback to leverage the accessibility and usability of the site. 
        - Explore if Sphinx can include Google Analytics to track the usability of the SymPy site.
    * **Challenges**
        - Foster the participation of the SymPy community to answer the survey.
        - Update the SymPy site integrating newly organized content and recommendations from the community.
    * **Proposed solutions**
        - Launch the survey using Google Forms because the community is already familiar with using Google groups.
        - Set up the new Test Environment for the SymPy site at the early stages of the project.

5. **Test SymPy site (medium effort)**
    * **Ideas**
        - Test the new SymPy site for readiness, accessibility, and usability.
        - Launch to production the new site.
    * **Challenges**
        - No challenges identified

---
## **2. How would you interact with the SymPy community during Season of Docs?**
I have different points of contact I can use to interact with the SymPy community. 
* I will become part of the community. As an end-user and contributor to [SymPy](https://docs.sympy.org/latest/index.html), I will understand the mechanisms of interaction and logistics underneath making a PR, for example. 
* My approach to a broader audience, such as the SymPy community, will be through the [SymPy Google group](SymPy Google group). Alternatively, I can use other communication channels such as [Gitter](https://gitter.im/sympy/sympy?at=58988c0421d548df2cd2648b). 
* I will plan to have weekly sessions with mentors of the SymPy project to provide updates and check progress.
* I will suggest using an alternative communication channel such as Hangouts or Slack to keep constant communication with mentors. Communication should be straightforward because there is only one hour difference between our time zones.

---
## **3. Finally, we would like to ask if you would prefer to work 10 hours or 20 hours a week for this project.**
I can commit to an average of 10 to 15 hours per week to achieve the goals of this project. 