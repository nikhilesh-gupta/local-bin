#!/usr/bin/perl -wT
# CGI script for listing the IP addresses contained in a CIDR netblock.
# Written by Rayner Lucas, March 2005.

BEGIN {
    my $base_module_dir = (-d '/home/magiccoo/perl' ? '/home/magiccoo/perl' : ( getpwuid($>) )[7] . '/perl/');
    unshift @INC, map { $base_module_dir . $_ } @INC;
}

use CGI;
use CGI::Carp qw(warningsToBrowser fatalsToBrowser);
use Net::CIDR qw(:all);
use strict;

my $cgi = new CGI;

my $w = $cgi->param('ipw');
my $x = $cgi->param('ipx');
my $y = $cgi->param('ipy');
my $z = $cgi->param('ipz');
my $mask = $cgi->param('mask');
my $submit;

print $cgi->header;
print $cgi->start_html;

# Argument checking:
my $validate_fail = 0;
foreach my $octet ($w, $x, $y, $z) {
    if (($octet !~ /^\d+$/) || ($octet < 0) || ($octet > 255)) {
        $validate_fail = 1;
    }
}

if ($mask !~ /^\d+$/) {
    $validate_fail = 1;
}

# If the things that are meant to be numbers weren't numbers, complain.
if ($validate_fail) {
    print "Invalid address or netmask.<br><br>";
    print "<a href=\"../iplist.html\">Try again</a>";
    print $cgi->end_html;
    exit;
}

# Check that the address is valid.
if (!cidrvalidate("$w.$x.$y.$z")) {
    print "Address specified was not valid.<br><br>";
    print "<a href=\"../iplist.html\">Try again</a>";
    print $cgi->end_html;
    exit;
}

# Check netmask is within the limits of server resources and
# mathematical possibility.
if ($mask < 16 || $mask > 32) {
    print "Netmask must be a value from 16 to 32.";
    print "<a href=\"../iplist.html\">Try again</a>";
    print $cgi->end_html;
    exit;
}

# Right, lets get to work.
my $num = 2**(32 - $mask);
print "$num addresses<br><br>";

my @cidr_list = ("$w.$x.$y.$z/$mask");
my @range_list = cidr2range(@cidr_list);
print "IP address range: ";
print $range_list[0];
print "<br><br>";

# Find the starting address in the netblock and store it in $w, $x, $y, $z.
my @addresses = split(/\-/, $range_list[0]);
my @octets = split(/\./, $addresses[0]);
$w = $octets[0];
$x = $octets[1];
$y = $octets[2];
$z = $octets[3];

# Count up through the addresses and print each one.
for (my $count = 2**(32 - $mask); $count > 0; $count--) {
    # If the other error checks work properly, this error should never happen.
    if ($w > 255) {
        print "Invalid address/mask specified: leftmost octet would be greater than 255.";
        print $cgi->end_html;
        exit;
    }
    print "$w.$x.$y.$z<br>";
    $z++;
    if ($z > 255) {
        $y++;
        $z = 0;
    }
    if ($y > 255) {
        $x++;
        $y = 0;
    }
    if ($x > 255) {
        $w++;
        $x = 0;
    }
}

print $cgi->end_html;
exit;
