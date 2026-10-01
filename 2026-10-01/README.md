# Homework: Team Git Practice and Introduction to Next.js

## Goal

Prepare for next lesson's mini-hackathon by practising:

- feature branches and pull requests;
- reviewing and merging another person's changes;
- basic Next.js pages, components and API endpoints;
- planning a small application.

Estimated time: approximately 1½–2 hours, including coordination with your team.

---

# Part 1: Feature Branching with Your Current Team

Complete this part with the teammates from this week's mini-hackathon.

## 1. Create a Shared Practice Repository

One teammate creates a GitHub repository named:

`team-git-practice`

Add all current teammates as collaborators.

Create these files on `main` before everyone starts:

```text
README.md
team-notes.md
practice/
  .gitkeep
```

Put this line in `team-notes.md`:

```text
Team motto: To be decided.
```

Everyone clones the repository.

## 2. Each Person Creates Their Own Feature Branch

Start from an up-to-date `main`:

```bash
git switch main
git pull origin main
git switch -c feat/your-name-practice
```

Use your actual name in the branch name.

Do not commit your practice work directly to `main`.

## 3. Add a Small Function and a Test

Each person creates two uniquely named files:

```text
practice/your-name.cjs
practice/your-name.test.cjs
```

Choose one small function:

- `isValidTitle(value)`: true for a string whose trimmed length is 1–80.
- `isValidMinutes(value)`: true for an integer from 1 to 180.
- `countCompleted(items)`: count items whose `completed` value is `true`.
- `getTotalQuantity(items)`: sum the numeric `quantity` fields.

Use a different function from your teammates where possible.

Use Node.js's built-in test tools; no test library installation is required.

Example function file:

```js
function isValidTitle(value) {
  // Your implementation.
}

module.exports = { isValidTitle };
```

Example test file:

```js
const test = require('node:test');
const assert = require('node:assert/strict');
const { isValidTitle } = require('./your-name.cjs');

test('accepts a normal title', () => {
  assert.equal(isValidTitle('Learn Next.js'), true);
});
```

The `.cjs` extension explicitly uses CommonJS for this standalone exercise.
Continue using `import` and `export` in your React and Next.js projects.

Write at least three tests:

1. A normal case.
2. An empty or invalid case relevant to the function.
3. A boundary case, such as exactly 80 characters or an empty array.

Run your test:

```bash
node --test practice/your-name.test.cjs
```

Also replace the team motto in `team-notes.md` with your own suggestion.

## 4. Commit, Push and Open a Pull Request

```bash
git add practice/your-name.cjs practice/your-name.test.cjs team-notes.md
git commit -m "feat: add title validation practice"
git push -u origin feat/your-name-practice
```

Adapt the commit message to your actual work.

On GitHub, open a pull request into `main`.

Include:

- what you changed;
- why;
- how you tested it.

## 5. Review a Teammate's Pull Request

Each person reviews someone else's pull request.

Check:

- Does the function satisfy its description?
- Are the tests meaningful?
- Are filenames and function names clear?
- Is anything unrelated included?

Leave at least one useful comment or review.
The author should respond and make any necessary correction.

## 6. Practise Resolving a Merge Conflict

Make sure everyone creates their branch and changes the original motto
before the first pull request is merged.

Merge the first reviewed pull request.

The other branches should now conflict on the motto line.

On a conflicting feature branch:

```bash
git fetch origin
git merge origin/main
```

Open `team-notes.md`, discuss the final wording and resolve the conflict.

Remove conflict markers such as:

```text
<<<<<<<
=======
>>>>>>>
```

Then:

```bash
git add team-notes.md
git commit -m "fix: resolve team motto conflict"
git push
```

Do not resolve the conflict by blindly discarding a teammate's work.

After review, merge the remaining pull requests.

## 7. Update Everyone's Local Main

```bash
git switch main
git pull origin main
node --test
```

All practice tests should pass.

## Submit

Each person submits:

- the shared repository link;
- their own pull request link;
- the pull request they reviewed;
- two or three sentences explaining how the conflict was resolved.

Be ready to explain the difference between:

- a branch;
- a commit;
- a push;
- a pull request;
- a merge.

---

# Part 2: Individual Next.js Introduction

Complete this part individually.

Build a tiny application called **Next.js Warm-up**.
Do not migrate your entire previous project.

## 1. Create and Run the Project

Use:

```bash
npx create-next-app@latest nextjs-warmup
```

Customise the setup rather than accepting settings you do not understand:

- JavaScript;
- ESLint;
- App Router;
- no Tailwind CSS needed;
- no `src` directory for this exercise;
- keep the default import alias.

If other options appear, leave them at their defaults.

Then:

```bash
cd nextjs-warmup
npm run dev
```

Open the address printed in the terminal.

## 2. Understand the Main Files

Find and inspect:

