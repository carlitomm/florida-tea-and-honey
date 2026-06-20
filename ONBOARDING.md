# Onboarding — working on the Florida Tea and Honey store with Claude

Welcome. This guide is for a **non-technical** teammate who will make changes to the
Florida Tea and Honey Shopify store by talking to **Claude Code** (an AI assistant that
runs in the terminal). You do **not** need to know how to code. You describe what you want;
Claude does the technical work and shows you the result.

Read this once, then keep it open for the first few sessions.

---

## 1. What you are working on

- **The store:** https://floridateaandhoney.com (sells tea, honey and cacao).
- **The theme:** the visual design + layout of the store. We use a customized version of
  Shopify's "Horizon" theme with a special look.
- **This folder** (on the computer) holds all the theme's files. Claude edits files here, and
  we "push" them to the live store when approved.
- **Claude Code** is the assistant. You open it inside this folder and chat with it in plain
  language (Spanish or English).

There are two copies of the store you'll hear about:
- **Live store** — what real customers see. Changing it is serious. We only do it on purpose.
- **Preview / dev** — a private practice copy at `http://127.0.0.1:9292` that Claude uses to
  try things. Changing the preview does **not** affect customers.

---

## 2. The 5 golden rules (most important part)

Claude is instructed to follow these automatically (they live in `CLAUDE.md`), but **you
should know them** so you can tell if something is off. If Claude ever seems about to skip
one, stop and ask it to follow the rule.

1. **Pull first, every time.** Before changing anything, Claude downloads ("pulls") the
   latest version of the store. This captures any edits the owner made in the Shopify admin
   so we never accidentally erase them. → You can say: *"Pull the latest first."*

2. **Never go live without your explicit OK.** Claude will NEVER publish changes to the real
   store until you clearly say **"go live"**. Each "go live" approves **one** change only.
   Until then, everything stays in the private preview. If you're not ready, just keep
   reviewing.

3. **Always see the change before trusting it.** Claude shows you **screenshots** of the
   preview on desktop and phone sizes. Always look at the screenshot before approving. If it
   doesn't look right, say so — describe what's wrong in your own words.

4. **Everything is written in English.** The code, notes, and history are kept in English so
   the project stays consistent. You can still **chat** with Claude in Spanish.

5. **Always save to GitHub.** After a change is approved, Claude saves a backup to GitHub so
   the project is never lost and always matches what's live. → You can say: *"Push to GitHub."*

---

## 3. How a normal session goes

1. **Open Claude** in this folder (ask Carlos to set up the shortcut once).
2. **Tell Claude what you want**, in plain language. Examples:
   - *"On the shop page, make the search bar a bit smaller."*
   - *"Change the homepage banner text to 'Summer sale now on'."*
   - *"The Cacao product images look too dark — can we brighten the section?"*
3. **Claude pulls the latest, makes the change in the preview, and shows you a screenshot.**
4. **You review.** Happy? Say so. Not happy? Describe the problem; Claude adjusts and shows
   you again. Repeat until it's right.
5. **When you're satisfied, say "go live".** Claude publishes just that change to the real
   store and shows you the live result.
6. **Claude saves the backup to GitHub.**

You stay in control the whole time. Nothing reaches customers without your "go live".

---

## 4. How to ask for changes well

- **Say what you want, not how to build it.** "Make the button bigger and gold" is perfect.
- **Point to where.** Mention the page (homepage, shop page, a product page) and the part
  (header, search bar, banner, product card).
- **One thing at a time** is easiest to review, but you can batch related tweaks.
- **It's fine to be unsure.** Ask *"What are my options?"* and Claude will suggest a few.
- **Send a screenshot or a reference** if you have one ("make it look like this site").

---

## 5. Safety — what to be careful about

- ✅ **Safe anytime:** asking Claude to try things in the **preview**, taking screenshots,
  reviewing, asking questions. None of this touches customers.
- 🟡 **Needs your clear "go live":** anything that reaches the real store.
- 🔴 **Avoid / ask Carlos first:**
  - Don't ask Claude to "publish the whole theme" or "push everything" — changes go out
    **file by file** to protect the owner's admin edits.
  - Don't delete files, products, or collections unless Carlos confirmed it.
  - If Claude warns you that a change could overwrite the owner's work, **stop** and check
    with Carlos.
- If anything looks broken on the live store, tell Carlos — there are backup copies of the
  theme to roll back to.

---

## 6. Words you'll hear (quick glossary)

- **Pull** = download the latest version of the store into this folder.
- **Push / go live** = upload a change to the real store so customers see it.
- **Preview / dev server** = the private practice copy (`127.0.0.1:9292`), customers can't see it.
- **Commit** = save a snapshot of a change with a short note.
- **GitHub** = the online backup of the whole project.
- **Theme** = the design/layout of the store.
- **Playwright** = the tool Claude uses to take the screenshots you review.

---

## 7. If you get stuck

- Ask Claude: *"Explain what you're about to do in simple terms."*
- Ask Claude: *"Did you pull the latest first?"* / *"Show me a screenshot."*
- Nothing is final until you say **"go live"**, so it's safe to experiment in the preview.
- When in doubt, ask Carlos.

The detailed technical rules Claude follows are in **`CLAUDE.md`** (same folder) — you don't
need to read it, but it's there if you're curious.
