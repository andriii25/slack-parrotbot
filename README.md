# Async ParrotBot
An asynchronous rewrite of CUSF slack tools, now supporting both Slack and Discord.

## Parrotmaker
<pre>
T h e    P a r r o t    G o d s    S p e a k    T o    U s
</pre>

use it with `/parrot message`

![parrotmaker example](parrotmaker_example.gif)

This does not really work in Discord due to the combination 
of the 2000 character message limit and emojis counted by their 
long name + emoji id. 
A 3x3 font could work but it would be practically illegible.

## PONG

Pong was removed as it would have been a bit annoying to reimplement for now.
Something better will come, probably. I think. Maybe not, we'll see.

## RegEx responses

![regex_responses_example](regex_responses_example.png)

Ever needed your bot to chat shit on your behalf when you're asleep?
RegEx responses has got your back, have a look at [example_response.yaml](example_response.yaml) to see how it works
and drop your responses in the directory specified in the main configuratio file.
When multiple option are present one is randomly chosen, and each response has a cooldown
so parrotbot won't spam the server constantly either. 

This only works on Discord because I was lazy to find how to add multiple
on_message listeners in the Slack Bolt API, probably an easy fix.

## Google Drive Auto Upload
Literally the only thing useful about parrotbot. But it's boring so that's why
it's at the bottom.
Works both on Slack and Discord.

## Setting it up

Something like:

```
# cd /opt && git clone https://github.com/smh-my-head/async-parrotbot
# apt install rclone python3-pip
# pip3 install slack_bolt
# mkdir -p /var/opt/async-parrotbot/files
# rclone config
2021/04/26 12:19:08 NOTICE: Config file "/root/.config/rclone/rclone.conf" not found - using defaults
No remotes found - make a new one
n) New remote
s) Set configuration password
q) Quit config
n/s/q> n
name> parrotbot-gdrive
Type of storage to configure.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
.
.
Storage> drive
.
. (defaults)
.
Scope that rclone should use when requesting access from drive.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
.
.
scope> 1
.
. (defaults)
.
Remote config
Use auto config?
 * Say Y if not sure
 * Say N if you are working on a remote or headless machine or Y didn't work
y) Yes
n) No
y/n> n
If your browser doesn't open automatically go to the following link: <snip>
Log in and authorize rclone for access
Enter verification code> <snip>
Configure this as a team drive?
y) Yes
n) No
y/n> n
--------------------
[parrotbot-gdrive]
scope = drive
token = <snip>
--------------------
y) Yes this is OK
e) Edit this remote
d) Delete this remote
y/e/d> y
Current remotes:

Name                 Type
====                 ====
parrotbot-gdrive     drive

e) Edit existing remote
n) New remote
d) Delete remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
e/n/d/r/c/s/q> q

# rclone sync --drive-shared-with-me parrotbot-gdrive:CUSF/slack-staging /var/opt/async-parrotbot/files
# cp async-parrotbot.service /etc/systemd/system/
# systemctl daemon-reload
# systemctl start async-parrotbot
```
