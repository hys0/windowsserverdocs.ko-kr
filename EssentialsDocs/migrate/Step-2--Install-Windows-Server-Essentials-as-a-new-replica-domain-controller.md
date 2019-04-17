---
title: "새로운 복제 도메인 컨트롤러도 2 단계: Windows Server Essentials를 설치"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c7ccfc34-63fd-436b-a1cd-e05810f60bfe
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 757012b7d1a57a001e3b55cdc0604b63852a3d3c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="step-2-install-windows-server-essentials-as-a-new-replica-domain-controller"></a>새로운 복제 도메인 컨트롤러도 2 단계: Windows Server Essentials를 설치

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

이 섹션에는 Windows Server Essentials 및 Windows Server 2012 r 2 표준 도메인 컨트롤러 (활성화 Windows Server Essentials 경험 역할)를 설치 하는 방법을 설명 합니다.  
  
 장치 50 최대 25 명의 사용자와의 환경에 대 한이 가이드 SBS Windows의 이전 버전의 Windows Server Essentials 하 게 마이그레이션하의 단계를 따릅니다 수 있습니다. 최대 100 사용자와 200 디바이스와의 환경에 대 한 Windows Server Essentials 경험 역할이 설치와 Windows Server 2012 r 2의 표준 및 Datacenter edition 하 게 마이그레이션하는 동일한 지침을 따를 수 있습니다. 두 경우가이 문서에 적용 됩니다.  
  
> [!IMPORTANT]
>  Windows Server essentials 마이그레이션할 경우 다음과 같은 오류 메시지가 소스 서버 네트워크에서 제거 될 때까지 21 일 유예 기간 동안 매일 이벤트 로그에 추가 됩니다. 21 일 유예 기간이 지나면 원본 서버 종료 됩니다. <br> **라이선스 정책 준수 보이지 않는 귀하의 환경에 상태를 감지 FSMO 역할 확인 합니다. 주 도메인 컨트롤러 및 도메인 마스터 Active Directory 역할 명명 관리 서버 누르고 있어야 합니다. 이제 관리 서버에 Active Directory 역할 이동 하세요. 이 서버는 자동으로 종료할 때가이 상태를 찾았습니다 처음부터 21 일에 문제가 해결 되지 않으면**합니다.   
  
#### <a name="install-windows-server-essentials-or-windows-server-2012-r2-standard-on-the-destination-server"></a>Windows Server Essentials 또는 Windows Server 2012 r 2 표준 대상 서버의 설치  
  
1.  지침에 따라 사용 하도록 설정한 Windows Server Essentials 경험 역할와 Windows Server Essentials 또는 Windows Server 2012 r 2 표준 설치 [설치 및 구성 Windows Server Essentials](../install/Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)합니다.  
  
    > [!NOTE]
    >  Windows Server Essentials 구성 마법사가 실행 취소 합니다.  
  
2.  원본 서버에서 FSMO 역할을 전송 합니다.  
  
    > [!NOTE]
    >  Windows Server Essentials 유일한 도메인 컨트롤러 도메인에 있는 경우, Windows Server Essentials 원본 서버 내릴 때 실행 하는 서버에 FSMO 역할 자동으로 이동 합니다.  
  
3.  서버 관리자를 열고 역할 추가 및 기능 마법사 실행 합니다.  
  
4.  설치 되지 않은 경우 Windows Server Essentials 경험 역할을 추가 합니다.  
  
5.  Windows Server Essentials 경험 역할을 설치한 후 Windows Server Essentials 구성 작업 알림 영역에 표시 됩니다. Windows Server Essentials 구성 마법사를 시작 작업을 클릭 합니다.  
  
6.  Windows Server Essentials의 구성을 완료 하 고 지침을 따릅니다. 마법사를 실행 하기 전에 다음을 수행 합니다.  
  
    -   Windows Server Essentials 구성 마법사를 완료 한 후 이름을 변경할 수 없는 서버 이름, 필요한 경우 변경 합니다.  
  
    -   서버에서 시간 및 설정이 올바른지 확인 합니다.  
  
