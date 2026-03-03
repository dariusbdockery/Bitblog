---
created: 2025-12-25
updated: 2026-03-02
tags:
  - mistral
  - pkm
  - writing
description: This is post 1/5 about how to set up a blog for free using Obsidian, Quartz, and Mistral AI
publish: true
title: Part 1. Install and Set Up Quartz
---

> [!info]+ This Post is Part of a Multi-part Series
> This post is **part 1 of 5** of the Using Mistral to Setup My Quartz Blog for Free Series. Feel free to jump to any part of the series if you've already covered previous steps or just want to see specific info:
> 
> **Navigate Through the Series**
> > - [[Using Mistral to Setup My Quartz Blog for Free - Part 1. Install and Set Up Quartz|Part 1. Install and Set Up Quartz]]
> > - [[Using Mistral to Setup My Quartz Blog for Free - Part 2. Set Up a GitHub Repository|Part 2. Set Up a GitHub Repository]]
> > - [[Using Mistral to Setup My Quartz Blog for Free - Part 3. Host Your Vault Online|Part 3. Host Your Vault Online]]
> > - [[Using Mistral to Setup My Quartz Blog for Free - Part 4. Set Your Vault Up for Publication|Part 4. Set Your Vault Up for Publication]]
> > - [[Using Mistral to Setup My Quartz Blog for Free - Part 5. Use Mistral to Modify Quartz Configuration Settings|Part 5. Use Mistral to Modify Quartz Configuration Settings]]

# The Project
![[Screenshot 2026-03-01 at 14.07.30.png]]

