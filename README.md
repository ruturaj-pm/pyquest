# 🐍 PyQuest

A free, gamified Python course that runs **entirely in the browser**. No accounts, no backend, no paywall — one HTML file.

**6 modules · 28 lessons · ~890 XP** — print & variables → f-strings → conditionals → loops → lists → functions → a capstone program. Each lesson is concept → quiz → real code challenge with instant pass/fail, XP, streaks, levels, and a printable certificate at the end.

Python runs on the visitor's own device via [Pyodide](https://pyodide.org) (Python compiled to WebAssembly), loaded from a CDN. Hosting this site costs nothing and scales to any number of learners.

---

## Run it locally

Download `index.html` and double-click it. That's the whole installation. (First load fetches the ~10 MB Python engine; after that it's cached.)

---

## Deploy on GitHub Pages (free, ~5 minutes)

1. Create a GitHub account at github.com if you don't have one.
2. Click **＋ → New repository**. Name it `pyquest`. Set it to **Public**. Click **Create repository**.
3. On the new repo page, click **uploading an existing file**, drag in `index.html`, `README.md`, and `LICENSE`, then click **Commit changes**.
4. Go to **Settings → Pages** (left sidebar).
5. Under **Build and deployment → Source**, choose **Deploy from a branch**. Branch: `main`, folder: `/ (root)`. Click **Save**.
6. Wait ~1 minute, refresh the page. Your site is live at:
   `https://YOUR-USERNAME.github.io/pyquest/`

Every future edit: change the file, commit, and the site updates itself.

---

## Add it to your own website

**Option A — link to it.** Simplest and best on mobile:

```html
<a href="https://YOUR-USERNAME.github.io/pyquest/">Learn Python free →</a>
```

**Option B — embed it** inside a page on your site:

```html
<iframe
  src="https://YOUR-USERNAME.github.io/pyquest/"
  style="width:100%; height:100vh; border:0; border-radius:12px"
  title="PyQuest — learn Python">
</iframe>
```

**Option C — custom domain.** In **Settings → Pages → Custom domain**, enter e.g. `learn.yourdomain.com`, then add a CNAME record at your domain registrar pointing `learn` → `YOUR-USERNAME.github.io`.

---

## Add or edit lessons (no framework, no build step)

The **entire curriculum** lives in one block near the top of the `<script>` in `index.html`, marked `CURRICULUM`. It's plain data — edit it and refresh.

A module looks like:

```js
{ id:"m7", num:7, title:"My new module",
  lessons:[
    { id:"m7l1", title:"Lesson name", sub:"one-line description", xp:25,
      steps:[ /* learn / quiz / code steps */ ]
    }
  ]
}
```

The three step types:

```js
// 1) LEARN — short explanation + optional runnable example
{ type:"learn", title:"Headline",
  body:["First short paragraph. HTML like <code>print()</code> allowed.",
        "Second paragraph."],
  example:'print("runnable demo code")',     // optional
  exampleInputs:["Priya"]                    // optional: auto-typed answers for input()
}

// 2) QUIZ — one multiple-choice question (+5 XP first try)
{ type:"quiz", title:"Quick check",
  q:"The question. HTML allowed.",
  opts:["Option A","Option B","Option C"],
  answer:1,                                  // index of the correct option (0-based)
  why:"Shown after a correct answer — explain the idea."
}

// 3) CODE — a challenge auto-checked against your rules
{ type:"code", title:"Your turn",
  task:"What to build. HTML allowed.",
  starter:'x = 5\n',                         // pre-filled code (\n = newline)
  inputs:["Rohan","6"],                      // optional: what the "test user" types into input()
  checks:[
    {kind:"output", mode:"exact",    value:"180",      msg:"Shown when this check fails"},
    {kind:"output", mode:"contains", value:"Welcome",  msg:"..."},
    {kind:"code",   contains:"for",                    msg:"Must use a for loop"},
    {kind:"code",   containsAny:['f"',"f'"],           msg:"Must use an f-string"}
  ],
  hint:'The solution or a strong nudge — shown only when "Need a hint?" is tapped.'
}
```

Rules of thumb:

- Give every lesson and module a **unique `id`** — progress is saved against it.
- `mode:"exact"` compares the *entire trimmed output*; use `"contains"` when learners personalise the answer.
- Modules unlock in order (beat the previous module's boss). Mark a boss lesson with `boss:true` and give it more XP.
- If you change the XP economy, adjust the `LEVELS` thresholds just below the curriculum.

---

## Features

- ✅ Real Python (Pyodide/WebAssembly) — not multiple-choice-only
- 🎮 XP, coin bursts, daily streaks, 7 level titles, module locking
- 🧯 Infinite-loop rescue (runaway code is stopped after 300k steps, with a friendly hint)
- 🗣️ Tracebacks translated into plain English for beginners
- 🧪 Simulated `input()` so interactive programs are auto-gradable
- 🏆 Printable certificate on 100% completion
- 📱 Mobile-friendly; progress saved on-device (localStorage)
- 🔓 MIT licensed — fork it, translate it, teach with it

## Credits

Curriculum and engine built with Claude (Anthropic). Python-in-the-browser by the Pyodide project. Maintained by you.