7.  다음과 같이 설치를 확인 합니다.  
  
    1.  대시보드를 엽니다.  
  
    2.  클릭 **사용자** 탭 하 고 사용자 계정 Active Directory에 나열 되어 있는지 확인 합니다.  
  
### <a name="transfer-the-operations-master-roles"></a>작업 마스터 역할 전환  
 작업 (단일 유연한 마스터 작업 나 FSMO 라고도 함) 마스터 역할을 Windows Server Essentials 대상 서버의 설치 21 일 이내 대상 서버 원본 서버에서 전송 되어야 합니다.  
  
##### <a name="to-transfer-the-operations-master-roles"></a>작업 마스터 역할 전환 하려면  
  
1.  대상 서버에서 관리자 권한으로 명령 프롬프트 창을 엽니다. 참조 [관리자 권한으로 명령 프롬프트 창을](https://technet.microsoft.com/library/cc947813\(v=WS.10\).aspx)합니다.  
  
2.  명령 프롬프트에 입력 **NETDOM 쿼리 FSMO**, ENTER 키를 누릅니다.  
  
3.  명령 프롬프트에 입력 **ntdsutil**, ENTER 키를 누릅니다.  
  
4.  에 **ntdsutil** 명령 프롬프트에서 다음 명령을 입력 합니다.  
  
    1.  입력 **인스턴스 NTDS 활성화**, ENTER 키를 누릅니다.  
  
    2.  입력 **역할**, ENTER 키를 누릅니다.  
  
    3.  입력 **연결**, ENTER 키를 누릅니다.  
  
    4.  입력 **서버에 연결** *< ServerName\ >* (여기서 *< ServerName\ >* 대상 서버 이름), ENTER 키를 누릅니다.  
  
    5.  명령 프롬프트에 입력 **q**, ENTER 키를 누릅니다.  
  
        1.  입력 **PDC 전송**를 enter 키를 클릭 한 다음 **예** 에 **역할 전송을 확인** 대화 상자가 합니다.  
  
        2.  입력 **전송 infrastructure 마스터**를 enter 키를 클릭 한 다음 **예** 에 **역할 전송을 확인** 대화 상자가 합니다.  
  
        3.  입력 **명명 마스터 전송**를 enter 키를 클릭 한 다음 **예** 에 **역할 전송을 확인** 대화 상자가 합니다.  
  
        4.  입력 **전송 RID 마스터**를 enter 키를 클릭 한 다음 **예** 에 **역할 전송을 확인** 대화 상자가 합니다.  
  
        5.  입력 **전송 스키마 마스터**를 enter 키를 클릭 한 다음 **예** 에 **역할 전송을 확인** 대화 상자가 합니다.  
  
    6.  입력 **q**, 명령 프롬프트 나타날 때까지 다음 ENTER 키를 누릅니다.  
  
> [!NOTE]
>  작업 마스터 역할 대상 서버에 전송 된 모든 서버 네트워크에서 확인할 수 있습니다. 관리자 권한으로 명령 프롬프트 창을 열고 (자세한 내용은 참조 [관리자 권한으로 명령 프롬프트 창을](https://technet.microsoft.com/library/cc947813\(v=WS.10\).aspx)). 입력 **netdom 쿼리 fsmo**, ENTER 키를 누릅니다.  
  
## <a name="next-steps"></a>다음 단계  
 Windows Server Essentials 새 복제 도메인 컨트롤러도 설치 되어 있습니다. 지금 이동 [3 단계: 컴퓨터를 새 Windows Server Essentials 서버에 가입](Step-3--Join-computers-to-the-new-Windows-Server-Essentials-server.md)합니다.  
  
모든 단계를 참조 [Windows Server essentials 마이그레이션](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)합니다.

