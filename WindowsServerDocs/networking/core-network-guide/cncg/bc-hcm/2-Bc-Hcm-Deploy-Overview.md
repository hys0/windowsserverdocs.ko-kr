---
title: BranchCache 호스트 캐시 모드 배포 개요
description: 이 가이드에서는 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache를 배포 하는 방법 지침을 제공
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: 55686a9c-60dd-47f4-9f1f-fe72c2873a44
ms.author: pashort
author: shortpatti
ms.openlocfilehash: dc6ade92eb5fe04271033973911ccb98e871d236
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406376"
---
# <a name="branchcache-hosted-cache-mode-deployment-overview"></a>BranchCache 호스트 캐시 모드 배포 개요

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

컴퓨터가 도메인에 가입 되어 있는 지점에 BranchCache 호스트 캐시 서버를 배포 하려면이 가이드를 사용할 수 있습니다. 이 항목은 BranchCache 호스트 캐시 모드 배포 프로세스의 개요를 사용할 수 있습니다.

이 개요에는 배포는 간단한 단계별 개요 뿐만 아니라 필요한 BranchCache 인프라에 포함 됩니다.

## <a name="bkmk_components"></a>호스트 캐시 서버 배포 인프라

이 배포에서는 호스트 캐시 서버는 Active Directory 도메인 서비스에 서비스 연결 지점을 사용 하 여 배포 된 \(AD DS\), Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012에서는 웹에서의 공유 콘텐츠 prehash 파일 기반된 콘텐츠 서버를 BranchCache와 옵션이 후 호스트 캐시 서버에서 콘텐츠를 미리 로드 합니다.

다음 그림에서는 BranchCache 호스트 캐시 서버를 배포 하는 데 필요한 인프라를 보여 줍니다.

![BranchCache 호스트 캐시 모드 개요](../../../media/BranchCache-Hcm-Overview/Bc-Hcm-Overview.jpg)

> [!IMPORTANT]
> 이 배포 클라우드 데이터 센터에 있는 콘텐츠 서버를 보여 주며, 있지만 배포할 콘텐츠 서버 – 본사에서 또는 클라우드 위치에 관계 없이 BranchCache 호스트 캐시 서버를 배포 하려면이 가이드를 사용할 수 있습니다.

### <a name="hcs1-in-the-branch-office"></a>지점에 HCS1

이 컴퓨터를 호스트 캐시 서버로 구성 해야 합니다. 호스트 캐시 서버에서 콘텐츠를 미리 로드할 수 있도록 콘텐츠 서버 데이터를 prehash 하기로 선택한 경우에 웹 및 파일 서버에서 콘텐츠를 포함 하는 데이터 패키지를 가져올 수 있습니다.

### <a name="web1-in-the-cloud-data-center"></a>클라우드 데이터 센터에 w e b 1

W e b 1에는 BranchCache는\-콘텐츠 서버를 사용 하도록 설정 합니다. 호스트 캐시 서버에서 콘텐츠를 미리 로드할 수 있도록 콘텐츠 서버 데이터를 prehash 하기로 선택한 경우에 WEB1 공유 콘텐츠 prehash 다음 HCS1를 복사 하는 데이터 패키지를 만들 수 있습니다.

### <a name="file1-in-the-cloud-data-center"></a>클라우드 데이터 센터에서 FILE1

FILE1는 BranchCache는\-콘텐츠 서버를 사용 하도록 설정 합니다. 호스트 캐시 서버에서 콘텐츠를 미리 로드할 수 있도록 콘텐츠 서버 데이터를 prehash 하기로 선택한 경우 파일을 1에서 공유 콘텐츠 prehash 다음 HCS1를 복사 하는 데이터 패키지를 만들 수 있습니다.
  
### <a name="dc1-in-the-main-office"></a>본사에서 d c 1

D c 1은 도메인 컨트롤러 및 기본 도메인 정책 또는 다른 정책 보다 적절 한 서비스 연결 지점에 있는 자동 호스트 캐시 검색을 사용 하도록 설정 하려면 BranchCache 그룹 정책 설정 사용 하 여 배포를 구성 해야 합니다.

