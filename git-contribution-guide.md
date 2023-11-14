# How to Contribute to the Second Life Viewer

🌟 **Thank you for showing interest in contributing to the Second Life Viewer!** 🌟

This guide is specially designed for those who are passionate about contributing but may be new to using Git. We aim to provide a clear and easy-to-follow path that will help you navigate the contribution process, from forking the repository to submitting your pull request.


#### Before beginning, ensure you have the following:

- A GitHub account.
- Git installed locally. Instructions can be found in [this manual](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git). Alternatively, you can use a Git GUI, like [GitHub Desktop](https://desktop.github.com/) or [Fork](https://git-fork.com/).
- After installing Git please follow the [first-time setup guide](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup).


## Preparations

### Forking the Repository

1. Visit the [Second Life Viewer repository](https://github.com/secondlife/viewer/).
2. Click the “Fork” button at the top right to create a copy in your GitHub account.

### Cloning Your Fork

1. Navigate to your fork on GitHub.
2. Click the “Code” button and copy the URL under “Clone with HTTPS”.
3. In your CLI or Git GUI console, clone your fork using 
    ```
    git clone [URL you just copied]
    ```
4. Go into the cloned directory.
5. Add the original repository as an upstream remote:
    ```
    git remote add upstream https://github.com/secondlife/viewer/
    ```

## Making and Submitting Changes

### Synchronizing your local copy with the Original Repository

1. Fetch the changes from the original repository:
    ```
    git fetch upstream
    ```
2. Switch to your `main` branch:
    ```
    git checkout main
    ```
3. Merge changes from the upstream main:
    ```
    git merge upstream/main
    ```

### Creating a New Branch

1. Create a new branch for your changes:
    ```
    git checkout -b [new-branch-name]
    ```
2. Make your changes in the new branch. Be sure to adhere to our [Coding Standard Guide](https://wiki.secondlife.com/wiki/Coding_standard).
3. Stage the changes:
    ```
    git add .
    ```
4. Commit the changes with a descriptive message:
    ```
    git commit -m "A brief description of changes"
    ```
    If you have a ticket number (e.g. BUG-12345), please add it to the commit message.

### Pushing Changes and Creating a Pull Request

1. Push the changes to your fork:
    ```
    git push origin [your-branch-name]
    ```
2. Visit your fork on GitHub.
3. You will likely see a prompt to create a pull request based on the recent push. If not, navigate to the "Pull requests" tab in the original Second Life Viewer repository.
4. Click the “New pull request” button.
5. Ensure the base repository is set to `secondlife/viewer` and the base branch is set to `main`.
6. For the head repository, select your fork and choose the branch where you've made your changes.
7. Click the “Compare & pull request” button.
8. Fill in the details of your changes, providing a clear and concise description of what you've done.
9. Submit the pull request.
10. If prompted to sign the Contributor License Agreement (CLA), please follow the instructions. This is usually required when contributing for the first time.
11. The Second Life Viewer maintainers will review your contribution shortly.

## Following Up

- Keep an eye on your pull request for any feedback. The review process is collaborative, and your responses may be needed.
- If you have any questions, please don't hesitate to contact us.
- We look forward to your innovative ideas and improvements. Thank you for being a part of our community!
