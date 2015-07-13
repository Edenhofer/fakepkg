=encoding utf8

=head1 NAME

fakepkg - reassemble Arch Linux packages 

=head1 SYNOPSIS

Usage: I<pacaur> E<lt>operationE<gt> [ options ] [ target(s) ]

=head1 DESCRIPTION

Pacman usually stores all downloaded packages in its package cache to enable the user to downgrade each and every package. However if the package cache was removed either by accident or by purpose to e.g. save disk space, it may be usefull to recrete the cache at a later point. The obvious choice would be to download all those packages again. However this is actually redundant since all files and folders from the packages should reside on your system. That is where fakepkg comes in handy. Its purpose is to recreate any given package as long as it is installed on your system. This probably saves you a lot of bandwith and time in comparison to building the package from source or downloading it from third parties.

B<Warning:> The files from your system are taken as they are, hence any modifications done to them by you or your system will be present in the assembled package. Distributing the recreated package is therefore discouraged. See ABS and Arch Rollback Machine for alternatives.

This might be seen as either downside or benefit.

B<Note:> Certain files and folders may only be read by root. Though fakepkg will warn you in those cases, consider running it as root.

=head1 EXAMPLES

To reassemble e.g. gzip and binutils, use the following command.

    fakepkg gzip binutils

You may as well specify a destination folder:

    fakepkg -o /var/cache/pacman/pkg tar xz

Recreating multiple packages at once with only one thread can take some time. This can be sped up by utilizing multiple jobs, in this case 4.

    fakepkg -j 4 linux slurm-llnl virtualbox qemu

Alternatively it may also make sense to set the tar environment variable for multi core compression. Hereby tar uses all the CPU power hence starting multiple jobs brings no performance gain.

    XZ_OPT="-T 0" fakepkg $(pacman -Qsq)

=head1 AUTHOR

Gordian Edenhofer

=head1 LICENSE

Unless otherwise stated, the files in this project may be distributed under the terms of the GNU General Public License as published by the Free Software Foundation; either version 2 of the License, or any later version. This work is distributed in the hope that it will be useful, but without any warranty; without even the implied warranty of merchantability or fitness for a particular purpose. See [version 2](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html) and [version 3] (https://www.gnu.org/copyleft/gpl-3.0.html) of the GNU General Public License for more details.
