---
title: Git Pretty or Git Lost - Beautifying Your Commit History One Message at a Time
draft: false
tags: 
  - tech
  - git
  - collaboration
  - best-practices
date: 2024-09-19
publish: true
---

> [!INFO] Gist
> In my recent efforts to bring more detail, structure, and simple aesthetic value into my life - both [[Taking Back Control - Part 2 | personal]] and professional, I completely changed the way I approach version control. 
> 
> While it might suffice on an individual level to write vague commit messages implicative of some action, with the belief that you'll be reminded of the details upon reading it, you only truly unlock the immense potential and value of a commit history once you take the leap into neat, formatted, and informative commit messages.
> 
> Here's how I do mine:

![[IMG-20240919233530908.png]]

////////////////////////////////////////////////////////////////////

## Gitting Started
Basics first - You likely don't know what a commit message is.

```git
ea89xxx  random fix, things work now 
```
⬆ This, is not a commit message. You know that sick one-liner you wrote 3 months ago when you encountered a similar bug as today, which you can't manage to find and reference because none of the messages convey anything meaningful? That's a **commit summary**, or **subject line**, which is only one part - the first part, of a commit message; and it's job is to do the *one thing* your old commit messages don't - summarize the change concisely, so you know exactly what it is at just a glance.

This is where 95% of people with bad commit messages mess up, because this is *all* that 95% of people include in their commits. No description, mention of related issues, TODO notes for future maintainers - just the summary. That's exactly why you should strive to get them right, because odds are, that's all you're going to write. The good news is, there's an easy formula to a good commit summay:

- **50 characters or less**. That's the space within which you should concisely describe the change. GitHub and GitLab will truncate anything beyond this, so try to stay within the limit!
- **Summarize the change concisely**. We don't need to know your methodology from the summary, just the resulting change! So don't say `"added a resize observer to prevent the overflow of user input"`, just say `"fix overflow of user input"`
- **Where possible, prefix with a type**. For example, `fix: type import error`. The type conveys even more information about what category of change your commit made. Some common types are:
	- `fix` - bug fixes
	- `feat` - new features
	- `docs` - changes to documentation
	- `refactor` - restructuring code without changing external behavior
	- `chore` - clean up, maintenance tasks
	- `style` - code style and formatting
- **Write in an imperative mood**. Don't say `"added a new function to handle outputs"`, instead say `"add a new method for output handling"`. Confused about what exactly imperative voice means? Essentially, you commit should fit neatly in the sentence: `"If you apply this commit, it will <Your Commit Summary here>"`

If you just put in the effort to write a good summary/subject line to your commits, I can guarantee your collaborators will be 10 times happier to work with you. Just think about it - No one wants to be the one *writing* the 200 pages of detailed documentation about a service, but no one has *ever* been unhappy about being able to reference it when they're in a pickle. Seeing as how a commit message is *just 50 characters* of effort, be that person that everyone is happy to have on their team.

## Committing to the details
So you've made the first step. Your subject lines are on point, and no one is leaving you messages on Teams asking what the code you just pushed does anymore; congratulations! But why stop there?

I'm sure you agree that it can be a challenge to really convey everything that matters about a change from a 50-character subject alone. What if you're anticipating a future addition to your current feature, and don't want to spend time re-reading your own code to understand it? It's time to dive into the **commit description** my friend.

First things first - *where* you're writing your commit messages matters. If you're using this simple input field in VSCode, you really can't write anything except the commit summary: 

![[IMG-20240919222243767.png]]

The same goes for if you're using the shorthand terminal command:
```bash
git commit -a -m "This is my commit's subject line"
```

If you're looking to delve into more detail in your commits, I'd recommend starting off by simply ditching the shorthand flag `-m` in your terminal command:
```bash
git commit -a
```
This will open your default configured text editor (likely nano or vim) where you can enter a full commit message:

![[IMG-20240919222755446.png]]

Now, lightweight text editors like `nano` and `vim` can be scary at first, **especially** vim. This is because they often don't allow you to simply point-and-click with your mouse to get things done, and to make matters worse, don't support *any* of the MS Word keyboard shortcuts that you're used to! Learning how to use these is an entire other topic that I'll save for another time, but for now, you con simply use your tried-and-tested favourite - Visual Studio Code. To set this up, simply run the following command in your terminal:

```bash
git config --global core.editor "code --wait"
```

This is of course, assuming that you've already [added the `code` command to your PATH](https://code.visualstudio.com/docs/setup/mac#_launching-from-the-command-line). Once you've set this up, running `git commit` will open a VSCode window for you to enter your commit message:

![[IMG-20240919224015132.png]]

Using vscode has another advantage. See those 2 vertical lines? That's not a visual bug, those are **guide lines** letting you know exactly where your message will be truncated/wrapped. The first line is for the summary/subject, which as we discussed, is truncated at 50 characters. The second line indicates the point at which you should ideally be wrapping your commit descriptions - **72 characters**. 

Now, you might be tempted to explain every step of your thought-process and methodology to the change in your description, but hold off on that. Use the description to explain the **what and the why** of the change, *not the how*; developers are usually smart enough to figure that out by reading the diffs, or discussing in MR/PR comments and issues.

Your description can be multiple paragraphs long, so if you feel that there's a lot of value to be had in providing extensive detail and context to the change, then by all means - go ham!

## Git to the Bottom - Sealing the Deal with Metadata
Finally, once you're done writing the entire script of The Bee Movie in the commit description, you still have one more place to shine - the **commit footer**, which is used for metadata. Most commits don't need a footer at all, but there's a significant amount of information that could be shared in the footer. Common uses include:
- Referencing issues: `Fixes: #1234`, `See also: #8888`
- Breaking changes: `BREAKING CHANGES: JSON Data Structure has changed.`
- Sign-offs: `Signed-off-by: That Random Indian Teacher on YouTube <seekho-coding@example.com>`

I personally haven't used footers much at all apart from the odd reference to related issues, but most of my metadata-sharing needs at work happen in **Merge Request Descriptions** (a future topic, perhaps). Nevertheless, simply knowing that such a thing is at your disposal could be very valuable in your next team project, so keep it in mind!

## The Final Push
We've now gone over the complete commit message - the **summary, description, and footer**. Now to put it all together for the ultimate addition to your messy git log. (Remember to separate each section with a blank line)

```
feat: Add user authentication system

 - I like to write my descriptions as bullets, but feel free to only
   use paragraphs
 - The new system includes:
	 - User registration
	 - Login/Logout functionality
	 - Password reset flow

Fixes: #123
Signed-off-by: Jane Smith <jane@example.com>
```

You probably won't need *all* of this for *every* commit that you make. In fact, most of your general commits should ideally be [atomic commits](https://dev.to/samuelfaure/how-atomic-git-commits-dramatically-increased-my-productivity-and-will-increase-yours-too-4a84) that only require the summary line; so at the very least, get that bit right. But for exceptionally important commits, or simply to provide a detailed summary of your entire week's development by providing more detail in the last commit before you push your changes, these aspects of a git message can drastically improve the readability and value of your repository's commit history.

Try it out! Or don't, I'm going to push this article to my blog regardless.

`git add .`

`git commit -m "whatever, im lazy"`

`git push -f`

....well, shit.

**Further Reading:**
- [How to Write a Git Commit Message](https://cbea.ms/git-commit/)
- [Git - Book](https://git-scm.com/book/en/v2)
- [Git - gittutorial Documentation](https://git-scm.com/docs/gittutorial)

---
Tokyo, Japan





