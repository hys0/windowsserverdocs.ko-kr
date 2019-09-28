---
title: 서비스 연결 지점별 BranchCache 기능 설치 및 호스트 캐시 서버 구성
description: 이 가이드에서는 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache를 배포 하는 방법 지침을 제공
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: 9adf420b-5a58-4e59-9906-71bd58f757fd
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fe2120310c6c410b410649aff1372f93e0ea5db7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356351"
---
# <a name="install-the-branchcache-feature-and-configure-the-hosted-cache-server-by-service-connection-point"></a>서비스 연결 지점별 BranchCache 기능 설치 및 호스트 캐시 서버 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

HCS1, 호스트 캐시 서버에서 BranchCache 기능을 설치 하 고 서비스 연결 지점이 등록 하려면 서버를 구성 하려면이 절차를 사용 하 여 수 \(SCP\) Active Directory 도메인 서비스에서 \(AD DS\)합니다.

AD DS에서 SCP를 사용 하 여 호스트 캐시 서버를 등록 하는 경우 scp를 사용 하면 SCP에 대 한 AD DS를 쿼리하여 호스트 캐시 서버를 자동으로 검색 하도록 클라이언트 컴퓨터를 구성할 수 있습니다. 이 작업을 수행 하도록 클라이언트 컴퓨터를 구성 하는 방법에 대 한 지침은이 가이드의 뒷부분에 나와 있습니다.

>[!IMPORTANT]
>이 절차를 수행 하기 전에 컴퓨터를 도메인에 가입 하 고 고정 IP 주소를 사용 하 여 컴퓨터를 구성 해야 합니다.

이 절차를 수행하려면 Administrators 그룹의 구성원이어야 합니다.

## <a name="to-install-the-branchcache-feature-and-configure-the-hosted-cache-server"></a>BranchCache 기능을 설치 하 고 호스트 캐시 서버를 구성 하려면  

1. 서버 컴퓨터에서 관리자 권한으로 Windows PowerShell을 실행 합니다. 다음 명령을 입력한 후 Enter 키를 누릅니다.

    ``` 
    Install-WindowsFeature BranchCache
    ```

2.  BranchCache 기능이 설치 된 후 컴퓨터를 호스트 캐시 서버로 구성 하 고 AD DS에 서비스 연결 지점을 등록 하려면 Windows PowerShell에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

    ```  
    Enable-BCHostedServer -RegisterSCP
    ```  

3. 호스트 캐시 서버 구성을 확인 하려면 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

    ```  
    Get-BCStatus  
    ```  
  
    명령 결과는 BranchCache 설치의 모든 측면에 대 한 상태를 표시 합니다. 다음은 몇 가지 BranchCache 설정 및 각 항목에 대 한 올바른 값입니다.  
  
    -   BranchCacheIsEnabled: True

    -   HostedCacheServerIsEnabled: True

    -   HostedCacheScpRegistrationEnabled: True

4. 콘텐츠 서버에서 호스트 캐시 서버로 데이터 패키지를 복사 하는 단계를 준비 하려면 호스트 캐시 서버의 기존 공유를 식별 하거나 새 폴더를 만든 다음 콘텐츠 서버에서 액세스할 수 있도록 폴더를 공유 합니다. 콘텐츠 서버에 데이터 패키지를 만든 후에는 해당 데이터 패키지를 호스트 캐시 서버의이 공유 폴더에 복사 합니다.
  
5. 호스트 캐시 서버를 두 개 이상 배포 하는 경우 각 서버에서이 절차를 반복 합니다.

이 가이드를 계속 하려면 참조 [이동 및 호스트 캐시 & #40; 옵션 & #41; 크기 조정](6-Bc-Move-Resize-Cache.md)합니다.
