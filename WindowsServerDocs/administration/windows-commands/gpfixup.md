---
title: gpfixup
description: 도메인 이름 바꾸기 작업 후 그룹 정책 개체 및 그룹 정책 링크의 도메인 이름 종속성을 수정 하는 gpfixup 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2b145410-fc75-4526-932d-f16b7ee3aaef
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c09efb2fc8b1de124cbefc1b2dff73df29d2a4f1
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924651"
---
# <a name="gpfixup"></a>gpfixup

도메인 이름 바꾸기 작업 후 그룹 정책 개체 및 그룹 정책 링크의 도메인 이름 종속성을 수정 합니다. 이 명령을 사용 하려면 서버 관리자를 통해 그룹 정책 관리 기능으로 설치 해야 합니다.

## <a name="syntax"></a>구문

```
gpfixup [/v]
[/olddns:<olddnsname> /newdns:<newdnsname>]
[/oldnb:<oldflatname> /newnb:<newflatname>]
[/dc:<dcname>] [/sionly]
[/user:<username> [/pwd:{<password>|*}]] [/?]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- |------------ |
| /v | 자세한 상태 메시지를 표시 합니다. 이 매개 변수를 사용 하지 않으면 오류 메시지 또는 요약 상태 메시지만 표시 하 고 **성공** 또는 **실패** 를 표시 합니다. |
| /olddns:`<olddnsname>` | 도메인 이름 `<olddnsname>` 바꾸기 작업에서 도메인의 dns 이름이 변경 될 때와 같이 이름이 바뀐 도메인의 이전 DNS 이름을 지정 합니다. 이 매개 변수를 사용 하 여 새 도메인 DNS 이름을 지정 하는 경우에만 **/newdns** 매개 변수를 사용할 수 있습니다. |
| /shdns:`<newdnsname>` | 도메인 이름 `<newdnsname>` 바꾸기 작업에서 도메인의 dns 이름이 변경 될 때와 같이 이름이 바뀐 도메인의 새 dns 이름을 지정 합니다. 이 매개 변수는 **/olddns** 매개 변수를 사용 하 여 이전 도메인 DNS 이름을 지정 하는 경우에만 사용할 수 있습니다. |
| /oldnb:`<oldflatname>` | 도메인 `<oldflatname>` 이름 바꾸기 작업에서 도메인의 netbios 이름을 변경할 때 처럼 이름이 바뀐 도메인의 이전 netbios 이름을 지정 합니다. 이 매개 변수는 **/newnb** 매개 변수를 사용 하 여 새 도메인 NetBIOS 이름을 지정 하는 경우에만 사용할 수 있습니다. |
| /nec:`<newflatname>` | 도메인 `<newflatname>` 이름 바꾸기 작업에서 도메인의 netbios 이름을 변경할 때 처럼 이름이 바뀐 도메인의 새 netbios 이름을 지정 합니다. 이 매개 변수는 **/oldnb** 매개 변수를 사용 하 여 이전 도메인 NetBIOS 이름을 지정 하는 경우에만 사용할 수 있습니다. |
| /dc`<dcname>` | `<dcname>`(DNS 이름 또는 NetBIOS 이름) 이라는 도메인 컨트롤러에 연결 합니다. `<dcname>`다음 중 하나에 표시 된 대로 도메인 디렉터리 파티션의 쓰기 가능한 복제본을 호스팅해야 합니다.<ul><li>`<newdnsname>` **/Newdns** 를 사용 하는 dns 이름</li><li>`<newflatname>` **/Newnb** 를 사용 하는 NetBIOS 이름</br>이 매개 변수를 사용 하지 않으면 또는로 표시 된 이름을 바꾼 도메인의 모든 도메인 컨트롤러에 연결할 수 있습니다 `<newdnsname>` `<newflatname>` .</li></ul> |
| /sionly | 는 관리 소프트웨어 설치 (그룹 정책 소프트웨어 설치 확장)와 관련 된 그룹 정책 픽스만 수행 합니다. Gpo에서 그룹 정책 링크 및 SYSVOL 경로를 수정 하는 작업을 건너뜁니다. |
| /user`<username>` |사용자의 보안 컨텍스트에서이 명령을 실행 합니다. `<username>` 여기서 `<username>` 은 domain\user 형식입니다. 이 매개 변수를 사용 하지 않으면이 명령은 로그인 한 사용자로 실행 됩니다. |
| /pwd`{<password> | *}` | 사용자에 대 한 암호를 지정합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예

이 예에서는 DNS 이름을 **Myolddnsname** 에서 **MyNewDnsName**로 변경한 도메인 이름 바꾸기 작업과 **MyOldNetBIOSName** 에서 **MyNewNetBIOSName**로의 NetBIOS 이름을 이미 수행 했다고 가정 합니다.

이 예제에서는 **gpfixup** 명령을 사용 하 여 **MyDcDnsName** 라는 도메인 컨트롤러에 연결 하 고 gpo와 링크에 포함 된 이전 도메인 이름을 업데이트 하 여 gpo 및 그룹 정책 링크를 복구 합니다. 상태 및 오류 출력은 **gpfixup**이라는 파일에 저장 됩니다.

```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /oldnb:MyOldNetBIOSName /newnb:MyNewNetBIOSName /dc:MyDcDnsName 2>&1 >gpfixup.log
```

이 예제는 도메인 이름 바꾸기 작업을 수행 하는 동안 도메인의 NetBIOS 이름이 변경 되지 않았다고 가정 하 고 이전 예제와 동일 합니다.

```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /dc:MyDcDnsName 2>&1 >gpfixup.log
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [Active Directory 도메인 이름 바꾸기 관리](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc794869(v=ws.10))
