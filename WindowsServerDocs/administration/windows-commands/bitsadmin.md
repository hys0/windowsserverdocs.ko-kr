---
title: bitsadmin
description: '**Bitsadmin**에 대 한 Windows 명령 항목-작업을 생성, 다운로드 또는 업로드 하 고 진행 상황을 모니터링 하는 데 사용 되는 명령줄 도구입니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4853036e-1df8-45ad-8be6-cfb097b8dd27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7a9cbf715474621b7102d0baf0c448e0ee578bf9
ms.sourcegitcommit: 1d83ca198c50eef83d105151551c6be6f308ab94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/30/2020
ms.locfileid: "82605563"
---
# <a name="bitsadmin"></a>bitsadmin

> **적용 대상**: windows Server (반기 채널), windows server 2016, windows Server 2012 R2, windows server 2012, windows 10

Bitsadmin은 작업을 만들고 다운로드 하거나 업로드 하 고 진행률을 모니터링 하는 데 사용 되는 명령줄 도구입니다. Bitsadmin 도구는 스위치를 사용 하 여 수행할 작업을 식별 합니다. 또는 `bitsadmin /help` 를 호출 `bitsadmin /?` 하 여 스위치 목록을 가져올 수 있습니다.

대부분의 스위치에 `<job>` 는 작업의 표시 이름 또는 GUID로 설정 하는 매개 변수가 필요 합니다. 작업의 표시 이름은 고유 하지 않아도 됩니다. **/Create** 및 **/list** 스위치는 작업의 GUID를 반환 합니다.

기본적으로 자신의 작업에 대 한 정보에 액세스할 수 있습니다. 다른 사용자의 작업에 대 한 정보에 액세스 하려면 관리자 권한이 있어야 합니다. 작업이 상승 된 상태에서 만들어진 경우에는 관리자 권한 창에서 **bitsadmin** 을 실행 해야 합니다. 그렇지 않으면 작업에 읽기 전용으로 액세스할 수 있습니다.

