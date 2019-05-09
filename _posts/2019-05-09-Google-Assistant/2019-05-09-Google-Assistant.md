---
layout: post
title: How To Run Voice Activated Google Assistant on Windows PC
category: Google
tags: [Education, Opioions]
---

<p align="right">Author：Richard</p>

## Run Voice Activated Google Assistant on Windows PC

### Prerequisites

Before going to install Google Assistant on windows pc, you should know a few necessary things and set up a few others.

On your Windows computer you will have to use Command Prompt, and on your macOS, you need Terminal to set up Google Assistant.
You must have Python 3 installed on your system. However, Mac and Linux system come with Python preinstalled. But if you are windows user then you need to install Python 3 on your system.



Table of Contents	
Install Python 3.x On Windows
Let’s check Python is installed or not in your system
Python
How To Install Google Assistant on Windows 10
Step 1: Configure Google Assistant API
Step 2: Install Google Assistant on Windows PC
Step 3: Testing Google Assistant


### Install Python 3 On Windows
1. Open a browser window and navigate to the [Download page for Windows](https://www.python.org/downloads/windows/) at python.org.
2. Underneath the heading at the top that says Python Releases for Windows, click on the link for the Latest Python 3 Release - Python 3.x.x. (As of this writing, the latest is Python 3.6.5.)
3. Scroll to the bottom and select either Windows x86-64 executable installer for 64-bit or Windows x86 executable installer for 32-bit. (See below.)

4. Check Python is installed or not in your system. Open Command Prompt as admin and type the following command and hit the enter button.

![python](1-python.png)

also look: [Python 3 Installation & Setup Guide](https://realpython.com/installing-python/#step-1-download-the-python-3-installer)

### Configure Google Assistant API
First, visit the Google Cloud Platform Console on your Windows computer.

Next, click on the Create Project button.

![project](Google\2-project.png)

In your project page click on __APIs & Services__ then select __Library__. Here search for Google Assistant in the search console. Select Google Assistant API and click on __Enable__ button. At right-hand side __select Credentials__ and click on Create Credential button.

![credentials](/Google/3-credentials.png)

After all of this, download JSON file to your system and save it somewhere you can easily access it.

![download](Google/4-download.png)

### Install Google Assistant on Windows PC
Open Command Prompt as admin and type the following command and hit enter after each one.

```bash
py -m pip install google-assistant-sdk[samples]
pip install -–upgrade google-auth-oauthlib[tool]
```

Above command will download the required dependencies which helps to run Google Cloud project. This process will take little bit of more time based on your internet speed.

Then enter this one:


```bash
google-oauthlib-tool --client-secrets F:\Google\client_secret_965769830407-******.apps.googleusercontent.com.json --scope https://www.googleapis.com/auth/assistant-sdk-prototype --save --headless
```

****** is the route of your json file.



```bash
C:\Users\108>google-oauthlib-tool --client-secrets F:\Google\client_secret_965769830407-******.apps.googleusercontent.com.json --scope https://www.googleapis.com/auth/assistant-sdk-prototype --save --headless


Please visit this URL to authorize this application: https://accounts.google.com
/o/oauth2/auth?re******

Enter the authorization code:
```
Once you run above command you will get URL as result just copy it and past it on your browser.
Select you Google account and you will get authentication code.

### Testing Google Assistant

Turn ON your system Speakers

After you install Google Assistant on your system first you need to check whether or not Assistant able to record audio from microphone.

To test it run the following command in cmd and it will record 10 seconds of audio and play it back to you.

```bash
python -m googlesamples.assistant.audio_helpers
```
or
```bash
googlesamples-assistant-audiotest –record-time 10
```

Eventually, you will get:
```bash
C:\Windows\system32>googlesamples-assistant-audiotest --record-time 10
INFO:root:Starting audio test.
INFO:root:Recording samples.
INFO:root:Finished recording.
INFO:root:Playing back samples.
INFO:root:Finished playback.
INFO:root:audio test completed.
```
## Problems & Next Step:
### Problems
1. Nothing happen in my surface after I entering the authorization code:
```bash
Enter the authorization code:
```
2. Can't go forward to add more function case this error:
```bash
F:\Google>googlesamples-assistant-devicetool register-model --manufacturer “Ass
istant SDK developer” --product-name “Assistant SDK light” --type LIGHT --mod
el Richard --project-id ultra-envoy-240008
Usage: googlesamples-assistant-devicetool [OPTIONS] COMMAND [ARGS]...

Error: Missing option "--project-id".

F:\Google>googlesamples-assistant-pushtotalk --project-id ultra-envoy-240008 --d
evice-model-id Richard
ERROR:root:Error loading credentials: HTTPSConnectionPool(host='oauth2.googleapi
s.com', port=443): Max retries exceeded with url: /token (Caused by NewConnectio
nError('<urllib3.connection.VerifiedHTTPSConnection object at 0x000000000535E9B0
>: Failed to establish a new connection: [WinError 10060] 由于连接方在一段时间后
没有正确答复或连接的主机没有反应，连接尝试失败。'))
ERROR:root:Run google-oauthlib-tool to initialize new OAuth 2.0 credentials.
```

### Next Steps
1. Run on Surface
2. Record my voice
3. Interactive with Google Assistant

## Source
[Google Assistant SDK](https://developers.google.com/assistant/sdk/guides/service/python/embed/run-sample)

[How to Install Google Assistant on Windows 10](https://troubleshooter.xyz/wiki/how-to-install-google-assistant-on-windows-10/)

[How To Run Voice Activated Google Assistant on Windows PC](http://www.techieleaf.net/how-to-run-voice-activated-google-assistant-on-windows-pc/)

[How to get Google Assistant on your Windows, Mac, or Linux Machine](https://www.xda-developers.com/how-to-get-google-assistant-on-your-windows-mac-or-linux-machine/)

