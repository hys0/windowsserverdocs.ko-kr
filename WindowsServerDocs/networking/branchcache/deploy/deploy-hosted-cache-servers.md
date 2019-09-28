---
title: 호스트 캐시 서버 배포(선택 사항)
description: 이 항목은 일부는 BranchCache 배포 가이드에 대 한 Windows Server 2016, 지사에 WAN 대역폭 사용량을 최적화 하기 위해 분산 및 호스트 캐시 모드로 BranchCache를 배포 하는 방법을 보여 주는
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 96d03b42-6cd9-4905-b6a2-dc36130dd24f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 69dc525a093c86d57b665e26ff5acaf2679c81a5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356439"
---
# <a name="deploy-hosted-cache-servers-optional"></a>호스트 캐시 서버 배포(선택 사항)

>적용 대상: Windows Server(반기 채널), Windows Server 2016

BranchCache 호스트 캐시 모드를 배포 하려는 지점에 위치한 BranchCache 호스트 캐시 서버 설치 및 구성 하려면이 절차를 사용할 수 있습니다. Windows Server 2016에서 branchcache 한 지점에 여러 호스트 캐시 서버를 배포할 수 있습니다.  
  
> [!IMPORTANT]  
> 분산된 캐시 모드 지점의 호스트 캐시 서버 컴퓨터를 필요 하지 않으므로이 단계는 선택 사항입니다. 에 계획이 없는 경우 배포 지점에서 캐시 모드, 호스트 캐시 서버를 배포할 필요가 없습니다 호스팅되며이 절차의 단계를 수행 해야 합니다.  
  
멤버 여야 **관리자**, 하거나이 절차를 수행 하려면 해당 합니다.  
  
### <a name="to-install-and-configure-a-hosted-cache-server"></a>설치 하 고 호스트 캐시 서버를 구성 합니다.  
  
1.  호스트 캐시 서버로 구성할 컴퓨터에서 BranchCache 기능을 설치 하려면 Windows PowerShell 프롬프트에서 다음 명령을 실행 합니다.  
  
    `Install-WindowsFeature BranchCache -IncludeManagementTools`  
  
2.  다음 명령 중 하나를 사용 하 여 호스트 캐시 서버와 컴퓨터를 구성 합니다.  
  
    -   비-도메인에 가입된 된 컴퓨터는 호스트 캐시 서버를 구성 하려면 Windows PowerShell 프롬프트에서 다음 명령을 입력 한 다음 ENTER 키를 누릅니다.  
  
        `Enable-BCHostedServer`  
  
    -   가입 된 컴퓨터를 호스트 캐시 서버로 도메인을 구성 하 고를 등록 하려면 서비스 연결 지점이 Active Directory에서 자동 호스트 캐시 서버 검색을 위한 클라이언트 컴퓨터에서 Windows PowerShell 프롬프트에서 다음 명령을 입력 한 다음 ENTER를 누릅니다.  
  
        `Enable-BCHostedServer -RegisterSCP`  
  
3.  호스트 캐시 서버 구성이 올바른지를 확인 하려면 Windows PowerShell 프롬프트에서 다음 명령을 입력 한 다음 ENTER 키를 누릅니다.  
  
    `Get-BCStatus`  
  
    > [!NOTE]  
    > 섹션에서이 명령을 실행 한 후 **HostedCacheServerConfiguration**, 에 대 한 값 **HostedCacheServerIsEnabled** 는 **True**합니다. 서비스 연결 지점 (SCP) 값에 대 한 Active Directory에 등록 하려면 도메인에 가입된 호스트 캐시 서버를 구성한 경우 **HostedCacheScpRegistrationEnabled** 는 **True**합니다.  
  

