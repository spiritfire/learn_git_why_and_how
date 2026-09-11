# Mastering Git: Inside and Out

**English** | [简体中文](./README.md)

---

<details><summary>The Story & The Three Areas + Remote</summary>
  On a dark and stormy night, my boss commissioned me to write a beautiful romance novel. With the deadline breathing down my neck, I tried to slack off by writing the shortest, most elegant love story on earth:
  
  ```text
  Meili and Junsheng were childhood sweethearts, and then they got married.
  ```
  
  Exactly 12 words. While I handed it in, I knew my boss would flip the table. This story was doomed to suffer endless rewrites, absurd plot twists, and schizophrenic alternate endings.
  If I had to rely on saving files as `Story_Final.txt`, `Story_Final_v2.txt`, `Story_RealFinal_I_Swear.txt`, I would lose my mind.
  
  So, I realized I needed a rigorous **Version & Branch Management System**.
  My dream workflow looked like this:
  ```text
  Doodle and draft on my 【Desk】 (wild, unconstrained changes)
  ===========> Once satisfied with a page, photocopy it into the 【Basket】 (staged for filing)
  ===========> Bind the pages in the basket, slap on a barcode, file it onto the 【Shelf】 (immutable history)
  ===========> Sync the shelf archives onto 【Boss's Cloud Drive】 (backup, cross-device, delivery)
  ```
  
  Accordingly, I need:
  - A `Desk` (Working Directory / Workspace)
  - A `Basket` (Staging Area / Index)
  - A `Shelf` (Local Repository / HEAD)
  - And `Boss's Cloud Drive` (Remote Repository)
</details>

<details><summary>git init</summary>
  
  To initialize this system, I:
  1. Created a folder named `story`;
  2. Created a file `story.txt` inside with the 12-word minimalist story;
  3. Opened the terminal, navigated into the folder, and typed:
  
  ```bash
  git init
  ```

  **Under the Hood:**  
  This command silently plants a **hidden folder** called `.git`.
  ```text
  ├── story/
  │   ├── story.txt      <--- Your 【Desk】 (Working Directory)
  │   └── .git/          <--- Houses your 【Basket】 (Staging Area) & 【Shelf】 (Repository)
  ```
  As long as `.git` exists, you can mess around on your desk freely. Delete it, and all Git magic evaporates.
</details>

<details><summary>git add</summary>

  Looking at my 12-word masterpiece on the desk, lazy as it was, it was still my baseline draft. I needed to put it into the filing basket:

  ```bash
  git add story.txt
  # Or toss everything on the desk into the basket at once:
  git add .
  ```

  **Metaphor in Action:**  
  Photocopied the draft from the desk (Working Directory) and dropped it neatly into the 【Staging Basket (Index)】.  
  *Note: The archive shelf hasn't changed yet; things are merely primed for storage.*
</details>

<details><summary>git commit -m "message"</summary>

  With my 12-word draft resting safely in the basket, I decided to formally bind and shelf it as the genesis of history:

  ```bash
  git commit -m "v1.0: Ultra-short 12-word edition, straight from childhood to marriage"
  ```

  **Metaphor in Action:**  
  Took the papers from the 【Basket】, bound them into a book, stamped it with a message note, and slotted it into the 【Shelf】 (Commit). The basket is now empty.  
  The shelf assigned it a unique, permanent barcode (SHA hash, like `a1b2c3d`). From this moment on, this snapshot is immortal.
</details>

<details><summary>git log</summary>

  As expected, the boss raged: "12 words?! Are you kidding me?! Add the meeting, the falling in love, the drama, the elopement!"  
  Over the next three days, I frantically expanded the plot:
  - Added "Chapter 2: Campus Meeting" -> `git add` -> `git commit`
  - Added "Chapter 3: Family Opposition" -> `git add` -> `git commit`
  - Added "Chapter 4: Rainy Night Elopement" -> `git add` -> `git commit`

  Now, I wanted to see the complete history on my shelf:

  ```bash
  git log
  # Want a clean, visual tree graph?
  git log --oneline --graph
  ```

  **Metaphor in Action:**  
  Opening the archivist's ledger. It logs in reverse chronological order: who filed which version, at what exact time, with what barcode and commit note.
</details>

