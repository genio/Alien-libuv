[![Actions Status](https://github.com/p5-UV/Alien-libuv/workflows/linux/badge.svg)](https://github.com/p5-UV/Alien-libuv/actions)
[![Actions Status](https://github.com/p5-UV/Alien-libuv/workflows/macos/badge.svg)](https://github.com/p5-UV/Alien-libuv/actions)
[![Actions Status](https://github.com/p5-UV/Alien-libuv/workflows/windows/badge.svg)](https://github.com/p5-UV/Alien-libuv/actions)

# NAME

Alien::libuv - Interface to the libuv library [http://libuv.org](http://libuv.org)

# SYNOPSIS

In your `Makefile.PL`:

```perl
use strict;
use warnings;

use ExtUtils::MakeMaker;
use Config;
use Alien::Base::Wrapper ();

WriteMakefile(
  Alien::Base::Wrapper->new('Alien::libuv')->mm_args2(
    ...
    CONFIGURE_REQUIRES => {
      'Alien::libuv' => '1.000',
    },
    ...
  ),
);
```

# DESCRIPTION

This package can be used by other [CPAN](https://metacpan.org) modules that
require [libuv](http://libuv.org).

# BACKWARDS COMPATIBILITY

Each upstream release of [libuv](http://libuv.org) adds new features.
To ensure your `XS` or `FFI` code using this module can work with the various
inconsistencies from new features across the version 1 release, you might
consider a backwards compatibility header file akin to:

```
#include <string.h>
#include <stdint.h>
#include <uv.h>


/* pulled from sys/signal.h in case we don't have it in Windows */
#if !defined(SIGPROF)
#define SIGPROF 27 /* profiling time alarm */
#endif

/* added in 1.14 */
#if !defined(UV_DISCONNECT)
#define UV_DISCONNECT 4
#endif
#if !defined(UV_PRIORITIZED)
#define UV_PRIORITIZED 8
#endif
#if !defined(UV_VERSION_HEX)
#define UV_VERSION_HEX                                                         \
    ((UV_VERSION_MAJOR << 16) | (UV_VERSION_MINOR << 8) | (UV_VERSION_PATCH))
#endif

/* not added until v1.23 */
#if !defined(UV_PRIORITY_LOW)
#define UV_PRIORITY_LOW 19
#endif
#if !defined(UV_PRIORITY_BELOW_NORMAL)
#define UV_PRIORITY_BELOW_NORMAL 10
#endif
#if !defined(UV_PRIORITY_NORMAL)
#define UV_PRIORITY_NORMAL 0
#endif
#if !defined(UV_PRIORITY_ABOVE_NORMAL)
#define UV_PRIORITY_ABOVE_NORMAL -7
#endif
#if !defined(UV_PRIORITY_HIGH)
#define UV_PRIORITY_HIGH -14
#endif
#if !defined(UV_PRIORITY_HIGHEST)
#define UV_PRIORITY_HIGHEST -20
#endif

/* not added until 1.24 */
#if !defined(UV_PROCESS_WINDOWS_HIDE_CONSOLE)
#define UV_PROCESS_WINDOWS_HIDE_CONSOLE (1 << 5)
#endif
#if !defined(UV_PROCESS_WINDOWS_HIDE_GUI)
#define UV_PROCESS_WINDOWS_HIDE_GUI (1 << 6)
#endif

/* not available until 1.26 */
#if !defined(UV_THREAD_NO_FLAGS)
#define UV_THREAD_NO_FLAGS 0x00
#endif
#if !defined(UV_THREAD_HAS_STACK_SIZE)
#define UV_THREAD_HAS_STACK_SIZE 0x01
#endif
#if !defined(MAXHOSTNAMELEN)
#define MAXHOSTNAMELEN 255
#endif
#if !defined(UV_MAXHOSTNAMESIZE)
#define UV_MAXHOSTNAMESIZE (MAXHOSTNAMELEN + 1)
#endif
#if !defined(UV_IF_NAMESIZE)
#if defined(IF_NAMESIZE)
#define UV_IF_NAMESIZE (IF_NAMESIZE + 1)
#elif defined(IFNAMSIZ)
#define UV_IF_NAMESIZE (IFNAMSIZ + 1)
#else
#define UV_IF_NAMESIZE (16 + 1)
#endif
#endif
```

# AUTHOR

Chase Whitener <`capoeirab@cpan.org`>

# CONTRIBUTORS

Graham Ollis <`plicease@cpan.org`>

# COPYRIGHT & LICENSE

Copyright (c) 2017 Chase Whitener. All rights reserved.

This program is free software; you can redistribute it and/or modify it
under the same terms as Perl itself.
