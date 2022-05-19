### A. Intro to Version Control Systems

* ==Version control systems== are tools to keep track of changes to files over time.
* Version control allows you to view or revert back to previous iterations of files.   **undo**

##### Intro to Git

* Git is a ==distributed== version control system.
* It means that every developer's computer stores the entire history of the entire project.
* We call the entire history if an entire project a ==repository==.

### B. Local Repositories (Keywords introduction)

* An example with recipes

* Linux keywords

 **cd** <dictionaryname>: current dictionary

**mkdir** <dictionaryname>: make dictionary

**subl** <textname.txt>: use sublime to edit or create a text (sublime is a text editor)

 

**git init**: initiation the <u>repository</u> 

**git add** <the document or the path>: add to the list of files to <u>track</u>	git add . (add all)

**git commit -m** ”comments for the operation” : <u>commit</u>

 

**git status**: check the status of files

**git log**: list all the commit

**git show** <commit ID>: look into one commit

 

**git checkout** <commit ID> <path or document> : rearranges files back

### C. Local Repositories (Technical Overview)



![File Status Lifecyle](https://sp18.datastructur.es/materials/guides/img/file-status.png)



### D. Remote Repositories

- `git clone [remote-repo-URL]`: Makes a copy of the specified repository, but on your local computer. Also creates a working directory that has files arranged exactly like the most recent snapshot in the download repository. Also records the URL of the remote repository for subsequent network data transfers, and gives it the special remote-repo-name “origin”.
- `git remote add [remote-repo-name] [remote-repo-URL]`: Records a new location for network data transfers.
- `git remote -v`: Lists all locations for network data transfers.
- `git pull [remote-repo-name] master`: Get the most recent copy of the files as seen in remote-repo-name
- `git push [remote-repo-name] master`: Pushes the most recent copy of your files to the remote-repo-name.