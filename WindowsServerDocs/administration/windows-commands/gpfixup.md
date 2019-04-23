---
title: gpfixup
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2b145410-fc75-4526-932d-f16b7ee3aaef
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fdbe9873cc15866037c4688aaac89095e4a85dec
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889424"
---
# <a name="gpfixup"></a>gpfixup



도메인 이름 바꾸기 작업 후 그룹 정책 개체 및 그룹 정책 링크의 도메인 이름 종속성을 해결 합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
Gpfixup [/v] 
[/olddns:<OLDDNSNAME> /newdns:<NEWDNSNAME>] 
[/oldnb:<OLDFLATNAME> /newnb:<NEWFLATNAME>] 
[/dc:<DCNAME>] [/sionly] 
[/user:<USERNAME> [/pwd:{<PASSWORD>|*}]] [/?]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/v|자세한 상태 메시지를 표시 합니다.</br>이 매개 변수를 사용 하지 않으면 하는 경우의 상태 요약 메시지나 오류 메시지만 **성공** 또는 **오류** 나타납니다.|
|/olddns:\<OLDDNSNAME>|으로 이름이 지정 된 도메인의 이전 DNS 이름을 지정  *\<OLDDNSNAME >* 도메인 이름 바꾸기 작업 도메인의 DNS 이름을 변경 하는 경우. 또한 사용 하는 경우에이 매개 변수를 사용할 수는 **/newdns** 매개 변수를 새 도메인 DNS 이름을 지정 합니다.|
|/newdns:\<NEWDNSNAME >|으로 이름이 지정 된 도메인의 새 DNS 이름을 지정  *\<NEWDNSNAME >* 도메인 이름 바꾸기 작업 도메인의 DNS 이름을 변경 하는 경우. 또한 사용 하는 경우에이 매개 변수를 사용할 수는 **/olddns** 매개 변수를 이전 도메인의 DNS 이름을 지정 합니다.|
|/oldnb:\<OLDFLATNAME>|으로 이름이 지정 된 도메인의 이전 NetBIOS 이름을 지정  *\<OLDFLATNAME >* 도메인 이름 바꾸기 작업 도메인의 NetBIOS 이름을 변경 하는 경우. 사용 하는 경우에이 매개 변수를 사용할 수는 **/newnb** 매개 변수를 새 도메인 NetBIOS 이름을 지정 합니다.|
|/newnb:\<NEWFLATNAME >|으로 이름이 지정 된 도메인의 새 NetBIOS 이름을 지정  *\<NEWFLATNAME >* 도메인 이름 바꾸기 작업 도메인의 NetBIOS 이름을 변경 하는 경우. 사용 하는 경우에이 매개 변수를 사용할 수는 **/oldnb** 매개 변수를 이전 도메인의 NetBIOS 이름을 지정 합니다.|
|/dc:\<DCNAME>|명명 된 도메인 컨트롤러에 연결할  *\<DCNAME >* (DNS 이름 또는 NetBIOS 이름). *\<DCNAME >* 다음 중 하나에 표시 된 대로 도메인 디렉터리 파티션에의 쓰기 가능한 복제본을 호스팅해야 합니다.</br>-DNS 이름  *\<NEWDNSNAME >* 사용 하 여 **/newdns**</br>-NetBIOS 이름  *\<NEWFLATNAME >* 사용 하 여 **/newnb**</br>이 매개 변수를 사용 하지 않으면 하는 경우에 나타난 이름이 지정 된 도메인의 모든 도메인 컨트롤러에 연결할  *\<NEWDNSNAME >* 하거나  *\<NEWFLATNAME >* 합니다.|
|/sionly|관리 되는 소프트웨어 설치 (그룹 정책 소프트웨어 설치 확장)에 연결 하는 그룹 정책 수정만 수행 합니다. Gpo에서 그룹 정책 링크 및 SYSVOL 경로 수정 하는 작업을 건너뜁니다.|
|/user:\<사용자 이름 >|이 명령은 사용자의 보안 컨텍스트에서 실행 됩니다  *\<사용자 이름 >* 여기서  *\<사용자 이름 >* 형식 도메인 \ 사용자는 합니다.</br>이 매개 변수를 사용 하지 않으면이 명령은 로그인된 한 사용자로 실행 됩니다.|
|/pwd:{\<PASSWORD>|*}|암호를 사용 하 여 표시 된 다른 보안 컨텍스트를 지정 **/user**합니다. 하는 경우 **&#42;** 암호 대신 지정 된 암호를 묻는 메시지가 나타납니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   **gpfixup** 명령은 Windows Server 2008 R2 및 Windows Server 2008에서 사용할 수 있는 Server Core 설치에서를 제외 하 고 있습니다.
-   그룹 정책 관리 콘솔 (GPMC)가 Windows Server 2008 R2 및 Windows Server 2008을 배포 하는 있지만 서버 관리자를 통해 기능으로 그룹 정책 관리를 설치 해야 합니다.

## <a name="BKMK_Examples"></a>예제

이 예제에서 DNS 이름을 변경 하는 도메인 이름 바꾸기 작업을 이미 수행한 것으로 가정 **MyOldDnsName** 하 **MyNewDnsName**, 및에서 NetBIOS 이름을  **MyOldNetBIOSName** 하 **MyNewNetBIOSName**합니다. 이 예제를 사용 하 여 합니다 **gpfixup** 이라는 도메인 컨트롤러에 연결 하려면 명령을 **MyDcDnsName** Gpo 및 그룹 정책 복구 및 Gpo 및 링크에 포함 된 이전 도메인 이름을 업데이트 하 여 링크 합니다. 상태 및 오류 출력 이라는 파일에 저장 됩니다 **gpfixup.log**합니다.
```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /oldnb:MyOldNetBIOSName /newnb:MyNewNetBIOSName /dc:MyDcDnsName 2>&1 >gpfixup.log
```
이 예제는 이전과 동일, 이름 바꾸기 작업 도메인의 NetBIOS 이름 도메인 중 변경 되지 않았는지 가정 한다는 점을 제외 하면 됩니다.
```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /dc:MyDcDnsName 2>&1 >gpfixup.log
```

#### <a name="additional-references"></a>추가 참조

-   [관리 Active Directory 도메인 이름 바꾸기](https://go.microsoft.com/fwlink/?LinkId=198385)
-   [그룹 정책 TechCenter](https://go.microsoft.com/fwlink/?LinkID=145531)
-   [명령줄 구문 키](command-line-syntax-key.md)