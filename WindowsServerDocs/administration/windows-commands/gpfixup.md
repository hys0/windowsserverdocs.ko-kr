---
title: gpfixup
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2b145410-fc75-4526-932d-f16b7ee3aaef
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6df3b2fabcbfad29576a8e8f48d6a1a87f0da2ce
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724968"
---
# <a name="gpfixup"></a>gpfixup



도메인 이름 바꾸기 작업 후 그룹 정책 개체 및 그룹 정책 링크의 도메인 이름 종속성을 수정 합니다.

## <a name="syntax"></a>구문

```
Gpfixup [/v] 
[/olddns:<OLDDNSNAME> /newdns:<NEWDNSNAME>] 
[/oldnb:<OLDFLATNAME> /newnb:<NEWFLATNAME>] 
[/dc:<DCNAME>] [/sionly] 
[/user:<USERNAME> [/pwd:{<PASSWORD>|*}]] [/?]
```

#### <a name="parameters"></a>매개 변수

|       매개 변수       |                                                                                                                                                                                                                               설명                                                                                                                                                                                                                               |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          /v           |                                                                                                                                                      자세한 상태 메시지를 표시 합니다.</br>이 매개 변수를 사용 하지 않으면 오류 메시지 또는 **성공** 또는 **실패** 의 요약 상태 메시지만 표시 됩니다.                                                                                                                                                       |
| /olddns:\<olddnsname> |                                                                                                           도메인 이름 바꾸기 작업에서 도메인의 DNS 이름이 변경 될 때>이름이 바뀐 도메인의 이전 DNS 이름을 * \<olddnsname* 으로 지정 합니다. 이 매개 변수를 사용 하 여 새 도메인 DNS 이름을 지정 하는 경우에만 **/newdns** 매개 변수를 사용할 수 있습니다.                                                                                                            |
| /newdns:\<NEWDNSNAME> |                                                                                                          도메인 이름 바꾸기 작업에서 도메인의 dns 이름이 변경 될 때 이름이 바뀐 도메인의 새 dns 이름을 * \<NEWDNSNAME>* 로 지정 합니다. 이 매개 변수는 **/olddns** 매개 변수를 사용 하 여 이전 도메인 DNS 이름을 지정 하는 경우에만 사용할 수 있습니다.                                                                                                           |
| /oldnb:\<OLDFLATNAME> |                                                                                                        도메인 이름 바꾸기 작업에서 도메인의 netbios 이름을 변경할 때 이름이 바뀐 도메인의 이전 netbios 이름을 * \<OLDFLATNAME>* 로 지정 합니다. 이 매개 변수는 **/newnb** 매개 변수를 사용 하 여 새 도메인 NetBIOS 이름을 지정 하는 경우에만 사용할 수 있습니다.                                                                                                        |
| /nec:\<NEWFLATNAME> |                                                                                                       도메인 이름 바꾸기 작업에서 도메인의 netbios 이름을 변경할 때 이름이 바뀐 도메인의 새 netbios 이름을 * \<NEWFLATNAME>* 로 지정 합니다. 이 매개 변수는 **/oldnb** 매개 변수를 사용 하 여 이전 도메인 NetBIOS 이름을 지정 하는 경우에만 사용할 수 있습니다.                                                                                                       |
|     /dc:\<DCNAME>     | * \<DCNAME>* (DNS 이름 또는 NetBIOS 이름) 라는 도메인 컨트롤러에 연결 합니다. DCNAME>는 다음 중 하나로 표시 된 것 처럼 도메인 디렉터리 파티션의 쓰기 가능한 복제본을 호스팅해야 합니다. * \<*</br>-Dns 이름 * \<NEWDNSNAME* **을 사용 하 여**></br>-NetBIOS 이름 * \<NEWFLATNAME* **을 사용 하 여**>합니다.</br>이 매개 변수를 사용 하지 않는 경우 * \<NEWDNSNAME>* 또는 * \<NEWFLATNAME>* 으로 표시 된 이름이 바뀐 도메인의 모든 도메인 컨트롤러에 연결 합니다. |
|        /sionly        |                                                                                                                           는 관리 소프트웨어 설치 (그룹 정책 소프트웨어 설치 확장)와 관련 된 그룹 정책 픽스만 수행 합니다. Gpo에서 그룹 정책 링크 및 SYSVOL 경로를 수정 하는 작업을 건너뜁니다.                                                                                                                           |
|   /user:\<USERNAME>   |                                                                                                                                   사용자 * \<이름>* 의 보안 컨텍스트에서이 명령을 실행 합니다. 여기서 * \<username>* 은 domain\user 형식입니다.</br>이 매개 변수를 사용 하지 않으면는 로그인 한 사용자로이 명령을 실행 합니다.                                                                                                                                    |
|   /pwd: {\<PASSWORD>   |                                                                                                                                                                                                                                   \*}                                                                                                                                                                                                                                   |
|          /?           |                                                                                                                                                                                                                  명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                                                                                   |

## <a name="remarks"></a>설명

-   **Gpfixup** 명령은 server Core 설치를 제외 하 고 windows Server 2008 R2 및 windows server 2008에서 사용할 수 있습니다.
-   그룹 정책 관리 콘솔 (GPMC)는 Windows Server 2008 R2 및 Windows Server 2008과 함께 배포 되지만 서버 관리자를 통해 그룹 정책 관리 기능으로 설치 해야 합니다.

## <a name="examples"></a>예

이 예에서는 DNS 이름을 **Myolddnsname** 에서 **MyNewDnsName**로 변경한 도메인 이름 바꾸기 작업과 **MyOldNetBIOSName** 에서 **MyNewNetBIOSName**로의 NetBIOS 이름을 이미 수행 했다고 가정 합니다. 이 예제에서는 **gpfixup** 명령을 사용 하 여 **MyDcDnsName** 라는 도메인 컨트롤러에 연결 하 고 gpo와 링크에 포함 된 이전 도메인 이름을 업데이트 하 여 gpo 및 그룹 정책 링크를 복구 합니다. 상태 및 오류 출력은 **gpfixup**이라는 파일에 저장 됩니다.
```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /oldnb:MyOldNetBIOSName /newnb:MyNewNetBIOSName /dc:MyDcDnsName 2>&1 >gpfixup.log
```
이 예제는 도메인 이름 바꾸기 작업을 수행 하는 동안 도메인의 NetBIOS 이름이 변경 되지 않았다고 가정 하 고 이전 예제와 동일 합니다.
```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /dc:MyDcDnsName 2>&1 >gpfixup.log
```

## <a name="additional-references"></a>추가 참조

-   [Active Directory 도메인 이름 바꾸기 관리](https://go.microsoft.com/fwlink/?LinkId=198385)
-   [그룹 정책 TechCenter](https://go.microsoft.com/fwlink/?LinkID=145531)
-   - [명령줄 구문 키](command-line-syntax-key.md)