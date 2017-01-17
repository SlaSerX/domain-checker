# Program: Domain Expiration Check <domain-check>
#
# Author: Matty < matty91 at gmail dot com >
#
# Current Version: 1.5
#
# Revision History:
#
#  Version 1.5
#    Updated the license to allow redistribution and modification
#
#  Version 1.4
#    Updated the documentation.
#
#  Version 1.3
#    Gracefully Handle the case where the expiration data is unavailable
#
#  Version 1.2
#    Added "-s" option to allow arbitrary registrars
#
#  Version 1.1
#    Fixed issue with 'e' getopt string -- Pedro Alves
#
#  Version 1.0
#    Initial Release
#
# Last Updated: 09-03-2007
#
# Purpose:
#  domain-check checks to see if a domain has expired. domain-check
#  can be run in interactive and batch mode, and provides faciltities 
#  to alarm if a domain is about to expire.
#
# License:
#  Copyright (C) 2007 Matty <matty91 at gmail dot com>
#  This program is free software; you can redistribute it and/or modify
#  it under the terms of the GNU General Public License as published by
#  the Free Software Foundation; either version 2 of the License, or
#  (at your option) any later version.
#
#  This program is distributed in the hope that it will be useful,
#  but WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
#  GNU General Public License for more details.
#
# Notes:
#   Since each registrar provides expiration data in a unique format (if
#   they provide it at all), domain-check is currently only able to
#   processess expiration information for a subset of the available
#   registrars.
#
# Requirements:
#   Requires whois
#
# Installation:
#   Copy the shell script to a suitable location
#
# Tested platforms:
#  -- Solaris 9 using /bin/bash
#  -- Solaris 10 using /bin/bash
#  -- OS X 10.4.2 using /bin/sh
#  -- OpenBSD using /bin/sh
#  -- FreeBSD using /bin/sh
#  -- Redhat advanced server 3.0MU3 using /bin/sh
#
# Usage:
#  Refer to the usage() sub-routine, or invoke domain-check
#  with the "-h" option.
#
# Example:
#
#  The first example will print the expiration date and registrar for prefetch.net:
#
#  $ domain-check.sh -d prefetch.net
#
#  Domain                              Registrar         Status   Expires     Days Left
#  ----------------------------------- ----------------- -------- ----------- ---------
#  prefetch.net                        INTERCOSMOS MEDIA Valid    13-feb-2006   64   
#
#  The second example prints the expiration date and registrar for the domains 
#  listed in the file "domains":
#
#  $ domain-check.sh -f domains    
#
#  Domain                              Registrar         Status   Expires     Days Left
#  ----------------------------------- ----------------- -------- ----------- ---------
#  sun.com                             NETWORK SOLUTIONS Valid    20-mar-2010   1560 
#  google.com                          EMARKMONITOR INC. Valid    14-sep-2011   2103 
#  ack.com                             NETWORK SOLUTIONS Valid    09-may-2008   880  
#  prefetch.net                        INTERCOSMOS MEDIA Valid    13-feb-2006   64   
#  spotch.com                          GANDI             Valid    03-dec-2006   357  
#
#  The third example will e-mail the address admin@prefetch.net with the domains that
#  will expire in 60-days or less:
#
#  $ domain-check -a -f domains -q -x 60 -e admin@prefetch.net  
#
