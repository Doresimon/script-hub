# systemctl

```bash
# systemctl [OPTIONS...] {COMMAND} ...
#   start NAME...                   Start (activate) one or more units
#   stop NAME...                    Stop (deactivate) one or more units
#   reload NAME...                  Reload one or more units
#   restart NAME...                 Start or restart one or more units
#   try-restart NAME...             Restart one or more units if active
#   reload-or-restart NAME...       Reload one or more units if possible,
#                                   otherwise start or restart
#   try-reload-or-restart NAME...   If active, reload one or more units,
#                                   if supported, otherwise restart
#   isolate NAME                    Start one unit and stop all others
#   kill NAME...                    Send signal to processes of a unit
```

## commands

```bash
export SERVICE=xxx
sudo systemctl start $SERVICE
sudo systemctl restart $SERVICE
```
