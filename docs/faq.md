# Frequently Asked Questions (F.A.Q.)

## Q: Why does Glide have the concept of sub-packages when Go doesn't?

In Go every directory is a package. This works well when you have one repo containing all of your packages. When you have different packages in different VCS locations things become a bit more complicated. A project containing a collection of packages should be handled with the same information including the version. By grouping packages this way we are able to manage the related information.

## Q: bzr (or hg) is not working the way I expected. Why?

These are works in progress, and may need some additional tuning. Please take a look at the [vcs package](https://github.com/masterminds/vcs). If you see a better way to handle it please let us know.

## Q: Should I check `vendor/` into version control?

That's up to you. It's not necessary, but it may also cause you extra work and lots of extra space in your VCS. There may also be unforeseen errors ([see an example](https://github.com/mattfarina/golang-broken-vendor)).

## Q: How do I import settings from GPM, Godep, or gb?

There are two parts to importing.

1. If a package you import has configuration for GPM, Godep, or gb Glide will recursively install the dependencies automatically.
2. If you would like to import configuration from GPM, Godep, or gb to Glide see the `glide import` command. For example, you can run `glide import godep` for Glide to detect the projects Godep configuration and generate a `glide.yaml` file for you.

Each of these will merge your existing `glide.yaml` file with the
dependencies it finds for those managers, and then emit the file as
output. **It will not overwrite your glide.yaml file.**

You can write it to file like this:

    $ glide import godep -f glide.yaml


## Q: Can Glide fetch a package based on OS or Arch?

Yes. Using the `os` and `arch` fields on a `package`, you can specify
which OSes and architectures the package should be fetched for. For
example, the following package will only be fetched for 64-bit
Darwin/OSX systems:

    - package: some/package
      os:
        - darwin
      arch:
        - amd64

The package will not be fetched for other architectures or OSes.

## Q: How did Glide get its name?

Aside from being catchy, "glide" is a contraction of "Go Elide". The
idea is to compress the tasks that normally take us lots of time into a
just a few seconds.
