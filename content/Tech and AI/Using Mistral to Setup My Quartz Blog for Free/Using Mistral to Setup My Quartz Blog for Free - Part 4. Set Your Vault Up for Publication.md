---
created: 2026-02-17
updated: 2026-03-02
tags:
  - mistral
  - pkm
  - writing
description: This is post 4/5 about how to set up a blog for free using Obsidian, Quartz, and Mistral AI
publish: true
title: Part 4. Set Your Vault Up for Publication
---

> [!info]+ This Post is Part of a Multi-part Series
> This post is **part 4 of 5** of the Using Mistral to Setup My Quartz Blog for Free Series. If you haven't read the previous posts yet, you should start there before working through this post:
> 
> **Navigate Through the Series**
> 
> - [Part 1. Install and Set Up Quartz](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%201.%20Install%20and%20Set%20Up%20Quartz.md)
> - [Part 2. Set Up a GitHub Repository](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%202.%20Set%20Up%20a%20GitHub%20Repository.md)
> - [Part 3. Host Your Vault Online](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%203.%20Host%20Your%20Vault%20Online.md)
> - [Part 4. Set Your Vault Up for Publication](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%204.%20Set%20Your%20Vault%20Up%20for%20Publication.md)
> - [Part 5. Use Mistral to Modify Quartz Configuration Settings](Using%20Mistral%20to%20Setup%20My%20Quartz%20Blog%20for%20Free%20-%20Part%205.%20Use%20Mistral%20to%20Modify%20Quartz%20Configuration%20Settings.md)
# Step 4. Set Your Vault Up For Publication

## Opening Your Quartz Repository In Obsidian

If you decided to start with a blank content folder, or copied a folder into it, you'll need to make sure you set up that new vault with all of the plugins and settings you have in your current Obsidian vault. You can easily do this by just copying over your `.obsidian` folder into your content folder as well. You can then open the `content` folder as a vault in Obsidian.

## Create a Note Template In Obsidian

