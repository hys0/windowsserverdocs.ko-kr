---
title: Windows 명령
description: 참고
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c703d07c-8227-4e86-94a6-8ef390f94cdc
author: jasongerend
ms.author: jgerend
manager: dongill
ms.date: 06/26/2019
ms.prod: windows-server
ms.openlocfilehash: 7baec3bbe532bbcedb8c17628fd88d2c8eac34c6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720728"
---
# <a name="windows-commands"></a>Windows 명령

지원 되는 모든 버전의 Windows (서버 및 클라이언트)에는에서 기본 제공 되는 Win32 콘솔 명령 집합이 있습니다.

이 설명서 집합에서는 스크립트나 스크립팅 도구를 사용 하 여 작업을 자동화 하는 데 사용할 수 있는 Windows 명령을 설명 합니다.

다음 ㄱ-ㅎ 메뉴에서 특정 명령에 대 한 정보를 찾기 위해 명령을 첫 글자를 클릭 하 고 명령 이름을 클릭 합니다.

[A](#a) |
[B](#b) | 
[M](#m)[D](#d) | 
[V](#v)[C](#c) |
[J](#j) | 
[W](#w)[F](#f) | 
[S](#s)[E](#e) | 
[R](#r)[G](#g) | 
[U](#u)[H](#h) | 
[X](#x) [I](#i) | 
[T](#t)[L](#l)[N](#n)[Q](#q)[O](#o)[P](#p)[K](#k)C D E F G H I J | 
K L M | 
N | 
O | 
P | 
Q R S T U V W X | | 
 | 
 | 
 | 
 | 
 | 
 | 
 | 
 Y | -

## <a name="prerequisites"></a>전제 조건

이 항목에 포함 된 정보는 다음에 적용 됩니다.

-   시작
-   Windows Server(반기 채널)
-   Windows Server 2016
-   Windows Server 2012 R2
-   Windows Server 2012 
-   Windows Server 2008 R2
-   Windows Server 2008
-   Windows 10
-   Windows 8.1

### <a name="command-shell-overview"></a>명령 셸 개요

명령 셸은 배치 (.bat) 파일을 사용 하 여 사용자 계정 관리 또는 야간 백업과 같은 일상적인 작업을 자동화 하기 위해 Windows에 기본 제공 되는 셸 이었습니다. Windows 스크립트 호스트를 사용 하면 명령 셸에서 보다 정교한 스크립트를 실행할 수 있습니다. 자세한 내용은 [cscript](cscript.md) 또는 [wscript](wscript.md)를 참조 하세요. 사용자 인터페이스를 사용 하는 것 보다 스크립트를 사용 하 여 작업을 보다 효율적으로 수행할 수 있습니다. 스크립트는 명령줄에서 사용할 수 있는 모든 명령을 허용 합니다.

Windows에는 명령 셸 및 [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting?view=powershell-6)이라는 두 개의 명령 셸이 있습니다. 각 shell은 사용자와 운영 체제 또는 응용 프로그램 간의 직접 통신을 제공 하 여 IT 운영을 자동화 하는 환경을 제공 하는 소프트웨어 프로그램입니다.

PowerShell은 cmdlet 이라는 PowerShell 명령을 실행 하기 위해 명령 셸의 기능을 확장 하도록 설계 되었습니다. Cmdlet은 Windows 명령과 비슷하지만 보다 확장 가능한 스크립트 언어를 제공 합니다. Powershell에서 Windows 명령 및 PowerShell cmdlet을 실행할 수 있지만 명령 셸은 PowerShell cmdlet이 아닌 Windows 명령만 실행할 수 있습니다.

가장 강력 하 고 최신 Windows automation의 경우 windows 용 windows 명령 또는 windows 스크립트 호스트 대신 PowerShell을 사용 하는 것이 좋습니다. 
> [!NOTE]
>Powershell의 오픈 소스 버전인 powershell [Core](https://docs.microsoft.com/powershell/scripting/whats-new/what-s-new-in-powershell-core-60?view=powershell-6)를 다운로드 하 여 설치할 수도 있습니다. 

> [!CAUTION]
> 레지스트리를 잘못 편집하면 시스템에 심각한 손상을 줄 수 있습니다. 레지스트리를 다음과 같이 변경 하기 전에 컴퓨터의 중요 한 데이터를 백업 해야 합니다.

> [!NOTE]
> 컴퓨터 또는 사용자 로그온 세션의 명령 셸에서 파일 및 디렉터리 이름 완성을 사용 하거나 사용 하지 않도록 설정 하려면 **regedit.exe** 를 실행 하 고 다음 **reg_DWOrd 값**을 설정 합니다.
> 
> HKEY_LOCAL_MACHINE \Software\Microsoft\Command Processor\completionChar\ reg_DWOrd
> 
> **Reg_DWOrd** 값을 설정 하려면 특정 함수에 대 한 제어 문자의 16 진수 값을 사용 합니다 (예: **0 9** 은 Tab, **0 08** 은 백스페이스). 사용자 지정 설정이 컴퓨터 설정 보다 우선 하며 명령줄 옵션 레지스트리 설정 보다 우선 합니다.

## <a name="command-line-reference-a-z"></a>명령줄 참조 ㄱ-ㅎ

특정 Windows 명령에 대 한 정보를 찾으려면 다음 A-z 메뉴에서 명령이 시작 되는 문자를 클릭 하 고 명령 이름을 클릭 합니다.

[A](#a) |
[B](#b) | 
[M](#m)[D](#d) | 
[V](#v)[C](#c) |
[J](#j) | 
[W](#w)[F](#f) | 
[S](#s)[E](#e) | 
[R](#r)[G](#g) | 
[U](#u)[H](#h) | 
[X](#x) [I](#i) | 
[T](#t)[L](#l)[N](#n)[Q](#q)[O](#o)[P](#p)[K](#k)C D E F G H I J | 
K L M | 
N | 
O | 
P | 
Q R S T U V W X | | 
 | 
 | 
 | 
 | 
 | 
 | 
 | 
 Y | -

### <a name="a"></a>A
-   [append](append.md)
-   [arp](arp.md)
-   [assoc](assoc.md)
-   [at](at.md)
-   [atmadm](atmadm.md)
-   [attrib](attrib.md)
-   [auditpol](auditpol.md)
-   [autochk](autochk.md)
-   [autoconv](autoconv.md)
-   [autofmt](autofmt.md)

### <a name="b"></a>b
- [bcdboot](bcdboot.md)
- [bcdedit](bcdedit.md)
- [bdehdcfg](bdehdcfg.md)
- [bitsadmin](bitsadmin.md)
  -   [bitsadmin addfile](bitsadmin-addfile.md)
  -   [bitsadmin addfileset](bitsadmin-addfileset.md)
  -   [bitsadmin addfilewithranges](bitsadmin-addfilewithranges.md)
  -   [bitsadmin cancel](bitsadmin-cancel.md)
  -   [bitsadmin complete](bitsadmin-complete.md)
  -   [bitsadmin create](bitsadmin-create.md)
  -   [bitsadmin getaclflags](bitsadmin-getaclflags.md)
  -   [bitsadmin getbytestotal](bitsadmin-getbytestotal.md)
  -   [bitsadmin getbytestransferred](bitsadmin-getbytestransferred.md)
  -   [bitsadmin getcompletiontime](bitsadmin-getcompletiontime.md)
  -   [bitsadmin getcreationtime](bitsadmin-getcreationtime.md)
  -   [bitsadmin getdescription](bitsadmin-getdescription.md)
  -   [bitsadmin getdisplayname](bitsadmin-getdisplayname.md)
  -   [bitsadmin geterror](bitsadmin-geterror.md)
  -   [bitsadmin geterrorcount](bitsadmin-geterrorcount.md)
  -   [bitsadmin getfilestotal](bitsadmin-getfilestotal.md)
  -   [bitsadmin getfilestransferred](bitsadmin-getfilestransferred.md)
  -   [bitsadmin getminretrydelay](bitsadmin-getminretrydelay.md)
  -   [bitsadmin getmodificationtime](bitsadmin-getmodificationtime.md)
  -   [bitsadmin getnoprogresstimeout](bitsadmin-getnoprogresstimeout.md)
  -   [bitsadmin getnotifycmdline](bitsadmin-getnotifycmdline.md)
  -   [bitsadmin getnotifyflags](bitsadmin-getnotifyflags.md)
  -   [bitsadmin getnotifyinterface](bitsadmin-getnotifyinterface.md)
  -   [bitsadmin getowner](bitsadmin-getowner.md)
  -   [bitsadmin get 우선 순위](bitsadmin-getpriority.md)
  -   [bitsadmin getproxybypasslist](bitsadmin-getproxybypasslist.md)
  -   [bitsadmin getproxylist](bitsadmin-getproxylist.md)
  -   [bitsadmin getproxyusage](bitsadmin-getproxyusage.md)
  -   [bitsadmin getreplydata](bitsadmin-getreplydata.md)
  -   [bitsadmin getreplyfilename](bitsadmin-getreplyfilename.md)
  -   [bitsadmin getreplyprogress](bitsadmin-getreplyprogress.md)
  -   [bitsadmin getstate](bitsadmin-getstate.md)
  -   [bitsadmin gettype](bitsadmin-gettype.md)
  -   [bitsadmin help](bitsadmin-help.md)
  -   [bitsadmin info](bitsadmin-info.md)
  -   [bitsadmin list](bitsadmin-list.md)
  -   [bitsadmin listfiles](bitsadmin-listfiles.md)
  -   [bitsadmin monitor](bitsadmin-monitor.md)
  -   [bitsadmin nowrap](bitsadmin-nowrap.md)
  -   [bitsadmin rawreturn](bitsadmin-rawreturn.md)
  -   [bitsadmin removecredentials](bitsadmin-removecredentials.md)
  -   [bitsadmin replaceremoteprefix](bitsadmin-replaceremoteprefix.md)
  -   [bitsadmin reset](bitsadmin-reset.md)
  -   [bitsadmin resume](bitsadmin-resume.md)
  -   [bitsadmin setaclflag](bitsadmin-setaclflag.md)
  -   [bitsadmin setcredentials](bitsadmin-setcredentials.md)
  -   [bitsadmin setdescription](bitsadmin-setdescription.md)
  -   [bitsadmin setdisplayname](bitsadmin-setdisplayname.md)
  -   [bitsadmin setminretrydelay](bitsadmin-setminretrydelay.md)
  -   [bitsadmin setnoprogresstimeout](bitsadmin-setnoprogresstimeout.md)
  -   [bitsadmin setnotifycmdline](bitsadmin-setnotifycmdline.md)
  -   [bitsadmin setnotifyflags](bitsadmin-setnotifyflags.md)
  -   [bitsadmin setpriority](bitsadmin-setpriority.md)
  -   [bitsadmin setproxysettings](bitsadmin-setproxysettings.md)
  -   [bitsadmin setreplyfilename](bitsadmin-setreplyfilename.md)
  -   [bitsadmin suspend](bitsadmin-suspend.md)
  -   [bitsadmin takeownership](bitsadmin-takeownership.md)
  -   [bitsadmin 전송](bitsadmin-transfer.md)
  -   [bitsadmin util](bitsadmin-util.md)
  -   [bitsadmin wrap](bitsadmin-wrap.md)
- [bootcfg](bootcfg.md)
  -   [bootcfg addsw](bootcfg-addsw.md)
  -   [bootcfg copy](bootcfg-copy.md)
  -   [bootcfg dbg1394](bootcfg-dbg1394.md)
  -   [bootcfg debug](bootcfg-debug.md)  
  -   [bootcfg default](bootcfg-default.md)
  -   [bootcfg delete](bootcfg-delete.md)
  -   [bootcfg ems](bootcfg-ems.md)
  -   [bootcfg query](bootcfg-query.md)
  -   [bootcfg raw](bootcfg-raw.md)
  -   [bootcfg rmsw](bootcfg-rmsw.md)
  -   [bootcfg timeout](bootcfg-timeout.md)
- [break](break_1.md)

### <a name="c"></a>C
- [cacls](cacls_1.md)
- [call](call.md)
- [cd](cd.md)
- [certreq](certreq_1.md)
- [certutil](certutil.md)
- [change](change.md)
  -   [change logon](change-logon.md)
  -   [change port](change-port.md)
  -   [change user](change-user.md)
- [chcp](chcp.md)
- [chdir](chdir_1.md)
- [chglogon](chglogon.md)
- [chgport](chgport.md)
- [chgusr](chgusr.md)
- [chkdsk](chkdsk.md)
- [chkntfs](chkntfs.md)
- [choice](choice.md)
- [cipher](cipher.md)
- [cleanmgr](cleanmgr.md)
- [clip](clip.md)
- [cls](cls.md)
- [Cmd](Cmd.md)
- [cmdkey](cmdkey.md)
- [cmstp](cmstp.md)
- [color](color.md)
- [comp](comp.md)
- [compact](compact.md)
- [convert](convert.md)
- [copy](copy.md)
- [cprofile](cprofile.md)
- [cscript](cscript.md)

### <a name="d"></a>D
-   [date](date.md)
-   [dcgpofix](dcgpofix.md)
-   [defrag](defrag.md)
-   [del](del.md)
-   [dfsrmig](dfsrmig.md)
-   [diantz](diantz.md)
-   [dir](dir.md)
-   [diskcomp](diskcomp.md)
-   [diskcopy](diskcopy.md)
-   [diskpart](diskpart.md)
-   [diskperf](diskperf.md)
-   [diskraid](diskraid.md)
-   [diskshadow](diskshadow.md)
-   [dispdiag](dispdiag.md)
-   [dnscmd](Dnscmd.md)
-   [doskey](doskey.md)
-   [driverquery](driverquery.md)

### <a name="e"></a>E
-   [echo](echo.md)
-   [edit](edit.md)
-   [endlocal](endlocal.md)
-   [erase](erase.md)
-   [eventcreate](eventcreate.md)
-   [eventquery](eventquery.md)
-   [eventtriggers](eventtriggers.md)
-   [evntcmd](Evntcmd.md)
-   [exit](exit_2.md)
-   [expand](expand.md)
-   [extract](extract.md)

### <a name="f"></a>F
- [fc](fc.md)
- [find](find.md)
- [findstr](findstr.md)
- [finger](finger.md)
- [flattemp](flattemp.md)
- [fondue](fondue.md)
- [for](for.md)
- [forfiles](forfiles.md)
- [format](format.md)
- [freedisk](freedisk.md)
- [fsutil](fsutil.md)
  -   [fsutil 8dot3name](fsutil-8dot3name.md) 
  -   [fsutil behavior](fsutil-behavior.md) 
  -   [fsutil file](fsutil-file.md)
  -   [fsutil fsinfo](fsutil-fsinfo.md)
  -   [fsutil hardlink](fsutil-hardlink.md)
  -   [fsutil objectid](fsutil-objectid.md)
  -   [fsutil quota](fsutil-quota.md)
  -   [fsutil repair](fsutil-repair.md)
  -   [fsutil reparsepoint](fsutil-reparsepoint.md)
  -   [fsutil resource](fsutil-resource.md)
  -   [fsutil sparse](fsutil-sparse.md)
  -   [fsutil tiering](fsutil-tiering.md)
  -   [fsutil transaction](fsutil-transaction.md)
  -   [fsutil usn](fsutil-usn.md)
  -   [fsutil volume](fsutil-volume.md)
  -   [fsutil wim](fsutil-wim.md)
- [p](ftp.md)
- [ftype](ftype.md)
- [fveupdate](fveupdate.md)

### <a name="g"></a>G
-   [getmac](getmac.md)
-   [gettype](gettype.md)
-   [goto](goto.md)
-   [gpfixup](gpfixup.md)
-   [gpresult](gpresult.md)
-   [gpupdate](gpupdate.md)
-   [graftabl](graftabl.md)

### <a name="h"></a>H
-   [help](help.md)
-   [helpctr](helpctr.md)
-   [hostname](hostname.md)

### <a name="i"></a>I
-   [icacls](icacls.md)
-   [if](if.md)
-   [inuse](inuse.md)
-   [ipconfig](ipconfig.md)
-   [ipxroute](ipxroute.md)
-   [irftp](irftp.md)

### <a name="j"></a>J
-   [jetpack](jetpack.md)

### <a name="k"></a>K
- [klist](klist.md)
- [ksetup](ksetup.md)
  -   [ksetup: setrealm](ksetup-setrealm.md)
  -   [ksetup: mapuser](ksetup-mapuser.md)
  -   [ksetup: addkdc](ksetup-addkdc.md)
  -   [ksetup: delkdc](ksetup-delkdc.md)
  -   [ksetup: addkpasswd](ksetup-addkpasswd.md)
  -   [ksetup: delkpasswd](ksetup-delkpasswd.md)
  -   [ksetup: 서버](ksetup-server.md)
  -   [ksetup: setcomputerpassword](ksetup-setcomputerpassword.md)
  -   [ksetup: removerealm](ksetup-removerealm.md)
  -   [ksetup: 도메인](ksetup-domain.md)
  -   [ksetup: changepassword](ksetup-changepassword.md)
  -   [ksetup: listrealmflags](ksetup-listrealmflags.md)
  -   [ksetup: setrealmflags](ksetup-setrealmflags.md)
  -   [ksetup: addrealmflags](ksetup-addrealmflags.md)
  -   [ksetup: delrealmflags](ksetup-delrealmflags.md)
  -   [ksetup: 상태를](ksetup-dumpstate.md)
  -   [ksetup: addhosttorealmmap](ksetup-addhosttorealmmap.md)
  -   [ksetup: delhosttorealmmap](ksetup-delhosttorealmmap.md)
  -   [ksetup: setenctypeattr](ksetup-setenctypeattr.md)
  -   [ksetup: getenctypeattr](ksetup-getenctypeattr.md)
  -   [ksetup: addenctypeattr](ksetup-addenctypeattr.md)
  -   [ksetup: delenctypeattr](ksetup-delenctypeattr.md) 
- [ktmutil](ktmutil.md)
- [ktpass](ktpass.md)

### <a name="l"></a>L
- [label](label.md)
- [lodctr](lodctr.md)
- [logman](logman.md)
  -   [logman create](logman-create.md)
  -   [logman query](logman-query.md)
  -   [logman start &124; 막을](logman-start-stop.md)
  -   [logman delete](logman-delete.md)
  -   [logman update](logman-update.md)
  -   [logman 가져오기 &124; 내보내기가](logman-import-export.md)
- [logoff](logoff.md)
- [lpq](lpq.md)
- [lpr](lpr.md)

### <a name="m"></a>M
- [macfile](macfile.md)
- [makecab](makecab.md)
- [manage-bde](manage-bde.md)
  -   [manage-bde: 상태](manage-bde-status.md)
  -   [manage-bde: on](manage-bde-on.md)
  -   [manage-bde: off](manage-bde-off.md)
  -   [manage-bde: pause](manage-bde-pause.md)
  -   [manage-bde: resume](manage-bde-resume.md)
  -   [manage-bde: lock](manage-bde-lock.md)
  -   [manage-bde: unlock](manage-bde-unlock.md)
  -   [manage-bde: autounlock](manage-bde-autounlock.md)
  -   [manage-bde: 보호기](manage-bde-protectors.md)
  -   [manage-bde: tpm](manage-bde-tpm.md)
  -   [manage-bde: setidentifier](manage-bde-setidentifier.md)
  -   [manage-bde: ForceRecovery](manage-bde-forcerecovery.md)
  -   [manage-bde: changepassword](manage-bde-changepassword.md)
  -   [manage-bde: changepin](manage-bde-changepin.md)
  -   [manage-bde: 변환](manage-bde-changekey.md)
  -   [manage-bde: KeyPackage](manage-bde-keypackage.md)
  -   [manage-bde: upgrade](manage-bde-upgrade.md)
  -   [manage-bde: WipeFreeSpace](manage-bde-wipefreespace.md)
- [mapadmin](mapadmin.md)
- [Md](Md.md)
- [mkdir](mkdir.md)
- [mklink](mklink.md)
- [mmc](mmc.md)
- [mode](mode.md)
- [more](more.md)
- [mount](mount.md)
- [mountvol](mountvol.md)
- [move](move.md)
- [mqbkup](mqbkup.md)
- [mqsvc](mqsvc.md)
- [mqtgsvc](mqtgsvc.md)
- [msdt](msdt.md)
- [msg](msg.md)
- [msiexec](msiexec.md)
- [msinfo32](msinfo32.md)
- [mstsc](mstsc.md)

### <a name="n"></a>N
- [nbtstat](nbtstat.md)
- [netcfg](netcfg.md)
- [netsh](netsh.md)
- [netstat](netstat.md)
- [Net print](net-print.md)
- [nfsadmin](nfsadmin.md)
- [nfsshare](nfsshare.md)
- [nfsstat](nfsstat.md)
- [nlbmgr](nlbmgr.md)
- [nslookup](nslookup.md)
  -   [nslookup exit 명령](nslookup-exit-command.md)
  -   [nslookup finger 명령](nslookup-finger-command.md)
  -   [nslookup help](nslookup-help.md)
  -   [nslookup ls](nslookup-ls.md)
  -   [nslookup lserver](nslookup-lserver.md)
  -   [nslookup root](nslookup-root.md)
  -   [nslookup server](nslookup-server.md)
  -   [nslookup set](nslookup-set.md)
  -   [nslookup set all](nslookup-set-all.md)
  -   [nslookup set class](nslookup-set-class.md)
  -   [nslookup set d2](nslookup-set-d2.md)
  -   [nslookup set debug](nslookup-set-debug.md)
  -   [nslookup set domain](nslookup-set-domain.md)
  -   [nslookup set port](nslookup-set-port.md)
  -   [nslookup set querytype](nslookup-set-querytype.md)
  -   [nslookup set recurse](nslookup-set-recurse.md)
  -   [nslookup set retry](nslookup-set-retry.md)
  -   [nslookup set root](nslookup-set-root.md)
  -   [nslookup set search](nslookup-set-search.md)
  -   [nslookup set srchlist](nslookup-set-srchlist.md)
  -   [nslookup set timeout](nslookup-set-timeout.md)
  -   [nslookup set type](nslookup-set-type.md)
  -   [nslookup set vc](nslookup-set-vc.md)
  -   [nslookup view](nslookup-view.md)
- [ntbackup](ntbackup.md)
- [ntcmdprompt](ntcmdprompt.md)
- [ntfrsutl](ntfrsutl.md)

### <a name="o"></a>O
-   [openfiles](openfiles.md)

### <a name="p"></a>P
-   [pagefileconfig](pagefileconfig.md)
-   [path](path.md)
-   [pathping](pathping.md)
-   [pause](pause.md)
-   [pbadmin](pbadmin.md)
-   [pentnt](pentnt.md)
-   [perfmon](perfmon.md)
-   [ping](ping.md)
-   [pnpunattend](pnpunattend.md)
-   [pnputil](pnputil.md)
-   [popd](popd.md)
-   [PowerShell](PowerShell.md)
-   [PowerShell_ise](PowerShell_ise.md)
-   [print](print.md)
-   [prncnfg](prncnfg.md)
-   [prndrvr](prndrvr.md)
-   [prnjobs](prnjobs.md)
-   [prnmngr](prnmngr.md)
-   [prnport](prnport.md)
-   [prnqctl](prnqctl.md)
-   [prompt](prompt.md)
-   [pubprn](pubprn.md)
-   [pushd](pushd.md)
-   [pushprinterconnections](pushprinterconnections.md)

### <a name="q"></a>Q
-   [qappsrv](qappsrv.md)
-   [qprocess](qprocess.md)
-   [쿼리](query.md)
-   [quser](quser.md)
-   [qwinsta](qwinsta.md)

### <a name="r"></a>R
- [rcp](rcp.md)
- [rd](rd.md)
- [rdpsign](rdpsign.md)
- [recover](recover.md)
- [reg](reg.md)
  -   [reg 추가](reg-add.md)
  -   [reg 비교](reg-compare.md)
  -   [reg 복사](reg-copy.md)
  -   [reg 삭제](reg-delete.md)
  -   [reg 내보내기](reg-export.md)
  -   [reg 가져오기](reg-import.md)
  -   [reg 로드](reg-load.md)
  -   [reg 쿼리](reg-query.md)
  -   [reg 복원](reg-restore.md)
  -   [reg 저장](reg-save.md)
  -   [레지스트리 언로드](reg-unload.md)
- [regini](regini.md)
- [regsvr32](regsvr32.md)
- [relog](relog.md)
- [rem](rem.md)
- [ren](ren.md)
- [rename](rename.md)
- [repair-bde](repair-bde.md)
- [replace](replace.md)
- [reset session](reset-session.md)
- [rexec](rexec.md)
- [risetup](risetup.md)
- [rmdir](rmdir.md)
- [robocopy](robocopy.md)
- [route_ws2008](route_ws2008.md)
- [rpcinfo](rpcinfo.md)
- [rpcping](rpcping.md)
- [rsh](rsh.md)
- [rundll32](rundll32.md)
- [rwinsta](rwinsta.md)

### <a name="s"></a>S
- [schtasks](schtasks.md)
- [scwcmd](Scwcmd.md)
  -   [scwcmd: 분석](scwcmd-analyze.md)
  -   [scwcmd: 구성](scwcmd-configure.md)
  -   [scwcmd: 등록](scwcmd-register.md) 
  -   [scwcmd: 롤백](scwcmd-rollback.md) 
  -   [scwcmd: 변환](scwcmd-transform.md) 
  -   [scwcmd: 뷰](scwcmd-view.md) 
- [secedit](secedit.md)
  -   [secedit: 분석](secedit-analyze.md)
  -   [secedit: 구성](secedit-configure.md)
  -   [secedit: 내보내기](secedit-export.md)
  -   [secedit: generaterollback](secedit-generaterollback.md)
  -   [secedit: 가져오기](secedit-import.md)
  -   [secedit: 유효성 검사](secedit-validate.md)
- [serverceipoptin](serverceipoptin.md)
- [Servermanagercmd](Servermanagercmd.md)
- [serverweroptin](serverweroptin.md)
- [set](set_1.md)
- [setlocal](setlocal.md)
- [setx](setx.md)
- [sfc](sfc.md)
- [shadow](shadow.md)
- [shift](shift.md)
- [showmount](showmount.md)
- [shutdown](shutdown.md)
- [sort](sort.md)
- [start](start.md)
- [subst](subst.md)
- [sxstrace](sxstrace.md)
- [sysocmgr](sysocmgr.md)
- [systeminfo](systeminfo.md)

### <a name="t"></a>T
-   [takeown](takeown.md)
-   [tapicfg](tapicfg.md)
-   [taskkill](taskkill.md)
-   [tasklist](tasklist.md)
-   [tcmsetup](tcmsetup.md)
-   [telnet](telnet.md)
-   [tftp](tftp.md)
-   [time](time.md)
-   [timeout](timeout_1.md)
-   [title](title_1.md)
-   [tlntadmn](tlntadmn.md)
-   [tpmvscmgr](tpmvscmgr.md)
-   [tracerpt](tracerpt_1.md)
-   [tracert](tracert.md)
-   [tree](tree.md)
-   [tscon](tscon.md)
-   [tsdiscon](tsdiscon.md)
-   [tsecimp](tsecimp_1.md)
-   [tskill](tskill.md)
-   [tsprof](tsprof.md)
-   [type](type.md)
-   [typeperf](typeperf.md)
-   [tzutil](tzutil.md)

### <a name="u"></a>U
-   [unlodctr](unlodctr_1.md)

### <a name="v"></a>V
-   [ver](ver.md)
-   [verifier](verifier.md)
-   [verify](verify_1.md)
-   [vol](vol.md)
-   [list](vssadmin.md)- 

### <a name="w"></a>W
- [waitfor](waitfor.md)
- [wbadmin](wbadmin.md)
  -   [wbadmin 백업 사용](wbadmin-enable-backup.md)
  -   [wbadmin 백업 사용 안 함](wbadmin-disable-backup.md)
  -   [wbadmin 백업 시작](wbadmin-start-backup.md)
  -   [wbadmin 중지 작업](wbadmin-stop-job.md)
  -   [wbadmin get 버전](wbadmin-get-versions.md)
  -   [wbadmin get 항목](wbadmin-get-items.md)
  -   [wbadmin 복구 시작](wbadmin-start-recovery.md)
  -   [wbadmin 가져오기 상태](wbadmin-get-status.md)
  -   [wbadmin get 디스크](wbadmin-get-disks.md)
  -   [wbadmin 시작 systemstaterecovery](wbadmin-start-systemstaterecovery.md)
  -   [wbadmin 시작 systemstatebackup](wbadmin-start-systemstatebackup.md)
  -   [wbadmin delete systemstatebackup](wbadmin-delete-systemstatebackup.md)
  -   [wbadmin 시작 sysrecovery](wbadmin-start-sysrecovery.md)
  -   [wbadmin 복원 카탈로그](wbadmin-restore-catalog.md)
  -   [wbadmin delete 카탈로그](wbadmin-delete-catalog.md)
- [wdsutil](wdsutil.md)
- [wecutil](wecutil.md)
- [wevtutil](wevtutil.md)
- [where](where_1.md)
- [whoami](whoami.md)
- [winnt](winnt.md)
- [winnt32](winnt32.md)
- [winpop](winpop.md)
- [winrs](winrs.md)
- [wmic](wmic.md)
- [wscript](wscript.md)

### <a name="x"></a>X
-   [xcopy](xcopy.md)
