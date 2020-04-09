---
title: 새 Windows Server Essentials server1에 컴퓨터 연결
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: cdfa9504-9881-4265-b308-c7ee8721bfaa
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: db00a395ebdb77ef65d99f58e6bbfbd9db4e53ed
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852566"
---
# <a name="join-computers-to-the-new-windows-server-essentials-server1"></a>새 Windows Server Essentials server1에 컴퓨터 연결

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_JoinComputers"></a>   
 마이그레이션 프로세스의 다음 단계에서는 새 Windows Server Essentials 네트워크에 클라이언트 컴퓨터를 연결 하 고 그룹 정책 설정을 업데이트 합니다.  
  
> [!NOTE]
>  클라이언트 컴퓨터가 이미 원본 서버에 연결되어 있으면 컴퓨터를 대상 서버에 연결하기 전에 먼저 클라이언트 컴퓨터에서 Connector 소프트웨어를 제거해야 합니다.  
  
 서버에 클라이언트 컴퓨터를 연결하는 프로세스는 도메인에 가입되거나 도메인 가입되지 않은 컴퓨터에 대해 동일합니다.  
  
- **http://** <em>destination-servername</em> **/connect**로 이동하고 새 컴퓨터인 것처럼 Windows Server Connector 소프트웨어를 설치합니다.  
  
> [!NOTE]
>  Windows Server Connector 소프트웨어에서는 Windows XP 또는 Windows Vista를 실행 중인 컴퓨터를 지원하지 않습니다. 이미 도메인에 가입된 Windows XP 또는 Windows Vista를 실행하는 컴퓨터에 있으면 이 단계를 건너뛸 수 있습니다.  
  
### <a name="ensure-that-group-policy-has-updated"></a>그룹 정책이 업데이트되었는지 확인  
  
> [!NOTE]
>  이 단계는 선택적 단계이고 원본 서버가 폴더 리디렉션과 같은 사용자 지정 그룹 정책 설정을 사용하여 구성된 경우에만 필요합니다.  
  
 원본 서버와 대상 서버가 온라인 상태인 동안 그룹 정책 설정이 대상 서버에서 클라이언트 컴퓨터로 복제되었는지 확인해야 합니다. 각 클라이언트 컴퓨터에서 다음 단계를 수행합니다.  
  
1.  명령 프롬프트 창을 엽니다.  
  
2.  명령 프롬프트에 **GPRESULT /R**을 입력하고 Enter 키를 누릅니다.  
  
3.  에서 적용 한 그룹 정책 섹션에 대 한 결과 출력을 검토 하 고 대상 서버 (예: **Destinationsrv. local. local**)가 나열 되는지 확인 합니다. 예를 들면 다음과 같습니다.  
  
    ```  
    USER SETTINGS  
    --------------  
        CN=User,OU=Users,DC=DOMAIN,DC=Local  
        Last time Group Policy was applied: 1/24/2011 at 1:26:27 PM  
        Group Policy was applied from:      DestinationSrv.Domain.local  
        Group Policy slow link threshold:   500 kbps  
        Domain Name:                        Domain  
        Domain Type:                        Windows 2011  
  
    ```  
  
4.  대상 서버가 나열되지 않으면 명령 프롬프트에서 **gpupdate /force**를 입력하고 Enter 키를 눌러 그룹 정책 설정을 새로 고칩니다. 그런 다음 다시 이전 절차를 수행합니다.  
  
5.  그래도 대상 서버가 나타나지 않으면 그룹 정책 설정에 오류가 있거나 이 특정 클라이언트 컴퓨터에 해당 설정을 적용하는 데 오류가 있을 수 있습니다. 대상 서버가 나타나지 않으면 다음 단계를 수행합니다.  
  
    1.  **시작**, **실행**을 차례로 클릭하고 **rsop.msc**(정책 결과 집합)를 입력하고 Enter 키를 누릅니다.  
  
    2.  노드에 도달할 때까지 X가 있는 트리를 확장 합니다.  
  
    3.  노드를 마우스 오른쪽 단추로 클릭하고 **오류 보기**를 클릭하여 나열된 컴퓨터에서 그룹 정책 설정이 실패하는 이유를 확인합니다.
