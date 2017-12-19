# Build instructions for usage within Adfinis SyGroup

These build instructions define how we want to "build" check_hpasm
resulting in a identical use and expectations on requirements and behaviour.


```
autoreconf -v
./configure \
 --prefix=$PWD/build \
 --with-perl=/usr/bin/perl \
 --with-nagios-user=nagios \
 --with-nagios-group=nagios \
 --with-degrees=celsius
make
make install
```

Afterwards check_hpasm will be located in `./build/libexec`.

Post-build cleanup:
```
git clean -d -f
git reset --hard
```

# Details on options choice

We first target Debian- and RHEL-based distributions first therefore
inheriting some of the choices and assumptions made there.

## --prefix=$PWD/build

This is only setting the location of check_hpasm for make install and make
certain it doesn't get put somewhere under /usr/local.

## --with-perl=/usr/bin/perl

Debian- and RHEL-based distributions always have their packaged Perl 5.x available in this location.

## --with-nagios-user=nagios

Most Debian- and RHEL-based distributions assume nagios as the user of the distiribution packages.
Currently this parameter isn't actually making anything as 'install' isn't called with the defined option.

## --with-nagios-group=nagios

Most Debian- and RHEL-based distributions assume nagios as the group of the distribution packages.
Currently this parameter isn't actually making anything as 'install' isn't called with the defined option.

## --with-degrees=celsius

We always want to output in degree Celsius.
