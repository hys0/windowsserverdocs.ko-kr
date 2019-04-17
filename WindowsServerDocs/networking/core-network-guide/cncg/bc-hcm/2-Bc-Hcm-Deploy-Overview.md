---
title: BranchCache 호스트 캐시 모드 배포 개요
description: 이 가이드 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache 배포에 대해 설명
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 55686a9c-60dd-47f4-9f1f-fe72c2873a44
ms.author: pashort
author: shortpatti
ms.openlocfilehash: feab3156b89637f64d1af0250df459533b1662c7
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="branchcache-hosted-cache-mode-deployment-overview"></a>BranchCache 호스트 캐시 모드 배포 개요

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 가이드 호스트 BranchCache 캐시 서버 지점 컴퓨터가 도메인에 가입 하는 어디에서 배포 하는 사용할 수 있습니다. 이 항목 파악 BranchCache 캐시 모드 호스트 하는 배포 프로세스에 사용할 수 있습니다.

이 개요 BranchCache 인프라 배포 단계별 간략하게 뿐만 아니라 필요한에 포함 되어 있습니다.

## <a name="bkmk_components"></a>호스트 된 캐시 서버 배포 infrastructure

이 배포에서의 Active Directory 도메인 서비스 \(AD DS\) 서비스 연결 포인트를 사용 하 여 호스팅된 캐시 서버 배포 될 수 있는 옵션이 BranchCache와 Windows Server 2012 R2, Windows Server 2016에 및 Windows Server 2012 prehash 웹 및 파일 공유 콘텐츠를 기반 콘텐츠 서버 다음 호스트 캐시 서버에 콘텐츠를 미리 로드할 합니다.

다음 그림에서는 호스트 BranchCache 캐시 서버를 배포 하는 데 필요한 infrastructure 보여 줍니다.

![호스트 캐시 모드 BranchCache 개요](../../../media/BranchCache-Hcm-Overview/Bc-Hcm-Overview.jpg)

> [!IMPORTANT]
> 하지만이 배포 클라우드 데이터 센터의 콘텐츠 서버 보여 주며를 또는 클라우드 위치 주 사무실에 – 콘텐츠 서버에 배포 위치와 관계 없이 호스트 BranchCache 캐시 서버 배포 하는이 가이드를 사용할 수 있습니다.

### <a name="hcs1-in-the-branch-office"></a>HCS1 지사에서

이 컴퓨터 호스트 캐시 서버 구성 해야 합니다. 를 선택 하 여 호스팅된 캐시 서버에 콘텐츠를 미리 로드할 수 있도록 콘텐츠 서버 데이터 prehash 파일 및 웹 서버에서 콘텐츠를 포함 하는 데이터 패키지를 가져올 수 있습니다.

### <a name="web1-in-the-cloud-data-center"></a>클라우드 데이터 센터에 WEB1

WEB1은 BranchCache\ 가능 콘텐츠 서버입니다. 을 선택 하 여 호스팅된 캐시 서버에 콘텐츠를 미리 로드할 수 있도록 콘텐츠 서버 데이터 prehash prehash WEB1에서 공유 콘텐츠 다음 HCS1에 복사 하는 데이터 패키지를 만들 수 있습니다.

### <a name="file1-in-the-cloud-data-center"></a>클라우드 데이터 센터에 파일 1

파일 1 BranchCache\ 가능 콘텐츠 서버입니다. 을 선택 하 여 호스팅된 캐시 서버에 콘텐츠를 미리 로드할 수 있도록 콘텐츠 서버 데이터 prehash prehash 파일 1에서 공유 콘텐츠 다음 HCS1에 복사 하는 데이터 패키지를 만들 수 있습니다.
  
### <a name="dc1-in-the-main-office"></a>D c 1 주 사무실에서

D c 1 도메인 컨트롤러 이며 기본 도메인 정책 또는 다른 정책 더 적합 한 배포 서비스 연결 지점에서 있는 자동 호스트 캐시 검색을 사용 하도록 설정 하려면 그룹 정책 BranchCache 설정 구성 해야 합니다.

