---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: /MFT_background_1.png
# some information about your slides (markdown enabled)
title: Welcome to Slidev
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
lineNumbers: true
---

# Welcome to *Git*ting comfortable

A short introduction to Git

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space or use keyboard arrows for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

---

# Basics of Git

Git is a version control system that helps you manage text files of all sorts in a collaborative and structured manner. <br>

The concept of git is that you work with a `repository` of which you can create `branches` (think shortlived variants of the codebase) that enables you to collaborate from the same point in time. You `commit` changes to a branch to create a record of your change for others and yourself to keep track of the history in changes. <br>

At the end you sync changes to a git server with `push` in order to save work and synchronize changes with your colleagues or automation systems.

```bash

git add <file> # Add a file to "staging"

git commit -m <message> # Records all changes that are staged by add with documentation on the work done in the files

git push -u origin <branch> # Push all missing commits from localhost (your machine) to a git server syncing your records with a server for collaboration

git checkout -b <branch> # Create and switch branch in a single command
```

---
layout: two-cols
---

# Basics of Git: Client-server

Git works as a client server paradigm 
<br>
<br>

Git works by a client (a user) cloning the source code from a `repository`, performing edits locally and pushing these edits to `origin` (the server from which you downloaded the source code). <br><br>
The benefit is here, that you can have multiple clients each with their own cloned repository, working on the same repo at the same time and continuously pushing code to origin.

::right::

<br>
<br>
<br>
<br>
<br>

```mermaid
graph TD

C1[Client 1] -->|push/pull| R[Remote Repository]
C2[Client 2] -->|push/pull| R[Remote Repository]

C1 -->|commit| L1[Local Repository]
C2 -->|commit| L2[Local Repository]
```

---
layout: two-cols-header
---

# Why Git?

Selling points:

::left::

<v-clicks>

- Multiple collaborators
  - 4 eyes principle

</v-clicks>

<v-clicks at=4>
<br>

*Joe; I like your change +1*

</v-clicks>

::right::

<div v-click> 

Git is an collaborative development solution that versions your code enabling multiple collaborators and pair-review processes built into the methodology.
</div>


<div v-click> 

```diff
public class Hello1
{
   public static void Main()
   {
-      System.Console.WriteLine("Hello, World!");
+      System.Console.WriteLine("Rock all night long!");
   }
}
```
</div>

<arrow v-click at=5 x1="250" y1="400" x2="550" y2="450" color="#953" width="2" arrowSize="1" />

---
layout: two-cols-header
---

# Why Git?

Selling points:

::left::

<div v-click at=1>

- Change history
  - Compliance
  - Reverting is easy
  - Versioning

</div v-click>

::right::
<div v-click at=2>
```mermaid
---
title: Example Git diagram
---
%%{init: { 'themeVariables': {
              'commitLabelFontSize': '10px',
              'branchFontSize': '10px',
       } } }%%
gitGraph
   commit id: "commit1"
   commit id: "commit2"
   branch feature/a
   checkout feature/a
   commit id: "commit3"
   commit id: "commit4"
   checkout main
   merge feature/a id: "merge"
   commit id: "commit5" tag:"v1"
```
</div v-click>

<div v-click at=3>
```mermaid
---
title: Example Revert
---
gitGraph
   commit id: "commit1" tag:"v1"
   commit id: "badCommit"
   commit id: "commit2" tag:"v2"
   commit id: "revert_badCommit" tag:"v2" type: REVERSE
```
</div v-click>

---
layout:  two-cols-header
---

# Why Git

Selling points:

::left::

<div v-click at=1>

- Automation
  - Quality check
  - Deployment

</div v-click>


::right::

<v-click>

Another benefit of Git is that we can integrate the version control with <span v-mark.circle.orange="3">automation tooling</span> which continuously <span v-mark.circle.red="4">quality checks</span> your code.

</v-click>

<v-click at=5>
```mermaid
---
title: Automation
---
flowchart LR
  id1(checkout code)
  id2(run quality check)
  id3(deploy service)
  
  id1 --> id2
  id2 --> id3
```
</v-click>
---

# Working with branches

Combining branches

When a change has been completed on a branch it is ready to be included in `main`. Combining two branches is refered to a *merging*. 
Before we dive into *how* to do it, it is important to talk about *when*. 

Ideally are branches short lived.
This means that we should strive to get meaningfull changes merged back into `main` as quickly as possilbe.
A good rule of thumb is that branches should not live for more than two days.
In reallity, this can be difficult to always do, but it is a good compass, none the less. 

