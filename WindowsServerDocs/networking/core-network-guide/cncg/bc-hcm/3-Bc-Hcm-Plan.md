---
title: BranchCache 캐시 모드 호스트 배포 계획
description: 이 가이드 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache 배포에 대해 설명
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: bc44a7db-f7a5-4e95-9d95-ab8d334e885f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e645dd96ec85e3a23df6717cfa43d7627cb938e7
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="branchcache-hosted-cache-mode-deployment-planning"></a>BranchCache 캐시 모드 호스트 배포 계획

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목 호스트 캐시 모드로 BranchCache 한 배포를 계획을 사용할 수 있습니다.

>[!IMPORTANT]
>Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 여 호스팅된 캐시 서버 실행 해야 합니다.

여 호스팅된 캐시 서버를 배포 하기 전에 다음과 같은 항목을 계획 해야 합니다.

- [기본 서버 구성 계획](#bkmk_basic)

- [요금제 도메인 액세스](#bkmk_domain)

- [호스트 캐시의 크기와 위치 계획](#bkmk_cachelocation)

- [계획 하는 콘텐츠 서버 패키지 복사 하는 공유](#bkmk_package)

- [요금제 prehashing 및 데이터 패키지 콘텐츠 서버에 만들기](#bkmk_prehash)

## <a name="bkmk_basic"></a>기본 서버 구성 계획
  
기존 서버 여 호스팅된 캐시 서버에 지사에서 사용 하 여 계획 하는 경우 컴퓨터 라고 이미 있으며 IP 주소 구성을 때문에이 계획 단계를 수행할 필요가 없습니다.

Windows Server 2016 호스트 캐시 서버의 설치한 후 컴퓨터의 이름을 바꿉니다 및 지정 하 고 구성 해야 로컬 컴퓨터에서 고정 IP 주소를 합니다.

>[!NOTE]
>하지만이 가이드에서는 호스트 캐시 서버에 배포를 위해 적합 한 서버 이름을 사용 해야, HCS1 라고 합니다.

## <a name="bkmk_domain"></a>요금제 도메인 액세스

기존 서버 여 호스팅된 캐시 서버에 지사에서 사용 하 여 계획 하는 경우 컴퓨터는 현재 도메인에 가입 하지 않은 계획이 단계를 수행 필요가 하지 합니다.
  
도메인에 로그온 할 때 켜져 있어야 하는 도메인 회원 컴퓨터와 사용자 계정에에서 만들어야 AD DS 로그온 시도가 하기 전에 합니다. 뿐만 아니라 도메인 적절 한 그룹 구성원 있는 계정으로 컴퓨터를 속해야 합니다.

## <a name="bkmk_cachelocation"></a>호스트 캐시의 크기와 위치 계획

HCS1, 위치 호스트 캐시 서버의 찾으려는 호스트 캐시를 결정 합니다. 예를 들어, 하드 디스크, 볼륨 및 캐시 저장 하려는 폴더 위치를 결정 합니다.

또한 호스트 캐시를 할당 하려는의 디스크 공간이 비율 결정 합니다.

## <a name="bkmk_package"></a>계획 하는 콘텐츠 서버 패키지 복사 하는 공유

콘텐츠 서버에 데이터 패키지를 만든 후 복사 해야 네트워크를 공유 하 여 호스팅된 캐시 서버에 합니다.

폴더 위치 하 고 공유 된 폴더에 대 한 권한 공유할 예정입니다. 또한 콘텐츠 서버 많은 양의 데이터를 호스트 하는 경우 사용자가 만든 패키지 큰 파일 됩니다 계획을 WAN 대역폭이 대역폭 일반 업무에 사용 해야 다른 시간 동안 복사 작업으로 사용 되지 않도록 off\-사용량이 복사 작업을 수행 합니다.

## <a name="bkmk_prehash"></a>요금제 prehashing 및 데이터 패키지 콘텐츠 서버에 만들기

콘텐츠 서버에 콘텐츠를 prehash 전에 데이터 패키지를 추가 하려면 콘텐츠가 포함 된 파일과 폴더를 확인 해야 합니다. 

또한 호스트 캐시 서버에 복사 하기 전에 데이터 패키지를 저장할 수 있는 로컬 폴더 위치에 계획 해야 합니다.

이 가이드를 계속 참조 [BranchCache 호스트 캐시 모드 배포](4-Bc-Hcm-Deployment.md)합니다.
