---
created: 2025-12-29
updated: 2026-03-03
tags:
  - mistral
  - pkm
  - writing
description: This is post 2/5 about how to set up a blog for free using Obsidian, Quartz, and Mistral AI
publish: true
title: Part 2. Set Up a GitHub Repository
---

> [!info]+ This Post is Part of a Multi-part Series
> This post is **part 2 of 5** of the Using Mistral to Setup My Quartz Blog for Free Series. If you haven't read the previous post yet, you should start there before working through this post.
>
> **Navigate Through the Series**
> 
> - [Part 1. Install and Set Up Quartz](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%201.%20Install%20and%20Set%20Up%20Quartz.md)
> - [Part 2. Set Up a GitHub Repository](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%202.%20Set%20Up%20a%20GitHub%20Repository.md)
> - [Part 3. Host Your Vault Online](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%203.%20Host%20Your%20Vault%20Online.md)
> - [Part 4. Set Your Vault Up for Publication](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%204.%20Set%20Your%20Vault%20Up%20for%20Publication.md)
> - [Part 5. Use Mistral to Modify Quartz Configuration Settings](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%205.%20Use%20Mistral%20to%20Modify%20Quartz%20Configuration%20Settings.md)

# Step 2. Set Up a GitHub Repository

You can see quartz's excellent documentation about this [here](https://quartz.jzhao.xyz/setting-up-your-GitHub-repository), but I will still outline them below.

## Create a GitHub Repository

