1. Create a repository in your [Git hub account](https://github.com/)
2. Create a local project folder
3. Inside the folder open git bash
4. Run the following commands:

**Create an empty Git repository or reinitialize an existing one**
```bash
git init
```

**Connect your local repository (folder) to the one created at your github**

```bash
git remote add origin [Your repo URL goes here]
```

**Add file contents to the index**

```bash
git add [file nname]
```

**Record changes to the repository**

```bash
git commit -m "your messge for update goes here"
```

**Set the remote as upstream**
```bash
git push --set-upstream origin master
```

Once the remote is set as upstream, The next push can be done simply by using the following command.
```bash
git push
```

If you want to integrate your git repo to a discord channel using a webhook, follow the guide to how to [[Add a webhook to discord]]