<details><summary>git reset --hard HEAD^ or (hash)</summary>

  **Disaster strikes!**  
  The boss drank cheap tequila last night and called at 2 AM screaming: "Readers want toxic melodrama! Make Meili and Junsheng long-lost biological siblings who discover the truth at the altar!"  
  Crying, I pulled an all-nighter, wrote the forbidden sibling drama, and committed it to the shelf.  

  At 10 AM, sober boss screamed: "What is this trash?! Who told you to write incest?! Roll it back! Take me back to the elopement chapter right now!"

  ```bash
  # Roll back to the previous commit (HEAD^ = 1 back, HEAD^^ = 2 back)
  git reset --hard HEAD^

  # Or jump directly using the barcode hash from the log (e.g., 1094a):
  git reset --hard 1094a
  ```

  **Metaphor in Action:**  
  Time travel! `--hard` is ruthless: it rewinds the reading pointer on the shelf AND **sets fire to all sibling-drama drafts currently on the desk and in the basket**. The desk is restored to the exact pristine state of Chapter 4.
</details>

<details><summary>git reflog</summary>

  **A crisis worse than the disaster!**  
  At 2 PM, after an iced Americano, the boss slapped his thigh: "Wait! Sibling angst is trending #1 on TikTok! Where is that sibling draft you deleted this morning?! Bring it back now!"  
  Dizzy with dread, I ran `git log`—the sibling commit was gone from the timeline! What now?!

  ```bash
  git reflog
  ```

  **Under the Hood:**  
  `git log` only views the currently reachable timeline. `reflog` is the **flight recorder black-box of the time machine itself**. It records every head movement, reset, and jump you ever performed.  
  Looking into the black box, I found: `commit: add sibling drama`, tagged with hash `f8e7d6c`!  
  Calmly, I typed:
  ```bash
  git reset --hard f8e7d6c
  ```
  The "incinerated" draft materialized back onto my desk out of thin air. The boss stared at me as if I were a wizard.
</details>

<details><summary>git revert</summary>

  The story progressed, and I had smoothly reached Chapter 8.  
  The boss rushed in, sweating profusely: "Legal just informed us that the luxury handbag the second male lead gave away in Chapter 3 infringes a trademark! Undo that product placement commit immediately! But DO NOT lose Chapters 4 through 8!"  

  If I used `reset` back to Chapter 3, the five chapters I sweated over would be wiped out. Enter `revert`:

  ```bash
  # Assuming the product placement commit hash is 33a22bb
  git revert 33a22bb
```
Metaphor in Action & Under the Hood:
Git isn't an AI ghostwriter; it doesn't write new storylines. It simply performs precise inverse mathematics (a Reverse Patch):
Back then, that commit added: + The guy flaunts a designer handbag.
revert calculates the exact inverse: - The guy flaunts a designer handbag, and cleanly snips that line right out of your current Chapter 8 manuscript on the desk.
It applies this deletion, preserves every other word from Chapters 4 to 8, and files a new receipt on the shelf: "This commit offsets commit 33a22bb".
Result: History remains honest, all 8 chapters survive, the illegal bag evaporates, and you avoid a lawsuit!
</details>

<details><summary>git diff HEAD -- story.txt</summary>

  I spent the whole afternoon tweaking `story.txt` on my desk. By sunset, staring at the screen, I blanked out: What on earth did I actually change today?

  ```bash
  git diff HEAD -- story.txt
  ```

  **Metaphor in Action:**  
  Holding the latest pristine copy from the shelf in my left hand, and the scribbled draft from the desk in my right, holding them against the light: Red lines show what was removed, green lines show what was added.
</details>

<details><summary>git restore &lt;file&gt;</summary>

  Late afternoon brain fog hit me: I typed an absurd paragraph where "Meili gets abducted by aliens to be their queen." Coming to my senses before adding it to the basket: I need to destroy the evidence before the boss sees it!

  ```bash
  git restore story.txt
  ```

  **Metaphor in Action:**  
  Crumpled the alien-graffiti-stained paper and fed it to the shredder. Photocopied a clean version from the shelf onto the desk. Life goes on as if aliens never existed.
</details>

<details><summary>git restore --staged &lt;file&gt;</summary>

  I wrote a scene where "Junsheng weeps in the rain," and instinctively ran `git add story.txt` into the basket.  
  Right after, I hesitated: "No, crying makes him look weak; he should sneer coldly. But it's already in the basket—how do I un-stage it?"

  ```bash
  git restore --staged story.txt
  ```

  **Metaphor in Action:**  
  Reaching into the 【Basket】 and tossing the papers back onto the desk. The edits on the desk remain untouched; they simply exit the "ready to be committed" line so you can keep polishing.
</details>