대부분의 스위치는 [BITS 인터페이스](https://docs.microsoft.com/windows/win32/bits/bits-interfaces)의 메서드에 해당 합니다. 스위치를 사용 하는 것과 관련 된 자세한 내용은 해당 메서드를 참조 하십시오.

다음 스위치를 사용 하 여 작업을 만들고, 작업의 속성을 설정 및 검색 하 고, 작업 상태를 모니터링할 수 있습니다. 이러한 스위치 중 일부를 사용 하 여 작업을 수행 하는 방법을 보여 주는 예제는 [bitsadmin 예](bitsadmin-examples.md)를 참조 하세요.

## <a name="available-switches"></a>사용 가능한 스위치

- [bitsadmin/addfile](bitsadmin-addfile.md)
- [bitsadmin/addfileset](bitsadmin-addfileset.md)
- [bitsadmin/addfilewithranges](bitsadmin-addfilewithranges.md)
- [bitsadmin/cache](bitsadmin-cache.md)
- [bitsadmin/cache/delete](bitsadmin-cache-and-delete.md)
- [bitsadmin/cache/deleteurl](bitsadmin-cache-and-deleteurl.md)
- [bitsadmin/cache/getexpirationtime](bitsadmin-cache-and-getexpirationtime.md)
- [bitsadmin/cache/getlimit](bitsadmin-cache-and-getlimit.md)
- [bitsadmin/cache/help](bitsadmin-cache-and-help.md)
- [bitsadmin 캐시/정보](bitsadmin-cache-and-info.md)
- [bitsadmin/cache/list](bitsadmin-cache-and-list.md)
- [bitsadmin/cache/setexpirationtime](bitsadmin-cache-and-setexpirationtime.md)
- [bitsadmin/cache/setlimit](bitsadmin-cache-and-setlimit.md)
- [bitsadmin 캐시/clear](bitsadmin-cache-clear.md)
- [bitsadmin/취소](bitsadmin-cancel.md)
- [bitsadmin/완료](bitsadmin-complete.md)
- [bitsadmin/create](bitsadmin-create.md)
- [bitsadmin/예제](bitsadmin-examples.md)
- [bitsadmin/getaclflags](bitsadmin-getaclflags.md)
- [bitsadmin/getbytestotal](bitsadmin-getbytestotal.md)
- [bitsadmin/getbytestransferred](bitsadmin-getbytestransferred.md)
- [bitsadmin/getclientcertificate](bitsadmin-getclientcertificate.md)
- [bitsadmin/getcompletiontime](bitsadmin-getcompletiontime.md)
- [bitsadmin/getcreationtime](bitsadmin-getcreationtime.md)
- [bitsadmin/getcustomheaders](bitsadmin-getcustomheaders.md)
- [bitsadmin/getdescription](bitsadmin-getdescription.md)
- [bitsadmin/getdisplayname](bitsadmin-getdisplayname.md)
- [bitsadmin/geterror](bitsadmin-geterror.md)
- [bitsadmin/geterrorcount](bitsadmin-geterrorcount.md)
- [bitsadmin/getfilestotal](bitsadmin-getfilestotal.md)
- [bitsadmin/getfilestransferred](bitsadmin-getfilestransferred.md)
- [bitsadmin/gethelpertokenflags](bitsadmin-gethelpertokenflags.md)
- [bitsadmin/gethelpertokensid](bitsadmin-gethelpertokensid.md)
- [bitsadmin/gethttpmethod](bitsadmin-gethttpmethod.md)
- [bitsadmin/getmaxdownloadtime](bitsadmin-getmaxdownloadtime.md)
- [bitsadmin/getminretrydelay](bitsadmin-getminretrydelay.md)
- [bitsadmin/getmodificationtime](bitsadmin-getmodificationtime.md)
- [bitsadmin/getnoprogresstimeout](bitsadmin-getnoprogresstimeout.md)
- [bitsadmin/getnotifycmdline](bitsadmin-getnotifycmdline.md)
- [bitsadmin/getnotifyflags](bitsadmin-getnotifyflags.md)
- [bitsadmin/getnotifyinterface](bitsadmin-getnotifyinterface.md)
- [bitsadmin/getowner](bitsadmin-getowner.md)
- [bitsadmin/getpeercachingflags](bitsadmin-getpeercachingflags.md)
- [bitsadmin/getpriority](bitsadmin-getpriority.md)
- [bitsadmin/getproxybypasslist](bitsadmin-getproxybypasslist.md)
- [bitsadmin/getproxylist](bitsadmin-getproxylist.md)
- [bitsadmin/getproxyusage](bitsadmin-getproxyusage.md)
- [bitsadmin/getreplydata](bitsadmin-getreplydata.md)
- [bitsadmin/getreplyfilename](bitsadmin-getreplyfilename.md)
- [bitsadmin/getreplyprogress](bitsadmin-getreplyprogress.md)
- [bitsadmin/getsecurityflags](bitsadmin-getsecurityflags.md)
- [bitsadmin/getstate](bitsadmin-getstate.md)
- [bitsadmin/gettemporaryname](bitsadmin-gettemporaryname.md)
- [bitsadmin/gettype](bitsadmin-gettype.md)
- [bitsadmin/getvalidationstate](bitsadmin-getvalidationstate.md)
- [bitsadmin/help](bitsadmin-help.md)
- [bitsadmin/정보](bitsadmin-info.md)
- [bitsadmin/list](bitsadmin-list.md)
- [bitsadmin/listfiles](bitsadmin-listfiles.md)
- [bitsadmin/makecustomheaderswriteonly](bitsadmin-makecustomheaderswriteonly.md)
- [bitsadmin/모니터](bitsadmin-monitor.md)
- [bitsadmin/nowrap](bitsadmin-nowrap.md)
- [bitsadmin/피어 캐싱](bitsadmin-peercaching.md)
- [bitsadmin/피어 캐싱/getconfigurationflags](bitsadmin-peercaching-and-getconfigurationflags.md)
- [bitsadmin/피어 캐싱/help](bitsadmin-peercaching-and-help.md)
- [bitsadmin/피어 캐싱/setconfigurationflags](bitsadmin-peercaching-and-setconfigurationflags.md)
- [bitsadmin/피어](bitsadmin-peers.md)
- [bitsadmin/피어/clear](bitsadmin-peers-and-clear.md)
- [bitsadmin/피어/검색](bitsadmin-peers-and-discover.md)
- [bitsadmin/피어/help](bitsadmin-peers-and-help.md)
- [bitsadmin/피어/list](bitsadmin-peers-and-list.md)
- [bitsadmin/rawreturn](bitsadmin-rawreturn.md)
- [bitsadmin/removeclientcertificate](bitsadmin-removeclientcertificate.md)
- [bitsadmin/removecredentials](bitsadmin-removecredentials.md)
- [bitsadmin/replaceremoteprefix](bitsadmin-replaceremoteprefix.md)
- [bitsadmin/reset](bitsadmin-reset.md)
- [bitsadmin/resume 재개](bitsadmin-resume.md)
- [bitsadmin/setaclflag](bitsadmin-setaclflag.md)
- [bitsadmin/setclientcertificatebyid](bitsadmin-setclientcertificatebyid.md)
- [bitsadmin/setclientcertificatebyname](bitsadmin-setclientcertificatebyname.md)
- [bitsadmin/setcredentials](bitsadmin-setcredentials.md)
- [bitsadmin/setcustomheaders](bitsadmin-setcustomheaders.md)
- [bitsadmin/setdescription](bitsadmin-setdescription.md)
- [bitsadmin/setdisplayname](bitsadmin-setdisplayname.md)
- [bitsadmin/sethelpertoken](bitsadmin-sethelpertoken.md)
- [bitsadmin/sethelpertokenflags](bitsadmin-sethelpertokenflags.md)
- [bitsadmin/sethttpmethod](bitsadmin-sethttpmethod.md)
- [bitsadmin/setmaxdownloadtime](bitsadmin-setmaxdownloadtime.md)
- [bitsadmin/setminretrydelay](bitsadmin-setminretrydelay.md)
- [bitsadmin/setnoprogresstimeout](bitsadmin-setnoprogresstimeout.md)
- [bitsadmin/setnotifycmdline](bitsadmin-setnotifycmdline.md)
- [bitsadmin/setnotifyflags](bitsadmin-setnotifyflags.md)
- [bitsadmin/setpeercachingflags](bitsadmin-setpeercachingflags.md)
- [bitsadmin/setpriority](bitsadmin-setpriority.md)
- [bitsadmin/setproxysettings](bitsadmin-setproxysettings.md)
- [bitsadmin/setreplyfilename](bitsadmin-setreplyfilename.md)
- [bitsadmin/setsecurityflags](bitsadmin-setsecurityflags.md)
- [bitsadmin/setvalidationstate](bitsadmin-setvalidationstate.md)
- [bitsadmin/일시 중단](bitsadmin-suspend.md)
- [bitsadmin/takeownership](bitsadmin-takeownership.md)
- [bitsadmin/transfer](bitsadmin-transfer.md)
- [bitsadmin/util](bitsadmin-util.md)
- [bitsadmin/util/enableanalyticchannel](bitsadmin-util-and-enableanalyticchannel.md)
- [bitsadmin/util/getieproxy](bitsadmin-util-and-getieproxy.md)
- [bitsadmin/util/help](bitsadmin-util-and-help.md)
- [bitsadmin/util/repairservice](bitsadmin-util-and-repairservice.md)
- [bitsadmin/util/setieproxy](bitsadmin-util-and-setieproxy.md)
- [bitsadmin/util/version](bitsadmin-util-and-version.md)
- [bitsadmin/wrap](bitsadmin-wrap.md)
