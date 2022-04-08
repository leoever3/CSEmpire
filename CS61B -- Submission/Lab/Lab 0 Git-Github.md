* Clone the repository of your repository in Github to submit assignments
* Add the skeleton remote repository (From the CS61B) to get starter code

### Steps:

1. Sign up in Github

2. Create a repository in Github name:“CS61B”

3. Create a local dictionary in c:/user/leoever  name:”cs61b”



4. Current dictionary to local dictionary “cs61b”

   ==Clone== mine own Github

   Current dictionary to the clone CS61B

   ![image-20211101132113244](/Users/morningstar/Library/Application Support/typora-user-images/image-20211101132113244.png)

5. ==Remote== add Github for Berkeley sp-18

![image-20211101132326249](/Users/morningstar/Library/Application Support/typora-user-images/image-20211101132326249.png)

6. List all the remote

![image-20211101132403971](/Users/morningstar/Library/Application Support/typora-user-images/image-20211101132403971.png)

7. ==Pull== are the files from sp-18 to local dictionary

   ![image-20211101132513622](/Users/morningstar/Library/Application Support/typora-user-images/image-20211101132513622.png)

8. Copy two .java files to lab1(local) then submit

![image-20211101132609555](/Users/morningstar/Library/Application Support/typora-user-images/image-20211101132609555.png)

9. ==Push== the modification to my own Gihub

![image-20211101132652559](/Users/morningstar/Library/Application Support/typora-user-images/image-20211101132652559.png)

### Codes:

```
 $ cd cs61b
 $ git clone https://github.com/Berkeley-CS61B-Student/sp18-**.git
 $ cd sp18-**
 
 $ git remote add skeleton https://github.com/Berkeley-CS61B/skeleton-sp18.git
 $ git remote -v
 
 $ git pull skeleton master
 $ git push origin master
```

### Tips:

```
Not a git repository (or any of the parent directories): .git

git init
```

```
git remote -v

//to check the push and fetch desitination
```

SSH key on Mac

open ~/.ssh/config

###### SSH

https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection

###### Personal Access Token

https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token