<details><summary>git rm &lt;file&gt;</summary>

  Earlier, I created `side_characters.txt` to track cast relations. Now that most of them have been killed off, I want this file gone from both my desk and future repository records:

  ```bash
  git rm side_characters.txt
  git commit -m "Cast is mostly dead, delete side characters sheet"
  ```

  **Metaphor in Action:**  
  Shredded the file from the desk and dropped a note into the basket: "File terminated, do not include in future archives." Once committed, Git ceases tracking it entirely.
</details>

<details><summary>git checkout -- &lt;file&gt;</summary>

  The legacy Git incantation for discarding unstaged modifications on your desk, identical to `git restore <file>`:

  ```bash
  git checkout -- story.txt
  ```

  **Under the Hood:**  
  Legacy Git overloaded `checkout` with too many responsibilities (switching branches, restoring files, detached HEADs). Modern Git introduced `restore` and `switch` for clarity. You'll see this everywhere in older stackoverflow threads.
</details>

<details><summary>git remote add origin &lt;git address&gt;</summary>

  After ten days of solo writing, my local shelf was packed. Boss knocked: "What if your laptop dies? I created a cloud repo on GitHub. Link your shelf to it now!"

  ```bash
  git remote add origin https://github.com/boss-corp/love-story.git
  ```

  **Metaphor in Action:**  
  Recording the remote cloud server address in my notebook under the standard nickname `origin`.
</details>

<details><summary>git push -u origin master</summary>

  With the link ready, I needed to upload my entire local shelf for the first time:

  ```bash
  git push -u origin master
  # If your default branch is main: git push -u origin main
  ```

  **Metaphor in Action:**  
  Hiring a freight truck to copy all files on my local `master` shelf over to the `master` bay of boss's cloud warehouse.  
  The `-u` (upstream) flag sets up an automatic track between them, so Git remembers where to sync next time.
</details>

<details><summary>git push origin master</summary>

  Next day, inspiration struck and I committed two more chapters locally. Time to sync with the boss:

  ```bash
  git push origin master
  ```

  **Metaphor in Action:**  
  With the `-u` tracks already laid, I just nudge the new parcels down the track to the cloud drive. If you're currently on `master`, simply running `git push` does the job.
</details>

<details><summary>git clone &lt;git address&gt;</summary>

  Over the weekend on my home PC, I wanted to write a bit. The desk was empty:

  ```bash
  git clone https://github.com/boss-corp/love-story.git
  ```

  **Metaphor in Action:**  
  Connecting to the cloud archive, downloading all history boxes, setting up the `.git` mechanism, and spreading the latest manuscript across the desk. Ready to write immediately.
</details>

<details><summary>git remote -v</summary>

  Juggling side gigs, I got confused: Is this local folder connected to my boss's repo, or my freelance client's?

  ```bash
  git remote -v
  ```

  **Metaphor in Action:**  
  Flipping open the address book (`-v` for verbose). It explicitly lists where fetches pull from and where pushes go.
</details>

<details><summary>git remote rm &lt;name&gt;</summary>

  Fought with the boss, and refused to push my story to his company cloud ever again:

  ```bash
  git remote rm origin
  ```

  **Under the Hood:**  
  This merely scratches the address out of your local book. No manuscripts on either side are deleted; only the link is severed.
</details>

<details><summary>git branch &lt;name&gt;</summary>

  Boss texted: "Happy endings don't sell. Keep the main draft, but spin off a parallel universe where both leads turn evil and die tragically. If readers like it, we make it canon."  
  I must not pollute my main manuscript. I need an alternate timeline:

  ```bash
  git branch tragedy
  ```

  **Metaphor in Action:**  
  Stuck a pink sticky note labeled `tragedy` onto the latest book on the shelf. The timeline branches, but I am still standing on the main line; the desk hasn't changed.
</details>

<details><summary>git switch &lt;name&gt;</summary>

  Parallel universe ready; time to jump into it:

  ```bash
  git switch tragedy
  ```

  **Metaphor in Action:**  
  Multiverse leap! Git whisks the main manuscripts into a drawer and spreads the `tragedy` draft onto the desk. Whatever I write from here stays in the tragedy universe.
</details>

<details><summary>git switch -c &lt;name&gt;</summary>

  Boss texted again: "Spin off a sci-fi universe! Meili is an android!"  
  Creating then switching takes two steps. I want it done in one breath:

  ```bash
  git switch -c scifi
  ```

  **Under the Hood:**  
  `-c` stands for create. Creates the `scifi` branch and leaps into it simultaneously (Equivalent to legacy `git checkout -b scifi`).
</details>

