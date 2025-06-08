### 14-without-exit-status.sh
The main disadvantage in shell scripting is we need to check every line through exit status, so to set exit automatically, we need to give "set -e" Here "e = automatically exit", mostly this wont work in the shellscript, so we dont use this method. Because if you take example of "id roboshop" and if you run the script for the first time, then id roboshop will be failed because there is no roboshop user exists for the first time, so if you set -e, it wont work.

- Instead of giving &>LOGFILE everywhere, we can give "exec &>LOGFILE" under logfile name. See in redis.sh
- To check the logs "sudo less /var/log/messages" in this logs, we can check wether the remote connections are
  successfully connected (or) not.
- unzip -o /tmp/web.zip ----> Here "o" is to overwrite, if you run the script multiple times.

### Roboshop shellscript in VS
- Mongodb ---> t3.small
- Catalogue ---> t2.micro
- Redis ---> t2.micro 
- User ---> t2.micro
- Cart ---> t2.micro
- Web ---> t2.micro
- Mysql ---> t3.small
- Shipping ---> t3.small
- RabbitMq ---> t2.micro
- Payment ---> t2.micro
- Dispatch ---> t2.micro

### Points to remember
- Even after changing anything in the configuration and if it is still not reflecting then you need to restart
  "systemctl restart"
- Make sure to add all internal servers (private) in the web cofiguration in the last step and make sure to
  restart after changing the configuration using "systemctl restart nginx" command.
- Dont forget to give public_IP of web instance in records to your domain.
- To check the logs "sudo less /var/log/messages" in this logs, we can check wether the remote connections are
  successfully connected (or) not.
