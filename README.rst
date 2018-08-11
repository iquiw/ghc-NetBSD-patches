================================================
Collection of patches for ghc specific to NetBSD
================================================

--------
Audience
--------
Those who want to build ghc on NetBSD (assume you already have other version of ghc).

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

In addition, there are some other fixes for NetBSD.

# They should be included in the upstream, but the patch is not yet much clean.

-----------
How to use?
-----------
1. Download one of patch file corresponding to ghc to be built.

2. Unpack ghc source tarball and go to libraries directory::

    $ tar xzf ghc-x.x.x.tar.gz
    (> 7.6) $ cd ghc-x.x.x
    (< 7.6) $ cd ghc-x.x.x/libraries

3. Apply the patch::

    (> 7.6) $ patch -p1 < /somewhere/ghc-x.x.x.NetBSD.patch
    (< 7.6) $ patch -p1 < /somewhere/ghc-x.x.x.NetBSD-ffi-wrappers.patch
    (< 7.6) $ cd ..

4. Run boot::

    (< 8.4) $ perl boot
    (> 8.4) $ python3.7 boot

6. Build ghc. (Requires working ghc)

   For example::

     $ ./configure --prefix=/opt/ghc-x.x.x \
       --with-gmp-includes=/usr/pkg/include --with-gmp-libraries=/usr/pkg/lib \
       --with-iconv-includes=/usr/pkg/include --with-iconv-libraries=/usr/pkg/lib

-----------------
Supported version
-----------------
ghc-6.12.3.NetBSD-ffi-wrappers.patch
   ghc-6.12.3

ghc-7.0.4.NetBSD-ffi-wrappers.patch
   ghc-7.0.1, ghc-7.0.2, ghc-7.0.3, ghc-7.0.4

ghc-7.4.2.NetBSD-ffi-wrappers.patch
   ghc-7.4.1, ghc-7.4.2

ghc-7.6.1.NetBSD.patch
   ghc-7.6.1

ghc-7.6.2.NetBSD.patch
   ghc-7.6.2, ghc-7.6.3

ghc-7.8.3.NetBSD.patch
   ghc-7.8.2, ghc-7.8.3

ghc-7.10.2.NetBSD.patch
   ghc-7.10.1, ghc-7.10.2

ghc-8.2.2.NetBSD.patch
   ghc-8.2.1, ghc-8.2.2

ghc-8.4.1.NetBSD.patch
   ghc-8.4.1, ghc-8.4.2, ghc-8.4.3
