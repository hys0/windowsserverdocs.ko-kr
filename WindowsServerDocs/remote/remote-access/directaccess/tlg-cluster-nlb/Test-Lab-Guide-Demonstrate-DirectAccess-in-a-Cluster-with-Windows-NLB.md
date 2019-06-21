---
title: 테스트 랩 가이드-Windows NLB 사용 하 여 클러스터에서 DirectAccess 시연
description: 이 항목은 일부 테스트 랩 가이드-Windows Server 2016 Windows NLB를 사용 하 여 클러스터에서 DirectAccess 시연
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: db15dcf5-4d64-48d7-818a-06c2839e1289
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2318fa58a343b24ec401390b3cbbd6f22fe86870
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281595"
---
# <a name="test-lab-guide-demonstrate-directaccess-in-a-cluster-with-windows-nlb"></a>테스트 랩 가이드: Windows NLB 사용 하 여 클러스터에서 DirectAccess 시연

>적용 대상: Windows Server (반기 채널), Windows Server 2016

원격 액세스는 Windows Server 2016에서는 원격 사용자가 안전 하 게 DirectAccess 또는 RRAS VPN을 사용 하 여 내부 네트워크 리소스에 액세스할 수 있는 Windows Server 2012 R2 및 Windows Server 2012 운영 체제에서에서 서버 역할을 합니다. 이 가이드에는 확장에 대 한 단계별 지침이 포함 되어 있습니다.는 [테스트 랩 가이드: IPv4 및 IPv6을 사용 하 여 DirectAccess 단일 서버 설치 시연](https://go.microsoft.com/fwlink/p/?LinkId=237004) DirectAccess 네트워크 부하 분산 및 클러스터 구성을 시연 하 합니다.  
  
## <a name="about-this-guide"></a>이 가이드 정보  
이 가이드에는 서버 6개와 클라이언트 컴퓨터 2대를 사용하여 원격 액세스를 구성 및 시연하는 지침이 나와 있습니다. 완료된 원격 액세스 테스트 랩(NLB 포함)은 인트라넷, 인터넷 및 홈 네트워크를 시뮬레이트하며 서로 다른 인터넷 연결 시나리오의 원격 액세스 기능을 시연합니다.  
  
> [!IMPORTANT]  
> 이 랩을 통해 컴퓨터의 개수를 최소한으로 사용하는 개념을 파악할 수 있습니다. 이 가이드에 나와 있는 세부 구성은 테스트 랩 전용이므로, 프로덕션 환경에서 사용해서는 안 됩니다.  
  
## <a name="KnownIssues"></a>알려진된 문제  
클러스터 시나리오를 구성할 때의 알려진 문제는 다음과 같습니다.  
  
-   IPv4 전용 배포에서 단일 네트워크 어댑터로 DirectAccess를 구성하여 기본 DNS64(":3333::"을 포함하는 IPv6 주소)가 자동으로 네트워크 어댑터에 구성된 후 원격 액세스 관리 콘솔을 통해 부하 분산 사용 설정을 시도하면 사용자가 IPv6 DIP를 공급하는 프롬프트가 만들어집니다. IPv6 DIP가 제공된 경우 **커밋** 클릭 후 다음 오류와 함께 구성에 실패합니다. 매개 변수가 잘못되었습니다.  
  
    이 문제를 해결하려면  
  
    1.  [원격 액세스 구성 백업 및 복원](https://gallery.technet.microsoft.com/Back-up-and-Restore-Remote-e157e6a6)에서 백업을 다운로드하고 스크립트를 복원합니다.  
  
    2.  다운로드된 Backup-RemoteAccess.ps1 스크립트를 사용하여 원격 액세스 GPO를 백업합니다.  
  
    3.  실패한 단계에서 부하 분산 사용 설정을 시도합니다. 부하 분산 사용 대화 상자에서 세부 정보 영역을 확장하여 세부 정보 영역에서 마우스 오른쪽 단추를 클릭한 다음 **스크립트 복사**를 클릭합니다.  
  
    4.  메모장을 열고 클립보드의 내용을 붙여넣습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
        ```  
        Set-RemoteAccessLoadBalancer -InternetDedicatedIPAddress @('10.244.4.19/255.255.255.0','fdc4:29bd:abde:3333::2/128') -InternetVirtualIPAddress @('fdc4:29bd:abde:3333::1/128', '10.244.4.21/255.255.255.0') -ComputerName 'DA1.domain1.corp.contoso.com' -Verbose  
        ```  
  
    5.  열려 있는 모든 원격 액세스 대화 상자와 원격 액세스 관리 콘솔을 닫습니다.  
  
    6.  붙여넣은 텍스트를 편집하고 IPv6 주소를 제거합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
        ```  
        Set-RemoteAccessLoadBalancer -InternetDedicatedIPAddress @('10.244.4.19/255.255.255.0') -InternetVirtualIPAddress @('10.244.4.21/255.255.255.0') -ComputerName 'DA1.domain1.corp.contoso.com' -Verbose  
        ```  
  
    7.  관리자 권한 PowerShell 창에서 이전 단계의 명령을 실행합니다.  
  
    8.  실행 동안 cmdlet이 실패하면(잘못된 입력 값 때문이 아닌 경우) Restore-RemoteAccess.ps1 명령을 실행하고 지침을 따라 원래 구성의 무결성이 유지되고 있는지 확인합니다.  
  
    9. 이제 원격 액세스 관리 콘솔을 다시 열 수 있습니다.  
  


