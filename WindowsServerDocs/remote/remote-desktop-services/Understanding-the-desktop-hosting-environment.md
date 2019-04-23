---
title: 데스크톱 호스팅 환경 이해
description: Azure IaaS를 사용 하 여 RDS deployhment 간략하게 설명 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 08/01/2016
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 880fc8f9fa2db5ec56d2117e02c069650c61584a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877924"
---
# <a name="understanding-the-desktop-hosting-environment"></a>데스크톱 호스팅 환경 이해

>적용 대상: Windows Server (반기 채널), Windows Server 2016

다음 정보는 데스크톱 호스팅 서비스의 구성 요소를 설명 합니다.  
  
## <a name="tenant-environment"></a>테 넌 트 환경  
데스크톱 호스팅 서비스 공급자의 격리 된 테 넌 트 환경 집합으로 구현 됩니다. 각 테 넌 트 환경 저장소 컨테이너, 가상 머신 집합 및 격리 된 virtual network를 통해 모든 통신 Azure 서비스의 조합으로 구성 됩니다. 각 가상 컴퓨터에는 테 넌 트의 호스 티 드 데스크톱 환경을 구성 하는 구성 요소 중 하나 이상을 포함 합니다. 다음 하위 섹션에서는 각 테 넌 트의 호스 티 드 데스크톱 환경을 구성 하는 구성 요소를 설명 합니다.

## <a name="remote-desktop-services"></a>원격 데스크톱 서비스
데스크톱 호스팅 환경에서 다양 한 가상 컴퓨터 간에 다음과 같은 원격 데스크톱 서비스 역할 설치 됩니다.

  - 원격 데스크톱 연결 브로커
  - 원격 데스크톱 게이트웨이
  - 원격 데스크톱 라이선싱
  - 원격 데스크톱 세션 호스트
  - 원격 데스크톱 웹 액세스

각 이러한 역할 및 서로 상호 작용 하는 방법에 대 한 자세한 내용은 참조 하십시오 합니다 [이해 RDS 역할](Understanding-RDS-roles.md) 문서.
  
##  <a name="azure-active-directory-domain-services"></a>(Azure) Active Directory Domain Services  
여러 가지 방법으로 연결 하 고 Azure에서 데스크톱 호스팅 환경에 대 한 Active Directory Domain Services (AD DS)를 관리 합니다.

1. AD DS 역할을 실행 하는 테 넌 트의 환경에서 가상 머신 만들기
2. 기존 AD DS를 사용 하도록 테 넌 트의 온-프레미스 환경을 사용 하 여 사이트 간 VPN 연결 만들기
3. 테 넌 트의 테 넌 트의 Azure Active Directory를 기반으로 가상 네트워크에서 도메인을 만드는 Azure AD Domain Services PaaS 역할을 사용 하 여

원격 데스크톱 서비스를 사용 하 여 테 넌 트 환경에서 사용자 프로필 저장소에 대 한 액세스를 관리 하려면 Active Directory 있어야 배포 내에서 모니터링 하 고 있습니다. 표준 (비 Azure) AD DS를 사용 하는 경우 테 넌 트의 포리스트는 공급자의 관리 포리스트와 트러스트 관계를 필요 하지 않습니다. 도메인 관리자 계정이 설정할 수 있습니다 테 넌 트의 도메인 공급자의 기술 담당자 (예: 시스템 상태를 모니터링 하 고 소프트웨어 업데이트를 적용) 테 넌 트의 환경에서 관리 작업을 수행 하는 데 도움이 수 있도록 문제 해결 및 구성 합니다.  
    
