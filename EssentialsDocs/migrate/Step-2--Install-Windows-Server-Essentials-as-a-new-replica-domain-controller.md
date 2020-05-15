---
title: '2단계: Windows Server Essentials를 새 복제본 도메인 컨트롤러로 설치'
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: c7ccfc34-63fd-436b-a1cd-e05810f60bfe
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d5d86f5ae25c67ffb9e0f00fc5d373e6a095df98
ms.sourcegitcommit: 2f072c0c02e3e0deae331ca64b375d63b89d0522
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2020
ms.locfileid: "83404554"
---
# <a name="step-2-install-windows-server-essentials-as-a-new-replica-domain-controller"></a>2단계: Windows Server Essentials를 새 복제본 도메인 컨트롤러로 설치

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials

이 섹션에서는 windows server essentials 및 windows server 2012 R2 Standard (Windows Server Essentials Experience 역할이 사용 하도록 설정 된 상태)를 도메인 컨트롤러로 설치 하는 방법을 설명 합니다.  
  
 최대 25 명의 사용자와 50 장치가 있는 환경의 경우이 가이드의 단계를 수행 하 여 이전 버전의 Windows SBS에서 Windows Server Essentials로 마이그레이션할 수 있습니다. 최대 100 명의 사용자 및 200 장치가 있는 환경의 경우 동일한 지침에 따라 Windows Server Essentials Experience 역할이 설치 된 Windows Server 2012 R2 Standard 및 Datacenter 버전으로 마이그레이션할 수 있습니다. 이 문서에서는 두 시나리오를 모두 설명합니다.  
  
> [!IMPORTANT]
>  Windows Server Essentials로 마이그레이션하는 경우 네트워크에서 원본 서버를 제거할 때까지 21 일 유예 기간에 매일 다음 오류 메시지가 이벤트 로그에 추가 됩니다. 21일 유예 기간 이후에 원본 서버가 종료됩니다. <br> **FSMO 역할 검사가 사용자 환경에서 라이선스 정책을 준수 하지 않는 조건을 검색 했습니다. 관리 서버는 주 도메인 컨트롤러 및 도메인 명명 마스터 Active Directory 역할을 보유 해야 합니다. 지금 Active Directory 역할을 관리 서버로 이동 하세요. 이 조건이 처음 감지 된 시간 으로부터 21 일 내에 문제가 해결 되지 않으면이 서버가 자동으로 종료**됩니다.   
  
#### <a name="install-windows-server-essentials-or-windows-server-2012-r2-standard-on-the-destination-server"></a>대상 서버에 Windows Server Essentials 또는 Windows Server 2012 R2 Standard 설치  
  
1.  Windows server essentials [설치 및 구성](../install/Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)의 지침에 따라 Windows Server essentials Experience 역할이 사용 하도록 설정 된 Windows server Essentials 또는 windows Server 2012 R2 Standard를 설치 합니다.  
  
    > [!NOTE]
    >  Windows Server Essentials 구성 마법사가 시작되면 취소합니다.  
  
2.  원본 서버에서 FSMO 역할을 전송합니다.  
  
    > [!NOTE]
    >  Windows Server Essentials가 도메인의 유일한 도메인 컨트롤러인 경우, 원본 서버의 수준을 내릴 때 FSMO 역할이 Windows Server Essentials를 실행 하는 서버로 자동으로 이동 합니다.  
  
3.  서버 관리자를 열고 역할 및 기능 추가 마법사를 실행합니다.  
  
4.  Windows Server 필수 패키지 환경 역할이 설치되어 있지 않으면 이를 추가합니다.  
  
5.  Windows Server 필수 패키지 환경 역할을 설치하고 나면 알림 영역에 Windows Server Essentials 구성 작업이 나타납니다. 이 작업을 클릭하여 Windows Server Essentials 구성 마법사를 시작합니다.  
  
