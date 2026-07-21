# Documentation project instructions

Docs for **Politi Tablet** (`va_policemdt`), a police MDT resource for FiveM
servers running ESX. The audience is **server owners and script developers**
integrating with the resource — not the police officers who use the tablet
in-game.

## About this project

- Built on [Mintlify](https://mintlify.com). Pages are MDX with YAML frontmatter
- Configuration and navigation live in `docs.json` — a new page must be added
  there or it will not appear
- Preview locally with `mint dev` (install: `npm i -g mint`)
- For Mintlify product knowledge (components, configuration, writing standards),
  install the Mintlify skill: `npx skills add https://mintlify.com/docs`

## Language

**Documentation is written in Danish.** Code, code comments, identifiers and
`fxmanifest` keys stay English — that is how the source is written.

Officer-facing product terms come from the tablet's own Danish UI: *udkald*,
*flådestyring*, *strafferegister*, *efterlysninger*, *aktindsigt*, *kaldesignal*.
Use them rather than inventing synonyms. The tablet UI itself ships in Danish,
Swedish and Norwegian; these docs do not.

## Terminology

- The product is **Politi Tablet**; the resource is **`va_policemdt`**. Use the
  resource name in anything a developer would grep for
- **Betjent**, not "spiller", when referring to someone with the police job
- **Udkald** for a dispatch call. **Opkald** is acceptable in running prose but
  prefer *udkald*
- Distinguish **politibetjent** (has the ESX job) from **logget ind i MDT'et**
  (has completed the tablet password login). They are not the same check, and
  conflating them is the most common integration mistake

## Style preferences

- Active voice, second person ("du")
- One idea per sentence
- Sentence case for headings
- Bold for UI elements: Klik **Indstillinger**
- Code formatting for file names, commands, paths and code references

### Writing FiveM code examples

Examples are read by people who will paste them into a live server. They must be
correct FiveM, not pseudocode.

- **Always label the context.** Use a code block title of `server.lua`,
  `client.lua` or `fxmanifest.lua`. A FiveM developer's first question about any
  snippet is which side it runs on
- **Capture `source` immediately**: `local src = source` as the first line of a
  net event handler. `source` is a global that later handlers clobber
- **Never trust the client.** Any snippet where a player can trigger the code
  must show the server-side gate (`IsPolice`, `IsMdtAuthed`,
  `HasMdtPermission`). Do not leave it as an exercise
- Use `exports.va_policemdt:Method()`. Mention the `exports['name']` form once,
  where the naming rule is explained — not in every snippet
- Prefer complete, runnable handlers over fragments. If a snippet needs cleanup
  (closing a call, releasing a vehicle), show the cleanup
- Use `SetTimeout` / `CreateThread` + `Wait` as FiveM does, not Lua's `os.clock`
  loops

## Content boundaries

- Document the **public export API**, not internal functions. Globals such as
  `RegisterPoliceCallback` or `BuildFullReport` are implementation detail unless
  they are exported
- Do not document NUI callback names or `mdt:`/`va_policemdt:` net events as
  integration points. They are internal plumbing and will change
- **Do document the sharp edges**: exports without permission checks, calls that
  are silently ignored, values that are `nil` more often than you would expect.
  A quiet failure the reader hits in production is worse than an ugly warning
- When something is missing (there are no events yet), say so plainly on the
  page where a reader would look for it