<details><summary>git branch</summary>

  Bouncing between android rebellions and poisonings, I got disoriented: Which timeline am I currently in?

  ```bash
  git branch
  ```

  **Metaphor in Action:**  
  Unfurling the roster of all parallel dimensions: `master`, `tragedy`, `scifi`. The one glowing green with an asterisk `*` is where you physically stand.
</details>

<details><summary>git merge &lt;name&gt;</summary>

  The `tragedy` route was completed: both leads perished in Chapter 10. Boss bawled his eyes out: "Masterpiece! Make this our official canon ending! Merge it into master!"

  ```bash
  # 1. Step back onto the master timeline
  git switch master

  # 2. Absorb the tragedy branch
  git merge tragedy
  ```

  **Under the Hood:**  
  The master timeline fast-forwards and incorporates the chapters from tragedy. If both branches modified the exact same sentence, Git pauses for a "Conflict", displaying both versions side-by-side for you to choose before finalizing with `add` + `commit`.
</details>

<details><summary>git branch -d &lt;name&gt;</summary>

  Now that the tragedy branch has safely merged into master, the temporary sticky note is just clutter:

  ```bash
  git branch -d tragedy
  ```

  **Metaphor in Action:**  
  Peeling the `tragedy` sticky note off the shelf and tossing it into the trash. The words are already part of the master archives, so nothing is lost.
</details>

<details><summary>git stash</summary>

  I was in the middle of `scifi`, writing "Android uprising destroys Earth." The desk was littered with half-finished drafts (impossible to commit yet).  
  Suddenly, boss kicked the door open: "Typo in Chapter 3 on master! Meili's name is misspelled! Fix it in 3 minutes for the printing press!"  
  What do I do with this messy desk? Git won't let me switch branches with uncommitted chaos!

  ```bash
  git stash
  ```

  **Metaphor in Action:**  
  Pulling a secret lockbox out from under the desk, sweeping all half-baked drafts into it, and slamming it shut. The desk is instantly pristine! Now you can safely `git switch master` to fix the typo.
</details>

<details><summary>git stash list</summary>

  Typo fixed on master, I jumped back into `scifi`. Scratching my head: "How many temporary draft boxes did I stash under the bed?"

  ```bash
  git stash list
  ```

  **Metaphor in Action:**  
  Inspecting the inventory of secret boxes under the bed: `stash@{0}`, `stash@{1}`, etc.
</details>

<details><summary>git stash pop</summary>

  Finding box `stash@{0}`, I'm ready to unpack and resume writing:

  ```bash
  git stash pop
  ```

  **Metaphor in Action:**  
  Popping open `stash@{0}`, scattering the unfinished drafts right back onto the desk, and **destroying the box** on the spot. Crime scene restored; back to writing!
</details>

<details><summary>git stash apply stash@[number]</summary>

  What if I want to apply the drafts from `stash@{1}`, but keep the box intact under the bed to reuse on other branches later?

  ```bash
  git stash apply stash@{1}
  ```

  **Under the Hood:**  
  `apply` simply photocopies the contents onto your desk while leaving the lockbox safely stored in the list.
</details>

<details><summary>git cherry-pick &lt;commit&gt;</summary>

  The boss hired an assistant writer, Xiao Li, who was drafting a side story. Glancing at his screen: "Damn, Xiao Li, your 'Kiss Under the Moonlight' scene in Act 3 is pure poetry! My master timeline needs this!"  
  I don't want his whole branch—I **only want that single kiss commit**!

  ```bash
  # Xiao Li's commit barcode is 7788abc
  git cherry-pick 7788abc
  ```

  **Metaphor in Action:**  
  Cherry picking! Reaching across branch boundaries to pluck the single sweetest cherry from someone else's tree, grafting it cleanly into our current branch.
</details>

<details><summary>git checkout -b dev origin/dev</summary>

  Boss promoted Xiao Li to co-author and created a shared `dev` branch on GitHub: "Both of you collaborate here; don't touch master directly!"

  ```bash
  git checkout -b dev origin/dev
  # Modern alternative: git switch -c dev origin/dev
  ```

  **Metaphor in Action:**  
  Setting up a `dev` shelf in my local office, reaching out to the remote `origin/dev` shelf, and welding them together in tandem.
</details>

<details><summary>git pull</summary>

  Arriving at the office, Xiao Li bragged: "Pushed 5,000 words to `dev` last night!"  
  Before writing a single word, I must sync up:

  ```bash
  git pull
  ```

  **Metaphor in Action:**  
  Snatching new chapters from the cloud and **immediately merging them onto my local desk** (A combo of `fetch` + `merge`). Golden Rule of Collaboration: Always pull before writing!
