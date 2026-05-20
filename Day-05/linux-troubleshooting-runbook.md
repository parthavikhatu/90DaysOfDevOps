##Command:
uname -a
##output:
Linux ip-172-31-32-12 7.0.0-1004-aws #4-Ubuntu SMP PREEMPT Mon Apr 13 13:14:24 UTC 2026 x86_64 GNU/Linux


##Command:
cat /etc/os-release

##output:
ubuntu@ip-172-31-32-12:~$ cat /etc/os-release
PRETTY_NAME="Ubuntu 26.04 LTS"
NAME="Ubuntu"
VERSION_ID="26.04"
VERSION="26.04 (Resolute Raccoon)"
VERSION_CODENAME=resolute
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=resolute
LOGO=ubuntu-logo

Observation
Kernel and architecture verified successfully.


##Command:
mkdir /tmp/runbook-demo
cp /etc/hosts /tmp/runbook-demo/hosts-copy
ls -l /tmp/runbook-demo

##output:
ubuntu@ip-172-31-32-12:~$ mkdir /tmp/runbook-demo
ubuntu@ip-172-31-32-12:~$ cp /etc/hosts /tmp/runbook-demo/hosts-copy
ubuntu@ip-172-31-32-12:~$ ls -l /tmp/runbook-demo
total 4
-rw-r--r-- 1 ubuntu ubuntu 221 May 20 16:10 hosts-copy

Observation
Temporary troubleshooting directory created successfully.

##Command:
top
##output:
top - 16:16:48 up 15 min,  1 user,  load average: 0.00, 0.00, 0.01
Tasks: 112 total,   1 running, 111 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.2 sy,  0.0 ni, 99.8 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st 
MiB Mem :    908.7 total,    298.4 free,    306.9 used,    412.8 buff/cache     
MiB Swap:      0.0 total,      0.0 free,      0.0 used.    601.8 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                                                                                           
   1725 ubuntu    20   0   10984   5728   3600 R   0.3   0.6   0:00.03 top                                                                                               
      1 root      20   0   25308  16036  10972 S   0.0   1.7   0:01.65 systemd                                                                                           
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.00 kthreadd                                                                                          
      3 root      20   0       0      0      0 S   0.0   0.0   0:00.00 pool_workqueue_release                                                                            
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-rcu_gp  


##Command:
ps -o pid,pcpu,pmem,comm -p 722

##output:
ubuntu@ip-172-31-32-12:~$ ps -o pid,pcpu,pmem,comm -p 947
    PID %CPU %MEM COMMAND
    947  0.0  1.2 sshd-session


##Command:
free -h
##output:
ubuntu@ip-172-31-32-12:~$ free -h
               total        used        free      shared  buff/cache   available
Mem:           908Mi       304Mi       300Mi       2.7Mi       412Mi       603Mi
Swap:             0B          0B          0B

Observation
CPU usage remained low and system load was stable.
SSH service is consuming minimal CPU and memory.
Enough free memory available; no swap pressure observed.

##Command:
df -h
##output:
ubuntu@ip-172-31-32-12:~$ df -h
Filesystem       Size  Used Avail Use% Mounted on
/dev/root        6.7G  2.1G  4.6G  32% /
tmpfs            455M     0  455M   0% /dev/shm
tmpfs            182M  888K  181M   1% /run
efivarfs         128K  3.3K  120K   3% /sys/firmware/efi/efivars
tmpfs            455M  4.0K  455M   1% /tmp
none             1.0M     0  1.0M   0% /run/credentials/systemd-journald.service
none             1.0M     0  1.0M   0% /run/credentials/systemd-resolved.service
/dev/nvme0n1p13  989M   96M  826M  11% /boot
/dev/nvme0n1p15  105M  6.3M   99M   7% /boot/efi
none             1.0M     0  1.0M   0% /run/credentials/systemd-networkd.service
none             1.0M     0  1.0M   0% /run/credentials/getty@tty1.service
none             1.0M     0  1.0M   0% /run/credentials/serial-getty@ttyS0.service
tmpfs             91M  8.0K   91M   1% /run/user/1000


##Command:
vmstat 1 5
##output:
ubuntu@ip-172-31-32-12:~$ vmstat 1 5
procs -----------memory---------- ---swap-- -----io---- -system-- -------cpu-------
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st gu
 0  0      0 307448  17648 405164    0    0   235    77   89    0  0  0 99  0  0  0
 0  0      0 307448  17648 405204    0    0     0     0   76   51  0  0 100  0  0  0
 0  0      0 307448  17648 405204    0    0     0     0   80   65  0  0 100  0  0  0
 0  0      0 307448  17648 405204    0    0     0     0   60   51  0  0 100  0  0  0
 0  0      0 307448  17648 405204    0    0     0     0   66   51  0  0 100  0  0  0

Observation:
Disk usage below 80%; no filesystem critically full.

