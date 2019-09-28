---
title: BranchCache 호스트 캐시 모드 배포 계획
description: 이 가이드에서는 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache를 배포 하는 방법 지침을 제공
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: bc44a7db-f7a5-4e95-9d95-ab8d334e885f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0fe55bc9971606559af652d592a91db7a89544a7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356367"
---
# <a name="branchcache-hosted-cache-mode-deployment-planning"></a>BranchCache 호스트 캐시 모드 배포 계획

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목의 BranchCache 호스트 캐시 모드에서 배포를 계획에 사용할 수 있습니다.

>[!IMPORTANT]
>호스트 캐시 서버는 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 실행 되어야 합니다.

호스트 캐시 서버를 배포 하기 전에 다음 항목을 계획 해야 합니다.

- [기본 서버 구성 계획](#bkmk_basic)

- [도메인 액세스 계획](#bkmk_domain)

- [호스트 캐시의 위치 및 크기를 계획 합니다.](#bkmk_cachelocation)

- [콘텐츠 서버 패키지를 복사할 공유 계획](#bkmk_package)

- [콘텐츠 서버에서 사전 해싱 및 데이터 패키지 만들기 계획](#bkmk_prehash)

## <a name="bkmk_basic"></a>기본 서버 구성 계획
  
지점 사무실에 기존 서버를 사용 하 여 호스트 캐시 서버에 계획 하는 경우 컴퓨터 이름이 지정 되어 있으며 IP 주소 구성을 때문에이 계획 단계를 수행할 필요가 없습니다.

호스트 캐시 서버에 Windows Server 2016를 설치한 후 컴퓨터 이름을 바꾸고 및 할당 하 고 구성 해야 로컬 컴퓨터에 대 한 고정 IP 주소입니다.

>[!NOTE]
>하지만이 가이드에서는 호스트 캐시 서버 배포에 적합 한 서버 이름을 사용 해야, HCS1 이라고 합니다.

## <a name="bkmk_domain"></a>도메인 액세스 계획

지점 사무실에 기존 서버를 사용 하 여 호스트 캐시 서버로 하려는 경우 필요가 없습니다이 계획 단계를 수행 하려면 컴퓨터가 현재 도메인에 가입 되지 않은 경우가 아니면 합니다.
  
하려면 도메인에 로그온 컴퓨터는 도메인 구성원 컴퓨터 및 사용자 계정에 로그온 하기 전에 AD DS에 만들어야 합니다. 또한 적절 한 그룹 멤버 자격 증명이 있는 계정 사용 하 여 도메인에 컴퓨터를 조인 해야 합니다.

## <a name="bkmk_cachelocation"></a>호스트 캐시의 위치 및 크기를 계획 합니다.

HCS1, 호스트 캐시 서버에 저장할 경우 호스트 캐시를 찾을 수를 결정 합니다. 예를 들어, 하드 디스크, 볼륨 및 캐시 저장 하려는 폴더 위치를 결정 합니다.

또한 호스트 캐시에 대 한 할당 하려는 디스크 공간의 백분율을 결정 합니다.

## <a name="bkmk_package"></a>콘텐츠 서버 패키지를 복사할 공유 계획

콘텐츠 서버에 데이터 패키지를 만든 후 복사 해야 네트워크를 통해 공유 호스트 캐시 서버에 있습니다.

공유 폴더에 대 한 사용 권한을 공유 및 폴더 위치를 계획 합니다. 또한 많은 양의 데이터를 호스트 하는 콘텐츠 서버 및 경우 패키지를 만들 수 큰 파일을 다른 사용자가 일반 업무에는 대역폭을 사용 해야 할 때 시간 동안 복사 작업에서 WAN 대역폭을 사용 하지 않은 되도록 해제 \ – 사용량이 복사 작업을 수행할 수 계획 합니다.

## <a name="bkmk_prehash"></a>콘텐츠 서버에서 사전 해싱 및 데이터 패키지 만들기 계획

콘텐츠 서버에서 콘텐츠를 prehash 전에 데이터 패키지를 추가 하려면 원하는 콘텐츠를 포함 하는 파일과 폴더를 식별 해야 합니다. 

또한 호스트 캐시 서버에 복사 하기 전에 데이터 패키지를 저장할 수 있는 로컬 폴더 위치에 계획 해야 합니다.

이 가이드를 계속 하려면 참조 [BranchCache 호스트 캐시 모드 배포](4-Bc-Hcm-Deployment.md)합니다.
