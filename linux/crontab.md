# Crontab Overview

`crontab` stands for "cron table" and is a configuration file that specifies shell commands to run periodically on a schedule. The `cron` daemon is responsible for executing these scheduled commands. The name "cron" comes from the Greek word "chronos", meaning time.

Each user on a Unix-based system can have their own crontab file, which allows them to schedule jobs without requiring system-level privileges.

## Understanding Crontab Entries

A crontab file consists of lines of six fields each. The fields are separated by spaces or tabs:

```shell
* * * * * /path/to/command
- - - - -
| | | | |
| | | | +---- Day of the week (0 - 6) [Both 0 and 7 represent Sunday]
| | | +------ Month (1 - 12)
| | +-------- Day of the month (1 - 31)
| +---------- Hour (0 - 23)
+------------ Minute (0 - 59)
```

## Checking if `cron` is running

The methods to check if `cron` is running can vary depending on the system you're using. Here are a couple of common methods:

1. **Using the `ps` command**:

    You can check if the `cron` daemon is running using the `ps` command:

    ```shell
    ps aux | grep cron
    ```

    If `cron` is running, you should see an output that includes a line for the `cron` process.

</br>

1. **Using the `systemctl` command** (for systems using `systemd`):

    ```shell
    systemctl status cron.service
    ```

    The output will tell you if the service is active (running) or inactive (not running).

    </br>

2. **Using the `service` command** (for older systems or those not using `systemd`):

    ```shell
    service cron status
    ```

Again, the output will indicate whether `cron` is running or not. </br>

If `cron` is not running, you can typically start it with:

-   `systemctl start cron.service` (for `systemd` systems)
-   `service cron start` (for non-`systemd` systems)

In my opinion, understanding and using `crontab` is an essential skill for anyone administering or working extensively on Unix-based systems. It offers powerful scheduling capabilities, but with that power comes the responsibility to ensure tasks are configured correctly to avoid potential issues.

## Add new cron job

**Open Crontab file**

```shell
crontab -e
```

**Insert path to file (bash script)**

```shell
*/3 * * * * /home/ec2-user/indulge-api/check_logs_and_restart.sh
```

Ex: `check_logs_and_restart.sh`:

```shell
#!/bin/bash

# Name of the app to check
APP_NAME="indulge"

# Check the last 20 lines of the logs for the specified strings
if pm2 logs $APP_NAME --lines 20 | grep -qE "Timeout|timeout|undefined|Undefined"; then
    # If any of the strings are found, restart the app
    pm2 restart $APP_NAME
fi
```

**Check crontab content**

```shell
crontab -e
```

**Check if running**

```shell
ps aux | grep cron
```
