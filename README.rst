================================================
Collection of patches for ghc specific to NetBSD
================================================

--------
Audience
--------
Those who want to build ghc on NetBSD.

-----------
What is it?
-----------
Have you ever seen warning messages like the following?
::

    warning: reference to compatibility gettimeofday(); include <sys/time.h> to generate correct reference

NetBSD keeps binary compatibilities by renaming functions incompatible with old
NetBSD binaries in header files and if proper header files are not included,
the linker complains above warning message.

This also happens when Haskell program calls FFI function that is renamed
in some header file,

These patches provide FFI wrappers for such functions in C files with
proper header files included.

-----------
How to use?
-----------
1. Download one of patch file corresponding to ghc to be built.

2. Unpack ghc source tarball and go to libraries directory::

    $ tar xzf ghc-x.x.x.tar.gz
    $ cd ghc-x.x.x/libraries

3. Apply the patch::

    $ patch -p1 < /somewhere/ghc-x.x.x.NetBSD-ffi-wrappers.patch

4. Run autoreconf in time::

    $ (cd time && autoreconf)

5. Run autoreconf in base (only for GHC 7)::

    $ (cd base && autoreconf)

6. Build ghc.

-----------------
Supported version
-----------------
ghc-6.12.3.NetBSD-ffi-wrappers.patch
   ghc-6.12.3 

ghc-7.0.3.NetBSD-ffi-wrappers.patch
   ghc-7.0.1, ghc-7.0.2, ghc-7.0.3