6.  지침에 따라 Windows Server Essentials 구성을 완료합니다. 마법사를 실행하기 전에 다음을 수행합니다.  
  
    -   Windows Server Essentials 구성 마법사를 완료한 후에는 이름을 변경할 수 없으므로 필요한 경우 서버 이름을 변경합니다.  
  
    -   서버의 시간과 설정이 올바른지 확인 합니다.  
  
7.  다음과 같이 설치를 확인합니다.  
  
    1.  대시보드를 엽니다.  
  
    2.  **사용자** 탭을 클릭하고 Active Directory의 사용자 계정이 나열되어 있는지 확인합니다.  
  
### <a name="transfer-the-operations-master-roles"></a>작업 마스터 역할 전송  
 작업 마스터 (신축 단일 마스터 작업 또는 FSMO 라고도 함) 역할은 대상 서버에 Windows Server Essentials를 설치한 후 21 일 이내에 원본 서버에서 대상 서버로 전송 되어야 합니다.  
  
##### <a name="to-transfer-the-operations-master-roles"></a>작업 마스터 역할을 전송하려면  
  
1.  대상 서버에서 관리자 권한으로 명령 프롬프트 창을 엽니다. [관리자 권한으로 명령 프롬프트 창을 열려면](https://technet.microsoft.com/library/cc947813\(v=WS.10\).aspx)을 참조하세요.  
  
2.  명령 프롬프트에 **NETDOM QUERY FSMO**를 입력하고 Enter 키를 누릅니다.  
  
3.  명령 프롬프트에 **ntdsutil**을 입력하고 Enter 키를 누릅니다.  
  
4.  **ntdsutil** 명령 프롬프트에 다음 명령을 입력합니다.  
  
    1.  **activate instance NTDS**를 입력하고 Enter 키를 누릅니다.  
  
    2.  **roles**을 입력하고 Enter 키를 누릅니다.  
  
    3.  **connections**를 입력하고 Enter 키를 누릅니다.  
  
    4.  **서버에 연결** *<\> ServerName* (여기서 *<servername \> * 은 대상 서버의 이름)을 입력 하 고 enter 키를 누릅니다.  
  
    5.  명령 프롬프트에 **q**를 입력하고 Enter 키를 누릅니다.  
  
        1.  **transfer PDC**를 입력하고 Enter 키를 누른 후 **역할 전송 확인** 대화 상자에서 **예**를 클릭합니다.  
  
        2.  **transfer infrastructure master**를 입력하고 Enter 키를 누른 후 **역할 전송 확인** 대화 상자에서 **예**를 클릭합니다.  
  
        3.  **transfer naming master**를 입력하고 Enter 키를 누른 후 **역할 전송 확인** 대화 상자에서 **예**를 클릭합니다.  
  
        4.  **transfer RID master**를 입력하고 Enter 키를 누른 후 **역할 전송 확인** 대화 상자에서 **예**를 클릭합니다.  
  
        5.  **transfer schema master**를 입력하고 Enter 키를 누른 후 **역할 전송 확인** 대화 상자에서 **예**를 클릭합니다.  
  
    6.  **q**를 입력한 후 명령 프롬프트로 돌아갈 때까지 Enter 키를 누릅니다.  
  
> [!NOTE]
>  네트워크의 모든 서버에서 작업 마스터 역할이 대상 서버로 전송되었는지 확인할 수 있습니다. 관리자 권한으로 명령 프롬프트 창을 엽니다(자세한 내용은 [관리자 권한으로 명령 프롬프트 창을 열려면](https://technet.microsoft.com/library/cc947813\(v=WS.10\).aspx)(영문) 참조). **netdom query fsmo**를 입력하고 Enter 키를 누릅니다.  
  
## <a name="next-steps"></a>다음 단계  
 Windows Server Essentials를 새 복제본 도메인 컨트롤러로 설치 했습니다. 이제 [3 단계: 새 Windows Server Essentials 서버에 컴퓨터 연결](Step-3--Join-computers-to-the-new-Windows-Server-Essentials-server.md)로 이동 합니다.  
  
모든 단계를 보려면 [Windows Server Essentials로 마이그레이션](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)을 참조 하세요.

