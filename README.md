# NAME

Alien::libuv - Interface to the libuv library [http://libuv.org](http://libuv.org)

# SYNOPSIS

In your `Makefile.PL`:

    use strict;
    use warnings;

    use ExtUtils::MakeMaker;
    use Config;
    use Alien::libuv;

    WriteMakefile(
      ...
      CONFIGURE_REQUIRES => {
        'Alien::libuv' => '0',
      },
      CCFLAGS => Alien::libuv->cflags . " $Config{ccflags}",
      LIBS    => [ Alien::libuv->libs ],
      ...
    );

# NOTICE

This will not yet work on Windows. However, it should function properly on
linux and unix platforms. We will be working hard to make things behave on
Windows as soon as possible.

# DESCRIPTION

This package can be used by other [CPAN](https://metacpan.org) modules that
require [libuv](http://libuv.org).

# AUTHOR

Chase Whitener <`capoeirab@cpan.org`>

# COPYRIGHT & LICENSE

Copyright (c) 2017 Chase Whitener. All rights reserved.

This program is free software; you can redistribute it and/or modify it
under the same terms as Perl itself.
