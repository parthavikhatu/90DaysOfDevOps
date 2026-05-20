# Linux Practice Notes-Day-04
## Process Checks
## Command-1
ps aux | head
## Command Result:

root           1  0.2  1.7  25196 16004 ?        Ss   06:00   0:02 /sbin/init
root           2  0.0  0.0      0     0 ?        S    06:00   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        S    06:00   0:00 [pool_workqueue_release]
root           4  0.0  0.0      0     0 ?        I<   06:00   0:00 [kworker/R-rcu_gp]
root           5  0.0  0.0      0     0 ?        I<   06:00   0:00 [kworker/R-sync_wq]
root           6  0.0  0.0      0     0 ?        I<   06:00   0:00 [kworker/R-kvfree_rcu_reclaim]
root           7  0.0  0.0      0     0 ?        I<   06:00   0:00 [kworker/R-slub_flushwq]
root           8  0.0  0.0      0     0 ?        I<   06:00   0:00 [kworker/R-netns]
root          10  0.0  0.0      0     0 ?        I<   06:00   0:00 [kworker/0:0H-kblockd]

## Command-2    
top
## Command Result:
top - 06:21:38 up 21 min,  1 user,  load average: 0.00, 0.00, 0.00
Tasks: 114 total,   1 running, 113 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st 
MiB Mem :    908.7 total,    380.9 free,    304.7 used,    332.6 buff/cache     
MiB Swap:      0.0 total,      0.0 free,      0.0 used.    604.0 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                                                                                                  
   1737 ubuntu    20   0   10984   5784   3656 R   0.3   0.6   0:00.03 top                                                                                                      
      1 root      20   0   25196  16004  10916 S   0.0   1.7   0:02.46 systemd                                                                                                  
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.00 kthreadd                                                                                                 
      3 root      20   0       0      0      0 S   0.0   0.0   0:00.00 pool_workqueue_release                                                                                   
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-rcu_gp                                                                                         
      5 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-sync_wq                                                                                        
      6 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-kvfree_rcu_reclaim                                                                             
      7 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-slub_flushwq                                                                                   
      8 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-netns                                                                                          
     10 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/0:0H-kblockd


## Command-3    
systemctl status ssh
## Command Result:
Check Service Status-ssh
 ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: enabled)
    Drop-In: /usr/lib/systemd/system/ssh.service.d
             └─ec2-instance-connect.conf
     Active: active (running) since Wed 2026-05-20 06:00:14 UTC; 22min ago
 Invocation: df37663904a4414cad8647b621aad15e
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 1015 (sshd)
      Tasks: 1 (limit: 627)
     Memory: 7.5M (peak: 14.8M)
        CPU: 1.076s
     CGroup: /system.slice/ssh.service


## Command-4    
systemctl list-units --type=service --state=running
## Command Result:
ubuntu@ip-172-31-32-12:~$ systemctl list-units --type=service --state=running
  UNIT                                           LOAD   ACTIVE SUB     DESCRIPTION                                                   
  acpid.service                                  loaded active running ACPI event daemon
  chrony.service                                 loaded active running chrony, an NTP client/server
  cron.service                                   loaded active running Regular background program processing daemon
  dbus.service                                   loaded active running D-Bus System Message Bus
  getty@tty1.service                             loaded active running Getty on tty1
  irqbalance.service                             loaded active running irqbalance daemon
  ModemManager.service                           loaded active running Modem Manager
  multipathd.service                             loaded active running Device-Mapper Multipath Device Controller
  networkd-dispatcher.service                    loaded active running Dispatcher daemon for systemd-networkd
  polkit.service                                 loaded active running Authorization Manager
  rsyslog.service                                loaded active running System Logging Service

