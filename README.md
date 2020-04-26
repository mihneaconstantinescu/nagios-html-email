PHP Nagios plugin for sending customizable email notifications, with graphs generated by pnp4nagios, displayed as inline messages.
Relies on PHPMailer for sending emails.

Nagios usage:
```
define command {
        command_name                    notify-host-by-html-email
        command_line                    $USER1$/php_mail_notif/host-mail.php "$NOTIFICATIONTYPE$" "$HOSTNAME$" "$HOSTALIAS$" "$HOSTSTATE$" "$HOSTADDRESS$" "$HOSTOUTPUT$" "$SHORTDATETIME$" "$CONTACTEMAIL$" "$TOTALHOSTSUP$" "$TOTALHOSTSDOWN$" "$NOTIFICATIONAUTHOR$" "$NOTIFICATIONCOMMENT$" "$LONGDATETIME$" "$HOSTDURATION$" "$HOSTDURATIONSEC$" "$LASTHOSTCHECK$" "$LASTHOSTSTATECHANGE$" "$NOTIFICATIONISESCALATED$" "$HOSTATTEMPT$" "$MAXHOSTATTEMPTS$" "$HOSTPERFDATA$" >> $USER1$/mail.log 2>&1
        register                        1
}

define command {
        command_name                    notify-service-by-email
        command_line                    /usr/bin/printf "%b" "***** Nagios *****\n\nNotification Type: $NOTIFICATIONTYPE$\n\nService: $SERVICEDESC$\nHost: $HOSTALIAS$\nAddress: $HOSTADDRESS$\nState: $SERVICESTATE$\n\nDate/Time: $LONGDATETIME$\n\nAdditional Info:\n\n$SERVICEOUTPUT$\n" | /usr/bin/mail -s "** $NOTIFICATIONTYPE$ Service Alert: $HOSTALIAS$/$SERVICEDESC$ is $SERVICESTATE$ **" $CONTACTEMAIL$
        register                        1
}
```
