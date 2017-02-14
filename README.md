## Setup
* Follow [Supervisord’s installation instructions](http://supervisord.org/installing.html).
* Place the `laravel_queue.conf` file in your `/etc/supervisord.conf` directory
* Run `$BINDIR/supervisord` to boot up supervisord. You may need to have root privileges. 
* Run `$BINDIR/supervisorctl` to open the supervisord shell console. You may need to have root privileges.
* Add the queue workers by running `add queue` in the supervisord shell.

## Options
* `program`: The name of your program. If you modify this, you will need to run `add $NEW_PROGRAM_NAME`instead of `add queue` in the supervisorctl shell in the setup step.
* `command`: You can use any queue options supported by Laravel here. Commone ones are `tries` to retry failed jobs before aborting and `timeout`to allow long-running jobs to finish before timing out.
* `directory`: set this to the root directory of your Laravel project
* `stdout_logfile`: the path and filename where you want your log file to be stored. A reasonable place might be `/$PATH_TO_YOUR_PROJECT/storage/logs/supervisor.log`
* `redirect_stderr`: a `true` value specifies that you want the terminal output to be logged to the log file.
* `numprocs`: the number of worker instances you wish to run. The more workers, the more concurrent jobs can be handled.
* `process_name`: if you set `numprocs` to a value greater than 1, you will need to give each worker instance a unique process name. The default `%(program_name)s_%(process_num)02d` value will assign unique names automatically

## Tips
* If you make modifications to a configuration file, run `reread $PROGRAM_NAME` in the supervisorctl shell to pull in the changes.
