# Cloudwatch
## Collectd
### What is it
- collectd is a popular open-source solution with plugins that can gather system statistics for a wide variety of applications
- is supported only on Linux servers
- use the collectd software to send the metrics to the CloudWatch agent. For the collectd metrics, the CloudWatch agent acts as the server while the collectd plugin acts as the client
### How to send data to cloudwatch using collectd
- Install collectd in server
- Add collectd section in cwagent configuration file
### How to send result of checkpoint to cloudwatch using collectd
- Using collectd.conf file 