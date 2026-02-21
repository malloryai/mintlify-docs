# DeepWiki structure review: user-facing concepts and content

This document reviews how DeepWiki and similar AI-generated/structured docs organize content, and applies those patterns to Mallory’s **user-facing** concepts and content (product usage, mental model, key ideas).

---

## Starting point: build on the template

We’re **building on the existing Mintlify template** (this repo, “Mint Starter Kit”), not starting from an empty site.

- **Keep:** Mintlify platform, `docs.json` schema, theme, repo, and any existing build/deploy setup.
- **Replace:** Site name, branding (colors, logo, favicon), and **all navigation** with the Mallory structure (First steps, Use Mallory, Build & integrate, API Reference).
- **Replace:** Placeholder pages (index, quickstart, development, essentials/_, ai-tools/_) with Mallory content; API reference with `https://api.mallory.ai/openapi.json` (remove the Plant Store example).
- **Remove or repurpose:** Template groups that don’t map to Mallory (e.g. “Customization”, “Writing content”, “AI tools”)—either delete those pages or repurpose the folders for Mallory pages.

So: same stack and repo, new nav and content. No need for a separate “fresh” docs repo.

---

## 1. What we looked at

- **DeepWiki (Devin)**: `.devin/wiki.json` steers auto-generated wikis with `repo_notes` (context/priorities) and `pages` (title, purpose, parent for hierarchy). Aimed at **codebase/developer** docs; the structural patterns still inform how to group and name user-facing topics.
- **DeepWiki (deepwiki.com)**: Public repo indexing; “AI documentation you can talk to.” We used it to inspect **wiki structure** (toc/hierarchy) for well-known repos.
- **Example wiki structures** (from DeepWiki `read_wiki_structure`):
  - **anthropics/anthropic-cookbook**: Overview (structure, getting started) → Development Guide → Skills → Tool use & memory → RAG → Multimodal → Advanced API → QA.
  - **stripe/stripe-python**: Overview (install, versioning) → Core architecture (HTTP, errors, object model) → API resources (by domain) → Service classes → Testing → Advanced.
  - **facebook/react**: Overview (structure) → Feature flags → Build system → Reconciler (Fiber, hooks, scheduling, etc.) → SSR → Platform implementations → DevTools.

---

## 2. Patterns relevant to user-facing docs

### Overview and getting started first

- All three put an **Overview** at the top, with **Getting started** (or equivalent) as a direct child or sibling.
- User-facing equivalent: **Overview** (what Mallory is, who it’s for) and **Quickstart** (first value in a few steps) as the first two items in “First steps.”

### Concepts by domain/capability, not by code

- Anthropic cookbook groups by **capability** (Skills, Tool use, RAG, Multimodal, Advanced API), not by folder.
- Stripe groups by **domain** (Payment, Customer, Billing, Terminal).
- For Mallory **user** docs: group by **what the user does** (Chat, Current events, Entities, Indicators), not by backend modules.

### Shallow hierarchy for concepts

- Top-level themes have **one or two levels** of children (e.g. “RAG” → Basic pipeline, Vector DBs, Advanced).
- Avoid deep trees (e.g. more than 2 levels) for main nav so “user-facing concepts” stay scannable.

### One “concepts” hub with clear children

- Anthropic’s Overview includes “Repository structure” and “Getting started” as explicit children.
- We can mirror that with a **Key concepts** page whose children are the core mental-model topics: **Sources**, **References & content chunks**, **Mentions**, **Entities**, **Indicators** (matching [docs-old user-guides/concepts](docs-old/user-guides/concepts.md)). That gives one place for “understand the model” and keeps the nav flat enough.

### Development vs product usage

- “Development Guide” (contributing, testing, CI) is separate from “Skills” / “Tool use” / “RAG.”
- For Mallory: **First steps** and **Use Mallory** = product usage and concepts; **Build & integrate** = integration/API/developer; **API Reference** = reference only.

### Advanced / reference at the end

- “Advanced API,” “Advanced topics,” “Testing” tend to come after the main capability groups.
- Our plan already puts **API Reference** last and keeps “Advanced” topics (e.g. monitoring, exports) under **Build & integrate**.

---

## 3. Recommended application to Mallory user-facing content

### First steps (everyone)

- **Overview** – What Mallory is, core value (CTI, SOC, VM). Short.
- **Quickstart** – Minimal path to first value (e.g. sign up, search, use Chat).
- **Key concepts** – Single “concepts hub” page that:
  - Explains the mental model in one place (sources → references & chunks → mentions → entities → indicators).
  - Optionally links to **child concept pages** for users who want depth:
    - **Sources** – Where data comes from (blogs, advisories, feeds, etc.).
    - **References & content chunks** – What a reference is, what chunks are, how they’re analyzed.
    - **Mentions** – How entities are linked to references (where/when/how an entity is discussed).
    - **Entities** – Threat actors, malware, vulns, organizations; how they’re updated and linked.
    - **Indicators** – IOCs/observables; how they’re enriched and tied to entities.
- **Changelog / What’s new** – Release notes, new features, and notable changes (see below).

This mirrors DeepWiki-style “Overview + Getting started + one concepts hub with optional children” so user-facing concepts are findable and not buried.

### Changelog / What’s new (required)

Include a dedicated **Changelog** or **What’s new** section in the nav (e.g. under First steps or as its own top-level group). It should:

- Surface **release notes** and **new features** so users and developers can see what changed without leaving the docs.
- Be easy to find—either a single “What’s new” page that links to or embeds release notes, or a versioned changelog (e.g. by date or version).
- Cover both product updates (UI, Chat, dashboards) and API/platform changes (new endpoints, breaking changes) as appropriate.

### Use Mallory (user-facing)

- **Chat** – How to use the conversational UI.
- **Current events & dashboards** – Curated events and dashboards.
- **Threat entities** – Browsing and understanding actors, malware, vulnerabilities, organizations.
- **Indicators** – Using the IOC/observables feed.

Grouped by **user task/capability**, not by code or API.

### Optional: concept deep-dives

If we add child pages under **Key concepts** (Sources, References & content, Mentions, Entities, Indicators), keep each to one clear idea and link back to the concepts hub and to the relevant “Use Mallory” page (e.g. Entities concept → Threat entities usage).

---

## 4. Summary

| DeepWiki pattern                 | Mallory application                                                     |
| -------------------------------- | ----------------------------------------------------------------------- |
| Overview + Getting started first | Overview + Quickstart in “First steps”                                  |
| Group by capability/domain       | Use Mallory: Chat, Current events, Entities, Indicators                 |
| Shallow hierarchy                | Key concepts = 1 hub + optional 1 level of children                     |
| One concepts hub                 | “Key concepts” with Sources, References, Mentions, Entities, Indicators |
| Development separate             | Build & integrate (and API Reference) separate from Use Mallory         |
| Advanced / reference last        | API Reference last; advanced topics under Build & integrate             |
| Changelog / What’s new           | Dedicated nav item under First steps; release notes and new features    |

This keeps **user-facing concepts and content** aligned with how DeepWiki-style docs stay scannable and capability-oriented, while still allowing deeper concept pages for users who want them.
