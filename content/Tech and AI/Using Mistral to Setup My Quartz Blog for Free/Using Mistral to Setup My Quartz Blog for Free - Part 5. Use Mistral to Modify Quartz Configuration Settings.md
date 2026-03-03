---
created: 2026-02-19
updated: 2026-03-02
tags:
  - mistral
  - pkm
  - writing
description: This is post 5/5 about how to set up a blog for free using Obsidian, Quartz, and Mistral AI
publish: true
title: Part 5. Use Mistral to Modify Quartz Configuration Settings
---

> [!info]+ This Post is Part of a Multi-part Series
> This post is **part 5 of 5** of the Using Mistral to Setup My Quartz Blog for Free Series. If you haven't read the previous posts yet, you should start there before working through this post:
> 
> **Navigate Through the Series**
> 
> - [Part 1. Install and Set Up Quartz](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%201.%20Install%20and%20Set%20Up%20Quartz.md)
> - [Part 2. Set Up a GitHub Repository](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%202.%20Set%20Up%20a%20GitHub%20Repository.md)
> - [Part 3. Host Your Vault Online](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%203.%20Host%20Your%20Vault%20Online.md)
> - [Part 4. Set Your Vault Up for Publication](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%204.%20Set%20Your%20Vault%20Up%20for%20Publication.md)
> - [Part 5. Use Mistral to Modify Quartz Configuration Settings](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%205.%20Use%20Mistral%20to%20Modify%20Quartz%20Configuration%20Settings.md)

