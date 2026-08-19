# AGENTS.md — principles for `docs/`

Read `docs/<lang>/OVERVIEW.md` first to see the current structure. A
prefix that forces a file or folder to sort first in its directory is a
structural device, not a naming rule — infer the existing convention
from what's already there rather than inventing a new one.

## Core principles

1. **Every content type has exactly one template, and every template
   implies exactly one content directory.** A real file is always a
   copy of one template — same sections, same order, same meaning per
   section, same notation conventions (diagram style, labeling, etc).
   Don't bend a single file to fit a special case; if something doesn't
   fit, that's a signal the template needs revising for every file of
   that type, not that one file needs an exception. Concrete
   conventions (how to name a diagram node, how many digits a sort
   prefix uses, and similar decisions) belong inside the template that
   governs them, not as a rule to remember separately — a template
   should be self-sufficient for whoever copies it.

   Setting up docs for a new project means creating one directory per
   template that exists (a template with nothing describing it is dead
   weight, and content with no template to follow is drift waiting to
   happen). The current set of templates happens to be `api`,
   `database`, and `infrastructure`, but that set isn't fixed — a
   project without a database, or one needing a fourth category, adds
   or removes a template-and-directory pair together, never one without
   the other.

2. **Documentation points at code, it doesn't restate it.** Anything
   readable directly from code should only be referenced by file name,
   never copied in — copied content drifts the moment the code changes
   and the doc doesn't.

3. **Record the reasoning, not the procedure.** A doc describes how a
   system behaves and why it was designed that way — not the steps to
   go use it. Procedural instructions belong only where a template
   itself explains how to fill it in, never inside a finished file.

4. **Structure and rationale stay in separate layers.** A diagram or
   table shows facts as they are; the reasoning, trade-offs, and
   constraints behind those facts live in their own prose section.
   Someone reading only the structure understands what happens; someone
   reading only the prose understands why.

5. **A change to behavior earns a record; a change to wording doesn't.**
   Anything resembling a history log records what altered how the
   system behaves, never a rephrasing with no behavioral effect. New
   entries are added chronologically from the most recent.

6. **Write at the abstraction level matching what's being described.**
   A file about business behavior speaks in business terms. A file
   about data speaks in concepts general enough to outlive the
   technology storing that data. Never let a document's accuracy depend
   on an implementation detail it wasn't scoped to track.

7. **One fact lives in exactly one place.** If something can be derived
   from content that already exists elsewhere, don't duplicate it —
   reference it. Duplication is what makes docs drift apart once one
   copy is updated and the other isn't.

## When unsure

If a change doesn't clearly fit an existing template or principle,
stop and ask before introducing new structure unilaterally.
