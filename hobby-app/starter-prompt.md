# Starter prompt

Paste as the first message in each model session. Nothing attached.

Rewrite any phrasing that does not sound like you before you use it. You are answerable for the
final text, and the idea reads better when the wording is yours.

Two things to set per session before pasting:

- Replace `MODEL` in the log filename with the model that session is running, so the file says
  who wrote it: `prompt-log-gemini.md`, `prompt-log-chatgpt.md`, `prompt-log-claude.md`. Add the
  version if you are running more than one model from the same vendor. One file per session,
  since two agents appending to the same file at once will overwrite each other. Merge them
  yourself later.
- Check the path is right for where that session is rooted. If the session is not opened at the
  repository root, give it the path it can actually see.

Set the filename yourself rather than letting the model pick it. The prompt also asks each model
to state its own name and version inside the entries, which is worth having, but models are
unreliable about their exact version and sometimes claim the wrong one. If a model's
self-reported version contradicts the filename you set, trust the filename.

If a session has no filesystem access, drop the third paragraph and paste its replies into the
log yourself.

---

```
I want to build a website that can help you choose a hobby. I like starting new hobbies quite often, but sometimes it is hard to pick one and know what it will take to start one. Sometimes I want to do something in the comfort of my couch, sometimes I need something that is cheap, and maybe I want to do something that is physically challenging. Finding out how much effort (mental, physical, monetary, and time availability) a hobby requires can be slow and difficult since the information is scattered. I might need to search up and watch multiple YouTube videos or buy some material to realize that this will take more effort than I was willing to put in. The website should have multiple hobby categories, and hobbies that show how much effort they will demand, in a form that you can explore and filter according to your wants. Once one is picked, the website provides some guidance on where to start: what to buy, what kind of things you should learn, and some guidance on how to progress on the hobby. Act as a product manager for this product and write a draft product vision statement. The name that I have for this product is NextHobby. 

Keep a log of our session as we go. After every reply you give me, including this one, append an entry to hobby-app/prompt-log-claude.md, creating the file if it does not exist. Each entry needs the date and time, my prompt copied verbatim and unedited, which model and version you are, and a short factual summary of what you produced.
```
