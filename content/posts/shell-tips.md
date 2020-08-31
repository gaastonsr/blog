---
title: "Shell Tips"
date: 2020-08-31T00:36:05-05:00
draft: true
---

### Documentation

When using the terminal, it's likely that you are doing common operations. Maybe
you want to create a new user, or you want to decompress a file. For those
cases, I recommend using tldr-pages. tldr-pages is a collection of
community-maintained help pages for command-line tools, that aims to be a
simpler, more approachable complement to traditional
[man pages](https://en.wikipedia.org/wiki/Man_page).

```sh
# Install it.
$ brew install tldr
# Use it.
$ tldr tar

tar

Archiving utility.
Often combined with a compression method, such as gzip or bzip.
More information: <https://www.gnu.org/software/tar>.

- Create an archive from files:
    tar cf target.tar file1 file2 file3

- Create a gzipped archive:
    tar czf target.tar.gz file1 file2 file3

- Create a gzipped archive from a directory using relative paths:
    tar czf target.tar.gz -C path/to/directory .

- Extract a (compressed) archive into the current directory:
    tar xf source.tar[.gz|.bz2|.xz]

... rest of the output truncated ...
```
