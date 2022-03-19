# MSF-screenrecord-on-MacOS
!!! This vulnerability has been simultaneously discovered or taken by Sudhakar Muthumani of Primefort Private Limited, Khiem Tran and listed as CVE-2022-22600. This is despite I already emailing Apple regarding this back in 2021.
## Affected Versions
As a student, I have limited access to devices in which I can test this vulnerability. The versions I have tested so far are `MacOS 12.1`, `MacOS 12.0`, and `MacOS 11.6.1`.

# POC
Files are in the POC directory. Just run 'POC.sh' and a screenshot will be produced without TCC prompt.

## So what is the bug?
As I have stated previously, I am not a professional and have limited knowledge of how MacOS works. However, the most important step of the process mentioned above is deleting the executable. I personally believe that by deleting the executable responsible for the process (meterpreter in this case),  MacOS is unable to check for permissions related to the Screen Recording. I have not tested whether this vulnerability applies to other permissions due to limited capabilities of metasploit-framework. However, the vulnerability does not seem to work when using the `screencapture` command. 
