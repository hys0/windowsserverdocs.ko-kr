---
title: 데스크톱 호스팅 환경 이해
description: Azure IaaS를 사용하는 RDS 배포의 개요입니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 08/01/2016
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 1bd672c52c892430339bb6c17c6324bf4d6d79a1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387815"
---
# <a name="understanding-the-desktop-hosting-environment"></a>데스크톱 호스팅 환경 이해

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

다음 정보는 데스크톱 호스팅 서비스의 구성 요소에 대해 설명합니다.  
  
## <a name="tenant-environment"></a>테넌트 환경  
서비스 공급자의 데스크톱 호스팅 서비스는 일련의 격리된 테넌트 환경으로 구현됩니다. 각 테넌트의 환경은 격리된 가상 네트워크를 통해 통신하는 스토리지 컨테이너, 가상 머신 세트 및 Azure 서비스 조합으로 구성됩니다. 각 가상 머신에는 테넌트의 호스팅된 데스크톱 환경을 이루는 하나 이상의 구성 요소가 포함되어 있습니다. 다음 하위 섹션에서는 각 테넌트의 호스팅된 데스크톱 환경을 이루는 구성 요소를 설명합니다.

## <a name="remote-desktop-services"></a>원격 데스크톱 서비스
데스크톱 호스팅 환경에서 다양한 가상 머신에서 다음과 같은 원격 데스크톱 서비스 역할이 설치됩니다.

  - 원격 데스크톱 연결 브로커
  - 원격 데스크톱 게이트웨이
  - 원격 데스크톱 라이선싱
  - 원격 데스크톱 세션 호스트
  - 원격 데스크톱 웹 액세스

이러한 각 역할 및 서로 상호 작용하는 방법에 대한 자세한 내용은 [RDS 역할 이해](Understanding-RDS-roles.md) 문서를 검토하세요.
  
##  <a name="azure-active-directory-domain-services"></a>(Azure) Active Directory Domain Services  
Azure의 데스크톱 호스팅 환경에서 AD DS(Active Directory Domain Services)에 연결하고 관리하는 여러 가지 방법이 있습니다.

1. 테넌트의 환경에서 AD DS 역할을 실행하는 가상 머신 만들기
2. 기존 AD DS를 사용하도록 테넌트의 온-프레미스 환경에 대해 사이트 간 VPN 연결 만들기
3. 테넌트의 Azure Active Directory를 기준으로 테넌트의 가상 네트워크에서 도메인을 만드는 Azure AD Domain Services PaaS 역할 사용

원격 데스크톱 서비스를 사용할 경우 테넌트에는 환경에 대한 액세스, 사용자 프로필 스토리지 및 배포 내의 모니터링을 관리하기 위해 Active Directory가 있어야 합니다. 표준(비 Azure) AD DS를 사용할 경우 테넌트의 포리스트는 서비스 공급자의 관리 포리스트와의 트러스트 관계가 필요하지 않습니다. 테넌트의 도메인에 도메인 관리자 계정을 설정하면 서비스 공급자의 기술 담당자가 테넌트 환경에서 관리 작업(예: 시스템 상태 모니터링 및 소프트웨어 업데이트 적용)을 수행할 수 있고, 문제 해결 및 구성에 도움이 될 수 있습니다.  
    
추가 정보:  
[Azure Active Directory Domain Services 설명서](https://azure.microsoft.com/documentation/services/active-directory-ds/)  
[Azure Virtual Network에서 새 Active Directory 포리스트 설치](https://azure.microsoft.com/documentation/articles/active-directory-new-forest-virtual-machine/)  
[Azure Portal을 사용하여 사이트 간 VPN 연결을 사용하여 Resource Manager VNet 만들기](https://azure.microsoft.com/documentation/articles/vpn-gateway-howto-site-to-site-resource-manager-portal/)  
  
## <a name="azure-sql-database"></a>Azure SQL 데이터베이스  
Azure SQL Database를 사용하면 호스터가 전체 SQL Server Always-On 클러스터를 배포 및 유지 관리하지 않고도 원격 데스크톱 서비스 배포를 확장할 수 있습니다. Azure SQL Database는 원격 데스크톱 연결 브로커가 현재 사용자의 호스트 서버 연결 매핑과 같은 배포 정보를 저장하는 데 사용합니다. 다른 Azure 서비스와 마찬가지로, Azure SQL DB는 모든 규모의 배포에 적합한 소비 모델을 따릅니다.   
  
추가 정보:  
[SQL Database란?](https://azure.microsoft.com/documentation/articles/sql-database-technical-overview/)  
  
## <a name="azure-active-directory-application-proxy"></a>Azure Active Directory 애플리케이션 프록시  
Azure Active Directory Application Proxy는 Azure Active Directory의 유료 SKU에 제공되는 서비스로, 사용자가 Azure의 고유한 역방향 프록시 서비스를 통해 내부 애플리케이션에 연결할 수 있도록 합니다. 이를 통해 RD 웹 및 RD 게이트웨이 엔드포인트를 가상 네트워크 내에서 숨길 수 있으므로 공용 IP 주소를 통해 인터넷에 노출할 필요가 없습니다. 또한 호스터가 전체 배포를 유지하면서 테넌트 환경의 가상 머신 수를 축소할 수 있습니다.
  
추가 정보:  
[Azure AD 애플리케이션 프록시 사용](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-enable/)  
    
## <a name="file-server"></a>파일 서버  
파일 서버는 SMB(서버 메시지 블록) 3.0 프로토콜을 사용하여 공유 폴더를 제공합니다. 공유 폴더는 사용자 프로필 디스크 파일(.vhdx)을 만들고 저장하며, 데이터를 백업하고, 사용자가 테넌트의 가상 네트워크에서 다른 사용자와 데이터를 공유할 수 있도록 하는 데 사용됩니다.
  
파일 서버를 배포하는 데 사용하는 VM에는 Azure 데이터 디스크가 연결되어 있고 공유 폴더가 구성되어 있어야 합니다. Azure 데이터 디스크는 동시 쓰기 캐시를 사용하여 디스크에 대한 쓰기가 VM을 다시 시작해도 유지되도록 합니다.  
  
소규모 테넌트의 경우, 테넌트 환경의 단일 가상 머신에서 RD 연결 브로커 및 RD 라이선싱 역할을 실행하는 가상 머신에 파일 서버를 결합하여 비용을 줄일 수 있습니다.  
  
추가 정보  
[파일 및 스토리지 서비스 개요](https://technet.microsoft.com/library/hh831487.aspx)  
[가상 머신에 데이터 디스크를 연결하는 방법](http://www.windowsazure.com/manage/windows/how-to-guides/attach-a-disk/)  
  
### <a name="user-profile-disks"></a>사용자 프로필 디스크  
사용자 프로필 디스크는 사용자가 한 컬렉션에 있는 RD 세션 호스트 서버의 세션에 로그인된 경우 개인 설정 및 파일을 저장한 후 해당 컬렉션의 다른 RD 세션 호스트 서버에 로그인할 때 동일한 설정 및 파일에 액세스할 수 있게 해줍니다. 사용자가 처음 로그인하면 테넌트의 파일 서버에 사용자 프로필 디스크가 생성되고, 해당 디스크는 사용자가 연결된 RD 세션 호스트 서버에 탑재됩니다. 이후 로그인할 때마다 사용자 프로필 디스크가 적절한 RD 세션 호스트 서버에 마운트되고, 로그아웃할 때마다 탑재 해제됩니다. 프로필 디스크의 내용은 해당 사용자만 액세스할 수 있습니다.  
  


