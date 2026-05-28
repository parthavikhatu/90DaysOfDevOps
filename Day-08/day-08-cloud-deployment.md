
## Commands Used

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
sudo systemctl status nginx
sudo cat /var/log/nginx/access.log
sudo cp /var/log/nginx/access.log ~/nginx-logs.txt
scp -i day08-key.pem ubuntu@<your-ip>:~/nginx-logs.txt .
```

## Challenges Faced

- SSH permission denied issue solved using chmod 400
- Nginx not accessible until port 80 was allowed in security group
- Learned how to manage services using systemctl

## What I Learned

- How to launch EC2 instance
- How to connect Linux server using SSH
- How to install and manage Docker and Nginx
- How to configure security groups
- How to extract logs from Linux server


## Why This Matters for DevOps

This task helped me understand:

- Cloud server provisioning
- Remote server management
- Service deployment
- Log management
- Linux administration
- Security group configuration
