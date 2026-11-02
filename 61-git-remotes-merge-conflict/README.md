# Esercizio di risoluzione di un merge conflict

**Il tempo massimo in laboratorio per questo esercizio è di _20 minuti_.
Se superato, sospendere l'esercizio e riprenderlo per ultimo!**

Si visiti https://github.com/APICe-at-DISI/OOP-git-merge-conflict-test.
Questo repository contiene due branch: `master` e `feature`

Per ognuna delle seguenti istruzioni, si annoti l'output ottenuto.
Prima di eseguire ogni operazione sul worktree o sul repository,
si verifichi lo stato del repository con `git status`.

1. Si cloni localmente il repository

$ git clone git@github.com:APICe-at-DISI/OOP-git-merge-conflict-test.git

2. Ci si assicuri di avere localmente entrambi i branch remoti

$ git branch -a
master
  remotes/origin/HEAD -> origin/master
  remotes/origin/feature
  remotes/origin/master

$ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean

3. Si faccia il merge di `feature` dentro `master`, ossia: si posizioni la `HEAD` su `master`
   e da qui si esegua il merge di `feature`
   
$ git log --graph --all --oneline
\* d809d3e (feature) switch to Java 25 IO.println
\* e4ee4cb switch to Java 25 compact source file
\* bed943f Print author information
| * 2f617a5 (HEAD -> master) switch to Java 25 IO.println
| * 9c519e7 switch to Java 25 compact source file
| * 8e0f29c Change HelloWorld to print the number of available processors
|/
\* d956df6 Create .gitignore
\* 700ee0b Create HelloWorld


4. Si noti che viene generato un **merge conflict**!

$git merge feature
Auto-merging HelloWorld.java
CONFLICT (content): Merge conflict in HelloWorld.java
Automatic merge failed; fix conflicts and then commit the result.

5. Si risolva il merge conflict come segue:
   - Il programma Java risultante deve stampare sia il numero di processori disponibili
     (funzionalità presente su `master`)
     che il nome dell'autore del file
     (funzionalità presente su `feature`)

Su VSCode:
final String AUTHOR = "Danilo Pianini";

int procNumber() {
	return Runtime.getRuntime().availableProcessors();
}

void main() {
	IO.println("This program is running in a PC with " + procNumber() + " logic processors!");
	IO.println("This program has been realised by " + AUTHOR);
}

$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   HelloWorld.java

no changes added to commit (use "git add" and/or "git commit -a")

$ git add HelloWorld.java
$ git status
On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:
        modified:   HelloWorld.java
		
$ git commit -m "Fixed the merge conflict"
\[master e9c16fb\] Fixed the merge conflict

$ git status
On branch master
nothing to commit, working tree clean

6. Si crei un nuovo repository nel proprio github personale

- Su GitHub > New repository

7. Si aggiunga il nuovo repository creato come **remote** e si elenchino i remote

$ git remote add origin https://github.com/VoyagerKat/oop-61-the-merge-conflict

$ git remote -v

- origin  git@github.com:VoyagerKat/oop-61-the-merge-conflict.git (fetch)

- origin  git@github.com:VoyagerKat/oop-61-the-merge-conflict.git (push)

8. Si faccia push del branch `master` sul proprio repository

$ git push -u origin master

9. Si setti il branch remoto `master` del nuovo repository come *upstream* per il proprio branch `master` locale

$ git branch -u origin/master
