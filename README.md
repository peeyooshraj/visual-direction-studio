# Visual Direction Studio

From an idea to an art-directed image, with every creative decision visible and editable.

You describe an idea. The studio proposes four art directions, each built from an explicit combination of visual techniques (composition, layering, colour, lighting, printmaking, texture, compositing, typography and more). You lock what works, swap or tune what doesn't, and get a generation prompt that reflects exactly those choices.

**The user stays the art director.** The system proposes, explains and compiles; you accept, reject, combine and modify.

## Workspaces

| Workspace | What it does |
| --- | --- |
| **Brief** | Idea, format, subject, message, emotional register, visual character, and a "don't repeat" list that keeps clichés out of the suggestions. |
| **Directions** | Four contrasting directions, each with a layout sketch, palette, every technique and its strength, and a "why this combination" note. |
| **Editor** | One row per technique: lock, swap the style, choose sub-techniques, set strength from subtle to dominant, randomise, remove, undo, save a version. Shows a coherence score from the compatibility graph. |
| **Prompt** | Compiles the direction into an image-generation prompt. Typography stays out of the image by default and is listed as an editable design layer. |
| **Tweak** | Natural-language revisions ("replace double exposure with silhouette fill, reduce paper grain") that change only the named rows and never touch locked ones. |
| **Library** | Searchable technique atlas: 22 families, 199 styles, 714 sub-techniques. Each style lists its effect, parameters, pairings, productive tensions and conflicts. |
| **History** | Every version with a sketch, side-by-side comparison of any two, and restore. |

## Data model

```
Domain → Family → Style → Sub-techniques
                       ↘ Parameters (family-level) + intensity
Rules: style ↔ style  (+ complement · ~ contrast · × conflict)
Direction: { name, concept, palette[4], picks: { family: { style, techs[], intensity, locked } } }
```

The library is plain data at the top of `index.html` (`ATLAS_SRC` and `RULES`). Add a style or a relationship there and the whole app picks it up.

## Running it

It's a single static HTML file with no build step and no dependencies. Open `index.html` in a browser, or serve the folder with GitHub Pages.

On its own, the page uses a built-in rule-based engine: keyword-scored direction archetypes, a compatibility graph, and a plain-command tweak parser. When the page is opened as a Claude artifact on claude.ai, it can also call Claude to write the brief, propose directions, apply tweaks (including comparing an uploaded output image), answer "why this?" questions, and teach any technique.

Versions are stored in the browser's `localStorage`, so they stay on that browser only.

## Status and roadmap

This is a V1 prototype. It plans and tracks art direction; it doesn't render the final image.

- [ ] Connect an image-generation API to the Generation Studio
- [ ] Editable composition layer (type, shapes, masks) on a canvas
- [ ] Shared projects and presets (e.g. Supabase)
- [ ] Learn from accepted and rejected combinations
- [ ] Expand the atlas: motion and video editing, 3D render looks, information design