# Step 5. Using Mistral To Modify Quartz Configuration Settings
Now that you have your blog set up and launched with Quartz and GitHub Pages, you probably want to personalize it. Out the box, Quartz sets up your site with sensible defaults for a nice looking page that mirrors the site that hosts the documentation. However, this means that your site page reads: "Quartz 4" in the top left corner and "Welcome to Quartz 4" on the homepage (i.e., index.md). To make the page your own, including the layout and features of your page, you can edit the [Typescript](https://www.typescriptlang.org/) pages yourself. 

If you have any programming experience, Typescript is designed to be **intuitive and expressive**, allowing you to describe complex data structures in a readable way. So, editing the files directly, along with the documentation is fairly straightforward for the basic elements of the site. But if you aren't a programmer (like myself), you may want to alter some aspects of the site and feel confident that you've done it right and well. You may also want to do more complex modifications of the site that aren't as straightforward as adding or removing plugin types.

This is where LLMs come in. With the power of AI, particularly in your IDE to manipulate the files directly, you can work with a model to customize and personalize your site. In this post, we'll show the basics of how you might do this. Let's get into it.

## My Logic For Using Continue

I am using [Continue](https://docs.continue.dev/ide-extensions/install) in VSCodium to have LLMs interact with my codebases and ultimately my Obsidian vault. This is because one of the limitations I keep running into with the AI plugins I have found in Obsidian is that even though you can chat with your notes, you can't iterate over a folder of notes and configurations and apply changes wholesale.

This is when I figured, it's just text, so I can use a text editor like [Emacs](https://www.gnu.org/software/emacs/) to do stuff to the files all at once. The issue I'm running into there is that I don't want to spend my entire life tweaking my setup anymore. I had my time with Emacs when I was working in gradschool, and love(d) it. But I have a full time job where I can't use Emacs at all. I *can* use VSCode, however, so I wanted to have similar environments between my devices and also protect my privacy by using the VSCodium fork. That way, I can also use one setup on my work computer, and on my personal machines. 

That said, since I settled on VSCodium for my setup, and this is where I can use a AI plugin like Continue to work within the IDE on my notes when I want to do things wholesale, since the AI plugins in Obsidian that I like using only work on one file at a time when applying changes.

## About Continue

I use VS Codium and a plugin called Continue. They also have a pretty nice CLI, but as I mentioned earlier, the ability to manage everything in my IDE and incorporate other plugins without context switching is a nice experience for me since I don't do a lot of work directly in the terminal. There are many others (e.g., RooCode, GitHub Copilot, or Cline), but I chose to try Continue because:

1. **Continue is free Though you can incur costs for third-party AI model APIs) and fully open-source.**
	1. It boasts **over 26,000 GitHub stars** and has a growing community, with active development and contributions.
	2. It also supports **both cloud and local AI models** and I use local models to interact with my notes because I don't want my personal thoughts and information getting sent to Elon or Altman.

2. **Unlike GitHub Copilot, for example, Continue offers transparency and control over configurations.**
	1. You can define both global and **project-specific rules** (e.g., coding standards, style guides) in a `.continue/rules/` directory to align suggestions with that project's particular needs or conventions.

3. **Works natively within VS Codium, providing inline suggestions, code generation, and refactoring without requiring a separate interface.**
	1. You can highlight code sections to **rewrite, optimize, or migrate** them by adding them to the chat easily.
	2. You can generate **new files or components** (e.g., Python scripts, React components) from natural language prompts.
	3. Supports **three interaction modes** (chat, inline edits, and command-based workflows) for versatile coding assistance.

---

### How Continue.dev Compares To Bigger Alternatives

| Feature               | **Continue.dev**                   | **GitHub Copilot**         | **Cursor**                     |
| --------------------- | ---------------------------------- | -------------------------- | ------------------------------ |
| **Open-Source**       | ✅ Yes                             | ❌ No (Proprietary)        | ❌ No                          |
| **Model Flexibility** | ✅ Choose any model (local/cloud)  | ❌ Locked to OpenAI/GitHub | ❌ Cursor's proprietary models | 
| **IDE Integration**   | ✅ VS Code, JetBrains              | ✅ VS Code, JetBrains      | ✅ Cursor's custom IDE fork    |
| **Privacy**           | ✅ Local hosting option            | ❌ Cloud-dependent         | ❌ Cloud-dependent             |
| **Customization**     | ✅ High (rules, models, workflows) | ❌ Limited                 | ❌ Limited                     |
| **Pricing**           | ✅ Free (API costs may apply)      | ❌ $10–19/month            | ❌ $20/month (Pro)             |

---

## Setup And Usage

This post isn't really about Continue, so I won't go into too much detail about the numerous ways you can set it up here, but you can always refer to their docs or any number of helpful tutorials that are out there. Check out my fellow Mistral Ambassador, [Fahd Mirza](https://www.youtube.com/@fahdmirza)'s tutorial [here](https://www.youtube.com/watch?v=PNUF_ZBa0Tg). The basic things you need to do are:

1. **Installation**:
   - Add the **Continue extension** to VS Code from the plugin marketplace.
   - Restart the IDE and sign in to the Continue hub.

2. **Configuration**:
   - Set up your **preferred AI model** (e.g., Mistral, Anthropic) by entering an API key.
   - Define **project-specific rules** (optional) in `.continue/rules/`.

### Using Mistral's Models

I have Mistral's [Mistral Large](https://mistral.ai/news/mistral-large) as the main AI I'm using in the plugin.

![[02-Merit/Bitblog/Posts/Tech and AI/Using Mistral to Setup My Quartz Blog for Free/Attachments/IMG-20260217192817.png|600]]

*Figure 1: Comparison of GPT-4, Mistral Large (pre-trained), Claude 2, Gemini Pro 1.0, GPT 3.5 and LLaMA 2 70B on MMLU (Measuring massive multitask language understanding).*

Mistral Large shows powerful reasoning capabilities for planning more complex tasks. It also has top performance in coding and math. In the table below, they report the performance across a suite of popular benchmarks to evaluate the coding and math performance for some of the top-leading LLM models:

![[IMG-20260217192817-1 1.png|600]]

_Figure 4: Performance on popular coding and math benchmarks of the leading LLM models on the market: HumanEval pass@1, MBPP pass@1, Math maj@4, GSM8K maj@8 (8-shot) and GSM8K maj@1 (5 shot)._

This allows the model to plan the tasks I give it, and also create code. I use [Codestral](https://mistral.ai/news/codestral-2501) to run my autocompletion, as it is also [recommended by the Continue team](https://docs.continue.dev/customize/model-roles/autocomplete).

### Continue Configuration

The Continue config is held within a `yaml` file, so it's easy to adjust. What this also means is I can even use the plugin itself to enhance my configuration settings.

At the moment, my config looks like this:

```yaml
name: Local Config
version: 1.0.0
schema: v1
models:
  - name: Codestral
    provider: mistral
    model: codestral-latest
    apiKey: 12345
    roles:
      - autocomplete
	promptTemplates:
      autocomplete: |
	      <|fim_prefix|>{{{prefix}}}<|fim_suffix|>{{{suffix}}}<|fim_middle|>
  - name: Codestral Embed
    provider: mistral
    model: codestral-embed
    apiKey: 12345
    roles:
      - embed
  - name: Mistral Large
    provider: mistral
    model: mistral-large-latest
    apiKey: 12345
    roles:
	  - edit
      - chat
      - apply
  - name: Mistral Embed
    provider: mistral
    model: mistral-embed
    apiKey: 12345
    roles:
      - embed
  - name: Gemini 2.5 Flash
    provider: gemini
    model: gemini-2.5-flash
    apiKey: 12345
    roles:
      - edit
      - chat
      - apply
  - name: Gemini 2.5 Pro Experimental
    provider: gemini
    model: gemini-2.5-pro-exp-03-25
    apiKey: 12345
    roles:
      - edit
      - chat
      - apply
  - name: Qwen 2.5 Coder 7b
    provider: ollama
    apiBase: http://localhost:11434
    model: qwen2.5-coder:14b
    roles:
      - autocomplete
      - edit
      - chat
      - apply
  - name: Qwen 3 Embedding
    provider: ollama
    apiBase: http://localhost:11434
    model: qwen3-embedding
    roles:
      - embed
  - name: Codestral
    provider: mistral
    model: codestral
    apiKey: 12345
    roles:
      - rerank
  - name: Voyage Reranker
    provider: voyage
    apiKey: 12345
    model: rerank-2
    roles:
      - rerank
mcpServers:
  - uses: continuedev/continue-docs-mcp
  - name: MCP_DOCKER
    command: docker
    args:
      - mcp
      - gateway
      - run
context:
  - provider: clipboard
  - provider: tree
  - provider: problems
  - provider: debugger
    params:
      stackDepth: 3
  - provider: repo-map
    params:
      includeSignatures: false
  - provider: os
  - provider: terminal
  - provider: code
```

With this setup, I am using the Voyage model recommended by the Continue team. So, I got an API key, but I haven't seen any usage stats on the website, so I'm not sure if it's being used. I'll revisit that setup at a later point.

### MCP Servers

I am also using [Docker](https://www.docker.com/) for my MCP servers. I worry, as many do, [worry about the security of my MCP servers](https://www.docker.com/blog/the-model-context-protocol-simplifying-building-ai-apps-with-anthropic-claude-desktop-and-docker/). I also wanted a simple setup to manage and launch my servers and to keep the config as simple and portable as possible. Since I use Docker on all of my machines and it provides a singular place for me to launch and connect to my servers from, so it seemed like the most obvious choice.

> [!note]+ A Note on Docker Model Runner
> I am thinking about using Docker Model Runner to run local models on my Mac devices because it's tailored for M-series chips and leverages Apple’s Metal API for fast inference. Thereby, maximizing performance by avoiding virtual machine overhead.
> 
> For now, I'm sticking with [Ollama](https://ollama.com/) until I have some time to dig in deeper.

On the Docker Desktop, head to the MCP Toolkit and enable some servers.

![[IMG-20260217192817-2 1.png|800]]

Some, like the Brave MCP server, require configuration or API keys to work properly.

![[IMGS-20260217192818 1.png]]

[Continue uses yaml to configure MCP servers](https://docs.continue.dev/reference/yaml-migration), so you have to convert the json configs from Docker into yaml. You can find these json configs at the bottom of most overview tabs in the Docker Toolkit.

![[IMG-20260217192818-1 1.png|800]]

Once you enable the servers and set up the config in Continue properly, you can have access to all of the servers you have running in Docker in Continue. I know there is a worry about having all of these servers take up the context window in Continue, but you can toggle them on and off to only use the servers you want in any particular environment. Continue can be loaded with project level configurations, so you can be selective about the servers and only enable the ones you want.

To prevent all of the tools from being loaded into Continue and burning up tokens, you can explicitly exclude tools from the config within the `Tools` settings in Continue:

![[IMG-20260217192818-2 1.png|300]]

#### Adding the Continue Documentation MCP Server

You can add MCP servers individually to Continue `config.yaml` file. Learn more about the configuration [here](https://docs.continue.dev/reference#mcpservers). You also add the [Continue Documentation MCP Server](https://docs.continue.dev/reference/continue-mcp) to your config, which allows you to search and retrieve information from the Continue documentation directly within your agent conversations. You can set that up in the following way:

1. Create a folder called `.continue/mcpServers` at the top level of your workspace
2. Add a file called `continue-docs-mcp.yaml` to this folder
3. Write the following contents and save:

```yaml
name: Continue Documentation MCP
version: 0.0.1
schema: v1
mcpServers:
  - uses: continuedev/continue-docs-mcp
```

Or, you can add this directly to the `config.yaml` file directly in the following way:

```yaml
# Your existing config.yaml content
models:
  # your models...

# Add this section
mcpServers:
  - uses: continuedev/continue-docs-mcp
```

This approach keeps all your Continue configuration in one place, rather than managing multiple files. Once configured, you can use the MCP server to search Continue documentation:

**Usage Examples**

[​Model Configuration Help](https://docs.continue.dev/reference/continue-mcp#model-configuration-help)

```plaintext
How do I add Claude 4 Sonnet as a model from Bedrock in Continue?
```

[​Context Providers](https://docs.continue.dev/reference/continue-mcp#context-providers)

```plaintext
What context providers are available in Continue?
```

[​Customization](https://docs.continue.dev/reference/continue-mcp#customization)

```plaintext
How do I add custom rules to my configuration in Continue?
```

> [!warning]+ Enable Agent Mode
> MCP servers only work in [Agent Mode](https://docs.continue.dev/ide-extensions/agent/quick-start). Make sure to switch to agent mode in Continue before use.


#### Enabling Tools In Continue

Additionally, unless you change the settings to `Automatic`, it will ask before each action committed, so you can accept or reject each step without the LLM making wholesale changes to your codebase:

![[IMG-20260217192818-4 1.png|300]]


## Using Mistral To Modify My Config

Now, your environment is set up. When you cloned the Quartz repo, you also downloaded the `docs` folder which holds all of the quartz documentation. You can use this to inform the LLM how the configuration is supposed to work and how you can modify your config files.

For example, I asked it:

```plaintext
Using the @ExplicitPublish.md documentation to add the "ExplicitPlublish" plugin to my config. You can remove the "Remove Drafts" plugin @RemoveDrafts.md since this is repetitive.
```

You can see that it correctly accessed the files as context and then made the correction to the proper spot in the config file.

![[IMG-20260217192818-3 1.png|800]]

You can see that Continue actually shows you where the diff is in your code, so you can see exactly what will be changed. You can accept each action individually in place, or accept all of the actions in bulk in the chat window.

> [!warning]+ Explicit Publish and the index.md file
> Your index.md file will be the landing page for your blog. If you decide to use the Explicit Publish plugin, you will need to explicitly publish it, else you will get a 404 error when someone tries to navigate to your homepage.

Upon accepting the changes, you can see the output of the LLM explain what it did and what the new changes are. You can also ask for these explanations in your prompt to make it a bit more robust as well.

![[IMG-20260217192818-5 1.png|800]]

### Adding More Plugins

Additionally, I asked it to add the [Citations](https://quartz.jzhao.xyz/plugins/Citations) and [HardLineBreaks](https://quartz.jzhao.xyz/plugins/HardLineBreaks) plugins to my config. There is no config for the Hard Line Breaks plugin, but according to the docs

> "This plugin automatically converts single line breaks in Markdown text into hard line breaks in the HTML output. This plugin is not enabled by default as this doesn't follow the semantics of actual Markdown but you may enable it if you'd like parity with [Obsidian](https://quartz.jzhao.xyz/features/Obsidian-compatibility).

The Citations plugin has a bit of configuration that you can understand from the docs:

> [!info] From [Citations](https://quartz.jzhao.xyz/plugins/Citations)
> This plugin accepts the following configuration options:
> - `bibliographyFile`: the path to the bibliography file. Defaults to `./bibliography.bib`. This is relative to git source of your vault.
> - `suppressBibliography`: whether to suppress the bibliography at the end of the document. Defaults to `false`.
> - `linkCitations`: whether to link citations to the bibliography. Defaults to `false`.
> - `csl`: the citation style to use. Defaults to `apa`. Reference [rehype-citation](https://rehype-citation.netlify.app/custom-csl) for more options.
> - `prettyLink`: whether to use pretty links for citations. Defaults to `true`.

You can see Mistral Large making the correct changes to the `quartz.config.ts` file:

![[IMG-20260217192818-6 1.png|800]]

> [!tip]+ A note about your.bib file
> If you have a `.bib` file elsewhere on your comp (for example in a different folder from your [Better BibTeX for Zotero](https://retorque.re/zotero-better-bibtex/) config), you can put the relative path here and have it referenced in quartz. Or, you could put a symlink to wherever you have it in the correct relative path and leave this as is. That way, Zotero can keep your source `.bib` file updated without manual copying or pasting!

You can even ask Mistral to create the symlink for you without leaving the environment:

![[IMG-20260217192818-7.png|800]]

You can see here that I ask Mistral Large to create the symlink. It provides the exact command to run. When you click `Run` it will populate the terminal with the command and you can run it from there.

Now, your config should be good to go for the next steps.

## About Continue's `Compact conversation` Command

As the conversation goes on, you will notice a bar start to appear next to the enter button. You can see it in the photo of the symlink command [[#Adding the Continue Documentation MCP Server|in the section above]]. You can click on the icon with four arrows for `Compact conversation` to generate a summary of the conversation so far so the LLM maintains context, but freeing up that crucial context window real estate. You can see what that looks like here:

![[IMG-20260217192818-8.png|800]]

The summary actually continues for 6 more sections, but you can see that the bar next to the `Enter` button is now gone. 

Now, let's get back to work.

## Changing the Theme

Next, I asked it to change the theme. I use the [Catppuccin](https://catppuccin.com/) Mocha theme in most places, so I figured I'd try that. I downloaded Catppucin's [palette.json](https://raw.githubusercontent.com/catppuccin/palette/main/palette.json) file and provided it to Mistral Large. It used it's advanced tool calling to read the file and to access the style guide. It then provided me with the correct HEX values for the appropriate aspects of my theme configs:

[[Crop and redact this picture before posting online]]

![[IMG-20260217192818-9.png|800]]

You can see the changes to the site here:

Quartz Light Mode:

![[IMG-20260217192818-10.png|800]]

Catppuccin Latte:

![[IMG-20260217192818-11.png|800]]

Quartz Dark Mode:

![[IMG-20260217192818-12.png|800]]

Catppuccin Mocha:

![[IMG-20260217192818-13.png|800]]

You can do a lot more with this via Quartz's `.scss` files, but we won't go over that here. You can take these concepts and get the LLM to change all aspects of your theme and css to make it just to your liking!

## About the Layout

Now that my plugins and themes are all set, I decided to move on to the layout of my site.

You can see [the docs](https://quartz.jzhao.xyz/layout), but here's a brief explanation of how layouts work:

Each page is composed of multiple different sections which contain different `QuartzComponents`. The following code snippet lists all of the valid sections that you can add components to:

`quartz/cfg.ts`

```typescript
export interface FullPageLayout {
  head: QuartzComponent // single component
  header: QuartzComponent[] // laid out horizontally
  beforeBody: QuartzComponent[] // laid out vertically
  pageBody: QuartzComponent // single component
  afterBody: QuartzComponent[] // laid out vertically
  left: QuartzComponent[] // vertical on desktop and tablet, horizontal on mobile
  right: QuartzComponent[] // vertical on desktop, horizontal on tablet and mobile
  footer: QuartzComponent // single component
}
```

These correspond to following parts of the page:

| Layout                          | Preview                        |
| ------------------------------- | ------------------------------ |
| Desktop (width > 1200px)        | ![[IMG-20260217192818-14.png]] |
| Tablet (800px < width < 1200px) | ![[IMG-20260217192818-15.png]] | 
| Mobile (width < 800px)          | ![[IMG-20260217192818-16.png]] |

See [a list of all the components](https://quartz.jzhao.xyz/tags/component) for all available components along with their configuration options. Additionally, Quartz provides several built-in, higher-order components for layout composition. See [layout-components](https://quartz.jzhao.xyz/layout-components) for more details.

You can also checkout the guide on [creating components](https://quartz.jzhao.xyz/advanced/creating-components) if you're interested in further customizing the behavior of Quartz.

### Setting Your Layout

I want to have the layout of the site slightly altered from it's current state. I want the search bar on the right hand side, backlinks at the bottom, and the search bar with dark and light mode in a flex component in the header. Let's see what Mistral Large can do about this...

We can see once again that Mistral Large is able to assess the situation and come up with a plan for altering the code to reflect my requests:

![[IMG-20260217192818-17.png|800]]

Here's the result:

**Before**

![[IMG-20260217192818-18.png|800]]

**After**

![[IMG-20260217192818-19.png|800]]

# Conclusion

In this post, we explored how to use **Continue** in **VSCodium** to interact with Mistral models, enabling you to modify Quartz configuration settings efficiently. From adding plugins like **Explicit Publish** and **Citations** to altering themes and layouts, Mistral Large demonstrated its capability to understand documentation, generate code, and even create symlinks—all while keeping the process transparent and user-friendly.

Customizing your Quartz blog with the help of AI tools like Mistral and Continue can transform a technical and potentially overwhelming process into a seamless and creative experience. Whether you're a seasoned programmer or a novice, leveraging AI within your IDE allows you to make precise, complex modifications to your site without needing deep expertise in TypeScript or web development.

The flexibility of **Continue**, with its open-source nature, support for local models, and customizable workflows—makes it an excellent choice for those who prioritize privacy and control. By integrating **MCP servers** from **Docker**, you can further streamline your setup and ensure that your AI tools are both powerful and secure.

Finally, the ability to tweak your blog’s appearance and functionality empowers you to create a truly personalized digital space. With AI assistance, the barriers to customization are lower than ever, allowing you to focus on what matters most: sharing your ideas with the world.

Now that your Quartz blog is tailored to your preferences, the next step is to fill it with content and continue refining it as your needs evolve. Happy blogging!