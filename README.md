# AGENCY

AGENCY is a small publishing system for generative, remixable comics.

A comic can ship with a **cartridge**: a durable, plain-text instruction
payload that an AI assistant can retrieve and use to regenerate that comic —
optionally substituting a supplied reference person into a designated role.

No framework, database, build system, JavaScript dependency, analytics,
cookies, authentication, or API. It's static files served by GitHub Pages.

## The cartridge convention

Each comic lives at `comics/<slug>/` and contains:

```
comics/<slug>/
  index.html    human-facing landing page
  prompt.txt    the cartridge — canonical machine-readable prompt payload
  README.md     short description of the comic and its cartridge
```

`prompt.txt` is the whole point. It opens with a short bootstrap header
identifying it as an AGENCY cartridge and stating the substitution rule
(if a person reference is supplied, use them; otherwise use the default),
followed by the complete image-generation prompt. It's plain UTF-8 text —
fetchable, pasteable, and readable without any tooling.

The human-facing `index.html` for a cartridge is a convenience layer: it
explains what the comic is and links to `prompt.txt`. It can be redesigned
freely. `prompt.txt`'s *URL* is the stable contract — the page around it
is not.

## Adding another comic

1. Create `comics/<slug>/`.
2. Write `prompt.txt`: bootstrap header (see any existing cartridge for the
   format) + the full image-generation prompt.
3. Write `index.html`: a short landing page linking to `prompt.txt`, with
   Open Graph metadata and a canonical URL.
4. Write a short `README.md` describing the comic.
5. Add a card for it to the root `index.html` cartridge list.

## Stability

`comics/<slug>/prompt.txt` is a stable public interface. Once a cartridge
is published, that URL should keep working and keep returning a valid
cartridge payload for that comic. Visual design, landing-page copy, and
even the underlying prompt's wording can evolve — but don't move or remove
a published `prompt.txt`.

## Deployment

This site is published with GitHub Pages, deployed from the `main` branch
(repository root). Pushing to `main` updates the live site — there is no
build step.
