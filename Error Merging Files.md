So, you've merged the master branch with itself, and you ended up with a merge commit nobody wanted.

The problem
Let me tell you a little story...
John and Pete are working together on a repo.

$ git log --graph --pretty=oneline --abbrev-commit  # an alias I have under 'git lol', but 'gitk' does just fine
* 812492b (master, origin/master, origin/HEAD) Add stuff
* 474c16e I am many things
* 12b7661 I am a Unicorn!
Pete wants to make some changes, and clones the repo/pulls those changes. He gets the same history.

Meanwhile, Jon continues working, building on top of that, and pushes his changes. Pete also makes some changes, without pulling first.

* 1c12c15 (HEAD, master) 123
* 8ee7d24 Do stuff
* d4f7393 Woo
* 812492b (origin/master, origin/HEAD) Add stuff
* 474c16e I am many things
* 12b7661 I am a Unicorn!
When comes the time to push...

$ git push
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to '/home/jon/dev3/foo'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
And so, he does what instructed. He pulls (and thus gets the status of origin)

$ git pull origin master
 * branch            master     -> FETCH_HEAD
Already up-to-date!
Merge made by the 'recursive' strategy.

*   1654d53 (HEAD, master) Merge branch 'master' of /home/jon/dev3/foo
|\  
| * 57b81dc (origin/master, origin/HEAD) Blah
| * 1794a9f Do other stuff
| * a235abc Correct more
* | 1c12c15 123
* | 8ee7d24 Do stuff
* | d4f7393 Woo
|/  
* 812492b Add stuff
* 474c16e I am many things
* 12b7661 I am a Unicorn!
Git suggests merging, and an ugly merge commit is born.

Explanation
Because Pete didn't pull the changes before committing, he committed on top of an old commit (812492b), one which Jon had already built upon. Indeed, Jon built a235abc, 1794a9f, etc. on top of it.

If Pete had pulled before committing, his master branch would've been updated to 57b81dc, and instead of on 812492b, d4f7393 would've been built on top of that (bearing another commit SHA).

In Git, the parent of a commit is a big deal, since that's what the commit bases its changes on. And that's why when we say we change a commit and put it on another base, we are rebasing.

The reason why origin didn't accept Pete's changes, 1c12c15, is that 1c12c15 wasn't a child of origin. In other words, there was no obvious way for origin to go from its position, 57b81dc, to the pushed position, 1c12c15. Hence, the push was denied.

By making a merge commit, 1654d53, Git suggested Pete creates a child of origin with Pete's own history. (Romantic, I know!)

Now, we have to undo that before pushing a clean history.

The Remedy
The strategy here is instead of Jon and Pete's commits to have the same parent (812492b), we are going to base Pete's commits on top of Jon's.

We are going to use the following tools:

git reset rewinds the branch to another commit.

git rebase rebases a dangling branch on top of another.

Let's examine the situation.

$ git lol
*   1654d53 (HEAD, master) Merge branch 'master' of /home/jon/dev3/foo
|\  
| * 57b81dc (origin/master, origin/HEAD) Blah
| * 1794a9f Do other stuff
| * a235abc Correct more
* | 1c12c15 123
* | 8ee7d24 Do stuff
* | d4f7393 Woo
|/  
* 812492b Add stuff
* 474c16e I am many things
* 12b7661 I am a Unicorn!
First things first, we have to get our branch back to where it was, at the top of Pete's changes (1c12c15). That's what he was trying to push.

$ git reset --hard 1c12c15
HEAD is now at 1c12c15 master

* 1c12c15 (HEAD, master) 123
* 8ee7d24 Do stuff
* d4f7393 Woo
* 812492b Add stuff
* 474c16e I am many things
* 12b7661 I am a Unicorn!
(We used the --hard switch because we didn't care about the leftovers. A --mixed or --soft reset would've kept the modified files in the working tree.)

What we just did was to undo the merge commit. Also, as a side effect of git pull, our Git now knows where origin/master is at, which is useful, so we can see it in our logs.

If we just want to know where a remote is, git fetch is there for next time instead of pull. Which brings us to...

Where were we
Now, we have to rebase our commits, which are based on 812492b, as you can see, and change that base for 57b81dc, aka origin/master.

The rebase command changes the branch of where we are (master) to get on top of what we give it as an argument. As we want master (Pete's) to be on top of origin/master, we'll give it that.

$ git rebase origin/master
First, rewinding head to replay your work on top of it...
Applying: Woo
Applying: Do stuff
Applying: 123

* b330a1c (HEAD, master) 123
* 15e4ded Do stuff
* 8bfd53a Woo
* 02f75fc (origin/master, origin/HEAD) foo
* 57b81dc Blah
* 1794a9f Do other stuff
* a235abc Correct more
* 812492b Add stuff
* 474c16e I am many things
* 12b7661 I am a Unicorn!

And here we are! We now have a linear history!

Our commits are now children of origin/master, and linear.

Note: I cheated a bit in my shell to get a demonstrable history, so there might be errors here and there. Corrections/improvements welcome!
