# silverblue-config
My Fedora silverblue configuration
# Prerequisite
1. Turn off selinux
```
# Set to permissive for this session
setenforce 0
# Set to permissive permanently
sudo sed -i 's/SELINUX=enforcing/SELINUX=permissive/' /etc/selinux/config 
# TODO: Fix SELinux for docker and set to enforce permanently
# sudo sed -i 's/SELINUX=permissive/SELINUX=/enforcing' /etc/selinux/config 
```
2. Install docker
```
rpm-ostree install moby-engine docker-compose
```
3. Add user to docker group
```
echo "$(getent group docker)" >> /etc/group
usermod -aG docker myusername
```
4. Install VSCode
```
sudo cat <<EOT >> /etc/yum.repos.d
name=Visual Studio Code
baseurl=https://packages.microsoft.com/yumrepos/vscode
enabled=1
gpgcheck=1
gpgkey=https://packages.microsoft.com/keys/microsoft.asc
EOT
rpm-ostree install code
```
4. Install VSCode remote container extension
5. Clone this repo into volume
6. Authorized your own SSH key to the host machine
7. Copy age keys
```
vi ~/.config/sops/age/keys.txt
chmod 600 ~/.config/sops/age/keys.txt
```
8. Run ansible
```
ansible-playbook main.yaml
```
# Software
## KDE Phone Connector
1. Overlay openssl
2. Install [GSConnector](https://extensions.gnome.org/extension/1319/gsconnect/)
# Installing Chromium with vaapi support
1. Add rpm-fusion repository
```
rpm-ostree install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
```
2. Install chromium with non-free extension for video playback
```
rpm-ostree install chromium-freeworld
```
This chromium has no google chrome sync without workaround however