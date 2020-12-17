# Aws-workshop-template

This project allows you to scaffold a workshop using a AWS-styled Hugo theme similar to those available at [lunar-lander.workshop.aws](https://lunar-lander.workshop.aws/), and [eksworkshop.com](https://eksworkshop.com/)


## Important note on workshop creation, review, and hosting

All workshops should be submitted to the [Tech Content 2.0 process](https://w.amazon.com/bin/view/AWS_Technical_Content/aws-tech-content-sim-dashboard/content-creation-plan/#H2.ReviewDomainPortals). This enables centralised tracking and review of content. Once your Tech Content review is complete, you can host your workshop using the workshop.aws publication+hosting mechanism. The Tech Content team will submit the tickets for hosting and publication.

You should not host a workshop under your own domain, nor should you host workshops in AWS accounts marked as 'invidivual use' - these actions can result in Sev2 security incidents.


## Repo structure

```bash
.
├── metadata.yml                      <-- Metadata file with descriptive information about the workshop
├── README.md                         <-- This instructions file
├── deck                              <-- Directory for presentation deck
├── resources                         <-- Directory for workshop resources
│   ├── code                          <-- Directory for workshop modules code
│   ├── policies                      <-- Directory for workshop modules IAM Roles and Policies
│   └── templates                     <-- Directory for workshop modules CloudFormation templates
└── workshop                          
    ├── config.toml                   <-- Hugo configuration file for the workshop website
    └── content                       <-- Markdown files for pages/steps in workshop
    └── static                        <-- Any static assets to be hosted alongside the workshop (ie. images, scripts, documents, etc)
    └── themes                        <-- AWS Style Hugo Theme (Do not edit!)
```

## What's Included

This project the following folders:

* `deck`: **UNUSED RIGHT NOW** Future location to store your presentation materials. For now, you should store them centrally in a system like KnowledgeMine or Wisdom. 
* `resources`:  **UNUSED RIGHT NOW** Store any example code, IAM policies, or Cloudformation templates needed by your workshop here.
* `workshop`: This is the core workshop folder. This is generated as HTML and hosted for presentation for customers.


## Requirements

1. [Clone this repository](https://help.github.com/articles/fork-a-repo/).
2. [Install Hugo locally](https://gohugo.io/overview/quickstart/). As of 1 Mar 2020, the workshop.aws build process uses [Hugo 0.64.1](https://github.com/gohugoio/hugo/releases/tag/v0.64.1)


# Getting Started

## Navigate to the `workshop` directory

All command line directions in this documentation assume you are in the `workshop` directory. Navigate there now, if you aren't there already.

```bash
cd my-first-workshop/workshop
```

## Create your first chapter page

Chapters are pages that contain other child pages. It has a special layout style and usually just contains a _brief abstract_ of the section.

```markdown
Discover what this template is all about and the core concepts behind it.
```

This template provides archetypes to create skeletons for your workshop. Begin by creating your first chapter page with the following command

```bash
cd workshop
hugo new --kind chapter intro/_index.en.md
```

By opening the given file, you should see the property `chapter=true` on top, meaning this page is a _chapter_.

By default all chapters and pages are created as a draft. If you want to render these pages, remove the property `draft = true` from the metadata.

## Create your first content pages

Then, create content pages inside the previously created chapter. Here are two ways to create content in the chapter:

```bash
hugo new intro/first-content.en.md
hugo new intro/second-content/_index.en.md
```

Feel free to edit thoses files by adding some sample content and replacing the `title` value in the beginning of the files. 

## Launching the website locally

Launch by using the following command:

```bash
hugo serve
```

Go to `http://localhost:1313`

You should notice three things:

1. You have a left-side **Intro** menu, containing two submenus with names equal to the `title` properties in the previously created files.
2. The home page explains how to customize it by following the instructions.
3. When you run `hugo server`, when the contents of the files change, the page automatically refreshes with the changes. Neat!

Alternatively, you can run the following command in a terminal window to tell Hugo to automatically rebuild whenever a file is changed. This can be helpful when rapidly iterating over content changes.

```bash
hugo server
```

## Things to be aware of:

* Remove the links to "Event Outfitters" from the bottom of the front page before you publish your workshop.
* Update the config.toml with your workshop name - the default is at the top, and also under the section [Languages.en]
```
title = "My AWS Workshop"
```
* The template includes two sample languages, French and English (eg "_index.en.md" and "_index.fr.md"). Please don't move everything to "_index.md" as other people may want to translate your workshop in future!
* However, you should remove the example French language selection from the config.toml unless you plan to provide a French translation. Delete the following lines:
```
[Languages.fr]
title = "Mon atelier AWS"
weight = 2
languageName = "Français"
```