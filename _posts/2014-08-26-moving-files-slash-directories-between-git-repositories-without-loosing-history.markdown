---
layout: post
title: "Moving Files / Directories between Git Repositories without loosing History"
date: 2014-08-26 21:16:10 +0200
comments: false
sharing: false
categories: Programming
---
<p>To Move some Files or Directories from one Git Repository to another one preserving the Git History you can use the "--subdirectory-filter".</p>
<p>With this option, all Commits are parsed to find everyone, matching your selected files.</p>
<p>Make always a copy of your Repositories before starting to Move something, so you wan't loose any Data if something get wrong.</p>
<p>Same procedure was already used by Linus Torvalds the principal force behind the development of the Linux kernel [1] in his "The coolest merge EVER!" [2]</p>
<p>&nbsp;</p>
<p>Here are the Initial two Repositories:</p>
<pre>.
|-- RepositoryA
| `-- ContentA
| `-- contentA.txt
`-- RepositoryB
 `-- ContentB
 `-- contentB.txt</pre>
 
 <!-- more -->

<p>&nbsp;</p>
<p>We start in RepositoryA and move the Files in the ContentA Directory to RepositoryB</p>
<pre class="lang:sh decode:true">cd RepositoryA
git remote rm origin
git filter-branch --subdirectory-filter ContentA -- --all
# everithing from the directory "ContentA" is now in the root dir of the repositoryA
mkdir ContentA
mv * ContentA</pre>
<p>&nbsp;</p>
<p>&nbsp;</p>
<pre class="lang:sh decode:true ">git add ContentA
git commit

# Do not push anything! Change to your Destinations Repository (RepositoryB)
cd RepositoryB
git remote add Repository-A ../RepositoryA
git pull Repository-A master
# Enter your Merge Commit Message and delete the temporary remote
git remote rm Repository-A</pre>
<p>&nbsp;</p>
<p>Finally you have to create the ContentA Directory again or some similar to clean up your new Repository<br />
mkdir ContentA<br />
mv contentA.txt ContentA</p>
<p>&nbsp;</p>
<pre>.
|-- ContentA
| `-- contentA.txt
`-- ContentB
 `-- contentB.txt</pre>
<p>&nbsp;</p>
<p>[1] http://en.wikipedia.org/wiki/Linus_Torvalds<br />
[2] http://thread.gmane.org/gmane.comp.version-control.git/5126/</p>
