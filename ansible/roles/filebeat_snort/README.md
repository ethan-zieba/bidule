Had trouble installing Snort at first, package wasn't located
Updated sources.list to add:
`deb http://http.us.debian.org/debian/ bullseye non-free contrib main`

Check manually for Filebeat and Snort:
```
sudo systemctl status filebeat
sudo systemctl status snort
sudo snort -T -c /etc/snort/snort.conf (Snort test mode)
ping -c 1 127.0.0.1 (trigger a Snort sign)
```
