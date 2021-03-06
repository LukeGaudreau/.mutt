## Run offlineimap by cron with gnome-keyring

`pullmail.sh` should be used to pull mail in cron. It will lookup for file named `~/.dbus/session-bus/$machine_id-$display_number` where
`$machine_id` is located in `/var/lib/dbus/machine-id` and `$display_number` is most of the time 0.

There is option to suppress warnings in script. Useful to debug script in cron (I use mailing cron output).
Also you can redirect all output (using `command-in-cron.sh >>/path/to/file.log 2>&1`) from cron.

## msmtp queue

By default mutt is configured to store all outgoing emails in queue.

To send emails you should add following line to your crontab:

```
*/5 * * * * /usr/bin/msmtp-runqueue.sh >>$HOME/.msmtpqueue.log 2>&1
```

## Timeout

Sometimes offlineimap can freeze due to suspend/hibernate for example.
For this case it can be useful to use timeout command.
Just add command to cron like that:

```
# Terminate task after 10 minutes
*/10 * * * * timeout 600 $HOME/.mutt/cron/pullmail.sh >>$HOME/.offlineimap/cron.log 2>&1
```
