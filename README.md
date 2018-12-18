# Sensu-Go-Pagerduty-Plugin-Quick-Start

This is a quick-start guide to installing the Sensu Go Pagerduty Handler

# Assumptions
1. You already have a Pagerduty account. Signup for one if you do not.
2. You have a working Sensu-Go installation
3. You know how to create sensu handlers

# Installation
The following steps were written and tested on Centos 7. However, it can be easily adapted to other OS.

Log on to your Sensu Server, and execute the following. For simplicity, we will run as root.

1.  Check for the latest version of the sensu-pagerduty-handler from for your platform from 
```
https://github.com/sensu/sensu-pagerduty-handler/releases
```
  
2.  Download the appropriate version for your platform. (Ex. Linux x86)
```
cd /usr/local/src
wget https://github.com/sensu/sensu-pagerduty-handler/releases/download/1.0.1/sensu-pagerduty-handler_1.0.1_linux_386.tar.gz
```
 
3.  Extract the `sensu-pagerduty-handler` from the tar ball
```
tar xvzf sensu-pagerduty-handler_1.0.1_linux_386.tar.gz
```

4.  For this version, the `sensu-pagerduty-handler` is in the `bin` directory. Verify for your platform.
```
[root@host src]# ls -l 
total 3808
drwxr-xr-x. 2 root     root          37 Dec 17 14:38 bin
-rw-rw-r--. 1     2000     2000     699 Dec 12 12:45 CHANGELOG.md
-rw-rw-r--. 1     2000     2000    1062 Dec 12 12:45 LICENSE
-rw-rw-r--. 1     2000     2000    2026 Dec 12 12:45 README.md
-rw-rw-r--. 1     user     user 3884211 Dec 12 12:54 sensu-pagerduty-handler_1.0.1_linux_386.tar.gz
```
```
[root@host src]# ls -l bin
total 10096
-rwxrwxr-x. 1 2000 2000 10337536 Dec 12 12:53 sensu-pagerduty-handler
```

5.	Create a sym-link to the binary in a folder in your path, say `usr/local/sbin`

```
ln -s /usr/local/src/bin/sensu-pagerduty-handler /usr/local/sbin/sensu-pagerduty-handler
```
NOTE: You may also just copy the binary to the folder, or put the full path to the binary in your check command.

6.	Read the help for the plugin

```
sensu-pagerduty-handler -h
```
```
The Sensu Go PagerDuty handler for incident management

Usage:
  sensu-pagerduty-handler [flags]

Flags:
  -h, --help           help for sensu-pagerduty-handler
  -t, --token string   The PagerDuty V2 API authentication token
```

7.  Create Sensu Pagerduty handler and complete your setup
```
sensuctl handler create pagerduty --type pipe --command "sensu-pagerduty-handler --token <your_integration_key>" --timeout 10
```

8.	Create check(s), Ex. using the Nagios `check_ssh` plugin, and set pagerduty as handler
```
sensuctl check create check_ssh --command "check_ssh -4 -p 22 127.0.0.1" --handlers pagerduty --interval 60 --ttl 120 --namespace default
```

See Also:
```
https://github.com/sensu/sensu-pagerduty-handler
```
