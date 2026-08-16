---
name: stack-profile
description: The crew's sole customization file. It defines the response language, primary and secondary stacks, UI conventions, high-risk areas, project rules, and test/type-check commands. The manager must load it at the start of EVERY task, including TRIVIAL, and pass every relevant rule to every agent prompt. The bundled default profile is TypeScript with Next.js App Router, Express, Tailwind CSS, and a Persian RTL UI.
---

# Stack profile

This is the crew's **sole customization file**. `CLAUDE.md` and the agent definitions are stack-neutral; do not edit them to change the response language, technology stack, UI conventions, risk model, or verification commands.

To adapt Claude Crew to another project, edit only the sections below.

## How the manager uses this profile

1. Load this file before sizing or dispatching **every task**, including `TRIVIAL` tasks.
2. Reply to the user in the **Response language** defined below.
3. Add every relevant stack, UI, risk, project, and verification rule to **every agent prompt**, regardless of the agent's role. An agent only knows the rules included in its task.
4. Treat the listed **High-risk areas** as `HIGH`-tier and `guardian` triggers in addition to stack-neutral risks.
5. If this profile is missing or does not answer a project-specific question, ask the user instead of guessing.

Internal plans and agent prompts remain in English unless the task explicitly requires another language.

---

## Response language

The manager replies to the user in **Persian (فارسی)**, with short, direct, result-first responses.

> Replace this with the language and register you want, such as English, Spanish, or formal Persian.

## Primary stack

The bundled default profile uses:

- **Language:** TypeScript
- **Web framework:** Next.js with the App Router
- **Standalone API framework:** Express
- **Styling:** Tailwind CSS

> Replace these values with the project's actual language, frameworks, and styling system.

## Secondary stacks

The bundled default profile occasionally covers small PHP or Go projects, such as a WordPress theme or plugin or a Go binary, usually in codebases shared with other developers. In those projects, follow the existing conventions exactly; do not modernize or restructure unrelated code.

> Remove this section if the project has no secondary stack, or list every secondary language and framework an agent may encounter.

## UI conventions

These defaults apply only when a task touches the bundled profile's user-facing UI, which is **Persian and right-to-left (RTL)**:

- Use logical CSS properties only: `ms`/`me`, not `ml`/`mr`; `ps`/`pe`, not `pl`/`pr`; `text-start`/`text-end`, not `text-left`/`text-right`; `start-`/`end-`, not `left-`/`right-`; and the corresponding logical border and radius utilities. A physical direction is a defect.
- Mirror direction-encoding icons such as arrows, chevrons, and back controls in RTL. Keep numbers, Latin text, code, and phone numbers LTR within the RTL flow, and isolate them so the bidirectional algorithm does not reorder surrounding punctuation.
- Write all user-facing copy in Persian. Do not ship English placeholder text. Layouts must tolerate Persian copy being longer than its English equivalent.
- Use real buttons and links for interactive controls. Every control must be keyboard-operable and have an accessible name; every input must have a label; every asynchronous UI must define loading, empty, and error states.

> Replace these rules with the project's UI direction, styling conventions, copy language, and accessibility requirements. Remove this section for a backend, CLI, or library project with no UI.

## High-risk areas

These entries drive the `HIGH` tier and `guardian`. In the bundled Next.js App Router and Express profile, they are:

- **Caching and data freshness:** `fetch` cache options, `revalidate`, `dynamic`, `force-static`, and `generateStaticParams`.
- **Rendering mode:** any change that moves a route between static and dynamic rendering, including framework features that do so implicitly.
- **Server/Client boundary:** placement of `"use client"` and server-only modules reachable from client components.
- **Routing:** route groups, dynamic segment names, `middleware.ts` matchers, redirects, and rewrites.
- **Express middleware order:** inserting or moving middleware changes every downstream route that runs after it.
- **Stack-neutral risks:** shared layouts, database schema, authentication or authorization, environment configuration, and public API response shapes.

> Replace the framework-specific entries with the project's silent-failure zones. Keep the stack-neutral risks unless the manager's operating rules already classify them more strictly.

## Project rules

- Do not add dependencies without reporting the need first.
- Do not put secrets in source or suppress type, lint, or test failures to make verification pass.
- Follow the existing conventions of the file and project over personal preference.

> Add any rule that every agent must follow in this project.

## Tests and type-checking

- **Test runner:** use the project's existing test framework; do not introduce a second one. If no runner exists, `tester` reports the gap instead of bootstrapping a suite inside an unrelated change.
- **Type-check command:** `tsc --noEmit`

> Replace these with the project's exact focused-test, full-test, type-check, lint, and build commands as applicable.
