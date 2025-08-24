# Abuse Bot

The Abuse Bot is a bot that monitors all of free infrastructure, and their resource usage, in order to detect abuse within these servers.
This is to ensure the experience is smooth, and satisfying to other users.

## What are some triggers to Abuse Bot?
The main triggers publicly visible are as follows:

- Average of over 15% vCPU for 60 seconds
- Average of over 500MB/minute Inbound network
- Average of over 500MB/minute Outbound network
- Suspicious Internet requests
- High (undefined) RAM usage

In addition to these resource limits, Abuse Bot also blocks Selfbots, Roblox PinCrackers, and more.

## What happens if Abuse Bot 'targets' my Server?

It will first send a `SIGINT` (Singal Interrupt) to your Server, which is the same signal you can invoke with CTRL+C in your terminal.
This asks the Server to stop nicely, and can prevent data from being lost, if the Application on the Server has a catch block that catches this.

If that `SIGINT` doesn't work, Abuse Bot will send a `SIGKILL` (Signal Kill) to the Server.
This will immediately terminate the process, potentially causing data loss, as this signal cannot be caught, ignored, or blocked.

This will cause these exit codes:
`130 = SIGINT`
`137 = SIGKILL`

## What to do if Abuse Bot keeps stopping my server?

Firstly, identify what you're doing that causes Abuse Bot to flag your Server.
Let's assume you're using too much CPU, this could be for various reasons, heavy image / video processing, continuously writing data into a big JSON, or whatever.

To stop Abuse Bot from shutting down your Server, optimize these actions within your code (if possible), to consume less Processing Power, if your case is the big JSON, you should switch to a proper Database, like SQLite or MongoDB.

If it is not possible to optimize it, all you could really do is purchase a Premium Server, as those are not monitored by Abuse Bot and do not have any 'hidden limits'.