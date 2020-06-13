---
title: Homework_lesson3 (1)
date: 2020-05-07
---
Example Python program Homework_lesson3 (1).py


## Code

Python example

    # Task 1.
    
    # Init git in some folder on your PC
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor  $git init
        # Initialized empty Git repository in /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor/.git/
    
    # Add new file with «From master branch» content
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor  $echo "# Cursor" >> README.md
    
    # Add this file to the git (Don’t forget about commit)
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor  $git add README.md
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor  $git commit  -m 'Adding readme.md file'
            # [master (root-commit) 43438d2] Adding readme.md file
            #  1 file changed, 1 insertion(+)
            #  create mode 100644 README.md
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor master $echo "First commit" >> firstfile.txt
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor master $git add firstfile.txt
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor master $git commit -m "first tes commit in master branch"
            # [master dea300c] first tes commit in master branch
            #  1 file changed, 1 insertion(+)
            #  create mode 100644 firstfile.txt
    
    # Checkout to the «feature/work_with_file» branch
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor master $git branch feature/work_with_file
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor master $git branch --list
            #   feature/work_with_file
            # * master
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor master $git checkout feature/work_with_file
            # Switched to branch 'feature/work_with_file'
    
    # Create new file with «n=a+b» content
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor feature/work_with_file $echo "n = a+b" >> secondtest_file.txt
    
    # Add this file to the git
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor feature/work_with_file $git add secondtest_file.txt
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor feature/work_with_file $git commit -m "second test file to new bransh"
            # [feature/work_with_file ebecca4] second test file to new bransh
            #  1 file changed, 1 insertion(+)
            #  create mode 100644 secondtest_file.txt
    
    # Create git repository on github
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor feature/work_with_file $git remote add origin https://github.com/ekut2104/Cursor.git
    
    # Push your local changes to the remote
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor feature/work_with_file $git push -u origin master
            # Username for 'https://github.com': ekut2104
            # Password for 'https://ekut2104@github.com':
            # Enumerating objects: 6, done.
            # Counting objects: 100% (6/6), done.
            # Delta compression using up to 4 threads
            # Compressing objects: 100% (3/3), done.
            # Writing objects: 100% (6/6), 509 bytes | 101.00 KiB/s, done.
            # Total 6 (delta 0), reused 0 (delta 0)
            # To https://github.com/ekut2104/Cursor.git
            #  * [new branch]      master -> master
            # Branch 'master' set up to track remote branch 'master' from 'origin'.
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor feature/work_with_file $git push -u origin master feature/work_with_file
            # Username for 'https://github.com': ekut2104
            # Password for 'https://ekut2104@github.com':
            # Enumerating objects: 4, done.
            # Counting objects: 100% (4/4), done.
            # Delta compression using up to 4 threads
            # Compressing objects: 100% (2/2), done.
            # Writing objects: 100% (3/3), 342 bytes | 342.00 KiB/s, done.
            # Total 3 (delta 0), reused 0 (delta 0)
            # To https://github.com/ekut2104/Cursor.git
            #  * [new branch]      feature/work_with_file -> feature/work_with_file
            # Branch 'master' set up to track remote branch 'master' from 'origin'.
    
    
    
    # Task 2.
    
    # Checkout from feature/work_with_file to the new branch(in repository from previous task, name is up to you)
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor feature/work_with_file $git branch task2
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor feature/work_with_file $git checkout task2
            # Switched to branch 'task2'
    
    # Update file with «n=5» content
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor task2 $cat secondtest_file.txt
            # n = a+b
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor task2 $gedit secondtest_file.txt
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor task2 $cat secondtest_file.txt
            # n = a
    #
    # Add changes to the git
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor task2 $git add secondtest_file.txt
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor task2 $git commit -m "update file secondtest_file.txt"
            # [task2 9910539] update file secondtest_file.txt
            #  1 file changed, 1 insertion(+), 1 deletion(-)
    
    # Merge this branch TO the feature/work_with_file branch
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor task2 $git checkout feature/work_with_file
            # Switched to branch 'feature/work_with_file'
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor feature/work_with_file $git merge task2
            # Updating ebecca4..9910539
            # Fast-forward
            #  secondtest_file.txt | 2 +-
            #  1 file changed, 1 insertion(+), 1 deletion(-)
    
    # Push your local changes to the remote
        #  ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor feature/work_with_file $git push origin
            # Username for 'https://github.com': ekut2104
            # Password for 'https://ekut2104@github.com':
            # Enumerating objects: 5, done.
            # Counting objects: 100% (5/5), done.
            # Delta compression using up to 4 threads
            # Compressing objects: 100% (2/2), done.
            # Writing objects: 100% (3/3), 275 bytes | 91.00 KiB/s, done.
            # Total 3 (delta 1), reused 0 (delta 0)
            # remote: Resolving deltas: 100% (1/1), completed with 1 local object.
            # To https://github.com/ekut2104/Cursor.git
            #    ebecca4..9910539  feature/work_with_file -> feature/work_with_file
    
    
    # Task 3.
    
    # Change on GitHub file feature/work_with_file with new content
    # Commit on GitHub your changes
        # 1  secondtest_file.txt
        # @@ -1 +1,2 @@
        # n = a
        # Change on GitHub file feature/work_with_file with new content
    
    # Change on your local git file feature/work_with_file with new content different from remote
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor feature/work_with_file $echo "Change on your local git file feature/work_with_file with new content different from remote" >> secondtest_file.txt
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor feature/work_with_file $cat secondtest_file.txt
            # n = a
            # Change on your local git file feature/work_with_file with new content different from remote
    
    # Add your changes to the git
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor feature/work_with_file $git add secondtest_file.txt
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor feature/work_with_file $git commit -m "Update secondtest_file some new 2nd str"
            # [feature/work_with_file 870d52e] Update secondtest_file some new 2nd str
            #  1 file changed, 1 insertion(+)
    
    # Pull origin feature/work_with_file
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor feature/work_with_file $git pull origin
            # remote: Counting objects: 3, done.
            # remote: Compressing objects: 100% (3/3), done.
            # remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
            # Unpacking objects: 100% (3/3), done.
            # From https://github.com/ekut2104/Cursor
            #    9910539..dfa389f  feature/work_with_file -> origin/feature/work_with_file
            # Auto-merging secondtest_file.txt
            # CONFLICT (content): Merge conflict in secondtest_file.txt
            # Automatic merge failed; fix conflicts and then commit the result.
    
    # Fix merge conflict left information from remote repository
    # Add your changes to the git
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor feature/work_with_file $gedit secondtest_file.txt
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor feature/work_with_file $git add secondtest_file.txt
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor feature/work_with_file $git commit -m "Fix merge conflict left information from remote repository"
            # [feature/work_with_file 8a6a68c] Fix merge conflict left information from remote repository
    
    # Push to the remote repository
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Cursor feature/work_with_file $git push origin
            # Username for 'https://github.com': ekut2104
            # Password for 'https://ekut2104@github.com':
            # Enumerating objects: 10, done.
            # Counting objects: 100% (10/10), done.
            # Delta compression using up to 4 threads
            # Compressing objects: 100% (6/6), done.
            # Writing objects: 100% (6/6), 664 bytes | 664.00 KiB/s, done.
            # Total 6 (delta 3), reused 0 (delta 0)
            # remote: Resolving deltas: 100% (3/3), completed with 2 local objects.
            # To https://github.com/ekut2104/Cursor.git
            #    dfa389f..8a6a68c  feature/work_with_file -> feature/work_with_file
            
            
     # Task 4*.
    
    # Clone remote repository from https://github.com/cursor-education/Git-lesson.git
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education  $git clone https://github.com/cursor-education/Git-lesson.git
            # Cloning into 'Git-lesson'...
            # remote: Enumerating objects: 9, done.
            # remote: Counting objects: 100% (9/9), done.
            # remote: Compressing objects: 100% (5/5), done.
            # remote: Total 9 (delta 2), reused 6 (delta 1), pack-reused 0
            # Unpacking objects: 100% (9/9), done.
    #
    # Send me your github login (for adding you as collaborators)
        # Done!
    
    # Checkout to the new branch bugfix/YOURLOGIN
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Git-lesson bugfix/ekut2104 $
    # Fix bug
        # Done!
    # Push your branch on the remote repository
        # ekut: /media/ekut/48D443B7D443A5D2/Users/Melnyk.D/OneDrive/Python_Projects_education/Git-lesson bugfix/ekut2104 $git push origin bugfix/ekut2104
            # Username for 'https://github.com': ekut2104
            # Password for 'https://ekut2104@github.com':
            # Enumerating objects: 5, done.
            # Counting objects: 100% (5/5), done.
            # Delta compression using up to 4 threads
            # Compressing objects: 100% (2/2), done.
            # Writing objects: 100% (3/3), 487 bytes | 487.00 KiB/s, done.
            # Total 3 (delta 0), reused 0 (delta 0)
            # remote:
            # remote: Create a pull request for 'bugfix/ekut2104' on GitHub by visiting:
            # remote:      https://github.com/cursor-education/Git-lesson/pull/new/bugfix/ekut2104
            # remote:
            # To https://github.com/cursor-education/Git-lesson.git
            #  * [new branch]      bugfix/ekut2104 -> bugfix/ekut2104
    
    # Create a pull request to the master
        # Done!

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