##Command:
ss -tulpn
##output:
ubuntu@ip-172-31-32-12:~$ ss -tulpn
Netid           State            Recv-Q           Send-Q                          Local Address:Port                       Peer Address:Port           Process           
udp             UNCONN           0                0                                   127.0.0.1:323                             0.0.0.0:*                                
udp             UNCONN           0                0                                  127.0.0.54:53                              0.0.0.0:*                                
udp             UNCONN           0                0                               127.0.0.53%lo:53                              0.0.0.0:*                                
udp             UNCONN           0                0                           172.31.32.12%ens5:68                              0.0.0.0:*                                
udp             UNCONN           0                0                                       [::1]:323                                [::]:*                                
tcp             LISTEN           0                4096                               127.0.0.54:53                              0.0.0.0:*                                
tcp             LISTEN           0                4096                            127.0.0.53%lo:53                              0.0.0.0:*                                
tcp             LISTEN           0                4096                                  0.0.0.0:22                              0.0.0.0:*                                
tcp             LISTEN           0                4096                                     [::]:22                                 [::]:*                                
ubuntu@ip-172-31-32-12:~$ 
Observation:
No critical errors found in recent SSH logs.

##Command:
Ping google.com
##output:
PING google.com (142.251.38.110) 56(84) bytes of data.
64 bytes from lcarna-ac-in-f14.1e100.net (142.251.38.110): icmp_seq=1 ttl=119 time=3.23 ms
64 bytes from lcarna-ac-in-f14.1e100.net (142.251.38.110): icmp_seq=2 ttl=119 time=3.25 ms
64 bytes from lcarna-ac-in-f14.1e100.net (142.251.38.110): icmp_seq=3 ttl=119 time=3.33 ms
64 bytes from lcarna-ac-in-f14.1e100.net (142.251.38.110): icmp_seq=4 ttl=119 time=3.27 ms
64 bytes from lcarna-ac-in-f14.1e100.net (142.251.38.110): icmp_seq=5 ttl=119 time=3.25 ms
64 bytes from lcarna-ac-in-f14.1e100.net (142.251.38.110): icmp_seq=6 ttl=119 time=3.25 ms
64 bytes from lcarna-ac-in-f14.1e100.net (142.251.38.110): icmp_seq=7 ttl=119 time=3.28 ms


##Command:
journalctl -u ssh -n 50
##output:
ubuntu@ip-172-31-32-12:~$ journalctl -u ssh -n 50
May 20 06:00:14 ip-172-31-32-12 systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
May 20 06:00:14 ip-172-31-32-12 sshd[1015]: Server listening on 0.0.0.0 port 22.
May 20 06:00:14 ip-172-31-32-12 sshd[1015]: Server listening on :: port 22.
May 20 06:00:14 ip-172-31-32-12 systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
May 20 06:01:30 ip-172-31-32-12 ec2-instance-connect[1254]: Querying EC2 Instance Connect keys for matching fingerprint: SHA256:koYxhfOcDrUccUMH7SXi1QZMHPkhv5/G2PULbpjX>
May 20 06:01:30 ip-172-31-32-12 ec2-instance-connect[1286]: Providing ssh key from EC2 Instance Connect with fingerprint: SHA256:koYxhfOcDrUccUMH7SXi1QZMHPkhv5/G2PULbpj>
May 20 06:01:30 ip-172-31-32-12 ec2-instance-connect[1403]: Querying EC2 Instance Connect keys for matching fingerprint: SHA256:koYxhfOcDrUccUMH7SXi1QZMHPkhv5/G2PULbpjX>
May 20 06:01:31 ip-172-31-32-12 sshd-session[1145]: Accepted publickey for ubuntu from 13.48.4.203 port 8276 ssh2: ED25519 SHA256:koYxhfOcDrUccUMH7SXi1QZMHPkhv5/G2PULbp>
May 20 06:01:31 ip-172-31-32-12 sshd-session[1145]: pam_unix(sshd:session): session opened for user ubuntu(uid=1000) by ubuntu(uid=0)
May 20 07:15:28 ip-172-31-32-12 systemd[1]: Stopping ssh.service - OpenBSD Secure Shell server...
May 20 07:15:28 ip-172-31-32-12 sshd[1015]: Received signal 15; terminating.


##command:
tail -n 50 /var/log/auth.log
##output:
 ubuntu@ip-172-31-32-12:~$ tail -n 50 /var/log/auth.log
2026-05-20T06:17:01.079968+00:00 ip-172-31-32-12 CRON[1701]: pam_unix(cron:session): session closed for user root
2026-05-20T06:25:01.086092+00:00 ip-172-31-32-12 CRON[1787]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
2026-05-20T06:25:01.100420+00:00 ip-172-31-32-12 CRON[1787]: pam_unix(cron:session): session closed for user root
2026-05-20T06:30:59.258937+00:00 ip-172-31-32-12 unix_chkpwd[1891]: password check failed for user (ubuntu)
2026-05-20T06:30:59.259461+00:00 ip-172-31-32-12 polkit-agent-helper-1[1889]: pam_unix(polkit-1:auth): authentication failure; logname= uid=0 euid=0 tty= ruser=ubuntu rhost=  user=ubuntu
2026-05-20T06:31:01.226355+00:00 ip-172-31-32-12 polkitd[662]: Operator of unix-process:1879:184825 FAILED to authenticate to gain authorization for action org.freedesktop.systemd1.manage-units for system-bus-name::1.22 [systemctl stop ssh] (owned by unix-user:ubuntu)