추가 정보:  
[Azure Active Directory Domain Services 설명서](https://azure.microsoft.com/documentation/services/active-directory-ds/)  
[Azure 가상 네트워크에 새 Active Directory 포리스트 설치](https://azure.microsoft.com/documentation/articles/active-directory-new-forest-virtual-machine/)  
[Azure Portal을 사용 하 여 사이트 간 VPN 연결을 사용 하 여 리소스 관리자 VNet 만들기](https://azure.microsoft.com/documentation/articles/vpn-gateway-howto-site-to-site-resource-manager-portal/)  
  
## <a name="azure-sql-database"></a>Azure SQL 데이터베이스  
Azure SQL Database 호스팅 서비스 공급자를 배포 하 여 전체 SQL Server Always-On 클러스터를 유지 관리 하지 않고도 원격 데스크톱 서비스 배포를 확장할 수 있습니다. Azure SQL Database는 현재 사용자가 최종 호스트 서버에 연결의 매핑 같은 배포 정보를 저장 하 원격 데스크톱 연결 브로커에서 사용 됩니다. 다른 Azure 서비스와 마찬가지로 Azure SQL DB는 모든 규모의 배포에 대 한 이상적인 소비 모델을 따릅니다.   
  
추가 정보:  
[SQL Database 란?](https://azure.microsoft.com/documentation/articles/sql-database-technical-overview/)  
  
## <a name="azure-active-directory-application-proxy"></a>Azure Active Directory 응용 프로그램 프록시  
Azure Active Directory Application Proxy는 유료 Sku Azure Active Directory의 사용자가 Azure의 역방향 프록시 서비스를 통해 내부 응용 프로그램에 연결할 수 있도록에서 제공 하는 서비스. 이렇게 하면 RD 웹 및 RD 게이트웨이 끝점을 공용 IP 주소를 통해 인터넷에 노출 될 필요가 없도록 하 여 가상 네트워크 내에서 숨길 수 있습니다. 추가 호스팅 서비스 공급자를 전체 배포를 유지 하면서 테 넌 트의 환경에서 가상 머신의 수를 축소 하 수 있습니다.
  
추가 정보:  
[Azure AD 응용 프로그램 프록시를 사용 하도록 설정](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-enable/)  
    
## <a name="file-server"></a>파일 서버  
파일 서버는 서버 메시지 블록 (SMB) 3.0 프로토콜을 사용 하 여 공유 폴더를 제공 합니다. 공유 폴더 만들기 및 백업 데이터를 사용자 프로필 디스크 (.vhdx) 파일을 저장 하 고 허용 사용자 테 넌 트의 가상 네트워크 내에서 다른 사용자를 사용 하 여 데이터를 공유할 수 있는 위치에 사용 됩니다.
  
파일 서버를 배포 하는 데 사용 하는 VM에 연결 하 고 공유 폴더를 사용 하 여 구성 된 Azure 데이터 디스크를 있어야 합니다. Azure 데이터 디스크는 write-through 캐싱을 보장 디스크에 기록 하는 VM의 다시 시작 후 유지 되는 사용 합니다.  
  
작은 테 넌 트에 대 한 테 넌 트의 환경에서 단일 가상 컴퓨터에서 RD 라이선싱 및 RD 연결 브로커 역할을 실행 하는 가상 컴퓨터를 사용 하 여 파일 서버를 결합 하 여 비용을 줄일 수 있습니다.  
  
추가 정보  
[File and Storage Services 개요](https://technet.microsoft.com/library/hh831487.aspx)  
[가상 머신에 데이터 디스크를 연결 하는 방법](http://www.windowsazure.com/manage/windows/how-to-guides/attach-a-disk/)  
  
### <a name="user-profile-disks"></a>사용자 프로필 디스크  
사용자 프로필 디스크 사용자가 컬렉션의 RD 세션 호스트 서버의 세션에 로그인 되어 있는 경우 개인 설정 및 파일을 저장 하도록 허용 하 고 컬렉션의 다른 RD 세션 호스트 서버에 로그인 할 때 동일한 설정 및 파일에 액세스할 수 있습니다. 사용자는 처음 로그인 하면 테 넌 트의 파일 서버에서 사용자 프로필 디스크 만들어지고 해당 디스크는 사용자가 연결 된 RD 세션 호스트 서버에 탑재 됩니다. 각 후속 로그인에 대 한 적절 한 RD 세션 호스트 서버에서 사용자 프로필 디스크를 탑재 되어 이므로 각 로그 아웃 되지 않은 unted 합니다. 프로필 디스크의 내용은 해당 사용자만 액세스할 수 있습니다.  
  


