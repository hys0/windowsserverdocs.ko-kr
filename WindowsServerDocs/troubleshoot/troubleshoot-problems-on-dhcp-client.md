---
title: DHCP 클라이언트에서 문제 해결
description: 이 artilce DHCP 클라이언트의 문제를 해결 하 고 데이터를 수집 하는 방법을 소개 합니다.
ms.prod: windows-server
ms.service: na
manager: dcscontentpm
ms.technology: server-general
ms.date: 5/26/2020
ms.topic: article
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: a6064b9e497fcd54671292ade77a08c06ba42920
ms.sourcegitcommit: ef089864980a1d4793a35cbf4cbdd02ce1962054
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2020
ms.locfileid: "84150301"
---
# <a name="troubleshoot-problems-on-the-dhcp-client"></a>DHCP 클라이언트에서 문제 해결

이 문서에서는 DHCP 클라이언트에서 발생 하는 문제를 해결 하는 방법을 설명 합니다.

## <a name="troubleshooting-checklist"></a>문제 해결 검사 목록

다음 장치 및 설정을 확인 합니다.

  - 케이블이 연결 되어 작동 하 고 있습니다.

  - MAC 필터링은 클라이언트가 연결 된 스위치에서 사용 하도록 설정 됩니다.

  - 네트워크 어댑터를 사용할 수 있습니다.

  - 올바른 네트워크 어댑터 드라이버를 설치 하 고 업데이트 합니다.

  - DHCP 클라이언트 서비스가 시작 되어 실행 되 고 있습니다. 이를 확인 하려면 **net start** 명령을 실행 하 고 **DHCP 클라이언트**를 찾습니다.

  - 클라이언트 컴퓨터에서 포트 67 및 68 UDP를 차단 하는 방화벽이 없습니다.

## <a name="event-logs"></a>이벤트 로그

Microsoft-Windows DHCP 클라이언트 이벤트/운영 및 Microsoft-DHCP 클라이언트 이벤트/관리 이벤트 로그를 검사 합니다. DHCP 클라이언트 서비스와 관련 된 모든 이벤트는 이러한 이벤트 로그에 전송 됩니다.  
Microsoft-Windows DHCP 클라이언트 이벤트는 **응용 프로그램 및 서비스 로그**아래 이벤트 뷰어에 있습니다.

"Get-netadapter-IncludeHidden" PowerShell 명령은 로그에 나열 된 이벤트를 해석 하는 데 필요한 정보를 제공 합니다. 예를 들어 인터페이스 ID, MAC 주소 등이 있습니다.

## <a name="data-collection"></a>데이터 수집

문제가 발생 하는 경우 DHCP 클라이언트 및 서버 쪽에서 동시에 데이터를 수집 하는 것이 좋습니다. 그러나 실제 문제에 따라 DHCP 클라이언트 또는 DHCP 서버에서 단일 데이터 집합을 사용 하 여 조사를 시작할 수도 있습니다.

서버 및 영향을 받는 클라이언트에서 데이터를 수집 하려면 [Wireshark](https://www.wireshark.org/download.html)를 사용 합니다. DHCP 클라이언트와 DHCP 서버 컴퓨터에서 동시에 수집을 시작 합니다.

문제가 발생 하는 클라이언트에서 다음 명령을 실행 합니다.

```console
ipconfig /release  
ipconfig /renew
```

그런 다음 클라이언트와 서버에서 Wireshark를 중지 합니다. 생성 된 추적을 확인 합니다. 적어도 통신이 중지 되는 단계를 알려 주어 야 합니다.