## Command-5      
journalctl -u ssh --no-pager | tail -n 20
## Command Result:
ubuntu@ip-172-31-32-12:~$ journalctl -u ssh --no-pager | tail -n 20
May 20 06:00:14 ip-172-31-32-12 systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
May 20 06:00:14 ip-172-31-32-12 sshd[1015]: Server listening on 0.0.0.0 port 22.
May 20 06:00:14 ip-172-31-32-12 sshd[1015]: Server listening on :: port 22.
May 20 06:00:14 ip-172-31-32-12 systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
May 20 06:01:30 ip-172-31-32-12 ec2-instance-connect[1254]: Querying EC2 Instance Connect keys for matching fingerprint: SHA256:koYxhfOcDrUccUMH7SXi1QZMHPkhv5/G2PULbpjXwQA
May 20 06:01:30 ip-172-31-32-12 ec2-instance-connect[1286]: Providing ssh key from EC2 Instance Connect with fingerprint: SHA256:koYxhfOcDrUccUMH7SXi1QZMHPkhv5/G2PULbpjXwQA, request-id: cce99629-a82d-43a9-b62e-a77c19da19c1, for IAM principal: arn:aws:iam::769369611777:user/parthavi
May 20 06:01:30 ip-172-31-32-12 ec2-instance-connect[1403]: Querying EC2 Instance Connect keys for matching fingerprint: SHA256:koYxhfOcDrUccUMH7SXi1QZMHPkhv5/G2PULbpjXwQA
May 20 06:01:31 ip-172-31-32-12 sshd-session[1145]: Accepted publickey for ubuntu from 13.48.4.203 port 8276 ssh2: ED25519 SHA256:koYxhfOcDrUccUMH7SXi1QZMHPkhv5/G2PULbpjXwQA
May 20 06:01:31 ip-172-31-32-12 sshd-session[1145]: pam_unix(sshd:session): session opened for user ubuntu(uid=1000) by ubuntu(uid=0)
## Command-6      
tail -n 50 /var/log/syslog
## Command Result:
ubuntu@ip-172-31-32-12:~$ tail -n 50 /var/log/syslog
2026-05-20T06:05:15.735968+00:00 ip-172-31-32-12 dbus-daemon[650]: [system] Activating via systemd: service name='org.freedesktop.timedate1' unit='dbus-org.freedesktop.timedate1.service' requested by ':1.11' (uid=0 pid=666 comm="/usr/lib/snapd/snapd" label="unconfined")
2026-05-20T06:05:15.741915+00:00 ip-172-31-32-12 systemd[1]: Starting systemd-timedated.service - Time & Date Service...
2026-05-20T06:05:15.787920+00:00 ip-172-31-32-12 systemd[1]: Started systemd-timedated.service - Time & Date Service.
2026-05-20T06:05:15.788748+00:00 ip-172-31-32-12 dbus-daemon[650]: [system] Successfully activated service 'org.freedesktop.timedate1'
2026-05-20T06:05:45.822498+00:00 ip-172-31-32-12 systemd[1]: systemd-timedated.service: Deactivated successfully.
2026-05-20T06:07:24.879370+00:00 ip-172-31-32-12 systemd[1448]: launchpadlib-cache-clean.service - Clean up old files in the Launchpadlib cache skipped, unmet condition check ConditionPathExists=/home/ubuntu/.launchpadlib/api.launchpad.net/cache
2026-05-20T06:10:13.976883+00:00 ip-172-31-32-12 systemd[1]: Starting sysstat-collect.service - system activity accounting tool...
2026-05-20T06:10:14.002771+00:00 ip-172-31-32-12 systemd[1]: sysstat-collect.service: Deactivated successfully.
2026-05-20T06:10:14.003038+00:00 ip-172-31-32-12 systemd[1]: Finished sysstat-collect.service - system activity accounting tool.
2026-05-20T06:15:04.881265+00:00 ip-172-31-32-12 systemd[1]: Starting systemd-tmpfiles-clean.service - Cleanup of Temporary Directories...
2026-05-20T06:15:04.988891+00:00 ip-172-31-32-12 systemd[1]: systemd-tmpfiles-clean.service: Deactivated successfully.
2026-05-20T06:15:04.989170+00:00 ip-172-31-32-12 systemd[1]: Finished systemd-tmpfiles-clean.service - Cleanup of Temporary Directories.
2026-05-20T06:17:01.079902+00:00 ip-172-31-32-12 CRON[1703]: (root) CMD (cd / && run-parts --report /etc/cron.hourly)
2026-05-20T06:20:13.976534+00:00 ip-172-31-32-12 systemd[1]: Starting sysstat-collect.service - system activity accounting tool...
2026-05-20T06:20:13.997880+00:00 ip-172-31-32-12 systemd[1]: sysstat-collect.service: Deactivated successfully.


## Mini Troubleshooting Steps

### Problem
SSH service was not running.

### Troubleshooting Steps

Checked service status:
```bash
systemctl status ssh
```

Started the service:
```bash
sudo systemctl start ssh
```

Verified again:
```bash
systemctl status ssh
```

### Result
Service became active and running.
 ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: enabled)
    Drop-In: /usr/lib/systemd/system/ssh.service.d
             └─ec2-instance-connect.conf
     Active: active (running) since Wed 2026-05-20 06:00:14 UTC; 22min ago
 Invocation: df37663904a4414cad8647b621aad15e
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 1015 (sshd)
      Tasks: 1 (limit: 627)
     Memory: 7.5M (peak: 14.8M)
        CPU: 1.076s
     CGroup: /system.slice/ssh.service