Quartz needs certain properties in the frontmatter to publish notes and manage your site structure. You _could_ just type these out each time, but an easier way to do this is to use a template. You can use either the core [Templates](https://help.obsidian.md/plugins/templates) plugin, or you could use the community plugin [Templater](https://github.com/SilentVoid13/Templater). I use Templater extensively throughout my vault, so install and enable that before continuing with this tutorial.

In Obsidian, create a note in your dedicated template folder called `quartz_draft` (or whatever you want it to be called). In that note, you can use this template when you go to create a new blog post:

```markdown
---<%*  
let title = tp.file.title  
if (title.startsWith("Untitled")) {  
title = await tp.system.prompt("Title?") ?? "Untitled";  
await tp.file.rename(`${title}`);  
} %>  
created: <% tp.date.now() %>  
updated: <% tp.date.now() %>  
title: "<% tp.file.title %>"
aliases: [<% await tp.system.prompt("Aliases? (Comma Separated)") %>]  
tags: [<% await tp.system.prompt("Tags? (Comma Separated)") %>]
description: "<% await tp.system.prompt("What's this post about?") %>"
publish: false
---

# <% tp.file.title %>

<% tp.file.cursor(0) %>
```


This Templater script is a **dynamic note template** for Obsidian that automates the creation of a new note with structured metadata. Here's what it does in brief:

- The little script at the top of the file checks and sets the note title.
  - If the note starts with "Untitled", it prompts the user to enter a custom title and renames the file accordingly.
- Then, it adds dynamic metadata fields automatically or via user prompt.
  - The `created` and `updated` fields are automatically populated with the current date's timestamp.
  - The `title` field uses the note's filename by default, but you can change this if you don't use filenames as the titles of your posts.
  - The `aliases`, `tags`, and `description` fields are filled by prompting the user to input these values (comma-separated for aliases/tags) and puts them in an array. (**Note**: I now use the QuickAdd plugin to manage my templates because it allows me to use a dynamic field that pulls up my tags as I type them to ensure I don't mistype, but this method is simpler to set up and should work to get you started. I plan to write another post on how I have my QuickAdd macros set up and how I have AI plugged into them to augment and enhance them as well).
  - The `publish` field is set to a default value of `false` for use with Quartz's [ExplicitPublish](https://quartz.jzhao.xyz/plugins/ExplicitPublish) plugin for easy publication management (more on this in the [[Using Mistral to Setup My Quartz Blog for Free - Part 5. Use Mistral to Modify Quartz Configuration Settings|next post]]).
- The `<% tp.file.cursor(0) %>` then places the cursor at the start of the note for immediate editing.

**Why Use This?**
- **Saves Time**: No manual typing for boilerplate frontmatter.
- **Consistency**: Ensures all notes have the same structure and fields (critical for Quartz publishing).
- **User-Friendly**: The interactive prompts guide you through your note setup.

**Example Output** (after filling prompts):

```markdown
---
created: 2023-11-15
updated: 2023-11-15
title: "My Awesome Post"
aliases: [awesome, blog post]
tags: [writing, productivity, obsidian]
description: "A guide to creating awesome content in Obsidian"
publish: false
---

# My Awesome Post

`<cursor position>`
```

> [!tip]+ How to Use this Template
> Remember! To use this template properly, you need to have the [ExplicitPublish](https://quartz.jzhao.xyz/plugins/ExplicitPublish) plugin enabled, which will filter out all notes except for any that have `publish: true` in the frontmatter.

Now in Obsidian, you can create a new note with your new template and change the `publish` key to the value of `true` to get quartz to publish that page to your site!

## Frontmatter In Quartz

You can add other yaml values to your notes as well. Their functions work alongside various Quartz plugins, but you can always refer to the [Quartz Documentation](https://quartz.jzhao.xyz/plugins/) to learn more. Quartz natively supports the following frontmatter:

- title
	- `title`
- description
	- `description`
- permalink
	- `permalink`
- comments
	- `comments`
- lang
	- `lang`
- publish
	- `publish`
- draft
	- `draft`
- enableToc
	- `enableToc`
- tags
	- `tags`
	- `tag`
- aliases
	- `aliases`
	- `alias`
- cssclasses
	- `cssclasses`
	- `cssclass`
- socialDescription
	- `socialDescription`
- socialImage
	- `socialImage`
	- `image`
	- `cover`
- created
	- `created`
	- `date`
- modified
	- `modified`
	- `lastmod`
	- `updated`
	- `last-modified`
- published
	- `published`
	- `publishDate`
	- `date`

### Plugin Settings

Quartz plugins run a series of transformations over your content.

![[IMG-20260217192817 1.png]]

`quartz.config.ts`

```typescript
plugins: {  
	transformers: [...],  
	filters: [...],  
	emitters: [...],
}
```

- [Transformers](https://quartz.jzhao.xyz/tags/plugin/transformer) **map** over content (e.g. parsing frontmatter, generating a description)
- [Filters](https://quartz.jzhao.xyz/tags/plugin/filter) **filter** content (e.g. filtering out drafts)
- [Emitters](https://quartz.jzhao.xyz/tags/plugin/emitter) **reduce** over content (e.g. creating an RSS feed or pages that list all files with a specific tag)

You can customize the behavior of Quartz by adding, removing and reordering plugins in the `transformers`, `filters`, and `emitters` fields.

To add the [ExplicitPublish](https://quartz.jzhao.xyz/plugins/ExplicitPublish) plugin (a [Filter](https://quartz.jzhao.xyz/tags/plugin/filter)), you would add the following line:

`quartz.config.ts`

```typescript
filters: [  
	...  
	Plugin.ExplicitPublish(),  
	...
],
```

To remove a plugin, you should remove all occurrences of it in the `quartz.config.ts`.

The configuration settings are fairly straightforward and written in Typescript. Typescript is fairly human-readable, but I am not a programmer, so I doubt my skills to make any significant or custom alterations to settings to get this site up like I want it. This is where Mistral comes in. 

Let's talk about [[Using Mistral to Setup My Quartz Blog for Free - Part 5. Use Mistral to Modify Quartz Configuration Settings|Part 5. Using Mistral to Modify Quartz Configuration Settings]] and how to work with LLMs to modify your config next.
