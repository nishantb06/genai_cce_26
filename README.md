# Deep Generative Models — CCE 2026

An [Obsidian](https://obsidian.md/) vault of lecture notes and concept maps for the **Deep Generative Models** course (CCE 2026) taught by **Dr. Prathosh A P** at IISc.

The vault is organized as a linked knowledge graph: probability foundations → generative modelling → VAEs, GANs, diffusion models, and LLMs.

**Start here in Obsidian:** [`home.md`](home.md)

---

## What's in this repo

| Path | Contents |
|------|----------|
| [`home.md`](home.md) | Course dashboard — syllabus, links, references |
| [`Topics/`](Topics/) | Concept notes (probability, divergences, generative models, …) |
| [`Lectures/`](Lectures/) | Lecture notes |
| [`Assignments/`](Assignments/) | Problem sets and implementations |
| [`Resources/`](Resources/) | Textbooks, papers, drive links |
| [`Instructor/`](Instructor/) | Instructor info |
| [`.obsidian/`](.obsidian/) | Vault settings (shared across clones) |

Course PDFs and scratch files (e.g. `ocr.md`) may also live at the repo root.

---

## Obsidian setup

### 1. Install Obsidian

Download from [obsidian.md](https://obsidian.md/) for macOS, Windows, Linux, iOS, or Android.

### 2. Clone this repo

```bash
git clone <repo-url>
cd genai_cce_26
```

### 3. Open as a vault

1. Launch Obsidian.
2. Click **Open folder as vault** (or **Open** on first launch).
3. Select the `genai_cce_26` folder — the one that contains `home.md` and `.obsidian/`.
4. Choose **Trust author and enable plugins** when prompted (the vault ships with core plugins pre-enabled).

You should see `home.md` in the file explorer. Open it to navigate the course.

### 4. Recommended first steps

- **Graph view** (`Cmd/Ctrl + G`) — visualize how topics link together.
- **Quick switcher** (`Cmd/Ctrl + O`) — jump to any note by name.
- **Backlinks panel** — see what references the note you're reading.
- **Command palette** (`Cmd/Ctrl + P`) — search all Obsidian commands.

### 5. Vault settings (already configured)

This repo includes shared vault config in `.obsidian/`:

- **Wikilinks** enabled (`[[Note Name]]`) — not standard Markdown links.
- **New notes** default to the `Topics/` folder.
- **Line numbers** in the editor are off.
- **Core plugins** on: graph, backlinks, outline, canvas, properties, tags.

Machine-specific files (`workspace.json`, `graph.json`, `hotkeys.json`) are in [`.gitignore`](.gitignore) so your local layout won't pollute git.

### 6. Math rendering

Notes use LaTeX heavily (`$...$` inline, `$$...$$` display). Obsidian renders these out of the box — no extra plugin required.

**Tips to avoid broken math / yellow highlighting:**

- Escape set braces: `$\{x_1, x_2\}$` not `$ {x_1, x_2} $`
- Use `\mid` instead of bare `|` in inline math: `$D(P_x \mid P_\theta)$`
- Use `\theta^*` not `\theta^_` for optimal parameters
- Keep `\text{...}` braces balanced — a stray `}` inside `\text{}` breaks rendering

### 7. Syncing across devices

Pick one approach:

| Method | How |
|--------|-----|
| **Git** (recommended) | Pull before lectures, push after taking notes. |
| **Obsidian Sync** | Paid; point sync at this vault folder. |
| **iCloud / Dropbox** | Place the cloned repo inside a synced folder. |

If you use git, pull before editing to avoid merge conflicts on the same note.

### 8. Optional: community plugins

Not required, but useful for a math-heavy course vault:

- **Latex Suite** — faster equation editing.
- **Excalidraw** — diagrams alongside notes.
- **Git** — commit and push from inside Obsidian.

Install via **Settings → Community plugins → Browse**. These are per-device and not committed to the repo.

---

## Course overview

**Instructor:** Dr. Prathosh A P — Assistant Professor, Electrical Communication Engineering, IISc

**Topics covered:** probabilistic foundations, variational divergence minimization, GANs/WGANs, VAEs/VQVAE, DDPMs, score-based and conditional diffusion, LLMs, RLHF (PPO, DPO).

**Prerequisites:** undergraduate degree, basic Python.

**Reference books:**

1. Kevin P. Murphy — *Probabilistic Machine Learning: Advanced Topics* (MIT Press, 2023)
2. Jakub M. Tomczak — *Deep Generative Models* (Springer, 2024)
3. Foster D. — *Generative Deep Learning* (O'Reilly, 2023)

---

## Contributing notes

1. Create new concept notes in `Topics/` (the vault default).
2. Link liberally with wikilinks: `[[Joint Distribution]]`, `[[Topics/KL-Divergence|KL divergence]]`.
3. Keep one idea per note when possible — the graph view works best with atomic notes.
4. Commit with a short message describing what lecture or topic you added.

---

## License

Course materials belong to their respective authors. Use this vault for personal study unless otherwise stated by the instructor.
