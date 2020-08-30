## Personal blog

Theme: [etch](https://themes.gohugo.io/etch/) ([more themes](https://themes.gohugo.io/)).

### How it was set up

```sh
# I installed hugo
$ brew install hugo
# Then created a new site
$ cd ~/git/gaastonsr
$ hugo new site blog
# Then installed the theme
$ cd ~/git/gaastonsr/blog
$ git init
$ git subdmodule add git@github.com:LukasJoswiak/etch.git themes/etch
# Then added the theme to `config.toml`
$ echo 'theme = "etch"' >> config.toml
# Then added the first blog post
$ hugo new posts/hello-world.md
# And added an about page
$ hugo new about/index.md
# Started the server
$ hugo server -D
```

### Recommended set up to update the blog

1. Install hugo: `bew install hugo` ([more info](https://gohugo.io/getting-started/installing/)).
2. Install a toml extension for you code editor.
