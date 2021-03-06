Hello hackers!

General remarks about contributing
----------------------------------

Contributions to the libnfc are welcome!
Here are some directions to get you started:

  1. Follow style conventions
     The source code of the library trend to follow some conventions so that it
     is consistent in style and thus easier to read.
     Look around and respect the same style.
     Don't use tabs. Increment unit is two spaces.
     Don't leave dandling spaces or tabs at EOL.
     Helper script to get some uniformity in the style:
     $ make style

     If you use vim see the [Vim: How to prevent trailing whitespaces](http://www.carbon-project.org/Vim__How_to_prevent_trailing_whitespaces.html).

  2. Chase warnings: no warning should be introduced by your changes
  Depending what you touch, you can check with:

    2.1 When using autotools

            $ autoreconf -Wall -vis

    2.2 When compiling

      2.2.1 Using extra flags:

            $ export CFLAGS="-Wall -g -O2 -Wextra -pipe -funsigned-char -fstrict-aliasing \
              -Wchar-subscripts -Wundef -Wshadow -Wcast-align -Wwrite-strings -Wunused \
              -Wuninitialized -Wpointer-arith -Wredundant-decls -Winline -Wformat \
              -Wformat-security -Wswitch-enum -Winit-self -Wmissing-include-dirs \
              -Wmissing-prototypes -Wstrict-prototypes -Wold-style-definition \
              -Wbad-function-cast -Wnested-externs -Wmissing-declarations"
         $ ./configure
         $ make clean
         $ make

      2.2.2 Using clang:

        You can use same CFLAGS but also `-Wunreachable-code`

            $ scan-build ./configure
         $ make clean
         $ scan-build make

      2.2.3 Using `cppcheck` (v1.58 or higher):

          $ make cppcheck

    2.3 When Debianizing

         $ lintian --info --display-info --display-experimental *deb
        or (shorter version)
         $ lintian -iIE *deb

  3. Preserve cross-platform compatility

     The source code should remain compilable across various platforms,
     including some you probably cannot test alone so keep it in mind.
     Supported platforms:

     - Linux
     - FreeBSD
     - Mac OS X
     - Windows with MinGW
