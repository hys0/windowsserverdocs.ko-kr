---
ms.assetid: e02bb152-d0db-40b0-9942-846dce75f6c7
title: AD DS 배포 요구 사항
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: dff95633b71d42e25aad33793abd609ac61adbdf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822926"
---
# <a name="ad-ds-deployment-requirements"></a>AD DS 배포 요구 사항

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기존 환경의 구조는 Windows Server 2008 Active Directory 도메인 서비스 (AD DS)를 배포 하기 위한 전략을 결정 합니다. AD DS 환경을 만들고 있는 경우 기존 도메인 구조 없는 AD DS 환경 만들기를 시작 하기 전에 AD DS 디자인을 완료 합니다. 그런 다음 새 포리스트 루트 도메인을 배포 하 고 디자인에 따라 도메인 구조의 나머지 부분을 배포할 수 있습니다.  
  
또한 AD DS 배포의 일환으로 업그레이드 하 고 사용자 환경의 구조를 변경 하는 경우가 있습니다. 예를 들어, 조직에서는 기존 Windows 2000 도메인 구조를 일부 도메인의 전체 업그레이드를 수행 하 고 다른 재구성할 수 있습니다. 또한 포리스트 간에 도메인 구조 변경 하거나 AD DS를 배포한 후 포리스트 내의 도메인 구조 변경 하 여 사용자 환경의 복잡성을 줄일 수도 있습니다.  
  
## <a name="deploying-a-windows-server-2008-forest-root-domain"></a>Windows Server 2008 포리스트 루트 도메인 배포  
AD DS 포리스트 인프라에 기반을 제공 하는 포리스트 루트 도메인. AD DS를 배포 하려면 먼저 포리스트 루트 도메인을 배포 해야 합니다. 이 작업을 수행 하려면 AD DS 디자인; 검토 해야 포리스트 루트 도메인;에 대 한 DNS 서비스를 구성 합니다. 포리스트 루트 도메인 컨트롤러를 배포, 포리스트 루트 도메인에 대 한 사이트 토폴로지를 구성 및 라고도 신축 단일 마스터 작업 또는 FSMO (); 작업 마스터 역할 구성 요소로 이루어진 포리스트 루트 도메인 만들기 포리스트 및 도메인 기능 수준 올리기 하 고 있습니다. 다음 그림에서는 포리스트 루트 도메인을 배포 하는 전체 프로세스를 보여 줍니다.  
  
![AD DS 요구 사항](media/AD-DS-Deployment-Requirements/033aad0b-25ff-4793-8825-88a6daa01a55.gif)  
  
자세한 내용은 참조 [Windows Server 2008 포리스트 루트 도메인 배포](https://technet.microsoft.com/library/cc731174.aspx)합니다.  
  
## <a name="deploying-windows-server-2008-regional-domains"></a>Windows Server 2008 지역 도메인 배포  
포리스트 루트 도메인의 배포를 완료 한 후 새 Windows Server 2008 지역 도메인 디자인 하 여 지정 된 배포 준비가 되었습니다. 이 위해 각 지역 도메인에 대 한 도메인 컨트롤러를 배포 해야 합니다. 다음 그림에서는 지역 도메인 배포 프로세스를 보여 줍니다.  
  
![AD DS 요구 사항](media/AD-DS-Deployment-Requirements/89a878c8-9a94-4180-ad43-ca75316a6318.gif)  
  
자세한 내용은 참조 [배포 Windows Server 2008 지역 도메인](https://technet.microsoft.com/library/cc755118.aspx)합니다.  
  
## <a name="upgrading-active-directory-domains-to-windows-server-2008"></a>Active Directory 도메인의 Windows Server 2008로 업그레이드  
Windows Server 2008 도메인에 Windows 2000 또는 Windows Server 2003 도메인을 업그레이드 하는 것은 추가 Windows Server 2008 기능 및 기능을 활용 하는 효율적이 고 간단한 방법입니다. 보안, 확장성 및 네트워크 인프라의 관리 효율성을 개선 하는 동안 현재 네트워크 및 도메인 구성 유지 관리 하는 도메인을 업그레이드할 수 있습니다. Windows 2000 또는 Windows Server 2003에서 Windows Server 2008로 업그레이드 최소한의 네트워크 구성이 필요 합니다. 사용자 작업에 거의 영향을 주지를 역시 업그레이드 합니다. 자세한 내용은 참조 [Windows Server 2008 및 Windows Server 2008 R2 AD DS 도메인에 Active Directory 도메인 업그레이드](https://technet.microsoft.com/library/cc731188.aspx)합니다.  
  
## <a name="restructuring-ad-ds-domains"></a>AD DS 도메인 구조 변경  
Windows Server 2008 포리스트 (포리스트 간 재구성) 간에 도메인을 재구성 하는 경우에 사용자 환경에서 도메인의 수를 줄일 수 있으며 관리 복잡성과 오버 헤드를 줄일 수 있습니다. 이 단계의 일부로 포리스트 간에 개체 재구성 프로세스를 마이그레이션할 원본 도메인 및 대상 도메인 환경 모두 동시에 존재 합니다. 이렇게 하면 롤백할 소스 환경으로 마이그레이션하는 동안 필요한 경우를 수 있습니다.  
  
Windows Server 2008 포리스트 (포리스트 간 재구성) 내의 Windows Server 2008 도메인을 재구성 하는 경우에 도메인 구조를 통합할 수 있으며 관리 복잡성과 오버 헤드를 줄일 수 있습니다. 포리스트 내의 도메인을 재구성 하는 경우 마이그레이션된 계정을 원본 도메인에서 더 이상 없습니다.  
  
도메인 구조 변경 Active Directory 마이그레이션 도구 (ADMT) 버전 3.1 (ADMT v3.1)를 사용 하는 방법에 대 한 자세한 내용은 참조 [ADMT v3.1 마이그레이션 가이드](https://go.microsoft.com/fwlink/?LinkId=93678)합니다.  
  


