# Overview
As part of HEALTHeLINK's continued advancement in areas of technology this page was established to provide a guide of _preferred_ development practices both for internal development teams as well as external development partners that HEALTHeLINK works with for projects. Below are some of the areas in solution development where HEALTHeLINK is attempting to use practices with a goal of creating a consistent approach in developing solutions to allow teams to seamlessly integrate into or work with HEALTHeLINK projects.

*Note the emphasis here is that these are **preferred** practices. Not all systems will meet these guidelines currently and there are always exceptions to the rule. However, meeting these guidelines should be the aim when developing new projects and during any technical debt cleanup phases of existing projects.*

## Source Control
Tracking and managing changes to code is critically important for maintaining technology solutions. When working across teams it also provides a single source of truth as well as establishing a pattern for collaboration. As such, it is preferred to use a Source Control management (SCM) system with the following attributes:

 - Stores source code in distributed system
 - Highly available
 - Allows for branching of repository
 - Provides review/acceptance process
 - Maintains revision history
 - Ability to manage and audit access to individual repositories
 
There are no shortage of SCMs readily available that accomplish these tasks and can be utilized to meet these needs. 

It is also important that repositories are kept separated in a logical fashion that gives the ability to meet all the above criteria as well as monitor and measure changes in each of the systems or sub-systems.

## Branching Strategy
It is important to unify around a strategy for using Source Control. Our strategy is to use a workflow popularized by GitHub, which is called [GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow). 

A few of the most important aspects of this workflow are:

 - Ability of development team to work on code changes or features in isolation
 - Integration of code into a single branch *before* pushing it to acceptance testing environment
 - Incorporation of Pull Request (PR) review and approval process for *code related to a given feature* 
   - Note that this emphasis should imply that PRs are not massive in scope or cross-cutting features. This keeps the PR process from becoming unwieldly and losing its value.

| **Environment** | **Situation**                                                                                                                                              | **PR Required?** |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| local/feature branch| Incomplete changes need to be committed in-progress: store locally and/or commit to a feature branch.                                                                  | No               |
| local/dev/int       | Completed features need integration with ongoing development or current codebase: merge to an 'integration' branch.                                         | No               |
| uat | Completed features have passed integration testing and require promotion user-acceptance testing environment: nerge to ‘uat’ branch.    | Yes              |
| prd | User acceptance testing approved and agreement to promote to production environment: merge to ‘prd’ branch. | Yes              |

Alternatively, for projects that may not fit well with the above workflow, another good resource on branching strategies can be found [here](https://nvie.com/posts/a-successful-git-branching-model/).

## Versioning
It is important to use versions to uniquely identify software change sets that are delivered or planned for delivery. This also helps teams unify in discussion of projects without having to adopt confusing nomenclature surrounding release of software. 

Our guidelines for versioning are as follows:

 - **Be consistent**
 - Create release notes whenever version numbers are changed
 - Never re-use the same identifier for two distinct versions
 - Choose an identifier which has a logical sequence pattern so non-technical user can understand what order versions belong in

HEALTHeLINK is using the [semantic versioning scheme](https://semver.org/) wherever possible. Key features being:
 - Given a version number following the {MAJOR}.{MINOR}.{PATCH} scheme, here are the situations for incrementing each:
   -   {MAJOR} - incompatible API changes are made
   -   {MINOR} - functionality is added with backwards compatibility in mind
   -   {PATCH} - backwards-compatible bug fixes are added

## Development Pipeline
As we continue to define/refine portions of SDLC it is becoming important to document a development process that teams can strive to have software projects meet. In the future it may become important that we can demonstrate our SDLC is being considered as well. As such, we are outlining a guideline for a common set of actions to be done throughout the dev process. 

 1. On/at merge to any defined 'integration' environment, complete following
 
    1.  Code linting
    2. Static code scanning
    3. Pull/merge request approved for environment
    4. Build is created with environment-specifics defined as part of the process
    5. Delivery of build to environment, using environment-specific variables
    6. Execution of pre-defined and repeatable set of unit tests, suitable for the environment
     
2. On/at merge to 'production' environment, complete following
   1. All steps from previous environments were completed and approval was provided to move to production
   2. Pull/merge request approved for environment
   3. Delivery of build to environment, using environment-specific variables
   4. Execution of pre-defined and repeatable set of acceptance tests, suitable for the environment

For all the above actions, it is preferred that each is automated and integrated as seamlessly as possible into the development workflow. The goal is to reap the value of each of these processes while integrating them as efficiently as can be.

## Code Reviews
As part of the Pull Request (PR) process, all commits should be reviewed by team members and approved before they can be merged. This is an effort to get “another set of eyes” on code to encourage collaboration such that it may lead to improved software if others lend their experience, domain knowledge, or subject matter expertise to new/changed code. Including other perspectives helps us eliminate blind spots and sheds light on approaches that may not have been considered for accomplishing the task at hand.

To summarize, a good code review has the following elements:

 - An effort to _collaborate_
 - An attempt to _share knowledge_
 - The objective to _improve_ the code delivered

A code review **is not** any of the following:

 - Replacement for good testing paradigms and execution
 - A scoreboard for competition among developers
 - Measure of a developer's productivity
 - Solution to poor design, ineffective project management, or anything else that ails your project

The list below contains suggestions of different elements a code review should consider

 1. Readability a.k.a. ‘Understandability’
 2. Maintainability
 3. Security
 4. Speed/Performance/Efficiency
 5. Documentation
 6. Reliability
 7. Scalability
 8. Reusability
 9. Test Coverage/Quality
 10. Scope

This is not meant to be a comprehensive list and each of these areas can be expanded on. More senior reviewers should strive to help notice bigger picture items or even recognize code that is missing (like error handling, auditing, etc.). For that reason, it is best practice to invite code reviews from others who have varying levels of breadth and depth for the software under review.
