# Error on pods
```log
Unhandled exception. System.IO.IOException: The configured user limit (128) on the number of inotify instances has been reached, or the per-process limit on the number of open file descriptors has been reached.
```
# Resolution
increase inotify limits:
```sh
# Current value
cat /proc/sys/fs/inotify/max_user_instances
sudo sysctl -w fs.inotify.max_user_instances=1024
echo "fs.inotify.max_user_instances=1024" | sudo tee -a /etc/sysctl.conf
sysctl --system
cat /proc/sys/fs/inotify/max_user_instances
```
