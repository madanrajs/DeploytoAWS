az login
az vm run-command invoke -g HomeAffairs-DevOps-PoC -n DevOps-Cloud-RHEL-Agent1 --command-id RunShellScript --scripts 'echo $1 $2' --parameters hello world

# Master
https://dev.azure.com/homeaffairs-devops-poc

# DevOps PAT to add Agent to Master - `DevOps-Cloud-RHEL-Agent1-Token`
2gsoi5v5ouyafsrvxu6db7h26jwsporgfo4oqrdezj4ogxz63vfa

# Github token - `azure-poc-token`
a1bf17ec382ca3926830c61f5a90565b47e16916

# SSH to agent
ssh -i DevOps-Cloud-RHEL-Agent1/.ssh/id_rsa DevOps-Cloud-RHEL-Agent1@devops-cloud-agent1.australiaeast.cloudapp.azure.com
# Download agent
[DevOps-Cloud-RHEL-Agent1@DevOps-Cloud-RHEL-Agent1 ~]$ wget https://vstsagentpackage.azureedge.net/agent/2.160.1/vsts-agent-linux-x64-2.160.1.tar.gz -P /tmp
[DevOps-Cloud-RHEL-Agent1@DevOps-Cloud-RHEL-Agent1 ~]$ mkdir myagent && cd myagent
[DevOps-Cloud-RHEL-Agent1@DevOps-Cloud-RHEL-Agent1 ~]$ tar xf /tmp/vsts-agent-linux-x64-2.160.1.tar.gz
# Configure
[DevOps-Cloud-RHEL-Agent1@DevOps-Cloud-RHEL-Agent1 ~]$ ./config.sh
# Run in foreground
[DevOps-Cloud-RHEL-Agent1@DevOps-Cloud-RHEL-Agent1 myagent]$ sudo ./svc.sh install
[DevOps-Cloud-RHEL-Agent1@DevOps-Cloud-RHEL-Agent1 myagent]$ sudo ./svc.sh start
[DevOps-Cloud-RHEL-Agent1@DevOps-Cloud-RHEL-Agent1 myagent]$ sudo ./svc.sh stop
https://docs.microsoft.com/en-gb/azure/devops/pipelines/agents/v2-linux?view=azure-devops

# Install tools
[DevOps-Cloud-RHEL-Agent1@DevOps-Cloud-RHEL-Agent1 ~]$ sudo yum install git
[DevOps-Cloud-RHEL-Agent1@DevOps-Cloud-RHEL-Agent1 ~]$ sudo yum install java-11-openjdk-devel
[DevOps-Cloud-RHEL-Agent1@DevOps-Cloud-RHEL-Agent1 ~]$ sudo yum install java-1.8.0-openjdk-devel
[DevOps-Cloud-RHEL-Agent1@DevOps-Cloud-RHEL-Agent1 ~]$ sudo alternatives --config java
[DevOps-Cloud-RHEL-Agent1@DevOps-Cloud-RHEL-Agent1 ~]$ wget https://www-us.apache.org/dist/maven/maven-3/3.6.2/binaries/apache-maven-3.6.2-bin.tar.gz -P /tmp
[DevOps-Cloud-RHEL-Agent1@DevOps-Cloud-RHEL-Agent1 ~]$ sudo tar xf /tmp/apache-maven-3.6.2-bin.tar.gz -C /opt/
[DevOps-Cloud-RHEL-Agent1@DevOps-Cloud-RHEL-Agent1 ~]$ sudo ln -s /opt/apache-maven-3.6.2 /opt/maven
[DevOps-Cloud-RHEL-Agent1@DevOps-Cloud-RHEL-Agent1 ~]$ sudo vi /etc/profile.d/maven.sh
[DevOps-Cloud-RHEL-Agent1@DevOps-Cloud-RHEL-Agent1 ~]$ sudo chmod +x /etc/profile.d/maven.sh
[DevOps-Cloud-RHEL-Agent1@DevOps-Cloud-RHEL-Agent1 ~]$ source /etc/profile.d/maven.sh
https://linuxize.com/post/how-to-install-apache-maven-on-centos-7/
https://linuxize.com/post/install-java-on-centos-7/
