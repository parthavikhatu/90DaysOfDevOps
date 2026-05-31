DevOps Incident Summary
1. Disk Full
Scenario: Server storage reaches 100%.
 Steps: Check disk usage → Find large files/logs → Clean old files → Verify free space.
 Commands: df -h, du -sh, rm, find

2. Service Down
Scenario: Application or web server stops.
 Steps: Check service status → Review logs → Restart service → Verify access.
 Commands: systemctl status, journalctl, systemctl restart

3. High CPU Usage
Scenario: Server becomes slow.
 Steps: Find high CPU process → Investigate → Stop/fix process.
 Commands: top, htop, ps aux, kill

4. High Memory Usage
Scenario: Application crashes or hangs.
 Steps: Check memory → Identify process → Restart service → Investigate memory leak.
 Commands: free -h, top, vmstat

5. SSH Access Failure
Scenario: Cannot connect to server.
 Steps: Check network → Verify SSH service → Check firewall/security rules → Validate SSH keys.
 Commands: ping, ssh, systemctl status sshd

6. Website Not Accessible
Scenario: Users cannot open website.
 Steps: Check web server → Check application → Verify ports → Review logs.
 Commands: curl, systemctl, ss, netstat

7. DNS Issue
Scenario: Domain name not resolving.
 Steps: Check DNS records → Verify nameservers → Test propagation.
 Commands: nslookup, dig, host

8. Jenkins Build Failure
Scenario: CI/CD pipeline fails.
 Steps: Check console logs → Identify failed stage → Fix code/config → Re-run build.
 Commands: git status, git pull

9. Docker Container Crash
Scenario: Container stops unexpectedly.
 Steps: Check container status → View logs → Fix issue → Restart container.
 Commands: docker ps, docker logs, docker restart

10. Database Connection Failure
Scenario: Application cannot connect to database.
 Steps: Check DB service → Verify connectivity → Check credentials → Restart if needed.
 Commands: mysql, telnet, nc, systemctl

11. Kubernetes Pod CrashLoopBackOff
Scenario: Pod keeps restarting.
 Steps: Check pod logs → Review events → Fix application/config issue → Redeploy.
 Commands: kubectl get pods, kubectl logs, kubectl describe

12. Kubernetes Node Not Ready
Scenario: Node unavailable.
 Steps: Check node status → Verify kubelet → Restart services.
 Commands: kubectl get nodes, kubectl describe node

13. Deployment Failure
Scenario: New release breaks application.
 Steps: Check deployment → Rollback → Verify service.
 Commands: kubectl rollout history, kubectl rollout undo

14. EC2 Instance Unreachable
Scenario: Cannot access AWS server.
 Steps: Check instance health → Verify Security Groups/NACLs → Verify SSH.
 Commands: aws ec2 describe-instances

15. Load Balancer Health Check Failure
Scenario: Traffic not reaching application.
 Steps: Check health endpoint → Verify target health → Fix configuration.
 Commands: curl, aws elbv2 describe-target-health

16. RDS Database Down
Scenario: Database unavailable.
 Steps: Check RDS status → Verify network → Failover/restore.
 Commands: aws rds describe-db-instances

17. Application Outage
Scenario: Application unavailable.
 Steps: Check web server → App → Database → Infrastructure → Restore service.
 Commands: curl, systemctl, docker, kubectl

18. Data Loss
Scenario: Important data deleted.
 Steps: Stop changes → Restore backup → Validate data.
 Commands: Backup/restore tools

19. Security Breach
Scenario: Unauthorized access detected.
 Steps: Isolate system → Rotate credentials → Review logs → Patch vulnerability.
 Commands: journalctl, auditctl, last, who

20. Complete Production Outage
Scenario: Entire system down.
 Steps: Check Network → DNS → Load Balancer → Web Server → App → Database → Kubernetes/Cloud → Restore service.
 Commands: ping, curl, systemctl, docker, kubectl, aws

