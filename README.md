[![Actions Status](https://github.com/lizmat/User-pwent/workflows/test/badge.svg)](https://github.com/lizmat/User-pwent/actions)

NAME
====

Raku port of Perl's User::pwent module

SYNOPSIS
========

    use User::pwent;
    $pw = getpwnam('daemon')       || die "No daemon user";
    if $pw.uid == 1 && $pw.dir ~~ m/ ^ '/' [bin|tmp]? $ / {
        print "gid 1 on root dir";
    }
     
    $real_shell = $pw.shell || '/bin/sh';
     
    use User::pwent qw(:FIELDS);
    getpwnam('daemon')             || die "No daemon user";
    if $pw_uid == 1 && $pw_dir ~~ m/ ^ '/' [bin|tmp]? $ / {
        print "gid 1 on root dir";
    }
     
    $pw = getpw($whoever);

DESCRIPTION
===========

This module tries to mimic the behaviour of Perl's `User::pwent` module as closely as possible in the Raku Programming Language.

This module's exports `getpwent`, `getpwuid`, and `getpwnam` functions that return `User::pwent` objects. This object has methods that return the similarly named structure field name from the C's passwd structure from pwd.h, stripped of their leading "pw_" parts, namely name, passwd, uid, gid, change, age, quota, comment, class, gecos, dir, shell, and expire.

You may also import all the structure fields directly into your namespace as regular variables using the :FIELDS import tag. Access these fields as variables named with a preceding pw_ in front their method names. Thus, $passwd_obj.shell corresponds to $pw_shell if you import the fields.

The `getpw` function is a simple front-end that forwards a numeric argument to `getpwuid` and the rest to `getpwnam`.

PORTING CAVEATS
===============

Not possible to port pw_has
---------------------------

The `pw_has` function has not been ported because there's currently no way to find the needed information in the Raku equivalent of `Config`.

Probably not on Windows
-----------------------

This module depends on the availability of POSIX semantics. This is generally not available on Windows, so this module will probably not work on Windows.

AUTHOR
======

Elizabeth Mattijsen <liz@raku.rocks>

Source can be located at: https://github.com/lizmat/User-pwent . Comments and Pull Requests are welcome.

COPYRIGHT AND LICENSE
=====================

Copyright 2018, 2019, 2020, 2021 Elizabeth Mattijsen

Re-imagined from Perl as part of the CPAN Butterfly Plan.

This library is free software; you can redistribute it and/or modify it under the Artistic License 2.0.

