---
title: Windows 명령
description: 참조
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c703d07c-8227-4e86-94a6-8ef390f94cdc
author: jasongerend
ms.author: jgerend
manager: dongill
ms.date: 06/09/2020
ms.prod: windows-server
ms.openlocfilehash: 66de80652f764840af70e88dfd39df2398ae495c
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721118"
---
# <a name="windows-commands"></a>Windows 명령

지원 되는 모든 버전의 Windows (서버 및 클라이언트)에는에서 기본 제공 되는 Win32 콘솔 명령 집합이 있습니다.

이 설명서 집합에서는 스크립트나 스크립팅 도구를 사용 하 여 작업을 자동화 하는 데 사용할 수 있는 Windows 명령을 설명 합니다.

다음 ㄱ-ㅎ 메뉴에서 특정 명령에 대 한 정보를 찾기 위해 명령을 첫 글자를 클릭 하 고 명령 이름을 클릭 합니다.

[A](#a)  |
 [B](#b)  |
 [C](#c)  |
 [D](#d)  |
 [E](#e)  |
 [F](#f)  |
 [G](#g)  |
 [H](#h)  |
 [I](#i)  |
 [J](#j)  |
 [K](#k)  |
 [L](#l)  |
 [M](#m)  |
 [N](#n)  |
 [O](#o)  |
 [P](#p)  |
 [Q](#q)  |
 [R](#r)  |
 [S](#s)  |
 [T](#t)  |
 [U](#u)  |
 [V](#v)  |
 [W](#w)  |
 [X](#x) | Y | -

## <a name="prerequisites"></a>필수 조건

이 항목에 포함 된 정보는 다음에 적용 됩니다.

- Windows Server 2019
- Windows Server(반기 채널)
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2
- Windows Server 2008
- Windows 10
- Windows 8.1

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

[A](#a)  |
 [B](#b)  |
 [C](#c)  |
 [D](#d)  |
 [E](#e)  |
 [F](#f)  |
 [G](#g)  |
 [H](#h)  |
 [I](#i)  |
 [J](#j)  |
 [K](#k)  |
 [L](#l)  |
 [M](#m)  |
 [N](#n)  |
 [O](#o)  |
 [P](#p)  |
 [Q](#q)  |
 [R](#r)  |
 [S](#s)  |
 [T](#t)  |
 [U](#u)  |
 [V](#v)  |
 [W](#w)  |
 [X](#x) | Y | -

### <a name="a"></a>A

- [active](active.md)
- [add](add.md)
- [add alias](add-alias.md)
- [add volume](add-volume.md)
- [append](append.md)
- [arp](arp.md)
- [assign](assign.md)
- [assoc](assoc.md)
- [at](at.md)
- [atmadm](atmadm.md)
- [attach-vdisk](attach-vdisk.md)
- [attrib](attrib.md)
- [attributes](attributes.md)
  - [attributes disk](attributes-disk.md)
  - [attributes volume](attributes-volume.md)
- [auditpol](auditpol.md)
  - [auditpol backup](auditpol-backup.md)
  - [auditpol clear](auditpol-clear.md)
  - [auditpol get](auditpol-get.md)
  - [auditpol list](auditpol-list.md)
  - [auditpol remove](auditpol-remove.md)
  - [auditpol resourcesacl](auditpol-resourcesacl.md)
  - [auditpol restore](auditpol-restore.md)
  - [auditpol set](auditpol-set.md)
- [autochk](autochk.md)
- [autoconv](autoconv.md)
- [autofmt](autofmt.md)
- [automount](automount.md)

### <a name="b"></a>b

- [bcdboot](bcdboot.md)
- [bcdedit](bcdedit.md)
- [bdehdcfg](bdehdcfg.md)
  - [bdehdcfg driveinfo](bdehdcfg-driveinfo.md)
  - [bdehdcfg newdriveletter](bdehdcfg-newdriveletter.md)
  - [bdehdcfg quiet](bdehdcfg-quiet.md)
  - [bdehdcfg restart](bdehdcfg-restart.md)
  - [bdehdcfg size](bdehdcfg-size.md)
  - [bdehdcfg target](bdehdcfg-target.md)
- [begin backup](begin-backup.md)
- [begin restore](begin-restore.md)
- [bitsadmin](bitsadmin.md)
  - [bitsadmin addfile](bitsadmin-addfile.md)
  - [bitsadmin addfileset](bitsadmin-addfileset.md)
  - [bitsadmin addfilewithranges](bitsadmin-addfilewithranges.md)
  - [bitsadmin cache](bitsadmin-cache.md)
    - [bitsadmin cache and delete](bitsadmin-cache-and-delete.md)
    - [bitsadmin cache and deleteurl](bitsadmin-cache-and-deleteurl.md)
    - [bitsadmin cache and getexpirationtime](bitsadmin-cache-and-getexpirationtime.md)
    - [bitsadmin cache and getlimit](bitsadmin-cache-and-getlimit.md)
    - [bitsadmin cache and help](bitsadmin-cache-and-help.md)
    - [bitsadmin cache and info](bitsadmin-cache-and-info.md)
    - [bitsadmin cache and list](bitsadmin-cache-and-list.md)
    - [bitsadmin cache and setexpirationtime](bitsadmin-cache-and-setexpirationtime.md)
    - [bitsadmin cache and setlimit](bitsadmin-cache-and-setlimit.md)
    - [bitsadmin cache and clear](bitsadmin-cache-clear.md)
  - [bitsadmin cancel](bitsadmin-cancel.md)
  - [bitsadmin complete](bitsadmin-complete.md)
  - [bitsadmin create](bitsadmin-create.md)
  - [bitsadmin examples](bitsadmin-examples.md)
  - [bitsadmin getaclflags](bitsadmin-getaclflags.md)
  - [bitsadmin getbytestotal](bitsadmin-getbytestotal.md)
  - [bitsadmin getbytestransferred](bitsadmin-getbytestransferred.md)
  - [bitsadmin getclientcertificate](bitsadmin-getclientcertificate.md)
  - [bitsadmin getcompletiontime](bitsadmin-getcompletiontime.md)
  - [bitsadmin getcreationtime](bitsadmin-getcreationtime.md)
  - [bitsadmin getcustomheaders](bitsadmin-getcustomheaders.md)
  - [bitsadmin getdescription](bitsadmin-getdescription.md)
  - [bitsadmin getdisplayname](bitsadmin-getdisplayname.md)
  - [bitsadmin geterror](bitsadmin-geterror.md)
  - [bitsadmin geterrorcount](bitsadmin-geterrorcount.md)
  - [bitsadmin getfilestotal](bitsadmin-getfilestotal.md)
  - [bitsadmin getfilestransferred](bitsadmin-getfilestransferred.md)
  - [bitsadmin gethelpertokenflags](bitsadmin-gethelpertokenflags.md)
  - [bitsadmin gethelpertokensid](bitsadmin-gethelpertokensid.md)
  - [bitsadmin gethttpmethod](bitsadmin-gethttpmethod.md)
  - [bitsadmin getmaxdownloadtime](bitsadmin-getmaxdownloadtime.md)
  - [bitsadmin getminretrydelay](bitsadmin-getminretrydelay.md)
  - [bitsadmin getmodificationtime](bitsadmin-getmodificationtime.md)
  - [bitsadmin getnoprogresstimeout](bitsadmin-getnoprogresstimeout.md)
  - [bitsadmin getnotifycmdline](bitsadmin-getnotifycmdline.md)
  - [bitsadmin getnotifyflags](bitsadmin-getnotifyflags.md)
  - [bitsadmin getnotifyinterface](bitsadmin-getnotifyinterface.md)
  - [bitsadmin getowner](bitsadmin-getowner.md)
  - [bitsadmin getpeercachingflags](bitsadmin-getpeercachingflags.md)
  - [bitsadmin getpriority](bitsadmin-getpriority.md)
  - [bitsadmin getproxybypasslist](bitsadmin-getproxybypasslist.md)
  - [bitsadmin getproxylist](bitsadmin-getproxylist.md)
  - [bitsadmin getproxyusage](bitsadmin-getproxyusage.md)
  - [bitsadmin getreplydata](bitsadmin-getreplydata.md)
  - [bitsadmin getreplyfilename](bitsadmin-getreplyfilename.md)
  - [bitsadmin getreplyprogress](bitsadmin-getreplyprogress.md)
  - [bitsadmin getsecurityflags](bitsadmin-getsecurityflags.md)
  - [bitsadmin getstate](bitsadmin-getstate.md)
  - [bitsadmin gettemporaryname](bitsadmin-gettemporaryname.md)
  - [bitsadmin gettype](bitsadmin-gettype.md)
  - [bitsadmin getvalidationstate](bitsadmin-getvalidationstate.md)
  - [bitsadmin help](bitsadmin-help.md)
  - [bitsadmin info](bitsadmin-info.md)
  - [bitsadmin list](bitsadmin-list.md)
  - [bitsadmin listfiles](bitsadmin-listfiles.md)
  - [bitsadmin makecustomheaderswriteonly](bitsadmin-makecustomheaderswriteonly.md)
  - [bitsadmin monitor](bitsadmin-monitor.md)
  - [bitsadmin nowrap](bitsadmin-nowrap.md)
  - [bitsadmin peercaching](bitsadmin-peercaching.md)
    - [bitsadmin peercaching and getconfigurationflags](bitsadmin-peercaching-and-getconfigurationflags.md)
    - [bitsadmin peercaching and help](bitsadmin-peercaching-and-help.md)
    - [bitsadmin peercaching and setconfigurationflags](bitsadmin-peercaching-and-setconfigurationflags.md)
  - [bitsadmin peers](bitsadmin-peers.md)
    - [bitsadmin peers and clear](bitsadmin-peers-and-clear.md)
    - [bitsadmin peers and discover](bitsadmin-peers-and-discover.md)
    - [bitsadmin peers and help](bitsadmin-peers-and-help.md)
    - [bitsadmin peers and list](bitsadmin-peers-and-list.md)
  - [bitsadmin rawreturn](bitsadmin-rawreturn.md)
  - [bitsadmin removeclientcertificate](bitsadmin-removeclientcertificate.md)
  - [bitsadmin removecredentials](bitsadmin-removecredentials.md)
  - [bitsadmin replaceremoteprefix](bitsadmin-replaceremoteprefix.md)
  - [bitsadmin reset](bitsadmin-reset.md)
  - [bitsadmin resume](bitsadmin-resume.md)
  - [bitsadmin setaclflag](bitsadmin-setaclflag.md)
  - [bitsadmin setclientcertificatebyid](bitsadmin-setclientcertificatebyid.md)
  - [bitsadmin setclientcertificatebyname](bitsadmin-setclientcertificatebyname.md)
  - [bitsadmin setcredentials](bitsadmin-setcredentials.md)
  - [bitsadmin setcustomheaders](bitsadmin-setcustomheaders.md)
  - [bitsadmin setdescription](bitsadmin-setdescription.md)
  - [bitsadmin setdisplayname](bitsadmin-setdisplayname.md)
  - [bitsadmin sethelpertoken](bitsadmin-sethelpertoken.md)
  - [bitsadmin sethelpertokenflags](bitsadmin-sethelpertokenflags.md)
  - [bitsadmin sethttpmethod](bitsadmin-sethttpmethod.md)
  - [bitsadmin setmaxdownloadtime](bitsadmin-setmaxdownloadtime.md)
  - [bitsadmin setminretrydelay](bitsadmin-setminretrydelay.md)
  - [bitsadmin setnoprogresstimeout](bitsadmin-setnoprogresstimeout.md)
  - [bitsadmin setnotifycmdline](bitsadmin-setnotifycmdline.md)
  - [bitsadmin setnotifyflags](bitsadmin-setnotifyflags.md)
  - [bitsadmin setpeercachingflags](bitsadmin-setpeercachingflags.md)
  - [bitsadmin setpriority](bitsadmin-setpriority.md)
  - [bitsadmin setproxysettings](bitsadmin-setproxysettings.md)
  - [bitsadmin setreplyfilename](bitsadmin-setreplyfilename.md)
  - [bitsadmin setsecurityflags](bitsadmin-setsecurityflags.md)
  - [bitsadmin setvalidationstate](bitsadmin-setvalidationstate.md)
  - [bitsadmin suspend](bitsadmin-suspend.md)
  - [bitsadmin takeownership](bitsadmin-takeownership.md)
  - [bitsadmin transfer](bitsadmin-transfer.md)
  - [bitsadmin util](bitsadmin-util.md)
    - [bitsadmin util and enableanalyticchannel](bitsadmin-util-and-enableanalyticchannel.md)
    - [bitsadmin util and getieproxy](bitsadmin-util-and-getieproxy.md)
    - [bitsadmin util and help](bitsadmin-util-and-help.md)
    - [bitsadmin util and repairservice](bitsadmin-util-and-repairservice.md)
    - [bitsadmin util and setieproxy](bitsadmin-util-and-setieproxy.md)
    - [bitsadmin util and version](bitsadmin-util-and-version.md)
  - [bitsadmin wrap](bitsadmin-wrap.md)
- [bootcfg](bootcfg.md)
  - [bootcfg addsw](bootcfg-addsw.md)
  - [bootcfg copy](bootcfg-copy.md)
  - [bootcfg dbg1394](bootcfg-dbg1394.md)
  - [bootcfg debug](bootcfg-debug.md)
  - [bootcfg default](bootcfg-default.md)
  - [bootcfg delete](bootcfg-delete.md)
  - [bootcfg ems](bootcfg-ems.md)
  - [bootcfg query](bootcfg-query.md)
  - [bootcfg raw](bootcfg-raw.md)
  - [bootcfg rmsw](bootcfg-rmsw.md)
  - [bootcfg timeout](bootcfg-timeout.md)
- [break](break_1.md)

### <a name="c"></a>C

- [cacls](cacls.md)
- [call](call.md)
- [cd](cd.md)
- [certreq](certreq_1.md)
- [certutil](certutil.md)
- [change](change.md)
  - [change logon](change-logon.md)
  - [change port](change-port.md)
  - [change user](change-user.md)
- [chcp](chcp.md)
- [chdir](chdir.md)
- [chglogon](chglogon.md)
- [chgport](chgport.md)
- [chgusr](chgusr.md)
- [chkdsk](chkdsk.md)
- [chkntfs](chkntfs.md)
- [choice](choice.md)
- [cipher](cipher.md)
- [clean](clean.md)
- [cleanmgr](cleanmgr.md)
- [clip](clip.md)
- [cls](cls.md)
- [cmd](Cmd.md)
- [cmdkey](cmdkey.md)
- [cmstp](cmstp.md)
- [color](color.md)
- [comp](comp.md)
- [compact](compact.md)
- [compact vdisk](compact-vdisk.md)
- [convert](convert.md)
  - [convert basic](convert-basic.md)
  - [동적 변환](convert-dynamic.md)
  - [convert gpt](convert-gpt.md)
  - [convert mbr](convert-mbr.md)
- [copy](copy.md)
- [cprofile](cprofile.md)
- [create](create.md)
  - [파티션 efi 만들기](create-partition-efi.md)
  - [ [확장 된 파티션](create-partition-extended.md) 만들기
  - [논리적 파티션 만들기](create-partition-logical.md)
  - [파티션 msr 만들기](create-partition-msr.md)
  - [파티션 기본 만들기](create-partition-primary.md)
  - [볼륨 미러 만들기](create-volume-mirror.md)
  - [볼륨 raid 만들기](create-volume-raid.md)
  - [단순 볼륨 만들기](create-volume-simple.md)
  - [볼륨 스트라이프 만들기](create-volume-stripe.md)
- [cscript](cscript.md)

### <a name="d"></a>D

- [date](date.md)
- [dcgpofix](dcgpofix.md)
- [defrag](defrag.md)
- [del](del.md)
- [delete](delete.md)
  - [디스크 삭제](delete-disk.md)
  - [파티션 삭제](delete-partition.md)
  - [그림자 삭제](delete-shadows.md)
  - [delete volume](delete-volume.md)
- [분리 vdisk](detach-vdisk.md)
- [세부 정보](detail.md)
  - [디스크 세부 정보](detail-disk.md)
  - [세부 정보 파티션](detail-partition.md)
  - [세부 정보 vdisk](detail-vdisk.md)
  - [세부 정보 볼륨](detail-volume.md)
- [dfsdiag](dfsdiag.md)
  - [dfsdiag testdcs](dfsdiag-testdcs.md)
  - [dfsdiag testdfs 구성](dfsdiag-testdfsconfig.md)
  - [dfsdiag testdfs 무결성](dfsdiag-testdfsintegrity.md)
  - [dfsdiag testreferral](dfsdiag-testreferral.md)
  - [dfsdiag testsites](dfsdiag-testsites.md)
- [dfsrmig](dfsrmig.md)
- [diantz](diantz.md)
- [dir](dir.md)
- [diskcomp](diskcomp.md)
- [diskcopy](diskcopy.md)
- [diskpart](diskpart.md)
- [diskperf](diskperf.md)
- [diskraid](diskraid.md)
- [diskshadow](diskshadow.md)
- [dispdiag](dispdiag.md)
- [dnscmd](dnscmd.md)
- [doskey](doskey.md)
- [driverquery](driverquery.md)

### <a name="e"></a>E

- [echo](echo.md)
- [edit](edit.md)
- [endlocal](endlocal.md)
- [복원 종료](end-restore.md)
- [erase](erase.md)
- [eventcreate](eventcreate.md)
- [eventquery](eventquery.md)
- [eventtriggers](eventtriggers.md)
- [Evntcmd](evntcmd.md)
- [exec](exec.md)
- [exit](exit_2.md)
- [expand](expand.md)
- [vdisk 확장](expand-vdisk.md)
- [노출](expose.md)
- [넘으면](extend.md)
- [extract](extract.md)

### <a name="f"></a>F

- [fc](fc.md)
- [filesystems](filesystems.md)
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
  - [fsutil 8dot3name](fsutil-8dot3name.md)
  - [fsutil behavior](fsutil-behavior.md)
  - [fsutil dirty](fsutil-dirty.md)
  - [fsutil file](fsutil-file.md)
  - [fsutil fsinfo](fsutil-fsinfo.md)
  - [fsutil hardlink](fsutil-hardlink.md)
  - [fsutil objectid](fsutil-objectid.md)
  - [fsutil quota](fsutil-quota.md)
  - [fsutil repair](fsutil-repair.md)
  - [fsutil reparsepoint](fsutil-reparsepoint.md)
  - [fsutil resource](fsutil-resource.md)
  - [fsutil sparse](fsutil-sparse.md)
  - [fsutil tiering](fsutil-tiering.md)
  - [fsutil transaction](fsutil-transaction.md)
  - [fsutil usn](fsutil-usn.md)
  - [fsutil volume](fsutil-volume.md)
  - [fsutil wim](fsutil-wim.md)
- [ftp](ftp.md)
  - [ftp append](ftp-append.md)
  - [ftp ascii](ftp-ascii.md)
  - [ftp bell](ftp-bell_1.md)
  - [ftp binary](ftp-binary.md)
  - [ftp bye](ftp-bye.md)
  - [ftp cd](ftp-cd.md)
  - [ftp close](ftp-close_1.md)
  - [ftp debug](ftp-debug.md)
  - [ftp delete](ftp-delete.md)
  - [ftp dir](ftp-dir.md)
  - [ftp disconnect](ftp-disconnect_1.md)
  - [ftp get](ftp-get.md)
  - [ftp glob](ftp-glob_1.md)
  - [ftp hash](ftp-hash_1.md)
  - [ftp lcd](ftp-lcd.md)
  - [ftp literal](ftp-literal_1.md)
  - [ftp ls](ftp-ls_1.md)
  - [ftp mget](ftp-mget.md)
  - [ftp mkdir](ftp-mkdir.md)
  - [ftp mls](ftp-mls_1.md)
  - [ftp mput](ftp-mput_1.md)
  - [ftp open](ftp-open_1.md)
  - [ftp prompt](ftp-prompt_1.md)
  - [ftp put](ftp-put.md)
  - [ftp pwd](ftp-pwd_1.md)
  - [ftp quit](ftp-quit.md)
  - [ftp quote](ftp-quote.md)
  - [ftp recv](ftp-recv.md)
  - [ftp remotehelp](ftp-remotehelp_1.md)
  - [ftp rename](ftp-rename.md)
  - [ftp rmdir](ftp-rmdir.md)
  - [ftp send](ftp-send_1.md)
  - [ftp status](ftp-status.md)
  - [ftp trace](ftp-trace_1.md)
  - [ftp type](ftp-type.md)
  - [ftp user](ftp-user.md)
  - [ftp verbose](ftp-verbose_1.md)
  - [ftp mdelete](ftp-.mdelete_1.md)
  - [ftp mdir](ftp.mdir.md)
- [ftype](ftype.md)
- [fveupdate](fveupdate.md)

### <a name="g"></a>G

- [getmac](getmac.md)
- [gettype](gettype.md)
- [goto](goto.md)
- [gpfixup](gpfixup.md)
- [gpresult](gpresult.md)
- [gpt](gpt.md)
- [gpupdate](gpupdate.md)
- [graftabl](graftabl.md)

### <a name="h"></a>H

- [help](help.md)
- [helpctr](helpctr.md)
- [hostname](hostname.md)

### <a name="i"></a>I

- [icacls](icacls.md)
- [if](if.md)
- [가져오기 (shadowdisk)](import.md)
- [가져오기 (diskpart)](import_1.md)
- [inactive](inactive.md)
- [inuse](inuse.md)
- [ipconfig](ipconfig.md)
- [ipxroute](ipxroute.md)
- [irftp](irftp.md)

### <a name="j"></a>J

- [jetpack](jetpack.md)

### <a name="k"></a>K

- [klist](klist.md)
- [ksetup](ksetup.md)
  - [ksetup addenctypeattr](ksetup-addenctypeattr.md)
  - [ksetup addhosttorealmmap](ksetup-addhosttorealmmap.md)
  - [ksetup addkdc](ksetup-addkdc.md)
  - [ksetup addkpasswd](ksetup-addkpasswd.md)
  - [ksetup addrealmflags](ksetup-addrealmflags.md)
  - [ksetup changepassword](ksetup-changepassword.md)
  - [ksetup delenctypeattr](ksetup-delenctypeattr.md)
  - [ksetup delhosttorealmmap](ksetup-delhosttorealmmap.md)
  - [ksetup delkdc](ksetup-delkdc.md)
  - [ksetup delkpasswd](ksetup-delkpasswd.md)
  - [ksetup delrealmflags](ksetup-delrealmflags.md)
  - [ksetup domain](ksetup-domain.md)
  - [ksetup dumpstate](ksetup-dumpstate.md)
  - [ksetup getenctypeattr](ksetup-getenctypeattr.md)
  - [ksetup listrealmflags](ksetup-listrealmflags.md)
  - [ksetup mapuser](ksetup-mapuser.md)
  - [ksetup removerealm](ksetup-removerealm.md)
  - [ksetup server](ksetup-server.md)
  - [ksetup setcomputerpassword](ksetup-setcomputerpassword.md)
  - [ksetup setenctypeattr](ksetup-setenctypeattr.md)
  - [ksetup setrealm](ksetup-setrealm.md)
  - [ksetup setrealmflags](ksetup-setrealmflags.md)
- [ktmutil](ktmutil.md)
- [ktpass](ktpass.md)

### <a name="l"></a>L

- [label](label.md)
- [list](list.md)
  - [목록 공급자](list-providers.md)
  - [섀도 목록 표시](list-shadows.md)
  - [작성기 나열](list-writers.md)
- [메타 데이터 로드](load-metadata.md)
- [lodctr](lodctr.md)
- [logman](logman.md)
  - [logman create](logman-create.md)
  - [logman 경고 만들기](logman-create-alert.md)
  - [logman api 만들기](logman-create-api.md)
  - [logman cfg 만들기](logman-create-cfg.md)
  - [logman 카운터 만들기](logman-create-counter.md)
  - [logman 추적 만들기](logman-create-trace.md)
  - [logman delete](logman-delete.md)
  - [logman 가져오기 및 logman 내보내기](logman-import-export.md)
  - [logman query](logman-query.md)
  - [logman start 및 logman stop](logman-start-stop.md)
  - [logman update](logman-update.md)
  - [logman 업데이트 경고](logman-update-alert.md)
  - [logman api를 업데이트 합니다.](logman-update-api.md)
  - [logman update cfg](logman-update-cfg.md)
  - [logman 업데이트 카운터](logman-update-counter.md)
  - [logman update trace](logman-update-trace.md)
- [logoff](logoff.md)
- [lpq](lpq.md)
- [lpr](lpr.md)

### <a name="m"></a>M

- [macfile](macfile.md)
- [makecab](makecab.md)
- [manage-bde 관리](manage-bde.md)
  - [manage-bde 상태 관리](manage-bde-status.md)
  - [manage-bde on 관리](manage-bde-on.md)
  - [manage-bde off 관리](manage-bde-off.md)
  - [manage-bde 일시 중지 관리](manage-bde-pause.md)
  - [manage-bde resume 관리](manage-bde-resume.md)
  - [manage-bde 잠금 관리](manage-bde-lock.md)
  - [manage-bde 잠금 해제 관리](manage-bde-unlock.md)
  - [manage-bde autounlock 관리](manage-bde-autounlock.md)
  - [manage-bde 보호기 관리](manage-bde-protectors.md)
  - [manage-bde tpm 관리](manage-bde-tpm.md)
  - [manage-bde setidentifier 관리](manage-bde-setidentifier.md)
  - [manage-bde forcerecovery 관리](manage-bde-forcerecovery.md)
  - [manage-bde changepassword 관리](manage-bde-changepassword.md)
  - [manage-bde changepin 관리](manage-bde-changepin.md)
  - [manage-bde 변환 관리](manage-bde-changekey.md)
  - [manage-bde keypackage 관리](manage-bde-keypackage.md)
  - [manage-bde 업그레이드 관리](manage-bde-upgrade.md)
  - [manage-bde wipefreespace 관리](manage-bde-wipefreespace.md)
- [mapadmin](mapadmin.md)
- [md](md.md)
- [merge vdisk](merge-vdisk.md)
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
- [net 인쇄](net-print.md)
- [netsh](netsh.md)
- [netstat](netstat.md)
- [nfsadmin](nfsadmin.md)
- [nfsshare](nfsshare.md)
- [nfsstat](nfsstat.md)
- [nlbmgr](nlbmgr.md)
- [nslookup](nslookup.md)
  - [nslookup exit Command](nslookup-exit-command.md)
  - [nslookup finger Command](nslookup-finger-command.md)
  - [nslookup help](nslookup-help.md)
  - [nslookup ls](nslookup-ls.md)
  - [nslookup lserver](nslookup-lserver.md)
  - [nslookup root](nslookup-root.md)
  - [nslookup server](nslookup-server.md)
  - [nslookup set](nslookup-set.md)
  - [nslookup set all](nslookup-set-all.md)
  - [nslookup set class](nslookup-set-class.md)
  - [nslookup set d2](nslookup-set-d2.md)
  - [nslookup set debug](nslookup-set-debug.md)
  - [nslookup set domain](nslookup-set-domain.md)
  - [nslookup set port](nslookup-set-port.md)
  - [nslookup set querytype](nslookup-set-querytype.md)
  - [nslookup set recurse](nslookup-set-recurse.md)
  - [nslookup set retry](nslookup-set-retry.md)
  - [nslookup set root](nslookup-set-root.md)
  - [nslookup set search](nslookup-set-search.md)
  - [nslookup set srchlist](nslookup-set-srchlist.md)
  - [nslookup set timeout](nslookup-set-timeout.md)
  - [nslookup set type](nslookup-set-type.md)
  - [nslookup set vc](nslookup-set-vc.md)
  - [nslookup view](nslookup-view.md)
- [ntbackup](ntbackup.md)
- [ntcmdprompt](ntcmdprompt.md)
- [ntfrsutl](ntfrsutl.md)

### <a name="o"></a>O

- [라인인](offline.md)
  - [오프 라인 디스크](offline-disk.md)
  - [오프 라인 볼륨](offline-volume.md)
- [온라인](online.md)
  - [온라인 디스크](online-disk.md)
  - [온라인 볼륨](online-volume.md)
- [openfiles](openfiles.md)

### <a name="p"></a>P

- [pagefileconfig](pagefileconfig.md)
- [path](path.md)
- [pathping](pathping.md)
- [pause](pause.md)
- [pbadmin](pbadmin.md)
- [pentnt](pentnt.md)
- [perfmon](perfmon.md)
- [ping](ping.md)
- [pnpunattend](pnpunattend.md)
- [pnputil](pnputil.md)
- [popd](popd.md)
- [슬래시](powershell.md)
- [powershell ise](powershell_ise.md)
- [print](print.md)
- [prncnfg](prncnfg.md)
- [prndrvr](prndrvr.md)
- [prnjobs](prnjobs.md)
- [prnmngr](prnmngr.md)
- [prnport](prnport.md)
- [prnqctl](prnqctl.md)
- [prompt](prompt.md)
- [pubprn](pubprn.md)
- [pushd](pushd.md)
- [pushprinterconnections](pushprinterconnections.md)
- [pwlauncher](pwlauncher.md)

### <a name="q"></a>Q

- [qappsrv](qappsrv.md)
- [qprocess](qprocess.md)
- [쿼리](query.md)
  - [쿼리 프로세스](query-process.md)
  - [세션 쿼리](query-session.md)
  - [termserver 쿼리](query-termserver.md)
  - [사용자 쿼리](query-user.md)
- [quser](quser.md)
- [qwinsta](qwinsta.md)

### <a name="r"></a>R

- [rcp](rcp.md)
- [rd](rd.md)
- [rdpsign](rdpsign.md)
- [recover](recover.md)
- [디스크 그룹 복구](recover_1.md)
- [reg](reg.md)
  - [reg 추가](reg-add.md)
  - [reg 비교](reg-compare.md)
  - [reg 복사](reg-copy.md)
  - [reg 삭제](reg-delete.md)
  - [reg 내보내기](reg-export.md)
  - [reg 가져오기](reg-import.md)
  - [reg 로드](reg-load.md)
  - [reg 쿼리](reg-query.md)
  - [reg 복원](reg-restore.md)
  - [reg 저장](reg-save.md)
  - [레지스트리 언로드](reg-unload.md)
- [regini](regini.md)
- [regsvr32](regsvr32.md)
- [relog](relog.md)
- [rem 배치 파일](rem.md)
- [rem 스크립트](rem_1.md)
- [remove](remove.md)
- [ren](ren.md)
- [rename](rename.md)
- [복구](repair.md)
  - [manage-bde 복구](repair-bde.md)
- [replace](replace.md)
- [검사](rescan.md)
- [reset](reset.md)
  - [reset session](reset-session.md)
- [그대로](retain.md)
- [되돌립니다](revert.md)
- [rexec](rexec.md)
- [risetup](risetup.md)
- [rmdir](rmdir.md)
- [robocopy](robocopy.md)
- [ws2008 경로](route_ws2008.md)
- [rpcinfo](rpcinfo.md)
- [rpcping](rpcping.md)
- [rsh](rsh.md)
- [rundll32](rundll32.md)
- [rundll32.exe printui.dll](rundll32-printui.md)
- [rwinsta](rwinsta.md)

### <a name="s"></a>S

- [산마리노](san.md)
- [sc 구성](sc-config.md)
- [sc 만들기](sc-create.md)
- [sc 삭제](sc-delete.md)
- [sc 쿼리](sc-query.md)
- [schtasks](schtasks.md)
- [scwcmd](scwcmd.md)
  - [scwcmd 분석](scwcmd-analyze.md)
  - [scwcmd 구성](scwcmd-configure.md)
  - [scwcmd 레지스터](scwcmd-register.md)
  - [scwcmd 롤백](scwcmd-rollback.md)
  - [scwcmd 변환](scwcmd-transform.md)
  - [scwcmd 뷰](scwcmd-view.md)
- [secedit](secedit.md)
  - [secedit 분석](secedit-analyze.md)
  - [secedit 구성](secedit-configure.md)
  - [secedit 내보내기](secedit-export.md)
  - [secedit generaterollback](secedit-generaterollback.md)
  - [secedit 가져오기](secedit-import.md)
  - [secedit 유효성 검사](secedit-validate.md)
- [select](select.md)
  - [select disk](select-disk.md)
  - [파티션 선택](select-partition.md)
  - [vdisk 선택](select-vdisk.md)
  - [select volume](select-volume.md)
- [serverceipoptin](serverceipoptin.md)
- [servermanagercmd](servermanagercmd.md)
- [serverweroptin](serverweroptin.md)
- [환경 변수 설정](set_1.md)
- [섀도 복사본 설정](set_2.md)
  - [컨텍스트 설정](set-context.md)
  - [집합 id](set-id.md)
  - [setlocal](setlocal.md)
  - [메타 데이터 설정](set-metadata.md)
  - [set 옵션](set-option.md)
  - [자세한 정보 설정](set-verbose.md)
- [setx](setx.md)
- [sfc](sfc.md)
- [shadow](shadow.md)
- [shift](shift.md)
- [showmount](showmount.md)
- [축소](shrink.md)
- [shutdown](shutdown.md)
- [복원 시뮬레이트](simulate-restore.md)
- [sort](sort.md)
- [start](start.md)
- [하위 명령 설정 장치](subcommand-set-device.md)
- [하위 명령 설정 drivergroup](subcommand-set-drivergroup.md)
- [하위 명령 설정 drivergroupfilter](subcommand-set-drivergroupfilter.md)
- [하위 명령 설정 driverpackage](subcommand-set-driverpackage.md)
- [하위 명령 집합 이미지](subcommand-set-image.md)
- [하위 명령 set imagegroup](subcommand-set-imagegroup.md)
- [하위 명령 집합 서버](subcommand-set-server.md)
- [하위 명령 설정 서버](subcommand-set-transportserver.md)
- [하위 명령 set multicasttransmission](subcommand-start-multicasttransmission.md)
- [하위 명령 시작 네임 스페이스](subcommand-start-namespace.md)
- [하위 명령 시작 서버](subcommand-start-server.md)
- [하위 명령 시작 서버 시작](subcommand-start-transportserver.md)
- [하위 명령 서버 중지](subcommand-stop-server.md)
- [하위 명령 중지 서버 중지](subcommand-stop-transportserver.md)
- [subst](subst.md)
- [sxstrace](sxstrace.md)
- [sysocmgr](sysocmgr.md)
- [systeminfo](systeminfo.md)


### <a name="t"></a>T

- [takeown](takeown.md)
- [tapicfg](tapicfg.md)
- [taskkill](taskkill.md)
- [tasklist](tasklist.md)
- [tcmsetup](tcmsetup.md)
- [telnet](telnet.md)
  - [텔넷 닫기](telnet-close.md)
  - [텔넷 표시](telnet-display.md)
  - [텔넷 열기](telnet-open.md)
  - [텔넷 종료](telnet-quit.md)
  - [텔넷 송신](telnet-send.md)
  - [텔넷 집합](telnet-set.md)
  - [텔넷 상태](telnet-status.md)
  - [텔넷 설정 해제](telnet-unset.md)
- [tftp](tftp.md)
- [time](time.md)
- [timeout](timeout_1.md)
- [title](title_1.md)
- [tlntadmn](tlntadmn.md)
- [tpmtool](tpmtool.md)
- [tpmvscmgr](tpmvscmgr.md)
- [tracerpt](tracerpt_1.md)
- [tracert](tracert.md)
- [tree](tree.md)
- [tscon](tscon.md)
- [tsdiscon](tsdiscon.md)
- [tsecimp](tsecimp_1.md)
- [tskill](tskill.md)
- [tsprof](tsprof.md)
- [type](type.md)
- [typeperf](typeperf.md)
- [tzutil](tzutil.md)

### <a name="u"></a>U

- [숨깁니다](unexpose.md)
- [uniqueid](uniqueid.md)
- [unlodctr](unlodctr_1.md)

### <a name="v"></a>V

- [ver](ver.md)
- [verifier](verifier.md)
- [verify](verify_1.md)
- [vol](vol.md)
- [vssadmin](vssadmin.md)
  - [vssadmin delete shadows](vssadmin-delete-shadows.md)
  - [vssadmin list shadows](vssadmin-list-shadows.md)
  - [vssadmin list writers](vssadmin-list-writers.md)
  - [vssadmin resize shadowstorage](vssadmin-resize-shadowstorage.md)

### <a name="w"></a>W

- [waitfor](waitfor.md)
- [wbadmin](wbadmin.md)
  - [wbadmin delete 카탈로그](wbadmin-delete-catalog.md)
  - [wbadmin delete systemstatebackup](wbadmin-delete-systemstatebackup.md)
  - [wbadmin 백업 사용 안 함](wbadmin-disable-backup.md)
  - [wbadmin 백업 사용](wbadmin-enable-backup.md)
  - [wbadmin get 디스크](wbadmin-get-disks.md)
  - [wbadmin get 항목](wbadmin-get-items.md)
  - [wbadmin 가져오기 상태](wbadmin-get-status.md)
  - [wbadmin get 버전](wbadmin-get-versions.md)
  - [wbadmin 복원 카탈로그](wbadmin-restore-catalog.md)
  - [wbadmin 백업 시작](wbadmin-start-backup.md)
  - [wbadmin 복구 시작](wbadmin-start-recovery.md)
  - [wbadmin 시작 sysrecovery](wbadmin-start-sysrecovery.md)
  - [wbadmin 시작 systemstatebackup](wbadmin-start-systemstatebackup.md)
  - [wbadmin 시작 systemstaterecovery](wbadmin-start-systemstaterecovery.md)
  - [wbadmin 중지 작업](wbadmin-stop-job.md)
- [wdsutil](wdsutil.md)
- [wecutil](wecutil.md)
- [wevtutil](wevtutil.md)
- [where](where_1.md)
- [whoami](whoami.md)
- [winnt](winnt.md)
- [winnt32](winnt32.md)
- [winpop](winpop.md)
- [winrs](winrs.md)
- [winsat 메모리](winsat-mem.md)
- [winsat mfmedia](winsat-mfmedia.md)
- [wmic](wmic.md)
- [저자](writer.md)
- [wscript](wscript.md)

### <a name="x"></a>X

- [xcopy](xcopy.md)
