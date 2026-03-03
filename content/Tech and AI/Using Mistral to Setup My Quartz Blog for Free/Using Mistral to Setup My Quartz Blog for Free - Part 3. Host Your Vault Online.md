---
created: 2025-12-29
updated: 2026-03-02
tags:
  - mistral
  - pkm
  - writing
description: This is post 3/5 about how to set up a blog for free using Obsidian, Quartz, and Mistral AI
publish: true
title: Part 3. Host Your Vault Online
---
> [!info]+ This Post is Part of a Multi-part Series
> This post is **part 3 of 5** of the Using Mistral to Setup My Quartz Blog for Free Series. If you haven't read the previous posts yet, you should start there before working through this post:
> 
> **Navigate Through the Series**
> 
> - [Part 1. Install and Set Up Quartz](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%201.%20Install%20and%20Set%20Up%20Quartz.md)
> - [Part 2. Set Up a GitHub Repository](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%202.%20Set%20Up%20a%20GitHub%20Repository.md)
> - [Part 3. Host Your Vault Online](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%203.%20Host%20Your%20Vault%20Online.md)
> - [Part 4. Set Your Vault Up for Publication](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%204.%20Set%20Your%20Vault%20Up%20for%20Publication.md)
> - [Part 5. Use Mistral to Modify Quartz Configuration Settings](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%205.%20Use%20Mistral%20to%20Modify%20Quartz%20Configuration%20Settings.md)

# Step 3. Host Your Vault Online

Right now, you've got a local version of your site running. You should be able to preview it in your browser if you run `npx quartz build --serve`, but even if you run `npx quartz sync`, any changes will still be trapped in your GitHub repo as raw Markdown files. Now's the time to flip the switch and make them live on the web. This post will help you do that. 

In this step, we'll set up your GitHub page, so Quartz automatically builds and publishes your notes as a static site. No manual HTML exports, no extra steps. You just push your changes, and your site will update.

**Why This Matters**

- **Local vs. Live**: Running `npx quartz build --serve` is great for testing, but it's not public. We want your blog accessible to anyone, anywhere.
- **GitHub Pages**: Free, simple, and integrates seamlessly with Quartz. No need to spin up a server or mess with DNS (unless you want to go the extra step of setting your blog up with a custom domain).
- **Automation**: Once configured, every sync triggers a rebuild. Write a note, sync, and **boom** it's live.

Let's get started.

## Create a deploy.yml File

Make sure you're still in your quartz directory. From your terminal, you can run the following command to create a deploy.yml file:

```shell
touch .github/workflows/deploy.yml
```

Navigate to that folder and open up it in your file explorer. Make sure hidden files are visible as `.github` is a hidden file, so if you don't see it on a Mac, hit `cmd + opt + .` to see it listed in Finder. On other systems, you can usually right click and see the option in a menu.

The blank file should have opened in your default text editor. Alternatively, you can also run `vim .github/workflows/deploy.yml` to create and open the file simultaneously. 

Either way, you can just copy and paste this `yaml` configuration into it:

```yaml
name: Deploy Quartz site to GitHub Pages
 
on:
  push:
    branches:
      - v4
 
permissions:
  contents: read
  pages: write
  id-token: write
 
concurrency:
  group: "pages"
  cancel-in-progress: false
 
jobs:
  build:
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0 # Fetch all history for git info
      - uses: actions/setup-node@v4
        with:
          node-version: 22
      - name: Install Dependencies
        run: npm ci
      - name: Build Quartz
        run: npx quartz build
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: public
 
  deploy:
    needs: build
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

> [!warning]+ Make Sure You Have the Most Up-to-Date Version of This File!
> This was updated on February 21, 2026. If you're reading this much later than that, get the latest version of this from [the Quartz documentation](https://quartz.jzhao.xyz/hosting#github-pages).*

Save the file.

## Create a GitHub Action

Now, from the `Settings` tab of your forked repository and in the sidebar, click `Pages`. Under `Source`, select `GitHub Actions`.

![[IMG-20260217192817-2 2.png|800]]

You should see a final screen with nothing else to save or do here. Now, you can go back to your terminal to sync and commit these changes by running:

```plaintext
npx quartz sync
```

This should deploy your site to `<github-username>.github.io/<repository-name>`.

Verify that this worked by visiting `https://yourusername.github.io/<repository-name>` from your browser. You should see your site displayed, just as you saw it when you built it locally!

You can stop here if you're happy with the new URL above. But if you want to make customizations to your site, we'll talk about that in [[Using Mistral to Setup My Quartz Blog for Free - Part 4. Set Your Vault Up for Publication|Part 4. Setting Your Vault Up for Quartz]].
