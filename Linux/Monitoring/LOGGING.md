**LOGGING**

<img src="media/image1.png" style="width:4.49327in;height:2.81741in"
alt="Graphical user interface, text, application Description automatically generated" />

<img src="media/image2.png" style="width:3.83306in;height:1.16098in"
alt="Text Description automatically generated" />

\# journalctl -xe

\# mkdir -p /var/log/journald

\# systemctl restart systemd-journald

\# ll /var/log/journald

<img src="media/image3.png" style="width:4.69643in;height:2.67436in"
alt="Graphical user interface, text, application Description automatically generated" />

\# cat /var/log/messages

\# cat /var/log/secure

\# systemctl restart rsyslog

\# systemctl enable rsyslog

\# less –N /etc/logrotate.conf

\# ll /etc/logrotate.d

-------------------------------------------

Rotate Log files

<img src="media/image4.png" style="width:5.86131in;height:1.22111in"
alt="Graphical user interface, application Description automatically generated with medium confidence" />

Rsyslog Facilities

<img src="media/image5.png" style="width:4.775in;height:3.94167in"
alt="Table Description automatically generated" />

Rsyslog all priorities

<img src="media/image6.png" style="width:2.82665in;height:1.93147in"
alt="A picture containing table Description automatically generated" />

Rsyslog forced priority mail.=crit

Rsyslog ignore priority mail.!crit

Rsyslog all priorities mail.\*

Rsyslog property-based filter :msg, contains, “openvpn”

Filter hostname = server1 :hostname, isequal, “server1”

Synced static path cron.\* /var/log/cron.log

Non-synced static path cron.\* -/var/log/cron.log

Dynamic path cron\* ?dynamiccronlog

Template property %msg% %HOSTNAME% %PRI%

Template property with range %msg:1:10%

Template property with option %msg

Remote Log cron messages cron.\* @\<IP\>

Remote Log all messages [\*.\* @\<IP](mailto:*.*@%3cIP)\>

Remote Log all messages via TCP protocol \*.\* @@\<IP\>:\<port\>

\# vi /etc/rsyslog.conf

\# systemctl restart rsyslog

\# firewall-cmd –permanent –add-port=514/tcp

\# firewall-cmd --reload

\# logger “testt”

\# cd /etc/logrotate.d – ll