First, make sure you have Quartz [[Using Mistral to Setup My Quartz Blog for Free - Part 1. Install and Set Up Quartz|cloned and setup locally]]. Then, you need to create a new repository on [GitHub](https://github.com/) and synchronize the local Quartz repository that you've cloned to the remote repository on GitHub:

1. When logged into GitHub, click on the _New_ button to create a new repository.
2. In the `Repository name:` field, type `quartz` (or whatever you chose in [[Using Mistral to Setup My Quartz Blog for Free - Part 1. Install and Set Up Quartz|Part 1]]).
3. For the `Initialize this repository:` field, **do _not_ initialize the new repository with `README`, `license`, or `gitignore` files** (to avoid conflicts with the local Quartz clone). Since Quartz is already cloned, the local repo is pre-configured by Quartz (`npx quartz create` handles the `git init` part automatically), and the GitHub repo is just a remote destination.
	1. It should look something like this:
		1. ![[IMG-20260217192817-3.png|800]]
4. Click `Create repository` at the end to get started.

## Syncing Your Repo

On the next page, you are presented with a couple options. You can start coding, add collaborators, create a new repo or push one from an existing repo you want to add to GitHub. 

![[02-Merit/Bitblog/Posts/Tech and AI/Using Mistral to Setup My Quartz Blog for Free/Attachments/IMG-20260217192817-1.png|800]]

We're going to obviously push the cloned Quartz repo we created in the previous steps. For our purposes, to do so, we're going to just follow the steps outlined in the quartz documentation.

**HTTPS vs. SSH?**

SSH is more secure, but it has its disadvantages. While HTTPS is easier for one-off setups, it frequently triggers the credential pop-ups you mentioned. 

> [!tip] Generating a SSH Key
> If you'd like to use SSH, you can ask your LLM (in my case Mistral) to help them "Generate an SSH key" to avoid entering passwords entirely in the future.

Unless you have a preference, I recommend you choose HTTPS for this initial setup.

**Terminal Commands**

Now, in your terminal, run:

``` shell
git remote -v
```

You should see something like:

```shell
origin  https://github.com/jackyzha0/quartz.git (fetch)
origin  https://github.com/jackyzha0/quartz.git (push)
upstream        https://github.com/jackyzha0/quartz.git (fetch)
upstream        https://github.com/jackyzha0/quartz.git (push)
```

Here, we can see that there are already two remotes that are set up, `origin` and `upstream`, each of which has a `fetch` and a `push`. You need to now set the remote to the repo you just created. So click on the copy button next to the url to copy it and paste that at the end of the following command--replacing `REMOTE-URL` with your copied url.

Now run:

```shell
git remote set-url origin REMOTE-URL
```

If you don't have upstream as a remote, add it so updates work

```shell
git remote add upstream https://github.com/jackyzha0/quartz.git
```

Check the remotes again:

```shell
git remote -v
```

You should see something like:

```shell
origin  https://github.com/dariusbdockery/Bitblog.git (fetch)
origin  https://github.com/dariusbdockery/Bitblog.git (push)
upstream        https://github.com/jackyzha0/quartz.git (fetch)
upstream        https://github.com/jackyzha0/quartz.git (push)
```

What this is saying is:

- **`origin`**: Your "home" remote (your fork or the repo you cloned).
- **`upstream`**: The original project (useful for syncing changes from the source).
- **`(fetch)`**: URL for downloading changes.
- **`(push)`**: URL for uploading changes.

**Sync your changes**

Now, you can sync the content of your vault to your repository. This command will do the initial push of your content to your repository (this skips pulling changes from remote before pushing, which is safe for the first push). Quartz defaults to a branch named `v4`. If you don't see their files on GitHub, they might need to switch the branch view on the GitHub website from `main` to `v4`:

```shell
npx quartz sync --no-pull
```

## Signing Into GitHub

After I ran this command, I saw this popup:

![[02-Merit/Bitblog/Posts/Tech and AI/Using Mistral to Setup My Quartz Blog for Free/Attachments/IMG-20260217192817-2.png|300]]

This popup is from **macOS Keychain Access**, specifically asking for permission to allow an application (in this case, the Git credential helper) to access your **Docker credentials** stored in the keychain. Here, you should enter your **Mac user account password** in the password field and click on `Always Allow`.

**GitHub Sign In**
I also had to sign into GitHub as this was my first time syncing with my account on this installation of VSCodium.

> [!tip]+ A Note About IDEs
> I recommend using an IDE like VSCodium (or VSCode) because it allows you to run terminal commands, access and alter files, while also using LLMs within your editor. We will walkthrough and use this setup later in the post, but you won't have to switch environments to accomplish everything if you do this all from an IDE. You can also use an editor like Vim or Neovim or Emacs, but if you have a good setup for those options, I'm also assuming you don't need me to guide you through most of this setup anyway. 😉

If it's the same for you, you might see another popup like this:

![[IMG-20260217192818.png|300]]

Click `Allow` and sign in by entering the one-time code that is shown:

![[IMGS-20260217192818-1.png]]

It will bring you through a series of screens to authorize the device. Walk through them and authorize VSCode for access to your account:

![[IMG-20260217192818-2.png|400]]

![[IMG-20260217192818-3.png|400]]

![[IMG-20260217192818-4.png|400]]

![[IMG-20260217192818-5.png|400]]

## Generating a Personal Access Token (PAT)

If you do this via a dedicated terminal outside of an IDE, you may have to sign in another way and generate a `Personal Access Token (PAT)`. PATs are now **required** for HTTPS authentication ([GitHub no longer accepts passwords](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)). You can follow these instructions to do so:

### Sign In With Git On Mac (GitHub)

1. Open Terminal and run:

	`git --version`

	Install if prompted.

2. **Set Git Username/Email**

	`git config --global user.name"Your Name"git config --global user.email"your.email@example.com"`

3. **Generate a Personal Access Token (PAT)**
	
	- Go to [GitHub → Settings → Developer settings → Personal access tokens](https://github.com/settings/tokens).
	- Generate a new token.

4. **Clone a Repository**

	`git clone https://github.com/username/repo.git`

5. **Authenticate**
	
	- When prompted for a password, you have to **paste the PAT**. Many users try their GitHub login password first and get frustrated when it fails.

6. **(Optional) Save Credentials**

	`git config --global credential.helper osxkeychain`

## Finishing the Setup

You should get some text that looks like this with a nice green `Done!` at the end:

```shell
Pushing your changes
Enumerating objects: 11896, done.
Counting objects: 100% (11896/11896), done.
Delta compression using up to 10 threads
Compressing objects: 100% (4401/4401), done.
Writing objects: 100% (11896/11896), 36.83 MiB | 741.00 KiB/s, done.
Total 11896 (delta 7418), reused 11851 (delta 7382), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (7418/7418), done.
To https://github.com/dariusbdockery/Bitblog.git
 * [new branch]      v4 -> v4
branch 'v4' set up to track 'origin/v4'.
Done!
```

If you saw text that said this:

```shell
Committer: YOUR NAME <AN AUTO-GENERATED EMAIL ADDRESS>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author
```

Just follow the instructions there and change YOUR NAME and the AUTO-GENERATED EMAIL ADDRESS to whatever you would like.

**Checking If It Worked**
To verify that everything worked, go back to GitHub and refresh that page you were on where you previously copied that text string containing your repository's address.

You should see something like this there instead: 

![[IMG-20260217192818-6.png|800]]

This means that your repositories are synced! From now on, you can simply run `npx quartz sync` every time you want to push updates to your repository. Now on to [[Using Mistral to Setup My Quartz Blog for Free - Part 3. Host Your Vault Online|Part 3. Hosting Your Vault Online]]. This will automatically build and deploy your Quartz blog to GitHub Pages. Make sure your GitHub repository is public for this to work. You can then view your blog at your repository's GitHub Pages URL.
