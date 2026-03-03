---
created: 2025-12-23
updated: 2026-02-19
tags: []
publish: false
---

# Overview

I am following the tutorial that [Matt Williams](https://www.youtube.com/@technovangelist) put out over a series of videos

1. [Saved Links Are Useless—Until You Automate with Karakeep and Ollama - YouTube](https://www.youtube.com/watch?v=2fbmlgu0Lkc&t=1s)
2. [Supercharge Bookmarks with n8n, Ollama, and Karakeep - YouTube](https://www.youtube.com/watch?v=eydMCTfbYz8&t=2s)
3. [Karakeep Automation on Steroids with Custom Node - YouTube](https://www.youtube.com/watch?v=ZkmsaNoaFNA&t=725s)

**Why n8n + Karakeep?**
- **Customizable automation**: Replace generic prompts with **webhooks, custom processing, and API updates**.
- **Unlimited flexibility**: Use any AI service and adapt workflows for any content type.

	> _"N8n transforms CareKeep from basic AI to completely customizable automation."_ (15:02) _"Webhook plus custom processing plus API update equals unlimited customization."_ (15:36)

They move from showing you how to set up AI features in Karakeep to auto tag and create summaries, to workin gwith his custom Karakeep node in [[n8n]] to create custom workflows that use the basic structure of:

```mermaid
flowchart LR
    A([webhook]) -->|trigger| B[[ai processing]]
    B -->|output| C[api]

    style A fill:#4CAF50,stroke:#2E7D32,color:white,stroke-width:2px
    style B fill:#2196F3,stroke:#0D47A1,color:white,stroke-width:2px
    style C fill:#FF9800,stroke:#BF360C,color:white,stroke-width:2px
```

## Workflow Ideas

These tutorials are just the beginning. I've already gotten some good ideas with some other programs now that I know how this flow should go. I am thinking about doing something with [[Zotero]] and [[Obsidian]] of course. As Matt Williams says, with this, the possibilities are endless and I can see his point. He describes some possible workflows:

**1. Research Workflows**

- **Auto-categorize academic papers** by methodology (qualitative, quantitative, mixed methods).
- **Extracts abstracts, research domains, and key findings**, adding structured metadata to bookmarks for better searchability.

	> _"When you bookmark a research paper, the workflow extracts the abstract, identifies whether it's qualitative, quantitative or mixed methods and tags it accordingly."_ (13:39)

**2. Content Workflows**
- **Extracts key quotes, themes, and argument structures** from articles.
- **Generates actionable summaries**: three most quotable sentences, main arguments, and supporting evidence.

	> _"Instead of generic summaries, you get the three most quotable sentences and the main argument structure and any supporting evidence."_ (14:02)

- Ideal for **content creators** and **literature reviews**.

**3. Learning Workflows**
- **Generates study notes** from educational content (tutorials, courses).
- **Creates flashcards, key concept definitions, and practice questions**.
- **Identifies learning objectives, prerequisites, and suggests related topics**.

	> _"Bookmark a tutorial or course and get automatically generated flashcards, key concept definitions and practice questions."_ (14:23)

**4. Business Workflows**
- **Analyzes competitor content and trends**.
- **Extracts strategies, tools mentioned, and recurring themes** from bookmarked blog posts or case studies.

	> _"You end up with competitive intelligence that's actually organized and actionable."_ (14:55)

## Why I'm Writing This Tutorial

The videos are great and enabled me to put this together, but I wanted to include how to network this with [[Tailscale]] and because there is no written version of this tutorial for people who prefer to follow with tutorials you can take in at your own pace and also copy/paste code.

## Installation

### Creating Credentials

![[06-Assets/Attachments/Karakeep and n8n Automation/IMG-20260217192817.png]]

### Webhook Node

Next, create a webhook node:

![[06-Assets/Attachments/Karakeep and n8n Automation/IMG-20260217192817-1.png]]

## n8n To Karakeep Header Auth

In his video that works with his custom node, he suggests putting credentials in the workflow to deal with some privacy concerns, but even though I don't think I need it while using [[Tailscale]]. If they can get to my service from there, they've got my whole system. So, since I don't expose my services to the internet, I decided to roll with it anyway to follow one of his tutorials all the way through.

So the bearer key I have to save elsewhere because once it's entered into n8n, it'll be inaccessible.

`Bearer a1b2c3d4-e5f6-7890-g1h2-i3j4k5l6m7n8`

## Webhook Error

I got a **critical error** in my KaraKeep logs when I tried saving a new article and getting the webhook to run:

`error: [webhook][342] Webhook to http://100.119.246.121:5678/webhook-test/782d15c7-9081-42ef-b1b3-9959e2dfa96d call failed: Error: Refusing to access disallowed IP address 100.119.246.121 (requested via http://100.119.246.121:5678/webhook-test/782d15c7-9081-42ef-b1b3-9959e2dfa96d)`

Now, the **root cause** of this error was because KaraKeep was **blocking the webhook request** because it considered `100.119.246.121` (a Tailscale IP) a **disallowed IP address**. This is a security feature to prevent SSRF (Server-Side Request Forgery) attacks.

Now, what this meant was that I had to allow the Tailscale IP in KaraKeep by configuring it to allow requests to my Tailscale IP.

The officially supported environment variable for allowing internal IP addresses (including webhooks) in KaraKeep is:

**`CRAWLER_ALLOWED_INTERNAL_HOSTNAMES`**[^1]

This variable allows you to specify a comma-separated list of internal hostnames or IP addresses that KaraKeep is permitted to access for server-initiated requests, such as webhooks. If your webhooks are targeting internal services (like your n8n instance on a Tailscale IP), you must explicitly allowlist them using this variable.

---

### **How To Use It**

1. Open your `.env` file and add:

	`CRAWLER_ALLOWED_INTERNAL_HOSTNAMES=100.119.246.121`

	If you have multiple IPs or domains, separate them with commas:

	`CRAWLER_ALLOWED_INTERNAL_HOSTNAMES=100.119.246.121,another.internal.ip`

2. Update your `docker-compose.yml` to pass this variable:

	```yaml
	---
	services:
	  web:
	    image: ghcr.io/karakeep-app/karakeep:${KARAKEEP_VERSION:-release}
	    container_name: karakeep
	    restart: unless-stopped
	    volumes:
	      - ./data:/data
	    ports:
	      - 5000:3000
	    env_file:
	      - .env
	    environment:
	      MEILI_ADDR: http://meilisearch:7700
	      BROWSER_WEB_URL: http://chrome:9222
	      CRAWLER_ALLOWED_INTERNAL_HOSTNAMES: ${CRAWLER_ALLOWED_INTERNAL_HOSTNAMES}
	```

3. Restart KaraKeep:

	`docker-compose down && docker-compose up -d`

---

It finally worked. I got the right output from Karakeep to the webhook! 🙌

![[06-Assets/Attachments/Karakeep and n8n Automation/IMG-20260217192817-2.png]]

```json
[
  {
    "headers": {
      "accept": "*/*",
      "accept-encoding": "gzip, deflate, br",
      "authorization": "Bearer a1b2c3d4-e5f6-7890-g1h2-i3j4k5l6m7n8",
      "content-length": "238",
      "content-type": "application/json",
      "user-agent": "node-fetch",
      "host": "100.119.246.121:5678",
      "connection": "keep-alive"
	    },
    "params": {},
    "query": {},
    "body": {
      "jobId": "424",
      "bookmarkId": "wiv1hy90lspe1o8kq6igyxfq",
      "userId": "fgxm0jbs3mx2ebssocxzu7i1",
      "url": "https://medium.com/@yongjinL/build-a-second-brain-from-zotero-highlights-with-n8n-and-rag-c761c2887fde",
      "type": "link",
      "operation": "crawled"
    },
    "webhookUrl": "http://100.119.246.121:5678/webhook-test/782d15c7-9081-42ef-b1b3-9959e2dfa96d",
    "executionMode": "test"
  }
]
```

Now, the world's my oyster.

## The Rest Of the Nodes

# **References**

[^1]: KaraKeep GitHub Releases:"All server-initiated requests (including webhooks) to internal IP addresses are now blocked by default unless explicitly allowed via CRAWLER_ALLOWED_INTERNAL_HOSTNAMES."](<https://github.com/karakeep-app/karakeep/releases>
