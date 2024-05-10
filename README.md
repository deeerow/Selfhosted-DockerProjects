### Selfhosted-DockerProjects


Should have a logrotate just in case if your logs get to full and unable to write to your docker logs anymore, so it is good practice to have a automatic log rotator cron job, that way you don't need to worry about logs getting to big or filling up your drive space.
```
# place this example code at /etc/logrotate.d/(logname) on your docker host server
# please adjust the custom file path below, where your logs are stored
# please adjust the below traefik container name to send the USR1 signal for log rotation

/var/log/crowdsec/*.log {
  size 10M
  rotate 5
  compress
  missingok
  notifempty
  postrotate
  dateext
  dateformat .%Y-%m-%d
  create 0666 root root
  docker kill --signal="USR1" traefik # adjust this line to your traefik container name
  endscript
}
```
