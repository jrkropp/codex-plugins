---
name: simplify-code
description: Reduce the reasoning required to understand and safely change code by removing accidental complexity and restoring conceptual integrity. Use when asked to simplify code or architecture, reduce cognitive load or change amplification, clarify ownership, data flow, or invariants, consolidate duplicate or legacy paths, remove unnecessary abstraction or indirection, or refactor for maintainability. Do not use for prose simplification, code golf, formatting-only cleanup, or performance tuning where simpler design is not the goal.
---

# Simplify Code

## Adopt the frame

Treat code as a model another engineer must load into working memory, not as text to compress.

Optimize for the cognitive cost of making a safe change. Preserve the complexity inherent in the domain. Remove the accidental complexity introduced by the implementation.

The unit of complexity is an independent fact that must be remembered and coordinated. Reasoning burden grows with the number of those facts, the distance between them, ambiguity about which one is authoritative, and the number of paths through which behavior can occur. Simplification removes, localizes, or makes explicit those facts without concealing real domain distinctions.

A simple system has conceptual integrity: its names, boundaries, ownership, data flow, and rules tell one coherent story. High cohesion gives each responsibility a natural home. Low coupling keeps changes local. Information hiding keeps incidental decisions behind clear boundaries. A single source of truth prevents competing explanations. Minimal indirection and minimal change amplification let an engineer follow behavior and alter it without reconstructing the whole system.

The goal is not fewer lines. The goal is fewer things to know, and less distance between the things that must be known together.

Every structure asks the engineer to carry a distinction:

- Every name proposes a concept.
- Every file or module proposes an owner and a place to look.
- Every branch proposes a distinct case.
- Every layer proposes a boundary.
- Every alias proposes another vocabulary.
- Every adapter proposes another path.
- Every exception proposes a rule outside the rule.
- Every abstraction promises leverage in return for indirection.

Require each distinction to earn its place. Preserve distinctions that express real domain behavior, operational constraints, or necessary compatibility. Remove distinctions that exist because of duplication, history, indecision, pass-through structure, or an abandoned design.

Line count and file count are shadows cast by the mental model. Measure the shadows, but simplify the thing casting them.

## Seek one coherent story

Make it possible for a competent engineer to answer quickly:

```text
What is this?
What owns it?
Where does it live?
How does data flow through it?
Where are the rules enforced?
Where would I change it?
What can be deleted?
```

Prefer a shape with one coherent answer:

```text
one concept        -> one name
one responsibility -> one owner
one behavior       -> one active path
one rule           -> one enforcement point
one normal change  -> one obvious area to edit
```

Reduce the number of plausible stories about how the system works. If two files appear authoritative, two names appear canonical, or two paths appear active, the engineer must understand both until the ambiguity is removed.

Do not erase real distinctions merely to make the story look uniform. A hidden distinction is harder to reason about than an explicit one.

## Reason before transforming

Trace the active behavior end to end before editing. Follow inputs, state, decisions, side effects, and outputs. Locate the owner of each rule and identify the compatibility surface.

State the reasoning burden in one sentence before choosing a solution. Name what the engineer must currently understand together and why. For example:

```text
Creating an account requires tracing three names and two entry paths because
validation and persistence each have multiple apparent owners.
```

Distinguish essential complexity from accidental complexity:

- Essential complexity represents the domain, a product requirement, an external system, or a real operational constraint.
- Accidental complexity represents how this implementation happened to evolve.

Simplify the accidental part. Do not wish away the essential part.

Choose the target shape only after the burden is clear. Prefer the design that makes the correct causal story easiest to discover and the normal change easiest to locate.

## Treat transformations as neutral

Judge every transformation by its effect on the mental model, not by its appearance.

- Deletion helps when a concept, path, exception, or obsolete responsibility stops existing.
- Consolidation helps when it creates one owner; it hurts when it merges unrelated responsibilities.
- Extraction helps when it names and owns a real concept; it hurts when it creates another place to look.
- Abstraction helps when it hides a volatile decision or removes repeated reasoning; it hurts when it merely forwards calls or erases domain language.
- Deduplication helps when duplicated code represents one rule; it hurts when superficially similar code represents different reasons to change.
- Explicit code helps when it reveals a hidden invariant, even if it adds lines.
- Standard terminology helps when it replaces local synonyms without losing domain meaning.

Every abstraction is a cost until it proves that it removes more reasoning than it introduces.

Prefer boring names, direct control flow, visible data flow, cohesive ownership, standard terminology, and boundaries that correspond to real responsibilities. Prefer no change over cosmetic churn.

## Perform the simplification

Respect the requested mode. For a review, diagnosis, or plan, inspect and report without editing. For a request to simplify, refactor, or implement, make the smallest coherent change that establishes the clearer model.

Work toward:

- fewer independent concepts
- fewer competing names
- fewer places claiming ownership
- fewer active paths to the same behavior
- fewer exceptions to the normal flow
- fewer layers that only translate or forward
- fewer files that must change together
- fewer rules enforced in more than one place

Delete obsolete paths when compatibility is not required. Determine compatibility from callers, public interfaces, tests, documentation, configuration, runtime discovery, and the user's constraints. If compatibility is uncertain and removal would be consequential, surface the uncertainty instead of silently guessing.

Preserve behavior unless a behavior change is explicit. Do not trade correctness, observability, security, debuggability, or necessary performance for aesthetic simplicity.

## Verify the mental-model delta

After changing the code, ask:

- Which concept, name, path, layer, exception, or owner ceased to exist?
- Where does the responsibility live now?
- Can the active behavior be explained with fewer independent facts?
- Does a normal change touch fewer places?
- Did any new abstraction create another place to look?
- Is the resulting story more truthful, or merely shorter?

If no reasoning burden was removed, do not claim simplification.

Verify behavior with the strongest relevant evidence available: focused tests, broader test suites, builds, type checks, static analysis, or direct execution. State any verification gap.

Inspect the size signal with `git diff --stat`, `git diff --numstat`, commit statistics, or direct file and line counts as appropriate. Account for untracked files and exclude unrelated pre-existing changes. Report:

```text
files added
files removed
files changed
lines added
lines removed
net line change
```

Treat these numbers as evidence and a by-product, never as the win. A larger diff may establish one clear path. A smaller diff may only compress confusion.

## Communicate the result

Report in this order:

1. The reasoning burden removed.
2. The owner, name, rule, or path that is now obvious.
3. What changed.
4. What was verified.
5. Files and lines added or removed.

Be direct. Do not say “cleaned up.” State what became easier to understand, trace, change, or delete.

Prefer:

```text
Account creation now has one owner and one validation path. The legacy adapter
is gone, so changing the creation rule no longer requires coordinating three
modules. As a by-product, this removed 3 files and 420 lines.
```

Avoid:

```text
Cleaned up account creation and reduced 420 lines.
```
