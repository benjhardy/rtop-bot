
# rtop-bot

[![Join the chat at https://gitter.im/rapidloop/rtop-bot](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/rapidloop/rtop-bot?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

*rtop-bot* is a bot front-end to *rtop*.

*rtop* can connect over SSH to Linux systems and display their vital system
metrics without needing any agent on the target system. *rtop-bot* can do
this when asked to, over HipChat or Slack. *rtop-bot* is independent of *rtop*.

*rtop-bot* is self-hosted. You can run it on a machine within your
secure network from which it can SSH to target systems. When run, it will
connect to Slack as a bot (or to a HipChat room as the user you specify), and
listen for mentions:

    you     | @rtop-bot status some.host
    rtop-bot| [some.host] up 34d 20h 1m 51s, load 0.08 0.03 0.05, procs 1 running of 131 total
    rtop-bot| [some.host] mem: 45.55 MiB of 489.57 MiB free, swap 0 bytes of 0 bytes free
    rtop-bot| [some.host] fs /: 16.18 GiB of 18.55 GiB free

*rtop-bot*'s [home page](http://www.rtop-monitor.org/rtop-bot) has more
information and screenshots!

## build

*rtop-bot* is written in [go](http://golang.org/), and requires Go version 1.2
or higher. To build, *go get* it:

    go get github.com/rapidloop/rtop-bot

You should find the binary *rtop-bot* under *$GOPATH/bin* when the command
completes. There are no runtime dependencies or configuration needed.

## setup

Once *rtop-bot* has been built, getting it running in a slack workspace can be done as follows.

1) There is currently an issue with the main branch rapidloop/rtop-bot in which rtop-bot does not work if the server to be queried is password-protected. rtop-bot will only work if the server the query is coming from can ssh into the server to be queried in a single line- in other words, no passwords. As a workaround solution, the user can follow the instructions http://linuxproblem.org/art_9.html. *Only recommended if security can be maintained.*
2) Create a slack bot in your workspace. We recommend using the existing Slack Bots app as a building block.
3) In the command line, navigate to the folder in which the binaries for rtop-bot are built. There, run ./rtop-bot -s <API-token-here>. The API token for your specific bot can be found on the Edit Configuration tab under the Integration Settings header.
4) Add the bot to a channel.
5) Type @mybot: status <server>

## contribute

Pull requests welcome. Keep it simple.

## changelog
* 12-Aug-2019: 0.2.1 hipchat support removed and fix ssh connection! [HostKeyCallback non-permissive by default](https://github.com/golang/go/issues/19767)
* 4-Sep-2015: 0.2 - Slack support added
* 11-Aug-2015: 0.1 - first public release