Following our previous branch we can now go back to main
<v-switch>
<template #1>
```mermaid
gitGraph
   commit id: "initial"
   branch feature/show-branching
   commit id: "first-feature-change"
   commit id: "another-change"
```
 </template>
<template #2>
```mermaid
gitGraph
   commit id: "initial"
   branch feature/show-branching
   commit id: "first-feature-change"
   commit id: "another-change"
   checkout main
   commit id: "main-first-feature"
   commit id: "main-another-change"
   merge feature/show-branching
```
 </template>
</v-switch>

---

# Working with merges / rebasing - in realtion to Pull-Requests

<v-switch>
<template #1>
A Pull-Request is a term used on a git server to faciliate the process of raising a merge from a branch to a target branch, such as a feature branch to main. <br>
The Pull-Request facilitates things like dicsussions, change requests to edits, diff views, approvals etc - more on this later.

But most importantly it faciliates what happens when a Pull-Request is completed
</template>

<template #2>
There exists different methods of completing a Pull-Request;

1. No fast-foward
1. Fast-forward
1. Squash commit
1. Rebase with fast-foward or merge commit

</template>

<template #3>

**No fast-forward** is the method of not rewriting history and simply adding on top of the target branch.

```mermaid
gitGraph
  commit id: "1"
  branch feature/1
  commit id: "2"
  checkout main
  merge feature/1
```

</template>

<template #4>

**Fast-foward** is the method of rewriting target branch to represent a linear history of events. In below graph you see a merge where the merged point is highlighted and represent a duplicate of the commit with id 2 that happened on the feature branch. If a git log is corretly drawn after the impact of the merge, the branch `feature/implement` will no longer be present.

```mermaid
gitGraph
  commit id: "1"
  branch feature/implement
  commit id: "2"
  checkout main
  merge feature/implement id: "duplicate_2" type: HIGHLIGHT
```

</template>

<template #5>

**Squash commit** is the method of squashing all your commits that happened on the feature branch to a single commit on the target. This method is much like fast-forward in the sense that the existence of the feature branch will be gone after the merge is complete. This method creates a very clean linear git history.


```mermaid
gitGraph
  commit id: "Init"
  branch squash-mr
  commit id: "commit 1"
  commit id: "commit 2"
  checkout main
  merge squash-mr id: "squashed commit" type: HIGHLIGHT
```

</template>

<template #6>

**Rebase** A rebase strategy works a in a sense reverse to how regular merges does. Instead of adding on top of the target branch, rebase tages each commit on the feature branch and merges one by one with the differences that happened on main since the feature branch got created.

```mermaid
gitGraph
  commit id: "Init"
  branch feature/rebase
  commit id: "commit 1"
  commit id: "commit 2"
  checkout main
  commit id: "commit main"
```

</template>

<template #7>
Rebase
<br>

```mermaid
gitGraph
  commit id: "Init"
  branch feature/rebase
  commit id: "_commit main"
  commit id: "rebased commit 1"
  commit id: "rebased commit 2"
  checkout main
  commit id: "commit main"
```

</template>

<template #8>
Rebase and merge
<br>

```mermaid
gitGraph
  commit id: "Init"
  commit id: "commit main"
  commit id: "rebased commit 1"
  commit id: "rebased commit 2"
```

</template>

<template #9>

For more information on read the following topics;