I am now a [Mistral Ambassador](https://docs.mistral.ai/ambassadors) and I want to share some of my projects with the community, so I wanted to set up my blog to share some write ups. I also wanted to share how you can use Mistral to help set the blog up. 

A lot of this installation and setup was taken from the [Quartz docs](https://quartz.jzhao.xyz/) and [Nicole van der Hoeven's](https://nicolevanderhoeven.com/) published blog [Fork My Brain](https://notes.nicolevanderhoeven.com/Fork+My+Brain), but since I'm not a programmer (and neither are many people who want to make use of both Obsidian and AI in different ways), I wanted to demonstrate how you can use Continue in VSCodium to help me make iterations to the TypeScript that Quartz is written in to both enhance the settings and aesthetics of your blog according to your own preferences. 

The setup is pretty straightforward, but it does require a few steps. However, once you have everything set up, you can also to potentially generate posts or newsletters to help with your content creation. The possibilities are really endless with this setup since Obsidian files are just plaintext markdown files that plugins like Continue and Models like [Mistral Large](https://mistral.ai/news/mistral-large) or [Codestral](https://mistral.ai/news/codestral) can create and manipulate easily. 

Here are some other Quartz tutorials that I found useful and that might help supplement anything I've missed in this series:

- [Turn Your Obsidian Notes Into A Website by isak](https://www.youtube.com/watch?v=zGFroBGud7w&t=1s)
- [Quartz 4 may be Obsidian Publish at Home and then some by Nephitejnf](https://www.youtube.com/watch?v=AO3YhsU2YJ4)
- [Publish your Obsidian Vault Online for Free with Quartz by Brandon Boswell](https://www.youtube.com/watch?v=ITiiuBNVue0)
	- [Brandon's Accompanying Article](https://brandonkboswell.com/blog/Publishing-your-Obsidian-Vault-Online-with-Quartz)

## Prerequisites

Below is a list of software I used for this project if you want to follow along:

- [Obsidian](https://obsidian.md/)
	- I call Obsidian my exocortex, meaning it's my external brain. I take notes with it and it's where I write the content for this blog. It's incredibly flexible and customizable, and with the software below, you can organize your thoughts and create a beautiful website. I’ve been using it for years and I highly recommend it for anyone looking for a powerful note-taking and writing tool.
- [Quartz](https://quartz.jzhao.xyz/)
	- This is the backbone of this project and what I am going to use to replace [Obsidian Publish](https://obsidian.md/publish) to publish the static site.
- [GitHub](https://github.com/)
	- I used [GitHub Pages](https://pages.github.com/) to host the site for public viewing.
- [Mistral](https://mistral.ai/)
	- I am going to use Mistral's models to work within my Quartz config. You can get an API key by following the steps [here](https://iamistral.com/api/) after signing up for an account.
- [Continue](https://docs.continue.dev/ide-extensions/quick-start)
	- I used Continue's IDE extension for [VSCodium](https://vscodium.com/), but you can use whatever IDE or assistant of your choice. The concepts and principles should be the same or very similar.

Quartz requires **at least** `Node v22` and `npm v10.9.2` to function correctly. Ensure you have this installed on your machine before continuing. You do not need to download NodeJS and NPM separately. When you install NodeJS, NPM (Node Package Manager) is installed automatically along with it. You'll also need `Git` running as well:

- [Git](https://github.com/git-guides/install-git) (check your version using `git --version`)
	- Git is a distributed version control system, essential for managing code changes and tracking modifications to files over time.
- [NodeJS & NPM](https://nodejs.org/en/download) (check your version using `node -v` or `npm -v`)
	- NodeJS is a JavaScript runtime environment that allows you to run JavaScript code outside of a web browser. NPM is the default package manager for NodeJS, enabling you to easily install and manage project dependencies.

> [!WARNING]+ A Note About Some Commands in This Guide
> I have machines that use MacOS and Linux. I have not used a Windows machine in years, so I apologize in advance for not having Windows-specific instructions. If you have any issues, please reach out and I’ll do my best to help. 
> 
> Since this project uses platform agnostic software, most of it should be compatible with any setup you have. 

# Step 1. Install And Set Up Quartz

Let's start by first setting up a fresh Quartz installation. We'll walk through everything step by step. Below, I use symlinks to a subfolder in my Obsidian vault, but any setup steps before and after setting up the symlink should be the same for any installation options you choose (i.e., copying a folder, or starting with an empty Quartz). 

## Clone the Quartz Repository

Navigate to the folder where you want your Quartz vault and run this command in your terminal:

```shell
git clone https://github.com/jackyzha0/quartz.git
```

Then, change into the newly created Quartz directory and install Quartz's dependencies by running:

```shell
cd quartz && npm i
```

## Initialize Quartz

Once the dependencies have been installed, you can set up the service by running:

```shell
npx quartz create
```

During the setup prompts, you are asked to choose between three different methods of getting content in your quartz project. You can choose any of the following:

```shell
┌   Quartz v4.5.2 
│
◆  Choose how to initialize the content in `/path_to/quartz/content`
│  ○ Empty Quartz
│  ○ Copy an existing folder
│  ● Symlink an existing folder (don't select this unless you know what you are doing!)
└
```

I chose to use a symlink (even though Git can run into issues with symlinks). If you also go with this option it will prompt you and tells you: "don't select this unless you know what you are doing!", so let's make sure you know what's going on here.

## About Symlinks

For this project, I chose to symlink a subfolder in my Obsidian vault instead of creating an empty or copied directory. I have one massive vault (there are pros and cons to this), but I like the idea of fostering "emergence" by keeping my life, work, and project notes in one place. I naturally learn from all of these things and they connect in my own mind, so why wouldn't I connect all of them in my Obsidian vault?

That said, I wanted to be able to write posts in both my Obsidian and VSCodium environments (which we will use later) because I have spent a lot of time setting them up and why recreate my wobbly wheel in another new directory that I have to manage? Seems silly. 

So, I chose to symlink my vault and have the files within my quartz directory automatically update, instead of doing any manual copying or writing in an environment that's cut off from the rest of my notes. Normally, you can create a symlink to any folder/file on MacOS easily. Below are some steps to do so:

On macOS, you can create a **symbolic link** (symlink) to a file or folder using the `ln` command in your terminal.

**1. Create a Symlink to a File**

```bash
ln -s /path/to/original/file /path/to/symlink
```

- Replace `/path/to/original/file` with the actual file path.
- Replace `/path/to/symlink` with where you want the symlink to be created (include the symlink name).

**Example:**

```bash
ln -s ~/Documents/report.txt ~/Desktop/report_link.txt
```

This creates a symlink named `report_link.txt` on your Desktop, pointing to `report.txt` in Documents.

**2. Create a Symlink to a Folder**

```bash
ln -s /path/to/original/folder /path/to/symlink
```

- Replace `/path/to/original/folder` with the actual folder path.
- Replace `/path/to/symlink` with the desired symlink location and name.

**Example:**

```bash
ln -s ~/Projects/my_app ~/Desktop/app_link
```

This creates a symlink named `app_link` on your Desktop, pointing to the `my_app` folder in Projects.

**3. Verify the Symlink**
Run `ls -l` in the directory where the symlink was created to confirm it points to the correct target:

```bash
ls -l /path/to/symlink
```

The output will show the symlink (e.g., `symlink -> /path/to/original`).

**4. Remove a Symlink**
To delete a symlink (without affecting the original file/folder), use:

```bash
unlink /path/to/symlink
```

or

```bash
rm /path/to/symlink
```

**Some Best Practices for Symlinks:**
- Use **absolute paths** (e.g., `/Users/name/Documents/file.txt`) to avoid broken links if the symlink is moved.
- If the symlink path already exists, add `-f` (force) to overwrite:

  ```bash
  ln -sf /new/target /path/to/symlink
  ```

- For **Finder GUI**, hold `Option + Command` while dragging the file/folder to create an alias (similar to a symlink but macOS-specific).

### Quartz And Symlinks

Quartz will automatically make a symlink, so there is nothing for you to do per se, but you should realize that the `content` folder in the quartz directory will be shown as an opaque icon, but you can still access these files via Finder (or whatever your OS file browser is) and even in VSCodium.

You have to use your full path to the folder.

```shell
┌   Quartz v4.5.2 
│
◇  Choose how to initialize the content in `/path_to/quartz/content`
│  Symlink an existing folder
│
◆  Enter the full path to existing content folder
│  On most terminal emulators, you can drag and drop a folder into the window and it will paste the full path
└
```

For me, I use [Syncthing](https://syncthing.net/) to sync my vault across a variety of systems (i.e., MacOS, TrueNAS Scale, Ubuntu, iOS), so I choose the `absolute path` to my root folder within my Obsidian vault and I plan to use quartz's frontmatter settings to control what gets published on the blog. We'll talk about how to set up templates to manage this process in a sane way, so you don't have to worry about accidentally publishing private notes.

> [!warning]+ How Symlinks Work with Quartz and Obsidian
> Quartz generates a static site from your `content` folder, but it doesn’t replicate Obsidian’s dynamic link resolution. Here’s what actually happens:
>
> - **Obsidian’s Strength**: Obsidian automatically updates wikilinks (e.g., `[[Note]]`) even if you rename or move files, because it tracks links *internally* via metadata (e.g., the `.obsidian` folder).
> - **Quartz’s Limitation**: Quartz treats your `content` folder as a static filesystem. It resolves links *literally* during build time:
>   - Relative paths (e.g., `[[../Folder/Note]]`) must exist *exactly as written* in the `content` folder.
>   - Absolute paths (e.g., `[[Note]]`) rely on Quartz’s [link resolution rules](https://quartz.jzhao.xyz/features/link-resolution), which may not match Obsidian’s behavior.
>
> ### Why Symlinking a Subfolder Can Break Links
> If you symlink only a subfolder (e.g., `content/Posts`), but your notes use relative paths like `[[../Assets/Image.png]]`, Quartz will fail to find `Assets` unless:
> 1. You symlink *all* parent folders in the path (e.g., `content/Assets`), or
> 2. You use absolute paths (e.g., `[[Image.png]]`) and configure Quartz to resolve them correctly.
>
> ### Recommended Approaches
> 1. **Symlink the Entire Vault**:
>    - Simplest solution. Ensures all paths in `content` match your vault’s structure.
>    - *Downside*: May include unwanted files (e.g., `.obsidian`).
> 2. **Symlink Selectively + Fix Paths**:
>    - Symlink only the folders you need (e.g., `Posts`, `Assets`).
>    - Use absolute paths in notes and configure Quartz’s `ignorePatterns` to exclude non-content files.
> 3. **Manual Copy (No Symlinks)**:
>    - Copy files to `content` and use tools like [Obsidian Git](https://github.com/denolehov/obsidian-git) to sync changes.
>    - *Downside*: Manual updates required.

## The Content Directory

The `content` folder will be the root of your site. You need to have a file named `index.md` in the root, or else you'll get the following error:

``` shell
Warning: you seem to be missing an `index.md` home page file at the root of your `content` folder (`content/index.md does not exist`). This may cause errors when deploying.
```

The index.md file is going to be the landing page of your blog. A sample index.md file can be found on the [quartz GitHub page](https://github.com/jackyzha0/quartz/blob/v4/docs/index.md), and can be seen rendered at <https://quartz.jzhao.xyz/>:

```markdown
---
title: Welcome to Quartz 4
---

Quartz is a fast, batteries-included static-site generator that transforms Markdown content into fully functional websites. Thousands of students, developers, and teachers are [[showcase|already using Quartz]] to publish personal notes, websites, and [digital gardens](https://jzhao.xyz/posts/networked-thought) to the web.

## 🪴 Get Started

Quartz requires **at least [Node](https://nodejs.org/) v22** and `npm` v10.9.2 to function correctly. Ensure you have this installed on your machine before continuing.

Then, in your terminal of choice, enter the following commands line by line:

git clone https://github.com/jackyzha0/quartz.git
cd quartz
npm i
npx quartz create

This will guide you through initializing your Quartz with content. Once you've done so, see how to:

1. [[authoring content|Writing content]] in Quartz
2. [[configuration|Configure]] Quartz's behaviour
3. Change Quartz's [[layout]]
4. [[build|Build and preview]] Quartz
5. Sync your changes with [[setting up your GitHub repository|GitHub]]
6. [[hosting|Host]] Quartz online

If you prefer instructions in a video format you can try following Nicole van der Hoeven's
[video guide on how to set up Quartz!](https://www.youtube.com/watch?v=6s6DT1yN4dw&t=227s)

## 🔧 Features

- [[Obsidian compatibility]], [[full-text search]], [[graph view]], [[wikilinks|wikilinks, transclusions]], [[backlinks]], [[features/Latex|Latex]], [[syntax highlighting]], [[popover previews]], [[Docker Support]], [[i18n|internationalization]], [[comments]] and [many more](./features/) right out of the box
- Hot-reload on configuration edits and incremental rebuilds for content edits
- Simple JSX layouts and [[creating components|page components]]
- [[SPA Routing|Ridiculously fast page loads]] and tiny bundle sizes
- Fully-customizable parsing, filtering, and page generation through [[making plugins|plugins]]

For a comprehensive list of features, visit the [features page](./features/). You can read more about the _why_ behind these features on the [[philosophy]] page and a technical overview on the [[architecture]] page.

### 🚧 Troubleshooting + Updating

Having trouble with Quartz? Try searching for your issue using the search feature. If you haven't already, [[upgrading|upgrade]] to the newest version of Quartz to see if this fixes your issue.

If you're still having trouble, feel free to [submit an issue](https://github.com/jackyzha0/quartz/issues) if you feel you found a bug or ask for help in our [Discord Community](https://discord.gg/cRFFHYye7t).
```

You can choose how you want to run your own setup and once you make your selection, you will see another selection menu that's similar to this:

```shell
┌   Quartz v4.5.2 
│
◆  Choose how Quartz should resolve links in your content. This should match Obsidian's link format. You can
change this later in `quartz.config.ts`.
│  ● Treat links as shortest path ((default))
│  ○ Treat links as absolute path
│  ○ Treat links as relative paths
└
```

What you select here is dependent on how you prefer to handle links in Obsidian. By default, Obsidian uses the shortest path where possible, so unless you know you want a different setup, select the first option.

You should see something like this:

```shell
  You're all set! Not sure what to do next? Try:
  • Customizing Quartz a bit more by editing `quartz.config.ts`
  • Running `npx quartz build --serve` to preview your Quartz locally
  • Hosting your Quartz online (see: https://quartz.jzhao.xyz/hosting)
```

## Running Your Quartz Server

If you run `npx quartz build --serve` you should see it parsing, filtering, and emitting whatever files you have in the repo. All of these actions are dictated by frontmatter and settings you have in the files and your quartz config.

Once it's iterated through the files, you should see:

```shell
Started a Quartz server listening at http://localhost:8080
```

Now, navigate to that url, and you should see your quartz site up and running! While running the server, it will detect any changes you make to files and rebuild the site. You'll see `Detected change, rebuilding...` in your terminal. But this setup only really works for testing or for accessing your site locally. 

If you use a service like [Tailscale](https://tailscale.com/), you can make the site accessible to those on your [tailnet](https://tailscale.com/docs/concepts/tailnet), but beyond that, you'll need to host it somewhere and to make it accessible to the public.

There are a number of ways to do this at this point. For example, you could use a service like any of those listed on the [anderspitman/awesome-tunneling](https://github.com/anderspitman/awesome-tunneling?tab=readme-ov-file) repo which contains a "List of ngrok/Cloudflare Tunnel alternatives and other tunneling software and services" for self hosting projects. You'll need a domain name or at least a DNS provider like [Duck DNS](https://www.duckdns.org/) and a reverse proxy like [Caddy](https://github.com/caddyserver/caddy) to get a proper https url up, but you also need to host your server 24/7 if you want people to access your blog without interruption. We will talk a bit more about aspects of this setup later in a later post.

Alternatively, you can use a service like GitHub Actions to work in conjunction with quartz to launch your site on GitHub Pages for free. Let's talk about that now. Onto [[Using Mistral to Setup My Quartz Blog for Free - Part 2. Set Up a GitHub Repository|Part 2. Setting Up a GitHub Repository]].