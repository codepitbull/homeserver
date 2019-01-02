Generate a unique app-password
https://support.google.com/mail/answer/185833
The hostname in ssmtp.conf is set accordingly to the name given to the password in the google-form

#hosts file
Add a file named _hosts_ in the root of this repo with the following contents:

```
[nas]
 192.168.2.3
[nas:vars]
mail_user=<user>@gmail.com
mail_password=<app_password>
```

Test with:
ssmtp -vvv <user>@gmail.com
<type stuff and hit ctrl-d>

#run
ansible-playbook site.yml -i hosts --ask-sudo-pass


#ZFS
zpool create -f data raidz1 /dev/sda /dev/sdb /dev/sdc /dev/sdd
zfs create data/syncthing
zfs set quota=500G data/syncthing

zfs set quota=1T data/<USER>
useradd -d /data/<USER> -s /bin/nologin <USER>
chown <USER>.<USER> /data/<USER>


# TimeMachine on Mac
hdiutil create -volname jochen_tm -encryption -stdinpass -size 1000g -type SPARSEBUNDLE -fs "HFS+J" /Volumes/jochen/TimeMachine.sparsebundle

sudo tmutil setdestination /Volumes/jochen_tm

# Syncthing
ssh -L 127.0.0.1:8385:127.0.0.1:8384 <USER>@<synthingmachine>

# Burn

mkdir /mnt/docs_sav

truncate --size=25GB /data/media/docs.udf
mkudffs /data/media/docs.udf
mount -oloop,rw /data/media/docs.udf /mnt/docs_sav
cp -R /data/syncthing/Documents\ Jochen /mnt/docs_sav/
umount /mnt/docs_sav/
