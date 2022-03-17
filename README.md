# MSF-screenrecord-on-MacOS
!!! This vulnerability has been simultaneously discovered or taken by Sudhakar Muthumani of Primefort Private Limited, Khiem Tran and listed as CVE-2022-22600. This is despite I already emailing Apple regarding this back in 2021.
## Affected Versions
As a student, I have limited access to devices in which I can test this vulnerability. The versions I have tested so far are `MacOS 12.1`, `MacOS 12.0`, and `MacOS 11.6.1`.

## Pre-requisites
### Server (Remote or local):
I am not a professional and therefore used [metasploit](https://github.com/rapid7/metasploit-framework) to test the vulnerability. `netcat` was also used to receive a reverse shell.

IP must be accessible by the victim
### Victim
- The app
- Internet access
- Firewall off for outgoing connections (Apple's built in firewall is fine but no LuLu ig)

## Details (POC?)
First, the victim downloads an app with shellcode injected. In my case, I used [BDF](https://github.com/secretsquirrel/the-backdoor-factory) to inject the compiled version of [TouchBarDino](https://github.com/yuhuili/TouchBarDino) with `osx/x64/shell_reverse_tcp` generated from [metasploit](https://github.com/rapid7/metasploit-framework). The user downloads the malicious app and opens it.

At this point, I used `netcat` to listen on the tcp port specified in shellcode. Once the connection is established, The [metasploit](https://github.com/rapid7/metasploit-framework) `exploit/multi/script/web_delivery ` module was used with target set to 8 (Mac OS X) and set PAYLOAD `osx/x64/meterpreter_reverse_tcp`, LHOST (IP address) and LPORT (Listening port). 

After running `exploit/multi/script/web_delivery`, copy the resulting command. Make sure that the `netcat` shell is in an accessible directory ($HOME maybe). Then paste the command from metasploit and hit enter.

Once a meterpreter session is open on the server, interact with it and delete the executable downloaded from the command of the previous step. Then when you use the screenshot command from the meterpreter shell, it takes a screenshot without any popups or permissions.

## So what is the bug?
As I have stated previously, I am not a professional and have limited knowledge of how MacOS works. However, the most important step of the process mentioned above is deleting the executable. I personally believe that by deleting the executable responsible for the process (meterpreter in this case),  MacOS is unable to check for permissions related to the Screen Recording. I have not tested whether this vulnerability applies to other permissions due to limited capabilities of metasploit-framework. However, the vulnerability does not seem to work when using the `screencapture` command. 

## When it doesn't work
It doesn't work if LHOST is set to 127.0.0.1
It doesn't work with other metasploit payloads
It doesn't work when using `screencapture` command

