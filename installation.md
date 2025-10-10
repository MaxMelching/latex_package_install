# Installing LaTeX Packages

Installing LaTeX Packages is kind of a mess. There are many possibilities,
but every single one of them is a little cumbersome, depends on the
distribution you have installed, etc. For this reason, I list the ways that
I found most convenient, for the two operating systems that I have used up
until this day.

## The Basic Idea

Main source: the great Stefan Kottwitz at https://tex.stackexchange.com/a/1138

OS-independent, here is the idea of this small instruction:
Many recipes found online recommend just setting the `$TEXINPUTS` variable in
a certain manner, which then allows the system to find your `.sty` files.
However, we will do something different, mainly because (as far as I can see)
this must be run either before each compilation or for every shell/compiler
that you run LaTeX in.

Instead, we will utilize that the `~/texmf/tex/latex/` directory (or any
subfolder thereof) is searched by default, so there is no need to manually
refresh package directories. The other tweak is to use symlinks rather than
copying files. This allows you make changes yourself or pull in changes from
upstream, without having to repeat the installation process for these changes
to take effect.

***Note:*** it is not so easy to create symlinks on Windows. If something
doesn't work for you, just replace symlinking by copying and you can still
use the package. You just might have to repeat the copying from time to time.

As always, a check to verify that everything worked is to check the directory
displayed when running

```shell
kpsewhich <filename>
```

in the shell/compiler that you use.

## Windows

The explicit chain of command to run depends on the OS. In case of Windows:

```shell
mklink %USERPROFILE%\texmf\tex\latex\<linked_filename.ending> <path-to-your-repo\filename.ending>
```

or with the `/d` option, if you want to copy an entire directory.

For example, I usually install files in the `Documents/GitHub` folder. In case
of the [gwbar repo](https://github.com/MaxMelching/gwbar), the appropriate command is then

```shell
mklink %USERPROFILE%\texmf\tex\latex\gwbar.sty %USERPROFILE%\Documents\GitHub\gwbar\gwbar.sty
```

where you could very well type out the explicit path as well, instead of using
`%USERPROFILE%`. You could also create a subdirectory and place the file
in there, LaTeX will find it either way.

***Note:*** The `/texmf/tex/latex/` directory chain might not exist
yet. In that case, just create it.

***Note:*** Symlinking usually requires admin privileges on Windows. One
possibility to enable them is prepending a `sudo` to the above prompt.

## Linux

With the same command structure and only a few adjustments:

```shell
ln -s <path-to-your-repo/filename.ending> ~/texmf/tex/latex/<linked_filename.ending>
```
