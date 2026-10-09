---
title: 'Starting My Technical Learning Blog'
description: 'My first steps building a public technical blog with Astro and VS Code.'
pubDate: '2026-10-09'
tags: ['Astro', 'VS Code', 'Learning']
draft: false
---

## Why I started

I created this blog to document my learning in Python, AI, data engineering,
and DevOps through practical examples and project lessons.

## Creating the workspace

I created a separate My-Learning-Blog folder and opened it in VS Code.
The blog has its own dependencies and Git repository.

## Setting up Astro

I used the official Astro blog starter. The initial dependency installation
reported a timeout, so I ran `npm install` manually. It completed successfully.

## Checking the build

I ran `npm run build`. Astro generated the starter pages, RSS feed,
sitemap, and optimized images successfully.

## What I learned

After a terminal restart, PowerShell returned to a different project folder.
Running npm there failed because the blog's package.json was elsewhere.

Checking `Get-Location` before running project commands helped resolve it.

## Next steps

I will personalize the site, organize my learning notes, and review the
production configuration before publishing.
