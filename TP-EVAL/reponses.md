# TP

<br />

**On ajoute un utilisateur**

    root@debian:~# adduser test
    root@debian:~# passwd test
    root@debian:~# usermod -aG sudo test

<br />

**Utilisation des clés SSH**

    PS C:\Users\sheef> $key = Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"; ssh test@wilfart.fr -p 6221 "mkdir -p ~/.ssh && echo '$key' >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys && chmod 700 ~/.ssh"

<br />

**On desactive la connexion ssh root**

    root@debian:/home# nano /etc/ssh/sshd_config
        PermitRootLogin no

    root@debian:/home# /etc/init.d/ssh restart

<br />

**On change le mot de passe root**

    root@debian:/# passwd

    sd2V6FJ58ybhd1gjdf56mhklg7oc

<br />

**Gestion de log**

    root@debian:/# sudo apt-get install rsyslog

<br />

**Protection contre les attaques brute-force**

    root@debian:/# sudo apt install fail2ban

    root@debian:/# cp /etc/fail2ban/jail.conf  /etc/fail2ban/jail.local

    root@debian:/# systemctl start fail2ban

    root@debian:/# systemctl enable fail2ban

<br />

**On met a jour le tt**

    root@debian:/# apt update -y
    root@debian:/# apt upgrade
    root@debian:/# apt-get update
    root@debian:/# apt-get upgrade

<br />

**System backup** 

    root@debian:/# sudo apt install timeshift

    root@debian:/# nano timeshift.sh
        #!/bin/bash
        timeshift --create --scripted >> /var/log/timeshift_logs_from_cron.txt
        timeshift --list >> /var/log/timeshift_logs_from_cron.txt
        echo "--------------------------------------------------------------------->backupDate=$(date +"%Y-%m-%d")
        snapshotPath="/run/timeshift/backup/timeshift/snapshots/${backupDate}*"
        echo "Snapshot weight : $(du -sh $snapshotPath)" >> /var/log/timeshift_logs>echo "---------------------------------END--------------------------------->

    root@debian:/# chmod u+x timeshift.sh

    root@debian:/# crontab -e
        22 14 * * * /home/user/timeshift.sh

<br />

**On change le mdp de test**

    root@debian:/# passwd test

    T9dr*3bC2n:{,N+By)M59Py5

<br />

**Installation de nginx**

    root@debian:/# sudo apt install nginx

<br />

**On fait le firewall**

    root@debian:/# ufw allow ssh

    root@debian:/# ufw allow 'nginx HTTP'

    root@debian:/# systemctl restart ufw

    root@debian:/# ufw enable

<br />

**On remet a jour le tt**

    root@debian:/# apt update -y
    root@debian:/# apt upgrade
    root@debian:/# apt-get update
    root@debian:/# apt-get upgrade

<br />

**On veut detecter les intrusions**

    root@debian:/run# apt install aide

    root@debian:/# mkdir /etc/aide/aide.conf.d.disabled
    root@debian:/# mv /etc/aide/aide.conf.d/99_* /etc/aide/aide.conf.d.disabled/
    root@debian:/# mv /etc/aide/aide.conf.d/70_* /etc/aide/aide.conf.d.disabled/

    root@debian:/# aide --init --config /etc/aide/aide.conf

    root@debian:/# crontab -u root -e
        0 1 * * * /usr/bin/aide --config /etc/aide/aide.conf --check

    root@debian:/# dpkg -s aide | grep Status

    

