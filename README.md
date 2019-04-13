# mintslash-ansible

## Comparision to other popular automation tools on the market

[Comparison #1](https://www.edureka.co/blog/chef-vs-puppet-vs-ansible-vs-saltstack/)  
[Comparison #2](https://www.reddit.com/r/linuxadmin/comments/9ljveg/puppet_vs_salt_vs_chef_vs_ansible_which_to_choose/)  
[Comparison #3](https://gist.github.com/jaceklaskowski/bd3d06489ec004af6ed9)  
[Comparison #4](https://www.quora.com/Which-should-I-choose-Chef-Puppet-Ansible-SaltStack-Docker-or-something-else-if-I%E2%80%99m-looking-to-lead-an-effort-to-improve-automation-in-the-infrastructure-of-a-global-agency-with-dozens-of-simultaneous-client-specific-projects)  
[Comparison #5](https://www.linkedin.com/pulse/very-short-comparison-ansible-chef-puppet-saltstack-niels-goossens)

## Setting up windows host for remote management

Just run ConfigureRemotingForAnsible.ps1 script as an Administrator on a computer you'd like to be managed by Ansible.  
[Please check this page for more information](https://docs.ansible.com/ansible/latest/user_guide/windows_setup.html#setting-up-a-windows-host)

Download and run the setup script at once in a PowerShell terminal window (as Administrator):

```text
$url = "https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1"
$file = "$env:temp\ConfigureRemotingForAnsible.ps1"

(New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)

powershell.exe -ExecutionPolicy ByPass -File $file
```

## Ansible Galaxy

[Web page](https://galaxy.ansible.com/)  
[Documentation](https://galaxy.ansible.com/docs/)

Initialise new role:

```text
ansible-galaxy init tomcat-8.5.27
```

## Example ad-hoc commands (Linux remote host)

Execute first to add a remote host fingerprint to the known_hosts file:

```text
ssh automation@192.168.56.100
```

Gather all facts from a host given by an IP address:

```text
ansible all -i 192.168.56.100, -m setup -u automation -k
```

Gather all facts from a host given by a hostname:

```text
ansible all -i hostname.domain.com, -m setup -u automation -k
```

## Example playbooks

Linux:

```text
- hosts: tomcat:tomcat-8.5.27:&linux
  gather_facts: true
  become: yes
  roles:
    - role: linux/tomcat-8.5.27
```

Windows:

```text
- hosts: tomcat:tomcat-8.5.27:&windows
  gather_facts: true
  become: yes
  roles:
    - role: windows/tomcat-8.5.27
```

## Example inventories

Linux:

```text
[linux]
192.168.56.100 ansible_user=automation ansible_password=password ansible_become_pass=password

[tomcat]
192.168.56.100 tomcat_http_port=8080 tomcat_https_port=8443

[tomcat-8.5.23]
192.168.1.1 tomcat_http_port=8080 tomcat_https_port=8443
```

```text
[linux]
hostanme.domain.com ansible_user=automation ansible_password=password ansible_become_pass=password

[tomcat]
hostanme.domain.com tomcat_http_port=8080 tomcat_https_port=8443

[tomcat-8.5.23]
hostanme.domain.com tomcat_http_port=8080 tomcat_https_port=8443
```

Windows:

```text
[windows:vars]
ansible_connection=winrm
ansible_winrm_transport=ntlm
ansible_winrm_server_cert_validation=ignore

[windows]
192.168.56.200 ansible_user=Administrator ansible_password=P@ssw0rd

[tomcat]
192.168.56.200 tomcat_http_port=8080 tomcat_https_port=8443

[tomcat-8.5.23]
192.168.56.200 tomcat_http_port=8080 tomcat_https_port=8443
```

```text
[windows:vars]
ansible_connection=winrm
ansible_winrm_transport=ntlm
ansible_winrm_server_cert_validation=ignore

[windows]
hostanme.domain.com ansible_user=Administrator ansible_password=P@ssw0rd

[tomcat]
hostanme.domain.com tomcat_http_port=8080 tomcat_https_port=8443

[tomcat-8.5.23]
hostanme.domain.com tomcat_http_port=8080 tomcat_https_port=8443
```

## Running Ansible palybook

```text
ansible-playbook -i inventory playbook
```
