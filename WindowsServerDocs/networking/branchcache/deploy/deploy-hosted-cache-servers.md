---
title: 호스트 캐시 서버 (옵션)을 배포 합니다.
description: 이 항목은 Windows Server 2016을 지점에서 WAN 대역폭 사용을 최적화 하 분산 / 호스팅된 캐시 모드로 BranchCache 배포 하는 방법을 보여 주는 BranchCache 배포 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 96d03b42-6cd9-4905-b6a2-dc36130dd24f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d7345b9acf5ef5003cc2a811569083d7c12894a1
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-hosted-cache-servers-optional"></a>호스트 캐시 서버 (옵션)을 배포 합니다.

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

설치 하 고 배포 호스트 BranchCache 캐시 모드 하려는 지점에 있는 캐시 서버 호스트 BranchCache 구성이 절차를 사용할 수 있습니다. Windows Server 2016에 BranchCache와 한 지점에서 여러 호스트 캐시 서버의 배포할 수 있습니다.  
  
> [!IMPORTANT]  
> 이 단계는 선택적 분산된 캐시 모드 지점에서 호스트 캐시 서버 컴퓨터 필요 하지 않습니다. 에 하려는 경우 지점은에서 캐시 모드 호스트 배포 호스트 캐시 서버에 배포 필요가 없습니다 고이 절차의 단계를 수행 해야 합니다.  
  
소속 있어야 **관리자**, 나이 절차를 수행 하는 것과 같습니다.  
  
### <a name="to-install-and-configure-a-hosted-cache-server"></a>설치 하 여 호스팅된 캐시 서버 구성  
  
1.  호스트 캐시 서버로 구성 컴퓨터 BranchCache 기능을 설치 하려면 Windows PowerShell 프롬프트에서 다음 명령을 실행 합니다.  
  
    `Install-WindowsFeature BranchCache -IncludeManagementTools`  
  
2.  뒤 다음 명령을 중 하나를 사용 하 여 호스팅된 캐시 서버로 컴퓨터를 구성 합니다.  
  
    -   비 도메인 결합된 컴퓨터 호스트 캐시 서버 구성를 Windows PowerShell 프롬프트에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
        `Enable-BCHostedServer`  
  
    -   도메인 구성 하려면 컴퓨터 호스트 캐시 서버로 가입 하 고 서비스 연결 지점 Active Directory에 호스트 자동 캐시 서버 검색에 대 한 클라이언트 컴퓨터를 등록 Windows PowerShell 프롬프트에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
        `Enable-BCHostedServer -RegisterSCP`  
  
3.  잘못 구성 호스트 캐시 서버를 확인 하려면 Windows PowerShell 프롬프트에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
    `Get-BCStatus`  
  
    > [!NOTE]  
    > 이 명령을 섹션에서 실행 한 후 **HostedCacheServerConfiguration**에 대 한 값 **HostedCacheServerIsEnabled** 는 **진정한**합니다. (SCP) 서비스 연결 지점에 대 한 값 Active Directory에 등록 하는 도메인 결합된 호스트 캐시 서버 구성 **HostedCacheScpRegistrationEnabled** 는 **진정한**합니다.  
  