분기에서 클라이언트 컴퓨터 새로 그룹 정책에는이 정책 설정을 적용 때은 자동으로 찾아서 여 호스팅된 캐시 서버 지사에서 사용 하 여 시작 합니다.

### <a name="client-computers-in-the-branch-office"></a>지점에 컴퓨터 클라이언트

새로운 BranchCache 그룹 정책 설정을 적용 하려면 하 고 클라이언트가 찾아서 여 호스팅된 캐시 서버를 사용 하도록 허용 하는 클라이언트에서 그룹 정책을 복구 해야 합니다.

## <a name="bkmk_overview"></a>호스트 된 캐시 서버 배포 프로세스 개요

>[!NOTE]
>이러한 단계를 수행 하는 방법의 세부 정보 섹션에 제공 [BranchCache 호스트 캐시 모드 배포](4-Bc-Hcm-Deployment.md)합니다.

이러한 단계 BranchCache 호스트 캐시 서버 배포 프로세스에 발생 합니다.

>[!NOTE]
>아래 단계 중 일부는 prehash 호스트 캐시 서버의 콘텐츠를 미리 로드 하는 방법을 보여 주는 이러한 단계와 같은 선택적 합니다. 호스트 캐시 모드로 BranchCache 배포 하는 경우 사용자 필요 하지 않습니다 prehash 콘텐츠를 웹 및 파일 콘텐츠 서버에 데이터 패키지를 만들고 호스트 캐시 서버 콘텐츠를 미리 로드할 하기 위해 데이터 패키지 가져올. 단계는 했음을 알아차렸을 것으로 선택적 섹션 및이 섹션의 [BranchCache 호스트 캐시 모드 배포](4-Bc-Hcm-Deployment.md) 원하는 건너뛸 수 있도록 합니다.

1. HCS1에서 Windows PowerShell 명령을 사용 하 여 호스팅된 캐시 서버도 컴퓨터를 구성 하 고 서비스 연결 지점 Active Directory에 등록할 수 합니다.

2. HCS1, BranchCache 기본값 서버와 호스트 캐시 배포 목표 일치 하지 않는 경우 \(Optional\) 호스트 캐시를 할당 하려는 디스크 공간의 크기를 구성 합니다. 호스트 캐시를 선호 하는 디스크 위치를 구성할 수도 있습니다.

3. \(Optional\) prehash 서버의 콘텐츠를 콘텐츠를 호스트 캐시 서버에 데이터 패키지, 및 미리 로드 콘텐츠를 만듭니다.

    > [!NOTE]
    > 하지만 호스트 캐시 서버의 prehashing 및 미리 로드 콘텐츠는 선택적, prehash 하도록 선택 하 고 미리 로드을 수행 해야 하는 아래 단계를 모두 경우 배포에 적용할 수 있는 합니다. \ (예를 들어, 웹 서버 없는 경우 하지 필요가 prehashing 및 웹 서버 콘텐츠를 미리 로드 관련 된 단계를 수행 합니다. \)

    1. WEB1, prehash 웹 서버 콘텐츠를 다시 데이터 패키지를 만듭니다.

    2. 파일 1, 파일 서버 내용을 prehash 하 고 데이터 패키지를 만듭니다.

    3. WEB1 및 파일 1 HCS1 호스트 캐시 서버에 데이터 패키지를 복사 합니다.

    4. HCS1, 데이터 캐시 미리 로드 하는 데이터 패키지를 가져옵니다.

4. D c 1에서 그룹 정책을 BranchCache 정책 설정을 구성 하 여 도메인에 가입 지점 클라이언트 컴퓨터 호스트 캐시 모드에 대 한 구성 합니다.

5. 클라이언트 컴퓨터에서 그룹 정책을 새로 고칩니다.

이 가이드를 계속 참조 [BranchCache 호스트 캐시 모드 배포 계획](3-Bc-Hcm-Plan.md)합니다.