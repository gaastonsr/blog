## Personal tech blog

Theme: [etch](https://themes.gohugo.io/etch/) ([more themes](https://themes.gohugo.io/)).

### How it was set up

```sh
# I installed hugo.
$ brew install hugo
# Then created a new site.
$ cd ~/git/gaastonsr
$ hugo new site blog
# Then installed the theme.
$ cd ~/git/gaastonsr/blog
$ git init
$ git subdmodule add git@github.com:LukasJoswiak/etch.git themes/etch
# Then added the theme to `config.toml`.
$ echo 'theme = "etch"' >> config.toml
# Then added the first blog post.
$ hugo new posts/hello-world.md
# And added an about page.
$ hugo new about/index.md
# Started the server.
$ hugo server -D
```

### How it was deployed to GitHub Pages

[Here](https://gohugo.io/hosting-and-deployment/hosting-on-github/#step-by-step-instructions), are
the instructions that I followed.

I created a `gaastonsr.github.io` repository, and then added it as a submodule to
this repository.

```sh
$ cd ~/git/gaastonsr/blog
$ git submodule add -b master git@github.com:gaastonsr/gaastonsr.github.io.git public
Cloning into '~/git/gaastonsr/blog/public'...
warning: You appear to have cloned an empty repository.
fatal: 'origin/master' is not a commit and a branch 'master' cannot be created from it
Unable to checkout submodule 'public'
```

An error was returned. To fix that, let's add an empty commit to the repository.

```sh
$ cd ~/git/gaastonsr
$ git clone git@github.com:gaastonsr/gaastonsr.github.io.git
$ cd gaastonsr.github.io
$ git commit --allow-empty -m 'Initial commit'
$ git push
```

Now if I try to add the submodule again, it won't work because the previous
`git submodule add` operation had a fatal error and left the submodule in a
dirty state where the submodule wasn't added, that can be verified by checking
that there is not settings for the submodule in `.gitmodules` and `.git/config`
but at the same time the empty repository was copied locally, that can be
verified by checking that git repositories exist at `public/.git` and
`.git/modules/public`, so some cleanup is needed before the submodule can be
added again.

```sh
$ cd ~/git/gaastonsr/blog
# Remove resources created by the previous unsuccesful `git submodule add`.
$ rm -rf public && rm -rf .git/modules/public
$ git submodule add -b master git@github.com:gaastonsr/gaastonsr.github.io.git public
Cloning into '~/git/gaastonsr/blog/public'...
remote: Enumerating objects: 2, done.
remote: Counting objects: 100% (2/2), done.
remote: Total 2 (delta 0), reused 2 (delta 0), pack-reused 0
Receiving objects: 100% (2/2), done.
```

It worked now, yay!

### Deploying to GitHub Pages

To automate the process a `deploy.sh` script was created.

```sh
# Create the script.
$ cd ~/git/gaastonsr/blog
$ touch deploy.sh
# Give it execution permissions.
$ chmod u+x deploy.sh
```

Add the script shown [here](https://gohugo.io/hosting-and-deployment/hosting-on-github/#put-it-into-a-script). And now `./deploy.sh "Optional commit message"` can
be used to deploy your changes.

### Adding a custom domain

[Documentation](https://docs.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site#configuring-a-subdomain).

Go to the blog [settings](https://github.com/gaastonsr/gaastonsr.github.io/settings) and under
the "GitHub Pages" section add your domain, in this case `wwww.gaston.dev`.

Now go to your DNS provider and set up `CNAME` record that points to
`gaastonsr.github.io`. In this case `CNAME www.gaston.dev -> gaastonsr.github.io`.

### Recommended set up to update the blog

1. Install hugo: `bew install hugo` ([more info](https://gohugo.io/getting-started/installing/)).
2. Install a toml extension for you code editor.

### Common actions

- Start the server: `hugo server -D`.
- Create a post: `hugo new posts/hello-world.md`.
- Create a page: `hugo new about/index.md`.
- Deploy changes: `deploy.sh "Optional commit message"`. Don't forget commiting your changes after deploying.
