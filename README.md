<p align="center">
  <img src="https://user-images.githubusercontent.com/23141800/121086278-a1291c00-c7eb-11eb-92dd-b2a0d75d97b5.png" alt="banner" />
</p>

**WeaponizeKali.sh** is a Bash script aimed at automating the process of downloading and installing extra tools for internal penetration tests with Kali Linux.

Basic principles behind this project are:

1. Use bleeding-edge versions of offensive toolkits to possess their latest features and fixes.
2. When installing 3rd party software, use isolated environments to minimize potential dependency hell.
3. Keep Windows exploitation scripts and binaries on hand in case you find yourself in an "offline situation".

The script will create two directories within CWD: `tools` and `www`. The [first](#tools) one contains all the tools that will be installed on Kali. The [second](#www) one contains all the scripts and binaries that will be downloaded and may be delivered onto the victim host later.

## Usage

WeaponizeKali.sh heavily relies on Python virtual environments and uses [pipx](https://pipxproject.github.io/pipx/) and [poetry](https://python-poetry.org/) to orchestra venvs.

In order to launch the bleeding-edge version of a tool installed with pipx and not the version that is already shipped with Kali, you should modify the `PATH` variables:

1. Modify `PATH` for a normal user with any method you want (`.bashrc` / `.profile` / `.zshrc` / etc.): `export PATH="$HOME/.local/bin:$PATH"`.
2. Modify `PATH` for the superuser by modifying `secure_path` within sudoers (`sudo visudo`):

![sudoers](https://user-images.githubusercontent.com/23141800/103461896-b5e02000-4d32-11eb-936e-6764ceae1372.png)

Now you can download WeaponizeKali.sh and run it from your home directory (pip may prompt for unlocking the keyring during the process). When it's done, you can check the results in `~/tools` and `~/www`:

```console
~$ cd
~$ curl -sL https://github.com/penetrarnya-tm/WeaponizeKali.sh/raw/main/WeaponizeKali.sh | bash -s -- -idtw
~$ ls -la tools www
```

:warning: **Warning:** when using the `-i` switch, existing `./tools` and `./www` directories will be deleted.

If you only want to get the deliverable scripts and binaries (i.e., `www` directory), you can do it like this:

```console
~$ mkdir www
~$ curl -sL https://github.com/penetrarnya-tm/WeaponizeKali.sh/raw/main/WeaponizeKali.sh | bash -s -- -w
~$ ls -la www
```

It's recommended to run WeaponizeKali.sh **once** on a clean installation of Kali Linux.

### Rerun the Installations

To execute WeaponizeKali.sh with full set of arguments again after it has already been ran once, remove the existent virtual environments first and then run the script:

```console
~$ cd
~$ rm -rf ~/.local/pipx
~$ ./WeaponizeKali.sh -idtw
```

### Help

```
~$ ./WeaponizeKali.sh -h
                                                         )
 (  (                                                  ( /(       (                )
 )\))(   '   (     )                    (         (    )\())   )  )\ (          ( /(
((_)()\ )   ))\ ( /(  `  )    (    (    )\  (    ))\  ((_)\ ( /( ((_))\     (   )\())
_(())\_)() /((_))(_)) /(/(    )\   )\ )((_) )\  /((_) _ ((_))(_)) _ ((_)    )\ ((_)\
\ \((_)/ /(_)) ((_)_ ((_)_\  ((_) _(_/( (_)((_)(_))  | |/ /((_)_ | | (_)   ((_)| |(_
 \ \/\/ / / -_)/ _` || '_ \)/ _ \| ' \))| ||_ // -_) | ' < / _` || | | | _ (_-<| ' \
  \_/\_/  \___|\__,_|| .__/ \___/|_||_| |_|/__|\___| |_|\_\\__,_||_| |_|(_)/__/|_||_|
                     |_|
                           "the more tools you install, the more you are able to PWN"
                    { https://github.com/penetrarnya-tm/WeaponizeKali.sh } { vX.Y.Z }

usage: WeaponizeKali.sh [-h] [-i] [-d] [-t] [w]

optional arguments:
  -h                    show this help message and exit
  -i                    initialize filesystem (re-create ./tools and ./www directories)
  -d                    resolve dependencies
  -t                    download and install tools on Kali Linux
  -w                    download scripts and binaries for delivering onto the victim host
```

## Available Tools

### `tools`

* [x] [Amsi-Bypass-Powershell](https://github.com/S3cur3Th1sSh1t/Amsi-Bypass-Powershell/blob/master/README.md)
* [x] [BloodHound.py](https://github.com/fox-it/BloodHound.py)
* [x] [BloodHound](https://github.com/BloodHoundAD/BloodHound/releases)
* [x] [CVE-2019-1040-scanner](https://github.com/fox-it/cve-2019-1040-scanner)
* [x] [CVE-2020-1472-checker](https://github.com/SecuraBV/CVE-2020-1472)
* [x] [CrackMapExec](https://github.com/byt3bl33d3r/CrackMapExec)
* [x] [Creds](https://github.com/S3cur3Th1sSh1t/Creds)
* [x] [DivideAndScan](https://github.com/snovvcrash/DivideAndScan)
* [x] [DLLsForHackers](https://github.com/Mr-Un1k0d3r/DLLsForHackers)
* [x] [Ebowla](https://github.com/Genetic-Malware/Ebowla)
* [x] [Empire](https://github.com/BC-SECURITY/Empire)
* [x] [ItWasAllADream](https://github.com/byt3bl33d3r/ItWasAllADream)
* [x] [LDAPPER](https://github.com/shellster/LDAPPER)
* [x] [MS17-010](https://github.com/helviojunior/MS17-010)
* [x] [MeterPwrShell](https://github.com/GetRektBoy724/MeterPwrShell/releases)
* [x] [Neo-reGeorg](https://github.com/L-codes/Neo-reGeorg)
* [x] [Nim](https://nim-lang.org/install_unix.html) · [choosenim](https://github.com/dom96/choosenim)
* [x] [NimlineWhispers](https://github.com/snovvcrash/NimlineWhispers)
* [x] [Obsidian](https://github.com/obsidianmd/obsidian-releases/releases)
* [x] [OffensiveNim](https://github.com/byt3bl33d3r/OffensiveNim)
* [x] [PCredz](https://github.com/lgandx/PCredz)
* [x] [PEzor](https://github.com/phra/PEzor)
* [x] [PKINITtools](https://github.com/dirkjanm/PKINITtools)
* [x] [PetitPotam](https://github.com/topotam/PetitPotam)
* [x] [PrintNightmare (MS-RPRN)](https://github.com/cube0x0/CVE-2021-1675/blob/main/CVE-2021-1675.py) · [PrintNightmare (MS-PAR)](https://github.com/cube0x0/CVE-2021-1675/blob/main/SharpPrintNightmare/CVE-2021-1675.py)
* [x] [PrivExchange](https://github.com/dirkjanm/PrivExchange)
* [x] [Responder](https://github.com/lgandx/Responder)
* [x] [RustScan](https://github.com/RustScan/RustScan/releases)
* [x] [SharpShooter](https://github.com/mdsecactivebreach/SharpShooter)
* [x] [ShellPop](https://github.com/0x00-0x00/ShellPop)
* [x] [TrustVisualizer](https://github.com/snovvcrash/TrustVisualizer)
* [x] [Windows-Exploit-Suggester](https://github.com/a1ext/Windows-Exploit-Suggester)
* [ ] [ack3](https://github.com/beyondgrep/ack3)
* [x] [aclpwn.py](https://github.com/fox-it/aclpwn.py)
* [x] [adidnsdump](https://github.com/dirkjanm/adidnsdump)
* [x] [aquatone](https://github.com/michenriksen/aquatone/releases)
* [x] [bettercap](https://github.com/bettercap/bettercap/releases)
* [x] [bloodhound-quickwin](https://github.com/kaluche/bloodhound-quickwin)
* [x] [chisel](https://github.com/jpillora/chisel/releases)
* [x] [crowbar](https://github.com/galkan/crowbar)
* [x] [dementor.py](https://gist.github.com/3xocyte/cfaf8a34f76569a8251bde65fe69dccc)
* [x] [dsniff](https://github.com/tecknicaltom/dsniff)
* [x] [eavesarp](https://github.com/arch4ngel/eavesarp)
* [x] [enum4linux-ng](https://github.com/cddmp/enum4linux-ng)
* [x] [evil-winrm](https://github.com/Hackplayers/evil-winrm)
* [x] [ffuf](https://github.com/ffuf/ffuf/releases)
* [x] [gateway-finder-imp](https://github.com/whitel1st/gateway-finder-imp)
* [x] [gitjacker](https://github.com/liamg/gitjacker/releases)
* [x] [go-windapsearch](https://github.com/ropnop/go-windapsearch) · [Pre-Compiled](https://github.com/penetrarnya-tm/WeaponizeKali.sh/blob/main/bin/windapsearch)
* [x] [gobuster](https://github.com/OJ/gobuster/releases)
* [x] [impacket](https://github.com/SecureAuthCorp/impacket)
* [x] [impacket-adcs](https://github.com/ExAndroidDev/impacket/tree/ntlmrelayx-adcs-attack)
* [x] [ipmitool](https://github.com/ipmitool/ipmitool)
* [x] [kerbrute](https://github.com/ropnop/kerbrute/releases)
* [x] [krbrelayx](https://github.com/dirkjanm/krbrelayx)
* [x] [ldapdomaindump](https://github.com/dirkjanm/ldapdomaindump)
* [x] [ldapsearch-ad](https://github.com/yaap7/ldapsearch-ad)
* [x] [lsassy](https://github.com/Hackndo/lsassy)
* [x] [masscan](https://github.com/robertdavidgraham/masscan)
* [x] [mitm6](https://github.com/fox-it/mitm6)
* [x] [mscache](https://github.com/QAX-A-Team/mscache)
* [x] [nextnet](https://github.com/hdm/nextnet)
* [x] [nishang](https://github.com/samratashok/nishang)
* [x] [ntlm-scanner](https://github.com/preempt/ntlm-scanner)
* [x] [ntlmv1-multi](https://github.com/evilmog/ntlmv1-multi)
* [x] [nullinux](https://github.com/m8r0wn/nullinux)
* [x] [odat](https://github.com/quentinhardy/odat)
* [x] [pyGPOAbuse](https://github.com/Hackndo/pyGPOAbuse)
* [x] [pypykatz](https://github.com/skelsec/pypykatz)
* [x] [pywerview](https://github.com/the-useless-one/pywerview)
* [x] [pywhisker](https://github.com/ShutdownRepo/pywhisker)
* [x] [rbcd-attack](https://github.com/tothi/rbcd-attack)
* [x] [rbcd_permissions](https://github.com/NinjaStyle82/rbcd_permissions)
* [x] [rdp-tunnel](https://github.com/NotMedic/rdp-tunnel)
* [x] [sRDI](https://github.com/monoxgas/sRDI)
* [x] [smartbrute](https://github.com/ShutdownRepo/smartbrute)
* [x] [snmpwn](https://github.com/hatlord/snmpwn)
* [x] [spraykatz](https://github.com/aas-n/spraykatz)
* [x] [ssb](https://github.com/kitabisa/ssb/releases)
* [x] [sshuttle](https://github.com/sshuttle/sshuttle)
* [x] [traitor](https://github.com/liamg/traitor/releases)
* [x] [updog](https://github.com/sc0tfree/updog)
* [x] [webpage2html](https://github.com/snovvcrash/webpage2html)
* [x] [windapsearch](https://github.com/ropnop/windapsearch)
* [x] [xc](https://github.com/xct/xc)

### `www`

* [x] [ADCSPwn](https://github.com/bats3c/ADCSPwn/releases)
* [x] [ADRecon.ps1](https://github.com/adrecon/ADRecon/blob/master/ADRecon.ps1)
* [x] [ASREPRoast.ps1](https://github.com/HarmJ0y/ASREPRoast/blob/master/ASREPRoast.ps1)
* [x] [AccessChk (Sysinternals)](https://docs.microsoft.com/en-us/sysinternals/downloads/accesschk) · [AccessChk (accepteula)](https://xor.cat/2017/09/05/sysinternals-accesschk-accepteula/)
* [x] [Discover-PSMSExchangeServers](https://github.com/PyroTek3/PowerShell-AD-Recon/blob/master/Discover-PSMSExchangeServers)
* [x] [Discover-PSMSSQLServers](https://github.com/PyroTek3/PowerShell-AD-Recon/blob/master/Discover-PSMSSQLServers)
* [x] [DomainPasswordSpray.ps1](https://github.com/dafthack/DomainPasswordSpray/blob/master/DomainPasswordSpray.ps1)
* [ ] [Grouper2](https://github.com/l0ss/Grouper2/releases)
* [x] [HiveNightmare](https://github.com/GossiTheDog/HiveNightmare/releases) · [ShadowSteal](https://github.com/HuskyHacks/ShadowSteal) · [hive.exe](https://github.com/FireFart/hivenightmare/blob/main/release/hive.exe)
* [x] [Intercept-NG](http://sniff.su/)
* [x] [Inveigh.ps1](https://github.com/Kevin-Robertson/Inveigh/blob/master/Inveigh.ps1)
* [x] [InveighZero](https://github.com/Kevin-Robertson/InveighZero) · [Pre-Compiled](https://github.com/Flangvik/SharpCollection/blob/master/NetFramework_4.0_Any/Inveigh.exe)
* [x] [Invoke-ACLPwn.ps1](https://github.com/fox-it/Invoke-ACLPwn/blob/master/Invoke-ACLPwn.ps1)
* [x] [Invoke-ImpersonateUser-PTH.ps1](https://github.com/S3cur3Th1sSh1t/NamedPipePTH/blob/main/Invoke-ImpersonateUser-PTH.ps1)
* [x] [Invoke-Portscan.ps1](https://github.com/PowerShellMafia/PowerSploit/blob/master/Recon/Invoke-Portscan.ps1)
* [x] [Invoke-RunasCs.ps1](https://github.com/antonioCoco/RunasCs/blob/master/Invoke-RunasCs.ps1)
* [x] [Invoke-SMBClient.ps1](https://github.com/Kevin-Robertson/Invoke-TheHash/blob/master/Invoke-SMBClient.ps1)
* [x] [Invoke-SMBEnum.ps1](https://github.com/Kevin-Robertson/Invoke-TheHash/blob/master/Invoke-SMBEnum.ps1)
* [x] [Invoke-SMBExec.ps1](https://github.com/Kevin-Robertson/Invoke-TheHash/blob/master/Invoke-SMBExec.ps1)
* [x] [Invoke-WMIExec.ps1](https://github.com/Kevin-Robertson/Invoke-TheHash/blob/master/Invoke-WMIExec.ps1)
* [x] [JAWS](https://github.com/411Hall/JAWS/blob/master/jaws-enum.ps1)
* [x] [JuicyPotato64](https://github.com/ohpe/juicy-potato/releases) · [JuicyPotato32](https://github.com/ivanitlearning/Juicy-Potato-x86/releases)
* [x] [Out-EncryptedScript.ps1](https://github.com/PowerShellMafia/PowerSploit/blob/master/ScriptModification/Out-EncryptedScript.ps1)
* [x] [PEASS](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite) · [linPEAS.sh](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/blob/master/linPEAS/linpeas.sh) · [winPEAS.exe](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/blob/master/winPEAS/winPEASexe/binaries/Release/winPEASany.exe)
* [x] [PSPKIAudit](https://github.com/GhostPack/PSPKIAudit)
* [x] [PingCastle](https://github.com/vletoux/pingcastle/releases)
* [x] [PowerShellArmoury](https://github.com/cfalta/PowerShellArmoury) · [PSArmoury.json](https://github.com/penetrarnya-tm/WeaponizeKali.sh/blob/main/PSArmoury.json)
* [x] [PowerUp.ps1](https://github.com/PowerShellMafia/PowerSploit/blob/master/Privesc/PowerUp.ps1)
* [x] [PowerUpSQL.ps1](https://github.com/NetSPI/PowerUpSQL/blob/master/PowerUpSQL.ps1)
* [x] [PowerView2.ps1](https://github.com/PowerShellEmpire/PowerTools/blob/master/PowerView/powerview.ps1)
* [x] [PowerView3.ps1](https://github.com/PowerShellMafia/PowerSploit/blob/26a0757612e5654b4f792b012ab8f10f95d391c9/Recon/PowerView.ps1) [(New-GPOImmediateTask)](https://www.harmj0y.net/blog/redteaming/abusing-gpo-permissions/)
* [x] [PowerView3.ps1](https://github.com/PowerShellMafia/PowerSploit/blob/master/Recon/PowerView.ps1)
* [x] [PowerView4.ps1](https://github.com/ZeroDayLab/PowerSploit/blob/master/Recon/PowerView.ps1) [(ZeroDayLab)](https://exploit.ph/powerview.html)
* [x] [PowerSharpPack](https://github.com/S3cur3Th1sSh1t/PowerSharpPack)
* [x] [Powermad.ps1](https://github.com/Kevin-Robertson/Powermad/blob/master/Powermad.ps1)
* [x] [PrivescCheck.ps1](https://github.com/itm4n/PrivescCheck/blob/master/PrivescCheck.ps1)
* [x] [PrintSpoofer](https://github.com/itm4n/PrintSpoofer)
* [x] [ProcDump (Sysinternals)](https://docs.microsoft.com/en-us/sysinternals/downloads/procdump)
* [x] [RemotePotato0](https://github.com/antonioCoco/RemotePotato0/releases)
* [x] [RoguePotato](https://github.com/antonioCoco/RoguePotato)
* [x] [Rubeus](https://github.com/GhostPack/Rubeus) · [Pre-Compiled](https://github.com/r3motecontrol/Ghostpack-CompiledBinaries/blob/master/Rubeus.exe)
* [x] [Seatbelt](https://github.com/GhostPack/Seatbelt) · [Pre-Compiled](https://github.com/r3motecontrol/Ghostpack-CompiledBinaries/blob/master/Seatbelt.exe)
* [x] [SessionGopher.ps1](https://github.com/Arvanaghi/SessionGopher/blob/master/SessionGopher.ps1)
* [x] [SharpChrome](https://github.com/GhostPack/SharpDPAPI/tree/master/SharpChrome) · [Pre-Compiled](https://github.com/r3motecontrol/Ghostpack-CompiledBinaries/blob/master/SharpChrome.exe)
* [x] [SharpDPAPI](https://github.com/GhostPack/SharpDPAPI/tree/master/SharpDPAPI) · [Pre-Compiled](https://github.com/r3motecontrol/Ghostpack-CompiledBinaries/blob/master/SharpDPAPI.exe)
* [x] [SharpGPOAbuse](https://github.com/FSecureLABS/SharpGPOAbuse) · [Pre-Compiled](https://github.com/Flangvik/SharpCollection/blob/master/NetFramework_4.0_Any/SharpGPOAbuse.exe)
* [x] [SharpHandler](https://github.com/jfmaes/SharpHandler)  · [Pre-Compiled](https://github.com/Flangvik/SharpCollection/blob/master/NetFramework_4.0_Any/SharpHandler.exe)
* [x] [SharpHound.exe](https://github.com/BloodHoundAD/BloodHound/blob/master/Collectors/SharpHound.exe)
* [x] [SharpHound.ps1](https://github.com/BloodHoundAD/BloodHound/blob/master/Collectors/SharpHound.ps1)
* [x] [SharpNamedPipePTH](https://github.com/S3cur3Th1sSh1t/SharpNamedPipePTH) · [Pre-Compiled](https://github.com/Flangvik/SharpCollection/blob/master/NetFramework_4.0_Any/SharpNamedPipePTH.exe) · [Invoke-SharpNamedPipePTH.ps1](https://github.com/snovvcrash/PowerSharpPack/blob/master/PowerSharpBinaries/Invoke-SharpNamedPipePTH.ps1)
* [x] [SharpSecDump](https://github.com/G0ldenGunSec/SharpSecDump) · [Pre-Compiled](https://github.com/Flangvik/SharpCollection/blob/master/NetFramework_4.0_Any/SharpSecDump.exe)
* [x] [SharpView](https://github.com/tevora-threat/SharpView) · [Pre-Compiled](https://github.com/tevora-threat/SharpView/blob/master/Compiled/SharpView.exe)
* [x] [Sherlock.ps1](https://github.com/rasta-mouse/Sherlock/blob/master/Sherlock.ps1)
* [x] [Snaffler](https://github.com/SnaffCon/Snaffler/releases)
* [x] [SpoolSample](https://github.com/leechristensen/SpoolSample/) · [Pre-Compiled](https://github.com/BlackDiverX/WinTools/blob/master/SpoolSample-Printerbug/SpoolSample.exe)
* [x] [WinPwn](https://github.com/S3cur3Th1sSh1t/WinPwn)
* [x] [WerTrigger](https://github.com/sailay1996/WerTrigger)
* [x] [chisel](https://github.com/jpillora/chisel/releases)
* [x] [impacket-examples-windows](https://github.com/maaaaz/impacket-examples-windows)
* [x] [les.sh](https://github.com/mzet-/linux-exploit-suggester/blob/master/linux-exploit-suggester.sh)
* [x] [lse.sh](https://github.com/diego-treitos/linux-smart-enumeration/blob/master/lse.sh)
* [x] [mimikatz](https://github.com/gentilkiwi/mimikatz/releases)
* [x] [netcat for Windows](https://eternallybored.org/misc/netcat/)
* [x] [plink](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
* [x] [powercat.ps1](https://github.com/besimorhino/powercat/blob/master/powercat.ps1)
* [x] [pspy](https://github.com/DominicBreuker/pspy/releases)
* [x] [pypykatz.exe](https://github.com/skelsec/pypykatz/releases)
* [x] [rdp2tcp.exe](https://github.com/NotMedic/rdp-tunnel/blob/master/rdp2tcp.exe)
* [x] [static-binaries](https://github.com/andrew-d/static-binaries)
* [x] [suid3num.py](https://github.com/Anon-Exploiter/SUID3NUM/blob/master/suid3num.py)
