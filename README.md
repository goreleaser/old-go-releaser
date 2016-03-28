# go-releaser

It is boring to write release scripts, and I was like in need to write one more.

So, I changed what I already had in
[antibody](https://github.com/getantibody/antibody) and make it simple
enough so it can be used within any go project, basically.

## What it does?

1. Compiles the project with `gox` to several platforms, setting the
`main.version` ldflag to current git tag name;
2. Packages it in `tar.gz` files in the form of
`binary_$(uname -s)_$(uname -m).tar.gz`, so it could be easily scripted;
3. Creates a github release for the current tag, setting the description of it
with the commit log between the current and previous tags;
4. Finally, upload all `tar.gz` files to the created release.

This is kind of opinionated, so, your project will need to "follow some rules"
in order to use it.

## The rules

1. Go 1.5 or higher;
2. No Windows support - I just don't care;
3. `main.version` ldflag - it's useful to the users;
4. It has a `README*` and `LICENSE*` files - because of the users, again;
5. The `dist` folder should not contain anything important.

## Usage

Basically, all is done in a very simple `getopts` loop, so, you need to run it
like this:

```console
./release \
  -u caarlos0 \ # repo owner on github
  -r go-releaser \ # repo name on github
  -b release \ # binary filename
  -m ./cmd/main.go \ # your main go file
  -e "FILE1 FILE2 FILE3" # optional, extra files you want to add, besides the binary itself with LICENSE* and README*
```