분기에서 클라이언트 컴퓨터는 그룹 정책을 새로 고칠된 때이 정책 설정을 적용은 자동으로 찾아서 지점의 호스트 캐시 서버를 사용 하 여 시작 합니다.

### <a name="client-computers-in-the-branch-office"></a>지점에 클라이언트 컴퓨터

새 BranchCache 그룹 정책 설정을 적용 하 고 클라이언트를 찾아 호스트 캐시 서버를 사용 하도록 하려면 클라이언트 컴퓨터에서 그룹 정책을 새로 고쳐야 합니다.

## <a name="bkmk_overview"></a>호스트 캐시 서버 배포 프로세스 개요

>[!NOTE]
>이러한 단계를 수행 하는 방법에 대 한 세부 정보 섹션에 제공 됩니다 [BranchCache 호스트 캐시 모드 배포](4-Bc-Hcm-Deployment.md)합니다.

BranchCache 호스트 캐시 서버를 배포 하는 프로세스는 이러한 단계에서 수행 됩니다.

>[!NOTE]
>다음 단계 중 일부는 prehash 및 호스트 캐시 서버에서 콘텐츠를 미리 로드 하는 방법을 보여 주는 단계와 같은 선택적입니다. 호스트 캐시 모드로 BranchCache를 배포 하면 필요 하지 않습니다 prehash 콘텐츠를 파일과 웹 콘텐츠 서버에서 데이터 패키지를 만들려면 하 고 패키지를 가져올 데이터 콘텐츠를 사용 하 여 호스트 캐시 서버를 미리 로드 하려면. 이 섹션에서는 및 섹션의 단계를 옵션으로 명시 되어 [BranchCache 호스트 캐시 모드 배포](4-Bc-Hcm-Deployment.md) 원하는 경우 건너뛸 수 있도록 합니다.

1. 호스트 캐시 서버와 컴퓨터를 구성 하 고 Active Directory에서 서비스 연결 지점이 등록 HCS1, Windows PowerShell 명령을 사용 합니다.

2. HCS1에서 @no__t 옵션 @ no__t-1, BranchCache 기본값이 서버 및 호스트 캐시의 배포 목표와 일치 하지 않는 경우 호스트 캐시에 할당할 디스크 공간 크기를 구성 합니다. 또한 호스트 캐시에 대 한 선호 하는 디스크 위치를 구성 합니다.

3. @no__t (옵션) @ no__t-1은 콘텐츠 서버의 콘텐츠를 미리 해시 하 고, 데이터 패키지를 만들고, 호스트 캐시 서버에서 콘텐츠를 미리 로드 합니다.

    > [!NOTE]
    > 그러나 호스트 캐시 서버에서 prehashing 및 미리 로드 콘텐츠는 선택 사항, prehash 하도록 선택 하 고 미리 로드를 수행 해야 하는 다음 단계를 모두 있는 경우 적용할 수 있는 배포 합니다. \( 예를 들어 웹 서버가 없는 경우 웹 서버 콘텐츠를 미리 로드 하 고 미리 로드 하는 것과 관련 된 단계를 수행할 필요가 없습니다. \)

    1. WEB1 prehash 웹 서버 콘텐츠를 다시 데이터 패키지를 만듭니다.

    2. FILE1, prehash 파일 서버 콘텐츠를 다시 데이터 패키지를 만듭니다.

    3. W e b 1과 FILE1를 HCS1 호스트 캐시 서버에 데이터 패키지를 복사 합니다.

    4. HCS1, 데이터 캐시를 미리 로드할 데이터 패키지를 가져옵니다.

4. D c 1의 도메인에 가입 된 클라이언트 컴퓨터 본사 호스트 캐시 모드로 BranchCache 정책 설정을 사용 하 여 그룹 정책을 구성 하 여 구성 합니다.

5. 클라이언트 컴퓨터에서 그룹 정책을 새로 고칩니다.

이 가이드를 계속 하려면 참조 [BranchCache 호스트 캐시 모드 배포를 계획](3-Bc-Hcm-Plan.md)합니다.