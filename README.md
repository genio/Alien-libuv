# Alien::xz [![Build Status](https://secure.travis-ci.org/plicease/Alien-xz.png)](http://travis-ci.org/plicease/Alien-xz)

Find or build xz

# SYNOPSIS

In your Build.PL:

    use Module::Build;
    use Alien::xz;
    my $builder = Module::Build->new(
      ...
      configure_requires => {
        'Alien::xz' => '0',
        ...
      },
      extra_compiler_flags => Alien::xz->cflags,
      extra_linker_flags   => Alien::xz->libs,
      ...
    );
    
    $build->create_build_script;

In your Makefile.PL:

    use ExtUtils::MakeMaker;
    use Config;
    use Alien::xz;
    
    WriteMakefile(
      ...
      CONFIGURE_REQUIRES => {
        'Alien::xz' => '0',
      },
      CCFLAGS => Alien::xz->cflags . " $Config{ccflags}",
      LIBS    => [ Alien::xz->libs ],
      ...
    );

In your script or module:

    use Alien::xz;
    use Env qw( @PATH );
    
    unshift @ENV, Alien::xz->bin_dir;

# DESCRIPTION

This package can be used by other CPAN modules that require xz,
the compression utility, or liblzma, which comes with it.

# HELPERS

## xz

    %{xz}

Returns the name of the xz command.  Usually just `xz`.

# SEE ALSO

[Alien](https://metacpan.org/pod/Alien), [Alien::Base](https://metacpan.org/pod/Alien::Base), [Alien::Build::Manual::AlienUser](https://metacpan.org/pod/Alien::Build::Manual::AlienUser)

# AUTHOR

Graham Ollis <plicease@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2017 by Graham Ollis.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