- `app/page.js`: the home page;
- `app/layout.js`: the shared root layout;
- `app/globals.css`: global styling;
- `package.json`: dependencies and scripts.

The root layout must keep its `<html>` and `<body>` elements.

## 3. Create Two Pages

Create:

- `/`: a welcome page;
- `/about`: a short introduction about yourself.

Use:

```text
app/page.js
app/about/page.js
```

Add navigation with `Link` from `next/link`.

Do not install React Router.

## 4. Add One Interactive Component

Create:

```text
app/components/Counter.jsx
```

The component must:

- use `useState`;
- display a number;
- include a button that increases the number;
- begin with `'use client'`.

Import the counter into the home page.

Keep the home page as a Server Component.
Only the interactive component needs the client boundary.

## 5. Create Your First Next.js API Endpoint

Create:

```text
app/api/message/route.js
```

Export a `GET` function that returns:

```json
{ "message": "Hello from the Next.js backend!" }
```

Use `Response.json(...)`.

Open `/api/message` in your browser to check the response.

This code runs on the server. You do not need a separate Express application
for this endpoint.

## 6. Connect the Interface to the Endpoint

Create a small Client Component with a button labelled:

`Load server message`

When clicked, it should:

- call `fetch('/api/message')`;
- check whether the response succeeded;
- display the returned message;
- show a loading state;
- display an error message if the request fails.

Use an event handler for this exercise; a loading effect is not required.

## 7. Check the Build

Run:

```bash
npm run build
```

Fix any build errors.

Deployment is not required.

## 8. Explain What You Learned

Add brief answers to your README:

1. What does Next.js provide beyond React alone?
2. Why does the counter need `'use client'`?
3. Where does the code in `app/api/message/route.js` run?
4. How is this endpoint similar to an Express route?
5. Why must secrets remain on the server?

Keep each answer to one or two sentences.

## Supabase Preparation

Read the official Next.js and Supabase introduction.

Be ready to identify:

- which code belongs in the browser;
- which code belongs on the server;
- why database ownership policies are still required;
- why hiding a button does not protect an endpoint.

You do not need to implement database access or authentication in this
homework exercise. We will agree on the integration approach in class.

## Submit

- Your individual repository link.
- A screenshot of the page displaying the server's message.
- Your short README answers.

Use at least one feature branch and pull request in this individual project
to repeat the Git workflow.

---

# Part 3: Prepare a Simple App Pitch

Complete this part individually.

Prepare one idea to pitch at the beginning of next lesson.
Your idea does not have to be completely original.

## Scope

Your app should need approximately:

- one main page;
- one form;
- one list;
- one database table;
- two or three editable fields;
- GET, POST and DELETE endpoints;
- one small useful extra, such as a filter or total.

Possible themes include:

- studying;
- hobbies;
- campus life;
- personal organisation;
- sports;
- saving useful information.

Avoid payments, chat, complex booking systems, file uploads and external
AI integrations for this exercise.

## Prepare a 45–60 Second Pitch

Bring one slide or a short written pitch covering:

1. **User:** Who would use it?
2. **Problem:** What small problem does it solve?
3. **Solution:** What can the user do?
4. **Data:** What fields will be stored?
5. **Success:** What will you demonstrate after 90 minutes?

Example:

“Students lose useful course links in chat. My app lets them save a title
and URL, view their links and delete old ones. It uses one bookmarks table.
The extra feature is searching by title. A successful demo shows a saved
link still present after refreshing.”

## Choose a New Role

Write down:

- your role in this week's team;
- your preferred role next week;
- your second choice.

Choose a different role where possible:

- frontend;
- backend;
- database and integration;
- testing and integration, if a fourth member is needed.

Do not form next week's teams at home.

New teams will be formed in class, ideally with people you have not worked
with before.

Your new team will choose one of its members' ideas and may simplify it.

---

# Next Lesson's Technology Map

| Previous project | Next.js project |
|---|---|
| React + Vite frontend | React inside Next.js |
| React Router | App Router folders and pages |
| Shared layout component | `app/layout.js` |
| Express routes | Next.js Route Handlers |
| Separate frontend/backend servers | One Next.js application for this exercise |
| Supabase database | Supabase database |
| Backend validation and ownership checks | Still required in server-side code |

Next.js still uses React.
Its server-side code can run on Node.js.
You are reorganising familiar concepts, not starting programming again.

# Useful Reading

- Next.js installation:
  https://nextjs.org/docs/app/getting-started/installation
- Pages and layouts:
  https://nextjs.org/docs/app/getting-started/layouts-and-pages
- Server and Client Components:
  https://nextjs.org/docs/app/getting-started/server-and-client-components
- Route Handlers:
  https://nextjs.org/docs/app/getting-started/route-handlers
- Supabase with Next.js:
  https://supabase.com/docs/guides/getting-started/quickstarts/nextjs