</details>

<details><summary>git branch --set-upstream-to=origin/dev dev</summary>

  Sometimes after creating a local `dev` branch, running `git pull` fails: "Git doesn't know which remote branch to pull from!"

  ```bash
  git branch --set-upstream-to=origin/dev dev
  ```

  **Metaphor in Action:**  
  Tying a guide rope between local `dev` and remote `origin/dev`. With this tether in place, bare `git pull` and `git push` commands know exactly where to go.
</details>

<details><summary>git tag v1.0</summary>

  After surviving countless ordeals—typos fixed, tragedy merged, kiss scene cherry-picked—the book is finished! The boss signs off: "Send it to the printers! Release version 1.0!"

  ```bash
  git tag v1.0
  ```

  **Metaphor in Action:**  
  Commits have ugly barcode hashes (`e7a6b1...`). Tagging is like **stamping a shimmering golden wax seal onto the hardcover: 'v1.0 Release'**. Frozen in time forever.
</details>

<details><summary>git tag</summary>

  Years later, celebrated as a legendary author, I want to count my milestone releases:

  ```bash
  git tag
  ```

  **Metaphor in Action:**  
  Viewing the showcase of all golden wax seals in the room (`v1.0`, `v2.0`, `v3.0-final`).
</details>

<details><summary>git tag v0.9 f223344</summary>

  "Shoot! The preview edition `v0.9` submitted to literary awards was never officially sealed! Can we seal it retroactively?"

  ```bash
  git tag v0.9 f223344
  ```

  **Metaphor in Action:**  
  Retroactive medal awarding! Pulling up commit `f223344` from the archives and stamping a `v0.9` golden seal onto it. Git permits retro-tagging across spacetime.
</details>

<details><summary>git show v0.9</summary>

  An intern wants to inspect the historical `v0.9` milestone edition:

  ```bash
  git show v0.9
  ```

  **Metaphor in Action:**  
  Pulling out the book sealed with `v0.9`, revealing author details, timestamp, and the exact lines penned in that release.
</details>

<details><summary>git tag -a v0.1 -m "version 0.1 release" 12abda</summary>

  I want to immortalize my original 12-word draft as `v0.1`, accompanied by an author's self-deprecating note:

  ```bash
  git tag -a v0.1 -m "Where the dream began: slacking off with 12 words" 12abda
  ```

  **Under the Hood:**  
  A lightweight tag is just a sticky pin. An annotated tag (`-a` with message `-m`) creates a full Git object storing creator, email, date, and comments. Formal and tamper-proof.
</details>

<details><summary>git tag -d v0.1</summary>

  Boss yells: "You tagged that 12-word slapdash insult as a milestone?! Rip it off! Now!"

  ```bash
  git tag -d v0.1
  ```

  **Metaphor in Action:**  
  Scraping the `v0.1` sticker off the local cover. The underlying manuscript remains safe; only the tag name is discarded.
</details>

<details><summary>git push origin &lt;tagname&gt;</summary>

  By default, regular `git push` commands **never** transmit tags to the cloud.

  ```bash
  git push origin v1.0
  ```

  **Metaphor in Action:**  
  Special courier! Explicitly dispatching the `v1.0` golden seal to GitHub. The cloud "Releases" page illuminates, offering release bundles worldwide.
</details>

<details><summary>git push origin --tags</summary>

  If I locally tagged a dozen chapters (`v0.2`, `v0.3`, `v0.4`) and want them all pushed at once:

  ```bash
  git push origin --tags
  ```

  **Metaphor in Action:**  
  Backing up a truck full of tags, stamping every unpushed seal onto the cloud warehouse simultaneously.
</details>

<details><summary>git push origin :refs/tags/&lt;tagname&gt;</summary>

  **The Final Bomb Disposal!**  
  Disaster: That embarrassing `v0.1` tag I was ordered to delete was accidentally pushed to the public cloud earlier! Readers around the globe can witness my 12-word joke!  
  I must expunge it from the remote server immediately:

  ```bash
  # Modern, humane approach:
  git push origin --delete v0.1

  # The hardcore veteran way that reveals Git's inner mechanics:
  git push origin :refs/tags/v0.1
  ```

  **Under the Hood:**  
  Notice the mystical syntax: Ahead of the colon is **Nothing**, after the colon is the remote ref.  
  It literally commands: **"Push 'pure vacuum' to the remote target tag `v0.1`!"**  
  The vacuum overwrites the tag, annihilating it from existence. Boss refreshes the browser, finds nothing, and your career is saved by Git once more!
</details>
