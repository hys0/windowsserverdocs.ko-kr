---
title: ipconfig
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 15071c2c-4815-4893-93b2-ab30232e312e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: babcdaf6ae35770d48176c7c391fa41e295ce5d5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825054"
---
# <a name="ipconfig"></a>ipconfig



모든 현재 TCP/IP 네트워크 구성 값을 표시 하 고 동적 호스트 구성 프로토콜 (DHCP) 및 도메인 이름 시스템 (DNS) 설정을 새로 고칩니다. 매개 변수 없이 사용 **ipconfig** 인터넷 프로토콜 버전 4 (IPv4)를 표시 및 IPv6 주소, 서브넷 마스크 및 기본 게이트웨이 모든 어댑터에 대 한 합니다.

## <a name="syntax"></a>구문

```
ipconfig [/allcompartments] [/all] [/renew [<Adapter>]] [/release [<Adapter>]] [/renew6[<Adapter>]] [/release6 [<Adapter>]] [/flushdns] [/displaydns] [/registerdns] [/showclassid <Adapter>] [/setclassid <Adapter> [<ClassID>]]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/all|모든 어댑터의 전체 TCP/IP 구성을 표시합니다. 어댑터는 설치된 네트워크 어댑터 같은 실제 인터페이스 또는 전화 접속 연결 같은 논리 인터페이스를 나타낼 수 있습니다.|
|/allcompartments|모든 구획에 대 한 전체 TCP/IP 구성을 표시합니다.|
|/displaydns|최근에 로컬 Hosts 파일에서 미리 로드 된 두 항목을 포함 하 여 DNS 클라이언트 확인자 캐시의 내용을 표시 하는 컴퓨터에서 확인 한 이름 쿼리에 대 한 리소스 레코드를 가져옵니다. DNS 클라이언트 서비스가 구성된 된 DNS 서버를 쿼리 하기 전에 자주 쿼리 이름을 신속 하 게 확인 하기 위해이 정보를 사용 합니다.|
|/flushdns|해당 페이지를 플러시하고 DNS 클라이언트 확인자 캐시의 내용을 다시 설정 합니다. DNS 문제 해결 하는 동안 동적으로 추가 된 다른 항목 뿐만 아니라 부정 캐시 항목, 캐시에서 삭제 하려면이 절차를 사용할 수 있습니다.|
|/registerdns|DNS 이름 및 컴퓨터에 구성 된 IP 주소에 대 한 수동 동적 등록을 시작 합니다. 실패 한 DNS 이름 등록 문제를 해결 하거나 클라이언트 컴퓨터를 다시 부팅 하지 않고 클라이언트와 DNS 서버 간의 동적 업데이트 문제를 해결 하려면이 매개 변수를 사용할 수 있습니다. TCP/IP 프로토콜의 고급 속성에서 DNS 설정을 DNS에 등록 된 이름을 확인 합니다.|
|릴리스 / [\<어댑터 >]|하는 경우 현재 DHCP 구성을 해제 하 고 (어댑터를 지정 하지 않으면) 하는 경우 모든 어댑터에 대 한 IP 주소 구성을 삭제 하는 DHCP 서버에 또는 특정 어댑터에 대 한 DHCPRELEASE 메시지를 보냅니다는 *어댑터* 매개 변수가 포함 됩니다. 이 매개 변수는 IP 주소를 자동으로 가져오기 위해 구성 된 어댑터에 대 한 TCP/IP를 해제 합니다. 어댑터 이름을 지정 하려면 사용할 때 표시 되는 어댑터 이름을 입력 **ipconfig** 매개 변수 없이 합니다.|
|/release6[\<Adapter>]|면 DHCPv6 서버에 현재 DHCP 구성 해제 하 고 (어댑터를 지정 하지 않으면) 하는 경우 모든 어댑터 중 하나에 대해 구성 된 IPv6 주소를 삭제 하거나 특정 어댑터에 대 한 DHCPRELEASE 메시지를 보냅니다는 *어댑터* 매개 변수가 포함 됩니다. 이 매개 변수는 IP 주소를 자동으로 가져오기 위해 구성 된 어댑터에 대 한 TCP/IP를 해제 합니다. 어댑터 이름을 지정 하려면 사용할 때 표시 되는 어댑터 이름을 입력 **ipconfig** 매개 변수 없이 합니다.|
|갱신 / [\<어댑터 >]|경우 (어댑터를 지정 하지 않으면) 하는 경우 모든 어댑터에 대해 또는 특정 어댑터에 대 한 DHCP 구성을 갱신는 *어댑터* 매개 변수가 포함 됩니다. 이 매개 변수는 자동으로 IP 주소를 가져오도록 구성 된 어댑터를 사용 하는 컴퓨터에만 사용할 수 있습니다. 어댑터 이름을 지정 하려면 사용할 때 표시 되는 어댑터 이름을 입력 **ipconfig** 매개 변수 없이 합니다.|
|/renew6 [\<어댑터 >]|경우 DHCPv6 구성 (어댑터를 지정 하지 않으면) 하는 경우 모든 어댑터에 대해 또는 특정 어댑터에 대 한 갱신 된 *어댑터* 매개 변수가 포함 됩니다. 이 매개 변수는 자동으로 IPv6 주소를 가져오도록 구성 된 어댑터를 사용 하는 컴퓨터에만 사용할 수 있습니다. 어댑터 이름을 지정 하려면 사용할 때 표시 되는 어댑터 이름을 입력 **ipconfig** 매개 변수 없이 합니다.|
|/setclassid \<Adapter>[ <ClassID>]|지정된 된 어댑터에 대 한 DHCP 클래스 ID를 구성합니다. 모든 어댑터에 대 한 DHCP 클래스 ID를 설정 하려면 별표를 사용 하 여 (**&#42;**) 대신 와일드 카드 문자 *어댑터*합니다. 이 매개 변수는 자동으로 IP 주소를 가져오도록 구성 된 어댑터를 사용 하는 컴퓨터에만 사용할 수 있습니다. DHCP 클래스 ID를 지정 하지 않으면 현재 클래스 ID 제거 됩니다.|
|/showclassid \<Adapter>|지정된 된 어댑터에 대 한 DHCP 클래스 ID를 표시합니다. 모든 어댑터에 대 한 DHCP 클래스 ID를 확인 하려면 별표를 사용 하 여 (**&#42;**) 대신 와일드 카드 문자 *어댑터*합니다. 이 매개 변수는 자동으로 IP 주소를 가져오도록 구성 된 어댑터를 사용 하는 컴퓨터에만 사용할 수 있습니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   이 명령은 IP 주소를 자동으로 가져오도록 구성 된 컴퓨터에서 가장 유용 합니다. 그러면 사용자가 DHCP, 자동 개인 IP 주소 지정 APIPA (), 또는 대체 구성으로 구성 된 TCP/IP 구성 값을 확인할 수 있습니다.
-   이름을 제공 하는 경우 *어댑터* 어댑터 이름 주위에 따옴표 사용 하 여 공백을 포함 (예: **"***어댑터 이름***"**).
-   어댑터 이름에 대해 **ipconfig** 이름이 지정된 된 문자열 또는 이름이 지정된 된 문자열을 포함 하는 어댑터를 사용 하 여 시작 하는 어댑터를 지정 하는 별표 (*) 와일드 카드 문자 사용을 지원 합니다. 예를 들어 **로컬\***  로컬 문자열으로 시작 하는 모든 어댑터와 일치 하 고 **\*Con\*** Con 문자열이 포함 된 모든 어댑터와 일치 합니다.

## <a name="examples"></a>예

모든 어댑터에 대 한 기본 TCP/IP 구성 정보를 표시 하려면 다음을 입력 합니다.
```
ipconfig
```
모든 어댑터에 대 한 전체 TCP/IP 구성을 표시 하려면 다음을 입력 합니다.
```
ipconfig /all
```
로컬 영역 연결 어댑터만 대 한 DHCP 할당 된 IP 주소 구성을 갱신 하려면 다음을 입력 합니다.
```
ipconfig /renew "Local Area Connection"
```
DNS 이름 확인 문제를 해결 하는 경우 DNS 확인자 캐시를 플러시하려면를 입력 합니다.
```
ipconfig /flushdns
```
로컬으로 시작 하는 이름의 모든 어댑터에 대 한 DHCP 클래스 ID를 표시 하려면 다음을 입력 합니다.
```
ipconfig /showclassid Local*
```
테스트를 로컬 영역 연결 어댑터에 대 한 DHCP 클래스 ID를 설정 하려면 다음을 입력 합니다.
```
ipconfig /setclassid "Local Area Connection" TEST
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)