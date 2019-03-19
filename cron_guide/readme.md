# **Guide to cron jobs**

[Section 1: Setup](#setup)

[Section 2: Scheduling](#scheduling)

[Section 3: Useful Commands](#useful-commands)

[Section 4: Practical Examples](#practical-examples)

[Section 5: Resources](#resources)

---

## **Setup:**
#### 1) Open a `bash` terminal
#### 2) Type `crontab -e` to access the editor
#### 3) Type `i` to enter insert mode
#### 4) Enter your cron job in the following format: ` * * * * * command >> action`
- For example, `* * * * * echo 'Hello World' >> /tmp/test.txt` will print 'Hello World' to a text file every minute of every hour of every day.

#### 5) To save your cron job and exit the editor, press `esc` and type `:wq` to save and quit.
- You may have to give permissions to the terminal at this stage.

#### 6) Remove your cron job with `crontab -r`

---

## **Scheduling:**
#### General guide:
    # ┌───────────── minute (0 - 59)
    # │ ┌───────────── hour (0 - 23)
    # │ │ ┌───────────── day of month (1 - 31)
    # │ │ │ ┌───────────── month (1 - 12)
    # │ │ │ │ ┌───────────── day of week (0 - 6) (Sunday to Saturday)
    # │ │ │ │ │                                       
    # │ │ │ │ │
    # │ │ │ │ │
    # * * * * *  command_to_execute

#### Every x periods:
`*/10 * * * *`
- This will run a job once every 10 minutes, indefinitely.

#### Multiple values:
`0 0 1,15 * *`
- This will run at midnight on the 1st and 15th of every month.

#### Range of values:
`0 0-5 * * *`
- This will run on the hour, of the hours between 0-5 of every day, indefinitely.

#### Every x periods & range of values:
`23 0-20/2 * * *`
- This will run at the 23rd minute of every 2nd hour between 0-20, of every day, indefinitely.


---

## **Useful commands:**
#### List all current cron jobs
    crontab -l

#### Access cron editor
    crontab -e

#### Remove all cron jobs
    crontab -r

#### Edit another user's cron job
    crontab -u [USER] -e
    e.g. $ crontab -u user2 -e

#### Check the contents of a file you may have written to
    cat [PATH]
    e.g. $ cat /tmp/test.txt

#### Use crontab on the root account
    sudo crontab -l
    sudo crontab -e

#### Check local domain email (for cron logs)
    cat /var/mail/[username]
    e.g. $ cat /var/mail/johnsmith

#### Write comments in the crontab editor
    # This is a comment

---

## **Practical examples:**

#### Empty temp folder every Friday at 5pm
    0 5 * * 5 em -rf /tmp/*

#### Backup images to Google Drive every night at midnight
    0 0 * * * rsync -a ~/Pictures/ ~/Google\ Drive/Pictures/
    
#### Run a python file through Anaconda, every 10 minutes
    */10 * * * * cd /home/[user]/folder/ && /home/[user]/anaconda3/bin/python ./python_script.py   

---

## **Resources:**

#### Convert english to cron scheduling
https://crontab.guru

#### Monitor cron jobs
https://cronhub.io/
