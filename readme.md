# 学习git_知其然，知其所以然

<details><summary>美丽的故事和三区一远程</summary>
  假设在一个月黑风高的夜晚，我受老板委托，写一篇美丽的爱情故事，故事的内容简洁而优雅
  
  ```
  美丽和俊生从小就青梅竹马，然后他们结婚了。
  ```
  
  故事写完了，但是我预想到老板不会这样轻易放过我，这个事情肯定会经过无数次更改，和无数次推翻重写，以及产生很多种分支结局，最后才能“勉强”交活。
  于是我想，我需要一个**版本管理和分支管理的系统**，以帮助我整理所有的版本，以及故事分支。
  
  我想象中的工作方式是这样的：
  ```
  在我的`桌子`上几张纸写或改写几张稿子，新画或改画几张插画 ===========>觉得差不多了，就把改好的东西全部复印，好几张复印件放到一个`篮子`里 ===========> 然后把篮子里的东西倒在`架子`的某层上，表示一个版本 =======>最终确定以后，发送给老板的邮箱
  ```
  这样我就不怕到时候找不回旧版，或者版本混乱了。
  
  根据我的规划，我需要一个`桌子`，一个`篮子`，和一个`架子`，以及`老板的邮箱`
  
  
</details>

<details><summary>git init</summary>
  
  于是，我想到了GIT。为了使用GIT，我
  1. 新建一个文件夹`故事`，
  2. 并且新建并写作一个文本文件`故事.txt`，
  3. 然后在命令行里进入这个文件夹，输入git init，它便成功的开始使用GIT管理我的工程（实际上是这个文件夹）了。
  
  那么实际上git init做了什么事呢？首先它建了一个文件夹叫做`git`，用来存储他管理时要用的文件。
  ```
  ├── 故事
│   ├── 故事.txt
│   └── .git
  ```
  
  `故事`文件夹，就是我们的工作区。 而.git里面藏了两外两个区，其中一个叫暂存区（好象个盆子），还有一个成品区（好像库房）。
  当你的头脑没有发神经的时候，git是这样工作的：
  
  ```
  改啊改写啊写 ===========》 提交到暂存区 ===========》提交到成品区
  ```
  

</details>

<details><summary>git add</summary>

</details>

<details><summary>git commit -m "message"</summary>

</details>

<details><summary>git log</summary>

</details>

<details><summary>git reset --hard HEAD^或(1094a)</summary>

</details>

<details><summary>git reflog</summary>

</details>

<details><summary>git revert</summary>

</details>

<details><summary>git diff HEAD -- readme.md</summary>

</details>

<details><summary>git restore <file></summary>

</details>

<details><summary>git restore --staged <file></summary>

</details>

<details><summary>git rm <file></summary>

</details>

<details><summary>git checkout -- <file></summary>

</details>

<details><summary>git remote add origin <git adress></summary>

</details>

<details><summary>git push -u origin master</summary>

</details>

<details><summary>git push origin master</summary>

</details>

<details><summary>git clone <git address></summary>

</details>

<details><summary>git remote -v</summary>

</details>

<details><summary>git remote rm <name></summary>

</details>

<details><summary>git branch <name> </summary>

</details>

<details><summary>git switch <name></summary>

</details>

<details><summary>git switch -c <name></summary>

</details>

<details><summary>git branch</summary>

</details>

<details><summary>git merge <name></summary>

</details>

<details><summary>git branch -d <name></summary>

</details>

<details><summary>git stash</summary>

</details>

<details><summary>git stash list</summary>

</details>

<details><summary>git stash pop</summary>

</details>

<details><summary>git stash apply stash@[号码]</summary>

</details>

<details><summary>git cherry-pick <提交></summary>

</details>

<details><summary>git checkout -b dev origin/dev</summary>

</details>

<details><summary>git pull</summary>

</details>

<details><summary>git branch --set-upstream-to=origin/dev dev</summary>

</details>

<details><summary>git tag v1.0</summary>

</details>

<details><summary>git tag </summary>

</details>

<details><summary>git tag v0.9 f223344</summary>

</details>

<details><summary>git show v0.9</summary>

</details>

<details><summary>git tag -a v0.1 -m "version 0.1 release" 12abda </summary>

</details>

<details><summary>git tag -d v0.1</summary>

</details>

<details><summary>git push origin <tagname></summary>

</details>

<details><summary>git push origin --tags</summary>

</details>

<details><summary>git push origin :refs/tags/<tagname></summary>

</details>
