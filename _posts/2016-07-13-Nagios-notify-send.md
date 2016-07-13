---
layout: post
title: "Nagios notifications Using notify-send"
date: 2016-07-13 15:33:37
categories: nagios
---

I use Nagios to monitor our group workstations.
The Nagios server runs on my desktop, and I can the status of all the machines via a web-page served locally.
By default, Nagios can send notifications for status changes via email, but this requires running a mail server, and who has time for that.
What I'd like to do is to use `libnotify` to send a small pop-up notification.
`notify-send` is very simple to use:

    notify-send "Message title" "Message body"
    
However, there's a small snag: nagios runs as its own user, you can't use `notify-send` to send messages to other users, even on the same computer.
There are various solutions for sending yourself messages from scripts running under `cron`, but I've not found a robust solution to sending another user on the same machine a notification.
They all involve grabbing, or saving, the dbus information necessary to use `notify-send`.
Unfortunately, that dbus information is (at least on my system) viewable only by the user in question.

Well, the trick is to combine the solutions for the `cron` scripts with `sudo`.
Here is the script I use to grab the dbus info and send a notification:

    #!/bin/bash
    PATH=/usr/local/bin:/usr/bin:/bin:/usr/X11R6/bin
    export DISPLAY=:0
    export $(grep -z DBUS_SESSION_BUS_ADDRESS /proc/$(pgrep kwin)/environ )
    /usr/bin/notify-send "$1" "$2"

I then set a rule in the `sudoers` file to enable nagios to run this script as me:

    nagios ALL=(<username>) NOPASSWD: SETENV: /path/to/script
    
Then in `/usr/local/nagios/etc/objects/commands.cfg` add:

    # 'notify-host-by-notify' command definition
    define command{
    	command_name	notify-host-by-notify
    	command_line	sudo -u <username> /path/to/script "Nagios: $NOTIFICATIONTYPE$ Service Alert: $HOSTALIAS$/$SERVICEDESC$ is $SERVICESTATE$" "Host: $HOSTNAME$\nState: $HOSTSTATE$\nAddress: $HOSTADDRESS$\nInfo: $HOSTOUTPUT$\n\nDate/Time: $LONGDATETIME$\n"
    	}

    # 'notify-service-by-notify' command definition
    define command{
    	command_name	notify-service-by-notify
    	command_line	sudo -u <username> /path/to/script "Nagios $NOTIFICATIONTYPE$ Service Alert: $HOSTALIAS$/$SERVICEDESC$ is $SERVICESTATE$" "Service: $SERVICEDESC$\nHost: $HOSTALIAS$\nAddress: $HOSTADDRESS$\nState: $SERVICESTATE$\n\nDate/Time: $LONGDATETIME$\n\nAdditional Info:\n\n$SERVICEOUTPUT$\n"
    	}
        
Finally, I changed the `generic-contact` template in `/usr/local/nagios/etc/objects/templates.cfg` to use the two notify commands instead of the default `notify-X-by-email`.