1. [Merging vs Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing#:~:text=Integrating%20an%20approved%20feature&text=However%2C%20by%20performing%20a%20rebase,added%20during%20a%20pull%20request.)
1. [Git merge](https://www.atlassian.com/git/tutorials/using-branches/git-merge)

</template>

</v-switch>

---

# Video on git merge / rebase

<iframe width="560" height="315" src="https://www.youtube.com/embed/0chZFIZLR_0?si=wXEsqrpC528IVvkj" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

---

# Working with merges / rebasing - in realtion to local git

<v-switch>

<template #1>
It is not just at the git server we need to do merges / rebasing. These also happen locally, usually in order to synchronize a feature branch with changes from main before you create a pull request.

You can use the same methods as mentioned above locally, however there are a few rule-of-thumb's that we want to introduces: 
</template>

<template #2>

Pull newest changes of main into your feature branch with fast-forward strategy. This is the safest and cleanest method next to rebase

```bash
git checkout feature/branch
git pull origin main --ff
```

</template>

<template #3>

Pull newest changes of main into your feature branch with rebase strategy. You can use this in-case fast-foward fails or you need to be more in control wil merge conflicts

```bash
git checkout feature/branch
git pull origin main --rebase
```

</template>

<template #4>

Pull newest changes of main into your feature branch with rebase strategy. You can use this in-case fast-foward fails or you need to be more in control wil merge conflicts

```bash
git checkout feature/branch
git fetch omain
git merge origin/main
```

</template>

</v-switch>

---

# Merge conflicts

When you are more than one participant on a git repository, then you will at some point run into a merge conflict. <br>

<v-switch>

<template #1>

Think of a scenario where you and a colleague both created a branch from main:

```mermaid
gitGraph
  commit id: "1"
  branch feature/colleague1
  commit id: "2"
  checkout main
  branch feature/colleague2
  commit id: "3"
```

</template>

<template #2>

You both edited the same file `text.txt` on the same line 1:

(colleague1)
```diff

+echo "hello colleague1"

```

(colleague2)
```diff

+echo "hello colleague2"

```

</template>

</v-switch>

---

# Merge conflicts

When you are more than one participant on a git repository, then you will at some point run into a merge conflict. <br>

This will result in a conflict where both colleague1 and colleague2 have changed the exact same line on the exact same file;

```diff {all|3|5|all}
@@@ -1,1 -1,1 +1,5 @@@
++<<<<<<< HEAD
+echo "hello colleague1"
++=======
+ +echo "hello colleague2"
++>>>>>>> feature/colleague2
```

The diff is noted with all the special characters you in one block has what current revision marks as the "truth" and another block marks the incomming change as possible new "truth". Merge conflicts can happen both when doing local merge/rebase or when you open a PR. Often times the git server cannot handle merge conflicts for you, so you are required to do it locally.

Merge conflicts can be handled "easily" in your favorite IDE.

---


# Short video on git revert

<iframe width="560" height="315" src="https://www.youtube.com/embed/H2DuJNWbqLw?si=Ltw_X87fbonFOsqe" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

---

# Reverting / Reset

You can end up in a situation where you find yourself in a detached head state or you simply commited to the wrong branch or similar. This is where [git revert](https://git-scm.com/docs/git-revert) or [git reset](https://git-scm.com/docs/git-reset) comes in handy.

<v-switch>

<template #1>

Lets say you ended up in a situation where you did not want to have commited the files anyway.

```diff

echo "hello world"
+ echo "I did not want this change to be in the file
```

</template>

<template #2>

Your git status says that you have one change yet to be synced:

```{2}
On branch feature/merge_strategies
Your branch is ahead of 'origin/feature/merge_strategies' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

</template>

<template #3>

Then using git reset can help you get back to a point where you can edit the commit once again or scratch the commit entirely.

```bash
git reset --soft <commitid>
git reset --hard <commitid>
```

<br>

```bash
git reset --soft HEAD~1 # This will undo the latest commit happened on the current branch. 
  # --soft will make it so the edit is still changed and staged but not commited
```

<br>

```bash
git reset --hard HEAD~1 # This will undo the latest commit happened on the current branch. 
# --hard will make it so the edit of the commit is nowhere to be found anymore.
```

</template>

<template #4>

If you find yourself having commited and pushed the changes to a branch and you want to undo commit, then reset can be used, but it will be much cleaner to do a revert:

```bash
git revert <commitid>
```

<br>

```bash
git revert HEAD~1 # This will create a new commit undoing all changes from the latest commit on the branch
```

The main difference between revert and reset is that revert is for undoing changes with a new commit, whereas reset is mostly used before changes are synced with origin

</template>



</v-switch>

---

# Video on git stash

<iframe width="560" height="315" src="https://www.youtube.com/embed/lH3ZkwbVp5E?si=z4V07VS_zoSn5Qb0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

---

# Stashing changes

Git stashing is the method of saving your unstaged work for a later point. Often it can be used to save work in order to do a `git pull` or if you made changes on a branch that should not have been done from that revision.

Git stash works as a LIFO queue (last in - first out), where if you run `git stash push` then an entry is put into the cue with the current stages and unstaged changes. If you then run `git stash pop` then the edits you just put int op the queue are "popped" from the queue and the edits are present again.

```bash
git stash list # will list the current queue of stashed entries
git stash push # will push current edits into a stash entry for the queue
git stash list # Should now have a single entry in it
git stash pop # will remove the entry from the queue and apply the edits again in the local repo
```

---


# Time to do exercises!


- In the repo; https://github.com/mftenergy/Gitting-comfortable there are exercises
- Follow the path explained at https://github.com/mftenergy/Gitting-comfortable?tab=readme-ov-file#suggested-learning-path
- Path into an exercise directory, run `setup.sh` and read the README.md for instruction on what to do

```bash
cd basic-commits
./setup.sh
cat README.md
git magic
```

NOTE: There is a cheatsheet at the bottom of the README.md in the root of the repository.

You have two option;

1. **recommended** [Run in google cloud spaces (free)](https://console.cloud.google.com/cloudshell/editor?cloudshell_git_repo=https://github.com/mftenergy/git-course.git)
1. Run everything locally, if you choose that then read: [https://github.com/mftenergy/Gitting-comfortable/blob/main/setup-git/README.md](setup-git)

---

# What is Slidev? asdasd test

Slidev is a slides maker and presenter designed for developers, consist of the following features

- 📝 **Text-based** - focus on the content with Markdown, and then style them later
- 🎨 **Themable** - themes can be shared and re-used as npm packages
- 🧑‍💻 **Developer Friendly** - code highlighting, live coding with autocompletion
- 🤹 **Interactive** - embed Vue components to enhance your expressions
- 🎥 **Recording** - built-in recording and camera view
- 📤 **Portable** - export to PDF, PPTX, PNGs, or even a hostable SPA
- 🛠 **Hackable** - virtually anything that's possible on a webpage is possible in Slidev
<br>
<br>

Read more about [Why Slidev?](https://sli.dev/guide/why)

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/features/slide-scope-style
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

<!--
Here is another comment.
-->

---
transition: slide-up
level: 2
---

# Navigation

Hover on the bottom-left corner to see the navigation's controls panel, [learn more](https://sli.dev/guide/navigation.html)

## Keyboard Shortcuts

|     |     |
| --- | --- |
| <kbd>right</kbd> / <kbd>space</kbd>| next animation or slide |
| <kbd>left</kbd>  / <kbd>shift</kbd><kbd>space</kbd> | previous animation or slide |
| <kbd>up</kbd> | previous slide |
| <kbd>down</kbd> | next slide |

<!-- https://sli.dev/guide/animations.html#click-animation -->
<img
  v-click
  class="absolute -bottom-9 -left-7 w-80 opacity-50"
  src="https://sli.dev/assets/arrow-bottom-left.svg"
  alt=""
/>
<p v-after class="absolute bottom-23 left-45 opacity-30 transform -rotate-10">Here!</p>

---
layout: two-cols
layoutClass: gap-16
---

# Table of contents

You can use the `Toc` component to generate a table of contents for your slides:

```html
<Toc minDepth="1" maxDepth="1"></Toc>
```

The title will be inferred from your slide content, or you can override it with `title` and `level` in your frontmatter.

::right::

<Toc v-click minDepth="1" maxDepth="2"></Toc>

---
layout: image-right
image: https://cover.sli.dev
---

# Code

Use code snippets and get the highlighting directly, and even types hover![^1]

```ts {all|5|7|7-8|10|all} twoslash
// TwoSlash enables TypeScript hover information
// and errors in markdown code blocks
// More at https://shiki.style/packages/twoslash

import { computed, ref } from 'vue'

const count = ref(0)
const doubled = computed(() => count.value * 2)

doubled.value = 2
```

<arrow v-click="[4, 5]" x1="350" y1="310" x2="195" y2="334" color="#953" width="2" arrowSize="1" />

<!-- This allow you to embed external code blocks -->
<<< @/snippets/external.ts#snippet

<!-- Footer -->
[^1]: [Learn More](https://sli.dev/guide/line-highlighting)

<!-- Inline style -->
<style>
.footnotes-sep {
  @apply mt-5 opacity-10;
}
.footnotes {
  @apply text-sm opacity-75;
}
.footnote-backref {
  display: none;
}
</style>

<!--
Notes can also sync with clicks

[click] This will be highlighted after the first click

[click] Highlighted with `count = ref(0)`

[click:3] Last click (skip two clicks)
-->

---
level: 2
---

# Shiki Magic Move

Powered by [shiki-magic-move](https://shiki-magic-move.netlify.app/), Slidev supports animations across multiple code snippets.

Add multiple code blocks and wrap them with <code>````md magic-move</code> (four backticks) to enable the magic move. For example:

````md magic-move {lines: true}
```ts {*|2|*}
// step 1
const author = reactive({
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
})
```

```ts {*|1-2|3-4|3-4,8}
// step 2
export default {
  data() {
    return {
      author: {
        name: 'John Doe',
        books: [
          'Vue 2 - Advanced Guide',
          'Vue 3 - Basic Guide',
          'Vue 4 - The Mystery'
        ]
      }
    }
  }
}
```

```ts
// step 3
export default {
  data: () => ({
    author: {
      name: 'John Doe',
      books: [
        'Vue 2 - Advanced Guide',
        'Vue 3 - Basic Guide',
        'Vue 4 - The Mystery'
      ]
    }
  })
}
```

Non-code blocks are ignored.

```vue
<!-- step 4 -->
<script setup>
const author = {
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
}
</script>
```
````

---

# Components

<div grid="~ cols-2 gap-4">
<div>

You can use Vue components directly inside your slides.

We have provided a few built-in components like `<Tweet/>` and `<Youtube/>` that you can use directly. And adding your custom components is also super easy.

```html
<Counter :count="10" />
```

<!-- ./components/Counter.vue -->
<Counter :count="10" m="t-4" />

Check out [the guides](https://sli.dev/builtin/components.html) for more.

</div>
<div>

```html
<Tweet id="1390115482657726468" />
```

<Tweet id="1390115482657726468" scale="0.65" />

</div>
</div>

<!--
Presenter note with **bold**, *italic*, and ~~striked~~ text.

Also, HTML elements are valid:
<div class="flex w-full">
  <span style="flex-grow: 1;">Left content</span>
  <span>Right content</span>
</div>
-->

---
class: px-20
---

# Themes

Slidev comes with powerful theming support. Themes can provide styles, layouts, components, or even configurations for tools. Switching between themes by just **one edit** in your frontmatter:

<div grid="~ cols-2 gap-2" m="t-2">

```yaml
---
theme: default
---
```

```yaml
---
theme: seriph
---
```

<img border="rounded" src="https://github.com/slidevjs/themes/blob/main/screenshots/theme-default/01.png?raw=true" alt="">

<img border="rounded" src="https://github.com/slidevjs/themes/blob/main/screenshots/theme-seriph/01.png?raw=true" alt="">

</div>

Read more about [How to use a theme](https://sli.dev/themes/use.html) and
check out the [Awesome Themes Gallery](https://sli.dev/themes/gallery.html).

---

# Clicks Animations

You can add `v-click` to elements to add a click animation.

<div v-click>

This shows up when you click the slide:

```html
<div v-click>This shows up when you click the slide.</div>
```

</div>

<br>

<v-click>

The <span v-mark.red="3"><code>v-mark</code> directive</span>
also allows you to add
<span v-mark.circle.orange="4">inline marks</span>
, powered by [Rough Notation](https://roughnotation.com/):

```html
<span v-mark.underline.orange>inline markers</span>
```

</v-click>

<div mt-20 v-click>

[Learn More](https://sli.dev/guide/animations#click-animation)

</div>

---

# Motions

Motion animations are powered by [@vueuse/motion](https://motion.vueuse.org/), triggered by `v-motion` directive.

```html
<div
  v-motion
  :initial="{ x: -80 }"
  :enter="{ x: 0 }"
  :click-3="{ x: 80 }"
  :leave="{ x: 1000 }"
>
  Slidev
</div>
```

<div class="w-60 relative">
  <div class="relative w-40 h-40">
    <img
      v-motion
      :initial="{ x: 800, y: -100, scale: 1.5, rotate: -50 }"
      :enter="final"
      class="absolute inset-0"
      src="https://sli.dev/logo-square.png"
      alt=""
    />
    <img
      v-motion
      :initial="{ y: 500, x: -100, scale: 2 }"
      :enter="final"
      class="absolute inset-0"
      src="https://sli.dev/logo-circle.png"
      alt=""
    />
    <img
      v-motion
      :initial="{ x: 600, y: 400, scale: 2, rotate: 100 }"
      :enter="final"
      class="absolute inset-0"
      src="https://sli.dev/logo-triangle.png"
      alt=""
    />
  </div>

  <div
    class="text-5xl absolute top-14 left-40 text-[#2B90B6] -z-1"
    v-motion
    :initial="{ x: -80, opacity: 0}"
    :enter="{ x: 0, opacity: 1, transition: { delay: 2000, duration: 1000 } }">
    Slidev
  </div>
</div>

<!-- vue script setup scripts can be directly used in markdown, and will only affects current page -->
<script setup lang="ts">
const final = {
  x: 0,
  y: 0,
  rotate: 0,
  scale: 1,
  transition: {
    type: 'spring',
    damping: 10,
    stiffness: 20,
    mass: 2
  }
}
</script>

<div
  v-motion
  :initial="{ x:35, y: 30, opacity: 0}"
  :enter="{ y: 0, opacity: 1, transition: { delay: 3500 } }">

[Learn More](https://sli.dev/guide/animations.html#motion)

</div>

---

# LaTeX

LaTeX is supported out-of-box. Powered by [KaTeX](https://katex.org/).

<div h-3 />

Inline $\sqrt{3x-1}+(1+x)^2$

Block
$$ {1|3|all}
\begin{aligned}
\nabla \cdot \vec{E} &= \frac{\rho}{\varepsilon_0} \\
\nabla \cdot \vec{B} &= 0 \\
\nabla \times \vec{E} &= -\frac{\partial\vec{B}}{\partial t} \\
\nabla \times \vec{B} &= \mu_0\vec{J} + \mu_0\varepsilon_0\frac{\partial\vec{E}}{\partial t}
\end{aligned}
$$

[Learn more](https://sli.dev/features/latex)

---

# Diagrams

You can create diagrams / graphs from textual descriptions, directly in your Markdown.

<div class="grid grid-cols-4 gap-5 pt-4 -mb-6">

```mermaid {scale: 0.5, alt: 'A simple sequence diagram'}
sequenceDiagram
    Alice->John: Hello John, how are you?
    Note over Alice,John: A typical interaction
```

```mermaid {theme: 'neutral', scale: 0.8}
graph TD
B[Text] --> C{Decision}
C -->|One| D[Result 1]
C -->|Two| E[Result 2]
```

```mermaid
mindmap
  root((mindmap))
    Origins
      Long history
      ::icon(fa fa-book)
      Popularisation
        British popular psychology author Tony Buzan
    Research
      On effectiveness<br/>and features
      On Automatic creation
        Uses
            Creative techniques
            Strategic planning
            Argument mapping
    Tools
      Pen and paper
      Mermaid
```

```plantuml {scale: 0.7}
@startuml

package "Some Group" {
  HTTP - [First Component]
  [Another Component]
}

node "Other Groups" {
  FTP - [Second Component]
  [First Component] --> FTP
}

cloud {
  [Example 1]
}

database "MySql" {
  folder "This is my folder" {
    [Folder 3]
  }
  frame "Foo" {
    [Frame 4]
  }
}

[Another Component] --> [Example 1]
[Example 1] --> [Folder 3]
[Folder 3] --> [Frame 4]

@enduml
```

</div>

Learn More: [Mermaid Diagrams](https://sli.dev/guide/features/mermaid) and [PlantUML Diagrams](https://sli.dev/guide/features/plantuml)

---
foo: bar
dragPos:
  square: 690,32,168,_,-16
---

# Draggable Elements

Double-click on the draggable elements to edit their positions.

<br>

###### Directive Usage

```md
<img v-drag="'square'" src="https://sli.dev/logo.png">
```

<br>

###### Component Usage

```md
<v-drag text-3xl>
  <carbon:arrow-up />
  Use the `v-drag` component to have a draggable container!
</v-drag>
```

<v-drag pos="663,206,261,_,-15">
  <div text-center text-3xl border border-main rounded>
    Double-click me!
  </div>
</v-drag>

<img v-drag="'square'" src="https://sli.dev/logo.png">

###### Draggable Arrow

```md
<v-drag-arrow two-way />
```

<v-drag-arrow pos="67,452,253,46" two-way op70 />

---
src: ./pages/imported-slides.md
hide: false
---

---

# Monaco Editor

Slidev provides built-in Monaco Editor support.

Add `{monaco}` to the code block to turn it into an editor:

```ts {monaco}
import { ref } from 'vue'
import { emptyArray } from './external'

const arr = ref(emptyArray(10))
```

Use `{monaco-run}` to create an editor that can execute the code directly in the slide:

```ts {monaco-run}
import { version } from 'vue'
import { emptyArray, sayHello } from './external'

sayHello()
console.log(`vue ${version}`)
console.log(emptyArray<number>(10).reduce(fib => [...fib, fib.at(-1)! + fib.at(-2)!], [1, 1]))
```

---
layout: center
class: text-center
---

# Learn More

[Documentation](https://sli.dev) · [GitHub](https://github.com/slidevjs/slidev) · [Showcases](https://sli.dev/showcases.html)

<PoweredBySlidev mt-10 />
