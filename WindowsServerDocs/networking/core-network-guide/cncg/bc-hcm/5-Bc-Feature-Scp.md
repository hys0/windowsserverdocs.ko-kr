---
title: 서비스 지점 연결 하 여 호스팅된 캐시 서버 BranchCache 기능 설치 및 구성
description: 이 가이드 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache 배포에 대해 설명
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 9adf420b-5a58-4e59-9906-71bd58f757fd
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 854ff9f80a2221a857fab4e6ea7f7c8e6d51f1ef
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="install-the-branchcache-feature-and-configure-the-hosted-cache-server-by-service-connection-point"></a>서비스 지점 연결 하 여 호스팅된 캐시 서버 BranchCache 기능 설치 및 구성

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

호스트 캐시 서버의 HCS1, BranchCache 기능을 설치 하 고 서비스 연결 지점에 등록 하는 서버 구성 하려면이 절차를 사용할 수의 Active Directory 도메인 서비스 \(AD DS\) \(SCP\) 합니다.

호스트 캐시 서버 AD ds에서 SCP을 등록 하면 SCP AD DS SCP 쿼리 하 여 호스팅된 캐시 서버 자동 검색 올바르게 구성 된 컴퓨터를 클라이언트 있습니다. 이 가이드 뒷부분에 나오는 지침 클라이언트 컴퓨터를 구성 하는 방법에 대해이 작업을 수행할 제공 됩니다.

>[!IMPORTANT]
>이 절차를 수행 하기 전에 컴퓨터에서 도메인에 가입 하 고 컴퓨터에서 고정 IP 주소를 구성 합니다.

이 절차를 수행 하려면 관리자가 그룹의 회원 이어야 합니다.

## <a name="to-install-the-branchcache-feature-and-configure-the-hosted-cache-server"></a>호스트 캐시 서버 BranchCache 기능을 설치 및 구성 하려면  

1. 서버 컴퓨터에서 Windows PowerShell을 관리자 권한으로 실행 합니다. 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

    ``` 
    Install-WindowsFeature BranchCache
    ```

2.  BranchCache 기능을 설치한 후 호스트 캐시 서버로 컴퓨터를 구성 하 고 서비스 연결 지점 AD DS에 등록할 수 Windows PowerShell에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

    ```  
    Enable-BCHostedServer -RegisterSCP
    ```  

3. 호스트 캐시 서버 구성을 확인 하려면 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

    ```  
    Get-BCStatus  
    ```  
  
    명령 결과가 BranchCache 설치의 모든 측면에 대 한 상태를 표시 합니다. 다음은 몇 가지 BranchCache 설정 하 고 각 항목에 대 한 올바르지 값 다음과 같습니다.  
  
    -   BranchCacheIsEnabled: 진정한

    -   HostedCacheServerIsEnabled: 진정한

    -   HostedCacheScpRegistrationEnabled: 진정한

4. 여 호스팅된 캐시 서버에 데이터 패키지 콘텐츠 서버에서 복사 하는 단계를 준비 하 중 하나 기존 공유 호스트 캐시 서버에서 사용자의 신원을 확인 하거나 새 폴더를 만들고 공유 폴더 콘텐츠 서버에서 액세스할 수 있도록 합니다. 콘텐츠 서버에 데이터 패키지를 만든 후 데이터 패키지 호스트 캐시 서버의 공유이 폴더에 복사 합니다.
  
5. 둘 이상의 호스트 캐시 서버를 배포 하는 경우 각 서버의이 절차를 반복 합니다.

이 가이드를 계속 참조 [이동 및 크기 조정 호스트 캐시 & #40; 옵션 & #41; ](6-Bc-Move-Resize-Cache.md).
