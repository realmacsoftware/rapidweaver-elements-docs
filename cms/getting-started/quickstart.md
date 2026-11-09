---
description: Learn how to get started with the Elements CMS
icon: bolt
---

# Quickstart

Elements includes a built-in CMS that makes it easy to create a blog or content-driven site using Markdown files.

{% hint style="danger" %}
Elements CMS [requires PHP 8.4](system-requirements.md) or newer to be installed on your server. You'll need to **ensure your page extension is set to .php** on any pages you wish to access CMS data from.
{% endhint %}

#### Microblog Project

The Microblog project in the Elements New Projects window is a pre-built Blog that uses the Elements CMS. It's an excellent resource to examine and see how the CMS is integrated.

<figure><img src="../../.gitbook/assets/CleanShot 2026-05-27 at 9 .57.56@2x.png" alt=""><figcaption></figcaption></figure>

### How to Set Up the Elements CMS

This video series will walk you though setting sup the Elements CMS inside your Elements project.

{% embed url="https://www.youtube.com/watch?v=NgpV-dAxiJw" %}

{% embed url="https://www.youtube.com/watch?v=RGWDM9atj24" %}

{% embed url="https://www.youtube.com/watch?v=UN-VkwtFsB4" %}

#### How the CMS Is Structured

CMS content lives inside a dedicated CMS folder in your project. A typical blog setup looks like this:

*   posts

    Contains your blog posts as Markdown (.md) files
*   authors

    Contains author profiles, also as Markdown files

Each Markdown file includes two parts:

1. Frontmatter at the top of the file, which defines metadata like title, date, and author
2. Markdown content below, which is the body of the post

Elements uses this data to automatically populate your blog pages.

#### How Blog Pages Work

A basic blog in Elements uses two main page types:

*   Blog page

    Uses a CMS Collection component to list posts from the posts folder
*   Post page

    Uses a Single Item component to display one post at a time

The Collection controls where the content comes from, while the Item page defines how an individual post looks.

#### Writing Posts

To add a new post:

* Create a new Markdown file in the posts folder
* Fill in the frontmatter fields such as title, date, and author
* Write your content using standard Markdown

When you preview or publish the site, Elements automatically generates the blog listing and individual post pages.

#### Styling and Design

All visual styling is handled in Elements, not in the Markdown files.

This means you can change fonts, colors, layout, and spacing across your entire blog without touching your content.

#### Preview and Publish

You can preview the blog locally at any time using Preview in Browser.

When ready, publish as normal and your CMS-powered blog will be live.
