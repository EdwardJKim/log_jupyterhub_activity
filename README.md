# log jupyterhub user activity

Create an API token for an admin user of the Hub:

    export JPY_API_TOKEN=`jupyterhub token [admin_user]`

Run the script:

    ./log_activity

This fills a simple sqlite database (`activity.sqlite` by default) periodically with a bool value for whether each user has been seen since the last check.
The table has the form:

    date (utc) | username (str) | active (bool)

The default interval is ten minutes. It should be larger than the Hub's own activity update interval,
which is five minutes.

```
usage: log_activity [-h] [-f FILE] [--interval INTERVAL] [--hub HUB]

optional arguments:
  -h, --help            show this help message and exit
  -f FILE, --file FILE  The sqlite file where activity should be logged.
  --interval INTERVAL   The interval, in seconds, for polling activity. Should
                        be greater than Hub activity interval (5 minutes).
  --hub HUB             The hub's url. If no protocol is specified, http will
                        be assumed.
```