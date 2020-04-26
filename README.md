PHP Nagios plugin for sending customizable email notifications, with graphs generated by pnp4nagios, displayed as inline messages.
Relies on PHPMailer for sending emails.

## Installation
Process composer dependencies (or manually install PHPMailer):
```
wget -O composer.phar https://getcomposer.org/composer-stable.phar
sudo -u apache php composer.phar install
```

Add nagios commands:
```
define command {
        command_name                    notify-host-by-html-email
        command_line                    $USER1$/php_mail_notif/host-mail.php "$NOTIFICATIONTYPE$" "$HOSTNAME$" "$HOSTALIAS$" "$HOSTSTATE$" "$HOSTADDRESS$" "$HOSTOUTPUT$" "$SHORTDATETIME$" "$CONTACTEMAIL$" "$TOTALHOSTSUP$" "$TOTALHOSTSDOWN$" "$NOTIFICATIONAUTHOR$" "$NOTIFICATIONCOMMENT$" "$LONGDATETIME$" "$HOSTDURATION$" "$HOSTDURATIONSEC$" "$LASTHOSTCHECK$" "$LASTHOSTSTATECHANGE$" "$NOTIFICATIONISESCALATED$" "$HOSTATTEMPT$" "$MAXHOSTATTEMPTS$" "$HOSTPERFDATA$" >> $USER1$/mail.log 2>&1
        register                        1
}

define command {
        command_name                    notify-service-by-html-email
        command_line                    $USER1$/php_mail_notif/service-mail.php "$NOTIFICATIONTYPE$" "$HOSTNAME$" "$HOSTALIAS$" "$HOSTSTATE$" "$HOSTADDRESS$" "$SERVICEOUTPUT$" "$SHORTDATETIME$" "$SERVICEDESC$" "$SERVICESTATE$" "$CONTACTEMAIL$" "$SERVICEDURATIONSEC$" "$SERVICEEXECUTIONTIME$" "$TOTALSERVICESWARNING$" "$TOTALSERVICESCRITICAL$" "$TOTALSERVICESUNKNOWN$" "$NOTIFICATIONRECIPIENTS$" "$TOTALSERVICESOK$" "$SERVICENOTIFICATIONNUMBER$" "$SERVICEACKCOMMENT$" "$HOSTGROUPNAME$" "$SERVICEPERFDATA$" "$SERVICEDURATION$" "$NOTIFICATIONAUTHOR$" "$NOTIFICATIONCOMMENT$" "$LONGDATETIME$" "$HOSTPERFDATA$">> $USER1$/mail.log 2>&1
        register                        1
}
```
