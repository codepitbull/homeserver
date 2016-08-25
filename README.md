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
