## Man pages

Not all man-pages are in Alpine, but this will get you most of the way there:

   **apk add mandoc man-pages mandoc-apropos less less-doc**
   **export PAGER=less**

The above only provides _core_ man pages. Other packages typically don't include their own man pages (nor other documentation). Rather, they provide an associated package that carries such stuff. For example:

   $ **apk add curl**
   $ **man curl**
   man: No entry for curl in the manual.
   $ **apropos curl | wc -l**
   0    _After adding curl, there are no man pages_
   $ **apk add curl-doc**
   (1/1) Installing curl-doc (7.52.1-r2)
   Executing mandoc-apropos-1.13.3-r6.trigger
   OK: 60 MiB in 31 packages
   $ **apropos curl | wc -l**
   366  _Now, with curl-doc installed, there's a boatload of pages!_

**NOTE:** Not all packages separate out their documentation, but it is the _Alpine Way_ (e.g. small footprint). Some packages don't provide any installable documentation at all, neither within themselves nor an associated doc packages. Further, appending "-doc" is merely a convention. In fact, the core man documentations are in man-pages (as in the _apk add ..._ command, above). To find the right documentation package, try something like:

   $ **apk search gcc | grep ^gcc**
   gcc-objc-5.3.0-r0
   gcc-gnat-5.3.0-r0
   gcc-5.3.0-r0
   gcc-java-5.3.0-r0
   gcc-doc-5.3.0-r0    _Here it is!_

**FINALLY:** If you're wondering why I've added _less_ (and _less-doc_), it's because _man_ doesn't work correctly with _more_ (the default pager). Don't fret too much about bloating up Alpine, though - adding man pages has a bigger footprint than less (_"less is more than man"???_)

If you would like documentation packages to be pulled in automatically you can add the `docs` meta package.

## Operational hints

#### Shell @ commandline

Alpine comes with busybox by default. Busybox is an endpoint for numerous symlinks for various utilities. Though busybox is not that bad, the commands are impaired in functionality.

-   Funny characters at the console

Edit the file at /etc/rc.conf and change line 92 to:

 unicode="YES"

-   Bash

It is easy enough to have bash installed, but this does not mean the symlinks to busybox are gone.

Install bash with:

  apk add bash bash-doc bash-completion

-   Shell utilities (things like grep, [awk](https://wiki.alpinelinux.org/wiki/Awk "Awk"), ls are all busybox symlinks)

  apk add util-linux pciutils usbutils coreutils binutils findutils grep

-   /etc/{shadow,group} manipulation requires

  apk add shadow

#### Disk Management

Disk management is so much easier with udisks or udisks2

Installation

  apk add udisks2 udisks2-doc

See the mounted disks

  udisksctl status

## Compiling : a few notes and a reminder

Compiling in Alpine may be more challenging because it uses [musl-libc](http://www.musl-libc.org/) instead of glibc. Please review ['The functional differences with glibc'](http://wiki.musl-libc.org/wiki/Functional_differences_from_glibc) if you think of porting packages or just for the sake of knowing, of course.

Alpine offers the regular compiler stuff like gcc and cmake ... possible others

#### (unvalidated) apk packages to install so one can start building software

  apk add build-base gcc abuild binutils binutils-doc gcc-doc

#### a complete install for cmake looks like

  apk add cmake cmake-doc extra-cmake-modules extra-cmake-modules-doc

#### ccache is also available

  apk add ccache ccache-doc