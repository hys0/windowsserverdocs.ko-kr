---
title: Server Core 설치
description: Windows Server 2019, Windows Server 2016 또는 Windows Server(반기 채널)에 Server Core 설치를 가져오고 설치하는 방법입니다.
ms.prod: windows-server
ms.date: 05/21/2019
ms.technology: server-general
ms.topic: article
ms.assetid: 2d22818c-fbb7-487a-bb82-81ef0a3f7ede
author: jasongerend
ms.author: jgerend
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 13d36c233094511216483f0fb37dc6a004212a50
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80826976"
---
# <a name="install-server-core"></a>Server Core 설치

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server(반기 채널)
  
Windows Server를 처음 설치하는 경우 다음과 같은 설치 옵션이 있습니다.

>[!NOTE]
> 다음 목록에서 "데스크톱 환경"이 없는 버전은 Server Core 설치 옵션입니다.

-    Windows Server Standard
-    데스크톱 환경 포함 Windows Server Standard
-    Windows Server Datacenter
-    데스크톱 환경 포함 Windows Server Datacenter

Windows Server(반기 채널)를 설치하는 경우 다음과 같은 설치 옵션이 있습니다.

-    Windows Server Standard 
-    Windows Server Datacenter

Server Core 옵션을 사용하면 디스크에 필요한 공간과 공격 취약성이 감소합니다. 따라서 데스크톱 환경 포함 서버 옵션에 포함된 추가 사용자 인터페이스 요소와 그래픽 관리 도구가 특별히 필요한 경우가 아니라면 Server Core 설치 옵션을 선택하는 것이 좋습니다. 추가 사용자 인터페이스 요소가 필요하다고 생각되면 [데스크톱 환경 포함 서버 설치](Getting-Started-with-Server-with-Desktop-Experience.md)를 참조하세요. 

Server Core 옵션을 선택하면 표준 사용자 인터페이스(데스크톱 환경)가 설치되지 않으므로 명령줄이나 Windows PowerShell 또는 원격 메서드를 사용하여 서버를 관리해야 합니다.

>[!NOTE]
>
>일부 이전 릴리스의 Windows Server와 달리 설치 후 Server Core와 데스크톱 경험 기능이 설치된 서버 간에 변환할 수 없습니다. Server Core를 설치하고 나중에 데스크톱 경험이 설치된 서버를 사용하기로 결정하는 경우에는 새로 설치를 수행해야 합니다.

**사용자 인터페이스:** 명령 프롬프트

**로컬에서 서버 역할 설치, 구성, 제거:** Windows PowerShell의 명령 프롬프트 사용

서버 관리자, 원격 서버 관리 도구(RSAT), Windows PowerShell 또는 Windows Admin Center로 **Windows 클라이언트 컴퓨터(또는 데스크톱 환경이 설치된 서버)에서 원격으로 서버 역할 설치, 구성, 제거**

>[!NOTE]
>
>RSAT의 경우 Windows 10 버전을 사용해야 합니다.
>Microsoft Management Console은 로컬에서 사용할 수 없습니다.

**사용 가능한 예제 Server 역할:**

- Active Directory 인증서 서비스
- Active Directory 도메인 서비스
- DHCP 서버
- DNS 서버
- 파일 서비스(파일 서버 리소스 관리자 포함)
- AD LDS(Active Directory Lightweight Directory Services)
- Hyper-V
- 인쇄 및 문서 서비스
- 스트리밍 미디어 서비스
- 웹 서버(ASP.NET의 하위 집합 포함)
- Windows Server Update Server
- Active Directory Rights Management Server
- 라우팅 및 원격 액세스 서버와 다음 하위 역할
   - 원격 데스크톱 서비스 연결 브로커
   - 라이선싱
   - 가상화
   - 볼륨 정품 인증 서비스

Server Core에 포함되지 않은 역할은 [Windows Server - Server Core에 없는 역할, 역할 서비스 및 기능](../administration/server-core/server-core-removed-roles.md)을 참조하세요.

## <a name="installing-on-windows-server-2019-or-windows-server-2016"></a>Windows Server 2019 또는 Windows Server 2016에 설치

Windows Server(장기 서비스 채널)에 대한 일반 설치 단계 및 옵션은 [Windows Server 설치 및 업그레이드](installation-and-upgrade.md)를 참조하세요.

## <a name="installing-on-windows-server-semi-annual-channel"></a>Windows Server(반기 채널)에 설치

Windows Server(반기 채널)에 대한 설치 단계는(.ISO 이미지를 통한) Windows Server의 이전 버전 설치와 동일하지만 다음 예외가 있습니다.

- 이전 버전의 Windows Server로부터 Windows Server, 버전 1709로의 업그레이드가 지원되지 않습니다. 항상 새로 설치해야 합니다.
   즉, Windows 컴퓨터의 데스크톱에서 setup.exe 파일을 실행할 때 설치 환경이 업그레이드 옵션을 허용하지 않습니다(회색 처리됨).
- Windows Server(반기 채널)에 대한 평가판은 없습니다.
- OEM 또는 일반 정품 버전이 없습니다. Windows Server(반기 채널)는 Software Assurance 또는 구독 프로그램을 통해서만 사용 허가될 수 있습니다.

반기 채널에 대한 자세한 내용은 [서비스 채널 비교](../get-started-19/servicing-channels-19.md)를 참조하세요.

Windows Server 반기 채널의 새로운 기능을 보려면 [Windows Server의 새로운 기능](whats-new-in-windows-server.md)을 참조하세요.
