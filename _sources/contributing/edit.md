# Editing the Manual

The manual is purely written in [MyST Markdown](https://jupyterbook.org/en/stable/reference/cheatsheet.html) and the sources are hosted on GitHub. All kinds of contributions are very welcome and appreciated -- be it a typo fix, dead link update, or new tutorial addition.
This page describes how to make edits directly on the GitHub web editor.

## 1. Forking the repo

Go to the GitHub repo you want to fork (https://github.com/wengroup/group_manual in this case), and click `Fork` then `Create fork`.

```{figure} ../image/edit-1.png

```

```{figure} ../image/edit-2.png

```

## 2. Making edits

After forking, the repo will be copied to your GitHub account. Here, the `group_manual` repo from the `wengroup` GitHub account has been forked to the `mjwen` account.

Then, you can edit your forked version of the repo (`mjwen/group_manual` here). Navigate to the file you want to edit and then make changes to it. For example, you can select the `laptop.md` file and click the pencil button to start editing.

```{figure} ../image/edit-3.png

```

After changing a file, enter a commit message describing what you've done (e.g. `Typo fix`), select `Commit directly to the main branch`, and then click `Commit changes` to commit your edits.

```{figure} ../image/edit-4.png

```

```{tip}
Here, we use the GitHub web editor to make and commit changes. Alternatively, you can clone the repo, edit it locally, and push the commits. See [Using GitHub](using:github) for instructions.
When editing locally, you may also want to build the manual and view it. For this, see [Local Build](local:build).
```

## 3. Making a pull request

Now that you have made changes to your fork of the repo (e.g. `mjwen/group_manual`), you want to make a pull request to propose your changes to the upstream repo (e.g. `wengroup/group_manual`).

Go to the homepage of your fork of the repo, click `Contribute` and then `Open pull request`.

```{figure} ../image/edit-5.png

```

Then, enter a brief title and some additional message describing your pull request, check `Allow edits by maintainers`, and click `Create pull request`.

```{figure} ../image/edit-6.png

```

This is all you need to do. We will then take a look at the pull request and merge it.

```{tip}
You can commit multiple changes and then make a single pull request for them, i.e. performing step 2 multiple times for different files and then step 3 only once.
```
