# whiterabbit-backup-email
```sh
$ vim backup-email.py

import tarfile
import smtplib
import ssl

volumes = [ "wordpress_db-data" , "wordpress_wp-data" ]

for volume in volumes:

  src = "/var/lib/docker/volumes/{}/_data/".format(volume)
  archive = "{}.tar.gz".format(volume)
  tar = tarfile.open(archive,'w')
  tar.add(src)
  tar.close()
  



port = 465 
smtp_server = "smtp.gmail.com"
sender_email = "sender@gmail.com"  
receiver_email = "receiver@gmail.com"  
password = input("Type your password and press enter: ")
message = """\
Subject: Hi there

Script Executed."""

context = ssl.create_default_context()
with smtplib.SMTP_SSL(smtp_server, port, context=context) as server:
  server.login(sender_email, password)
  server.sendmail(sender_email, receiver_email, message)

```
