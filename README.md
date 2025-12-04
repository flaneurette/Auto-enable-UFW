# Auto-enable-UFW
Installs and enables UFW if uninstalled or disabled.

# Issue and why.

Some Linux packages can **silently** uninstall UFW because they conflict with it or are not compatible. For example, the package `netfilter-persistent` can remove UFW during installation, leaving your system without an active firewall!
See UFW bug report that I filed: https://bugs.launchpad.net/ubuntu/+source/ufw/+bug/2133823

To prevent this, check_ufw.sh is a Bash script that:

Checks every 5 minutes if the UFW firewall is running.

- If UFW is missing, installs it.

- If UFW is installed but inactive, enables it.

- Only sends an email notification to the site owner if something fails or UFW had to be installed/enabled.

You can customize the email address directly in the script.

# Install

`sudo apt install mailutils`

`sudo touch /usr/local/bin/check_ufw.sh`

`sudo nano /usr/local/bin/check_ufw.sh`

paste the check_ufw.sh script

`Ctrl+O`

`Ctrl+X`

`sudo chmod +x /usr/local/bin/check_ufw.sh`

`sudo crontab -e`

Paste at the end:

`*/5 * * * * /usr/local/bin/check_ufw.sh`
