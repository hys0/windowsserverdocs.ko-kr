---
title: Windows 명령
description: Windows 명령
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c703d07c-8227-4e86-94a6-8ef390f94cdc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/22/2018
ms.prod: windows-server-threshold
ms.openlocfilehash: 4cc9bc5c288eb063f333fa598dbb3511f7be5966
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820474"
---
# <a name="windows-commands"></a>Windows 명령

Windows (서버 및 클라이언트)의 모든 지원 되는 버전에는 기본 제공 하는 Win32 콘솔 명령 집합이.

이 설명서 집합 스크립팅 도구 또는 스크립트를 사용 하 여 작업을 자동화 하 여 Windows 명령을 설명 합니다.

다음 ㄱ-ㅎ 메뉴에서 특정 명령에 대 한 정보를 찾기 위해 명령을 첫 글자를 클릭 하 고 명령 이름을 클릭 합니다.

[A](#BKMK_a) |
[B](#BKMK_b) | 
[C](#BKMK_c) | 
[D](#BKMK_d) | 
[E](#BKMK_e) | 
[F](#BKMK_f) | 
[G](#BKMK_g) | 
[H](#BKMK_h) | 
[I](#BKMK_i) |
[J](#BKMK_j) | 
[K](#BKMK_k) | 
[L](#BKMK_l) | 
[M](#BKMK_m) | 
[N](#BKMK_n) | 
[O](#BKMK_o) | 
[P](#BKMK_p) | 
[Q](#BKMK_q) | 
[R](#BKMK_r) | 
[S](#BKMK_s) | 
[T](#BKMK_t) | 
[U](#BKMK_u) | 
[V](#BKMK_v) | 
[W](#BKMK_w) | 
[X](#BKMK_x) | 
[Y](#BKMK_y) | 
[Z](#BKMK_z)

## <a name="BKMK_PREREQ"></a>필수 구성 요소
이 PDF에 포함 된 정보에 적용 됩니다.

-   Windows Server 2019
-   Windows Server(반기 채널)
-   Windows Server 2016
-   Windows Server 2012 R2
-   Windows Server 2012 
-   Windows Server 2008 R2
-   Windows Server 2008
-   Windows 10
-   Windows 8.1

### <a name="BKMK_OVR"></a>명령 셸 개요
명령 셸에서 배치 (.bat) 파일을 사용 하 여 사용자 계정 관리 또는 야간 백업 같은 일상적인 작업을 자동화 하는 Windows에 기본 제공 되는 첫 번째 셸이 이었습니다. Windows 스크립트 호스트를 사용 하 여 명령 셸에서 보다 정교한 스크립트를 실행할 수 있습니다. 자세한 내용은 [cscript](cscript.md) 하거나 [wscript](wscript.md)합니다. 사용자 인터페이스를 사용 하 여 수 있는 것 보다 스크립트를 사용 하 여 작업을 보다 효율적으로 수행할 수 있습니다. 스크립트는 명령줄에서 사용할 수 있는 모든 명령에 동의 합니다.

Windows 명령 셸에서 두에 있습니다. 명령 셸 및 [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting?view=powershell-6)합니다. 각 shell은 하 고 운영 체제 또는 IT 작업을 자동화 하는 환경을 제공 하는 응용 프로그램 간의 직접 통신을 제공 하는 소프트웨어 프로그램입니다.

PowerShell은 cmdlet을 호출 하는 PowerShell 명령을 실행 하려면 명령 셸의 기능을 확장 하도록 설계 되었습니다. Cmdlet은 Windows 명령과 유사 하 게 하지만 보다 확장성이 뛰어난 스크립팅 언어를 제공 합니다. Powershell에서 Windows 명령 및 PowerShell cmdlet을 실행할 수 있지만 명령 셸은 Windows 명령 및 PowerShell cmdlet 없습니다만 실행할 수 있습니다.

Automation에 대 한 가장 강력 하 고 최신 Windows, Windows 명령 또는 Windows 스크립트 호스트에 대 한 Windows 자동화 하는 대신 PowerShell을 사용 하는 것이 좋습니다. 
> [!NOTE]
>또한 다운로드 하 고 설치할 수 있습니다 [PowerShell Core](https://docs.microsoft.com/powershell/scripting/whats-new/what-s-new-in-powershell-core-60?view=powershell-6), 오픈 소스 버전의 PowerShell. 

> [!CAUTION]
> 레지스트리를 잘못 편집하면 시스템에 심각한 손상을 줄 수 있습니다. 레지스트리를 다음과 같이 변경 하기 전에 컴퓨터의 중요 한 데이터를 백업 해야 합니다.

> [!NOTE]
> 를 사용 하거나 컴퓨터 또는 사용자 로그온 세션에서 명령 셸에서 있는 파일 및 디렉터리 이름 완성을 사용 하지 않도록 설정 하려면 실행 **regedit.exe** 다음을 설정 하 고 **reg_DWOrd 값**:
> 
> HKEY_LOCAL_MACHINE\Software\Microsoft\Command Processor\completionChar\reg_DWOrd
> 
> 설정 하는 **reg_DWOrd** 값을 특정 함수에 대 한 제어 문자의 16 진수 값을 사용 (예를 들어 **0 9** 은 탭 및 **0 08** 백스페이스). 사용자 지정 설정이 컴퓨터 설정 보다 우선 하며 명령줄 옵션 레지스트리 설정 보다 우선 합니다.

## <a name="BKMK_CmdRef"></a>명령줄 참조 ㄱ-ㅎ
다음 ㄱ-ㅎ 메뉴에서 특정 Windows 명령에 대 한 정보를 찾기 위해 명령을 첫 글자를 클릭 하 고 명령 이름을 클릭 합니다.

[A](#BKMK_a) |
[B](#BKMK_b) | 
[C](#BKMK_c) | 
[D](#BKMK_d) | 
[E](#BKMK_e) | 
[F](#BKMK_f) | 
[G](#BKMK_g) | 
[H](#BKMK_h) | 
[I](#BKMK_i) |
[J](#BKMK_j) | 
[K](#BKMK_k) | 
[L](#BKMK_l) | 
[M](#BKMK_m) | 
[N](#BKMK_n) | 
[O](#BKMK_o) | 
[P](#BKMK_p) | 
[Q](#BKMK_q) | 
[R](#BKMK_r) | 
[S](#BKMK_s) | 
[T](#BKMK_t) | 
[U](#BKMK_u) | 
[V](#BKMK_v) | 
[W](#BKMK_w) | 
[X](#BKMK_x) | 
[Y](#BKMK_y) | 
[Z](#BKMK_z)

### <a name="BKMK_a"></a>A
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

### <a name="BKMK_b"></a>B
-   [bcdboot](bcdboot.md)
-   [bcdedit](bcdedit.md)
-   [bdehdcfg](bdehdcfg.md)
-   [bitsadmin](bitsadmin.md)
  -   [bitsadmin addfile](bitsadmin-addfile.md)
  -   [bitsadmin addfileset](bitsadmin-addfileset.md)
  -   [bitsadmin 0 인](bitsadmin-addfilewithranges.md)
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
  -   [bitsadmin 도움말](bitsadmin-help.md)
  -   [bitsadmin info](bitsadmin-info.md)
  -   [bitsadmin 목록](bitsadmin-list.md)
  -   [bitsadmin listfiles](bitsadmin-listfiles.md)
  -   [bitsadmin 모니터](bitsadmin-monitor.md)
  -   [bitsadmin nowrap](bitsadmin-nowrap.md)
  -   [bitsadmin rawreturn](bitsadmin-rawreturn.md)
  -   [bitsadmin removecredentials](bitsadmin-removecredentials.md)
  -   [bitsadmin replaceremoteprefix](bitsadmin-replaceremoteprefix.md)
  -   [bitsadmin 재설정](bitsadmin-reset.md)
  -   [bitsadmin 다시 시작](bitsadmin-resume.md)
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
  -   [bitsadmin 일시 중단](bitsadmin-suspend.md)
  -   [bitsadmin takeownership](bitsadmin-takeownership.md)
  -   [bitsadmin 전송](bitsadmin-transfer.md)
  -   [bitsadmin util](bitsadmin-util.md)
  -   [bitsadmin 줄 바꿈](bitsadmin-wrap.md)
-   [bootcfg](bootcfg.md)
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
-   [break](break_1.md)

### <a name="BKMK_c"></a>C
-   [cacls](cacls_1.md)
-   [call](call.md)
-   [cd](cd.md)
-   [certreq](certreq_1.md)
-   [certutil](certutil.md)
-   [change](change.md)
  -   [로그온 변경](change-logon.md)
  -   [포트 변경](change-port.md)
  -   [change user](change-user.md)
-   [chcp](chcp.md)
-   [chdir](chdir_1.md)
-   [chglogon](chglogon.md)
-   [chgport](chgport.md)
-   [chgusr](chgusr.md)
-   [chkdsk](chkdsk.md)
-   [chkntfs](chkntfs.md)
-   [choice](choice.md)
-   [cipher](cipher.md)
-   [clip](clip.md)
-   [cls](cls.md)
-   [Cmd](Cmd.md)
-   [cmdkey](cmdkey.md)
-   [cmstp](cmstp.md)
-   [color](color.md)
-   [comp](comp.md)
-   [compact](compact.md)
-   [convert](convert.md)
-   [copy](copy.md)
-   [cprofile](cprofile.md)
-   [cscript](cscript.md)

### <a name="BKMK_d"></a>D
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

### <a name="BKMK_e"></a>E
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

### <a name="BKMK_f"></a>F
-   [fc](fc.md)
-   [find](find.md)
-   [findstr](findstr.md)
-   [finger](finger.md)
-   [flattemp](flattemp.md)
-   [fondue](fondue.md)
-   [for](for.md)
-   [forfiles](forfiles.md)
-   [format](format.md)
-   [freedisk](freedisk.md)
-   [fsutil](fsutil.md)
  -   [fsutil 8dot3name](fsutil-8dot3name.md) 
  -   [fsutil 동작](fsutil-behavior.md) 
  -   [fsutil file](fsutil-file.md)
  -   [fsutil fsinfo](fsutil-fsinfo.md)
  -   [fsutil hardlink](fsutil-hardlink.md)
  -   [Fsutil objectid](fsutil-objectid.md)
  -   [fsutil quota](fsutil-quota.md)
  -   [fsutil 복구](fsutil-repair.md)
  -   [fsutil reparsepoint](fsutil-reparsepoint.md)
  -   [fsutil 리소스](fsutil-resource.md)
  -   [fsutil 스파스](fsutil-sparse.md)
  -   [Fsutil 계층화](fsutil-tiering.md)
  -   [fsutil 트랜잭션](fsutil-transaction.md)
  -   [fsutil usn](fsutil-usn.md)
  -   [fsutil volume](fsutil-volume.md)
  -   [fsutil wim](fsutil-wim.md)
-   [ftp](ftp.md)
-   [ftype](ftype.md)
-   [fveupdate](fveupdate.md)

### <a name="BKMK_g"></a>G
-   [getmac](getmac.md)
-   [gettype](gettype.md)
-   [goto](goto.md)
-   [gpfixup](gpfixup.md)
-   [gpresult](gpresult.md)
-   [gpupdate](gpupdate.md)
-   [graftabl](graftabl.md)

### <a name="BKMK_h"></a>H
-   [help](help.md)
-   [helpctr](helpctr.md)
-   [hostname](hostname.md)

### <a name="BKMK_i"></a>I
-   [icacls](icacls.md)
-   [if](if.md)
-   [inuse](inuse.md)
-   [ipconfig](ipconfig.md)
-   [ipxroute](ipxroute.md)
-   [irftp](irftp.md)

### <a name="BKMK_j"></a>J
-   [jetpack](jetpack.md)

### <a name="BKMK_k"></a>K
-   [klist](klist.md)
-   [ksetup](ksetup.md)
  -   [ksetup:setrealm](ksetup-setrealm.md)
  -   [ksetup:mapuser](ksetup-mapuser.md)
  -   [ksetup:addkdc](ksetup-addkdc.md)
  -   [ksetup:delkdc](ksetup-delkdc.md)
  -   [ksetup:addkpasswd](ksetup-addkpasswd.md)
  -   [ksetup:delkpasswd](ksetup-delkpasswd.md)
  -   [ksetup:server](ksetup-server.md)
  -   [ksetup:setcomputerpassword](ksetup-setcomputerpassword.md)
  -   [ksetup:removerealm](ksetup-removerealm.md)
  -   [ksetup:domain](ksetup-domain.md)
  -   [ksetup:changepassword](ksetup-changepassword.md)
  -   [ksetup:listrealmflags](ksetup-listrealmflags.md)
  -   [ksetup:setrealmflags](ksetup-setrealmflags.md)
  -   [ksetup:addrealmflags](ksetup-addrealmflags.md)
  -   [ksetup:delrealmflags](ksetup-delrealmflags.md)
  -   [ksetup:dumpstate](ksetup-dumpstate.md)
  -   [ksetup:addhosttorealmmap](ksetup-addhosttorealmmap.md)
  -   [ksetup:delhosttorealmmap](ksetup-delhosttorealmmap.md)
  -   [ksetup:setenctypeattr](ksetup-setenctypeattr.md)
  -   [ksetup:getenctypeattr](ksetup-getenctypeattr.md)
  -   [ksetup:addenctypeattr](ksetup-addenctypeattr.md)
  -   [ksetup:delenctypeattr](ksetup-delenctypeattr.md) 
-   [ktmutil](ktmutil.md)
-   [ktpass](ktpass.md)

### <a name="BKMK_l"></a>L
-   [label](label.md)
-   [lodctr](lodctr.md)
-   [logman](logman.md)
  -   [logman 만들기](logman-create.md)
  -   [logman 쿼리](logman-query.md)
  -   [logman 시작 & 124; 중지](logman-start-stop.md)
  -   [logman 삭제](logman-delete.md)
  -   [logman 업데이트](logman-update.md)
  -   [logman 가져오기 및 124; 내보내기](logman-import-export.md)
-   [logoff](logoff.md)
-   [lpq](lpq.md)
-   [lpr](lpr.md)

### <a name="BKMK_m"></a>M
-   [macfile](macfile.md)
-   [makecab](makecab.md)
-   [manage-bde](manage-bde.md)
  -   [관리 bde: 상태](manage-bde-status.md)
  -   [관리 bde:에](manage-bde-on.md)
  -   [관리 bde: 해제](manage-bde-off.md)
  -   [관리 bde: 일시 중지](manage-bde-pause.md)
  -   [관리 bde: 다시 시작](manage-bde-resume.md)
  -   [관리 bde: 잠금](manage-bde-lock.md)
  -   [관리 bde: 잠금 해제](manage-bde-unlock.md)
  -   [관리 bde: 잠금](manage-bde-autounlock.md)
  -   [관리 bde: 보호기](manage-bde-protectors.md)
  -   [관리 bde: tpm](manage-bde-tpm.md)
  -   [관리 bde: setidentifier](manage-bde-setidentifier.md)
  -   [manage-bde: ForceRecovery](manage-bde-forcerecovery.md)
  -   [관리 bde: 암호 변경](manage-bde-changepassword.md)
  -   [관리 bde: changepin](manage-bde-changepin.md)
  -   [관리 bde: 변환](manage-bde-changekey.md)
  -   [manage-bde: KeyPackage](manage-bde-keypackage.md)
  -   [관리 bde: 업그레이드](manage-bde-upgrade.md)
  -   [manage-bde: WipeFreeSpace](manage-bde-wipefreespace.md)
-   [mapadmin](mapadmin.md)
-   [Md](Md.md)
-   [mkdir](mkdir.md)
-   [mklink](mklink.md)
-   [mmc](mmc.md)
-   [mode](mode.md)
-   [more](more.md)
-   [mount](mount.md)
-   [mountvol](mountvol.md)
-   [move](move.md)
-   [mqbkup](mqbkup.md)
-   [mqsvc](mqsvc.md)
-   [mqtgsvc](mqtgsvc.md)
-   [msdt](msdt.md)
-   [msg](msg.md)
-   [msiexec](msiexec.md)
-   [msinfo32](msinfo32.md)
-   [mstsc](mstsc.md)

### <a name="BKMK_n"></a>N
-   [nbtstat](nbtstat.md)
-   [netcfg](netcfg.md)
-   [netsh](netsh.md)
-   [netstat](netstat.md)
-   [Net 인쇄](net-print.md)
-   [nfsadmin](nfsadmin.md)
-   [nfsshare](nfsshare.md)
-   [nfsstat](nfsstat.md)
-   [nlbmgr](nlbmgr.md)
-   [nslookup](nslookup.md)
  -   [nslookup exit 명령](nslookup-exit-command.md)
  -   [nslookup 손가락 명령](nslookup-finger-command.md)
  -   [nslookup 도움말](nslookup-help.md)
  -   [nslookup ls](nslookup-ls.md)
  -   [nslookup lserver](nslookup-lserver.md)
  -   [nslookup root](nslookup-root.md)
  -   [nslookup server](nslookup-server.md)
  -   [nslookup set](nslookup-set.md)
  -   [nslookup set all](nslookup-set-all.md)
  -   [nslookup set 클래스](nslookup-set-class.md)
  -   [nslookup set d2](nslookup-set-d2.md)
  -   [nslookup set debug](nslookup-set-debug.md)
  -   [nslookup 도메인 설정](nslookup-set-domain.md)
  -   [nslookup set port](nslookup-set-port.md)
  -   [nslookup set querytype](nslookup-set-querytype.md)
  -   [nslookup set recurse](nslookup-set-recurse.md)
  -   [nslookup set retry](nslookup-set-retry.md)
  -   [nslookup 세트 루트](nslookup-set-root.md)
  -   [nslookup 집합 검색](nslookup-set-search.md)
  -   [nslookup set srchlist](nslookup-set-srchlist.md)
  -   [nslookup set timeout](nslookup-set-timeout.md)
  -   [nslookup 유형 설정](nslookup-set-type.md)
  -   [nslookup set vc](nslookup-set-vc.md)
  -   [nslookup 보기](nslookup-view.md)
-   [ntbackup](ntbackup.md)
-   [ntcmdprompt](ntcmdprompt.md)
-   [ntfrsutl](ntfrsutl.md)

### <a name="BKMK_o"></a>O
-   [openfiles](openfiles.md)

### <a name="BKMK_p"></a>P
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

### <a name="BKMK_q"></a>Q
-   [qappsrv](qappsrv.md)
-   [qprocess](qprocess.md)
-   [query](query.md)
-   [quser](quser.md)
-   [qwinsta](qwinsta.md)

### <a name="BKMK_r"></a>R
-   [rcp](rcp.md)
-   [rd](rd.md)
-   [rdpsign](rdpsign.md)
-   [recover](recover.md)
-   [reg](reg.md)
  -   [Reg 추가](reg-add.md)
  -   [reg 비교](reg-compare.md)
  -   [reg copy](reg-copy.md)
  -   [reg delete](reg-delete.md)
  -   [reg export](reg-export.md)
  -   [reg import](reg-import.md)
  -   [Reg 부하](reg-load.md)
  -   [reg query](reg-query.md)
  -   [reg 복원](reg-restore.md)
  -   [reg 저장](reg-save.md)
  -   [Reg 언로드](reg-unload.md)
-   [regini](regini.md)
-   [regsvr32](regsvr32.md)
-   [relog](relog.md)
-   [rem](rem.md)
-   [ren](ren.md)
-   [rename](rename.md)
-   [repair-bde](repair-bde.md)
-   [replace](replace.md)
-   [세션 다시 설정](reset-session.md)
-   [rexec](rexec.md)
-   [risetup](risetup.md)
-   [rmdir](rmdir.md)
-   [robocopy](robocopy.md)
-   [route_ws2008](route_ws2008.md)
-   [rpcinfo](rpcinfo.md)
-   [rpcping](rpcping.md)
-   [rsh](rsh.md)
-   [rundll32](rundll32.md)
-   [rwinsta](rwinsta.md)

### <a name="BKMK_s"></a>S
-   [schtasks](schtasks.md)
-   [scwcmd](Scwcmd.md)
  -   [scwcmd: analyze](scwcmd-analyze.md)
  -   [scwcmd: configure](scwcmd-configure.md)
  -   [scwcmd: register](scwcmd-register.md) 
  -   [scwcmd: rollback](scwcmd-rollback.md) 
  -   [scwcmd: transform](scwcmd-transform.md) 
  -   [scwcmd: view](scwcmd-view.md) 
-   [secedit](secedit.md)
  -   [secedit:analyze](secedit-analyze.md)
  -   [secedit:configure](secedit-configure.md)
  -   [secedit:export](secedit-export.md)
  -   [secedit:generaterollback](secedit-generaterollback.md)
  -   [secedit:import](secedit-import.md)
  -   [secedit:validate](secedit-validate.md)
-   [serverceipoptin](serverceipoptin.md)
-   [Servermanagercmd](Servermanagercmd.md)
-   [serverweroptin](serverweroptin.md)
-   [set](set_1.md)
-   [setlocal](setlocal.md)
-   [setx](setx.md)
-   [sfc](sfc.md)
-   [shadow](shadow.md)
-   [shift](shift.md)
-   [showmount](showmount.md)
-   [shutdown](shutdown.md)
-   [sort](sort.md)
-   [start](start.md)
-   [subst](subst.md)
-   [sxstrace](sxstrace.md)
-   [sysocmgr](sysocmgr.md)
-   [systeminfo](systeminfo.md)

### <a name="BKMK_t"></a>T
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

### <a name="BKMK_u"></a>U
-   [unlodctr](unlodctr_1.md)

### <a name="BKMK_v"></a>V
-   [ver](ver.md)
-   [verifier](verifier.md)
-   [verify](verify_1.md)
-   [vol](vol.md)
-   [vssadmin](vssadmin.md)- 

### <a name="BKMK_w"></a>W
-   [waitfor](waitfor.md)
-   [wbadmin](wbadmin.md)
  -   [wbadmin 백업 사용](wbadmin-enable-backup.md)
  -   [wbadmin 백업 사용 안 함](wbadmin-disable-backup.md)
  -   [wbadmin 백업 시작](wbadmin-start-backup.md)
  -   [wbadmin stop job](wbadmin-stop-job.md)
  -   [wbadmin get 버전](wbadmin-get-versions.md)
  -   [wbadmin get items](wbadmin-get-items.md)
  -   [wbadmin 시작 복구](wbadmin-start-recovery.md)
  -   [wbadmin get status](wbadmin-get-status.md)
  -   [wbadmin get 디스크](wbadmin-get-disks.md)
  -   [wbadmin 시작 systemstaterecovery](wbadmin-start-systemstaterecovery.md)
  -   [wbadmin 시작 systemstatebackup](wbadmin-start-systemstatebackup.md)
  -   [wbadmin delete systemstatebackup](wbadmin-delete-systemstatebackup.md)
  -   [wbadmin 시작 sysrecovery](wbadmin-start-sysrecovery.md)
  -   [wbadmin 복원 카탈로그](wbadmin-restore-catalog.md)
  -   [wbadmin delete 카탈로그](wbadmin-delete-catalog.md)
-   [wdsutil](wdsutil.md)
-   [wecutil](wecutil.md)
-   [wevtutil](wevtutil.md)
-   [where](where_1.md)
-   [whoami](whoami.md)
-   [winnt](winnt.md)
-   [winnt32](winnt32.md)
-   [winpop](winpop.md)
-   [winrs](winrs.md)
-   [wlbs](wlbs_1.md)
-   [wmic](wmic.md)
-   [wscript](wscript.md)

### <a name="BKMK_x"></a>X
-   [xcopy](xcopy.md)
