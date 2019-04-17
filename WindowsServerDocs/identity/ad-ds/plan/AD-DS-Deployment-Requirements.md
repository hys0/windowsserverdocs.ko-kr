---
ms.assetid: e02bb152-d0db-40b0-9942-846dce75f6c7
title: "AD DS 배포 요구 사항"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 7edd7de8077a077245416f859838a6bc55415edc
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ad-ds-deployment-requirements"></a>AD DS 배포 요구 사항

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기존 환경 구조 Windows Server 2008 Active Directory Domain Services (AD DS) 배포를 위해 전략을 결정 합니다. AD DS 환경을 만드는 경우 기존 도메인 구조 없는 AD DS 환경을 만드는 시작 하기 전에 AD DS 디자인을 완료 합니다. 다음 새 숲 루트 도메인 배포 하 고 설계에 따라 도메인 구조의 나머지 부분을 배포 수 있습니다.  
  
또한 AD DS 배포의 일환으로 업그레이드 하 고 귀하의 환경 재구성 결정할 수 있습니다. 예를 들어, 조직에는 기존 Windows 2000 도메인 구조를 일부 도메인의 현재 위치에서 업그레이드를 수행 및 재구성 다른 수 있습니다. 또한 재구성 숲 간에 도메인 하거나 AD DS 배포한 후 숲에 내 도메인 재구성 환경에 보다 간단 결정할 수 있습니다.  
  
## <a name="deploying-a-windows-server-2008-forest-root-domain"></a>Windows Server 2008 숲 루트 도메인을 배포합니다.  
숲 루트 도메인 기초 AD DS 숲 인프라를 제공 합니다. AD DS을 배포 하는 숲 루트 도메인을 배포 해야 합니다. 이렇게 하려면 AD DS 디자인; 검토 해야 이렇게; DNS 서비스 구성 숲 루트 도메인 컨트롤러 배포 이렇게, 사이트 토폴로지 구성 및 (단일 유연한 마스터 작업 또는 라고도 FSMO); 마스터 역할 작업 구성으로 구성 된 숲 루트 도메인을 만듭니다. 숲 및 도메인 기능 수준 발생 하 고 있습니다. 다음 그림을 이렇게 배포 전체 프로세스를 보여 줍니다.  
  
![광고 DS 요구 사항](media/AD-DS-Deployment-Requirements/033aad0b-25ff-4793-8825-88a6daa01a55.gif)  
  
자세한 내용은 참조 [Windows Server 2008 숲 루트 도메인 배포](https://technet.microsoft.com/library/cc731174.aspx)합니다.  
  
## <a name="deploying-windows-server-2008-regional-domains"></a>Windows Server 2008 지역 도메인을 배포합니다.  
숲 루트 도메인 배포를 완료 한 후 지정 설계 된 새 Windows Server 2008 지역 도메인 모든 배포할 준비가 됩니다. 이렇게 하려면 도메인 컨트롤러 각 지역 도메인에 대 한 배포 해야 합니다. 다음 그림에서는 지역 도메인 배포 프로세스를 보여 줍니다.  
  
![광고 DS 요구 사항](media/AD-DS-Deployment-Requirements/89a878c8-9a94-4180-ad43-ca75316a6318.gif)  
  
자세한 내용은 참조 [배포 Windows Server 2008 지역 도메인](https://technet.microsoft.com/library/cc755118.aspx)합니다.  
  
## <a name="upgrading-active-directory-domains-to-windows-server-2008"></a>Windows Server 2008 Active Directory 도메인 업그레이드  
Windows 2000 또는 Windows Server 2003 도메인 Windows Server 2008 도메인에 업그레이드 Windows Server 2008 기능 및 추가 기능을 활용 하는 효율적이 고 간단한 방법입니다. 현재 네트워크와 도메인 구성 보안과 확장성 관리 효율성 네트워크 인프라를 개선 하는 동안 유지 하는 도메인 업그레이드할 수 있습니다. Windows 2000 또는 Windows Server 2003에서 Windows Server 2008으로 업그레이드 하려면 최소 네트워크 구성이 필요 합니다. 사용자의 작업이 거의 영향을 미치지도 업그레이드 합니다. 자세한 내용은 참조 [Windows Server 2008 및 Windows Server 2008 R2 AD DS 도메인에 업그레이드 Active Directory 도메인](https://technet.microsoft.com/library/cc731188.aspx)합니다.  
  
## <a name="restructuring-ad-ds-domains"></a>AD DS 도메인 재구성  
Windows Server 2008 숲 (포리스트 내 재구성) 간에 도메인, 재구성 귀하의 환경에 도메인의 수를 줄일 수 있으며 관리 복잡성 및 오버를 줄일 수 있습니다. 재구성 프로세스의 일부로 숲 간에 개체 마이그레이션, 소스 도메인와 대상 도메인 환경 모두 동시에 존재 합니다. 이렇게 하면으로 롤백할 소스 환경 마이그레이션 중 필요한 경우 수 있습니다.  
  
내 Windows Server 2008 숲 (인트라포리스트 재구성) Windows Server 2008 도메인 재구성 도메인 구조 통합할 수 있으며 관리 복잡성 및 오버를 줄일 수 있습니다. 숲에 내 도메인 재구성 마이그레이션된 계정을 원본 도메인에 더 이상 존재 합니다.  
  
도메인 재구성 Active Directory 마이그레이션 도구 (ADMT) 3.1 (ADMT v3.1) 버전을 사용 하는 방법에 대 한 자세한 내용은 참조 [ADMT v3.1 마이그레이션 가이드](https://go.microsoft.com/fwlink/?LinkId=93678)합니다.  
  


