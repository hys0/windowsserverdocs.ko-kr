---
title: 데스크톱 호스팅 서비스
description: 데스크톱 호스팅 서비스의 구성 요소를 설명합니다.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 07/06/2018
ms.topic: article
author: heidilohr
manager: lizross
ms.openlocfilehash: 64e433ed379ca322996bcfe2d0ddd513e074b85e
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "80854716"
---
# <a name="desktop-hosting-service"></a>데스크톱 호스팅 서비스

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

이 문서에서는 서비스의 구성 요소를 호스팅하는 데스크톱에 대해 자세히 알려줍니다.

## <a name="tenant-environment"></a>테넌트 환경

[원격 데스크톱 서비스 역할](rds-roles.md)에 설명된 대로, 각 역할은 테넌트 환경에서 고유한 몫을 합니다.

서비스 공급자의 데스크톱 호스팅 서비스는 일련의 격리된 테넌트 환경으로 구현됩니다. 각 테넌트의 환경은 격리된 가상 네트워크를 통해 통신하는 스토리지 컨테이너, 가상 머신 세트 및 Azure 서비스 조합으로 구성됩니다. 각 가상 머신에는 테넌트의 호스팅된 데스크톱 환경을 이루는 하나 이상의 구성 요소가 포함되어 있습니다. 다음 하위 섹션에서는 각 테넌트의 호스팅된 데스크톱 환경을 이루는 구성 요소를 설명합니다.

## <a name="active-directory-domain-services"></a>Active Directory 도메인 서비스

AD DS(Active Directory Domain Services)는 테넌트의 사용자가 데스크톱 및 애플리케이션에 로그인하여 워크로드를 수행할 수 있도록 도메인과 포리스트 정보를 제공합니다. 따라서 Windows 애플리케이션에 필요한 파일 공유 및 데이터베이스를 설정하거나 연결할 수도 있습니다.

테넌트의 포리스트는 서비스 공급자의 관리 포리스트와의 트러스트 관계가 필요하지 않습니다. 테넌트의 도메인에 도메인 관리자 계정을 설정하면 서비스 공급자의 기술 담당자가 테넌트 환경에서 관리 작업(예: 시스템 상태 모니터링 및 소프트웨어 업데이트 적용)을 수행할 수 있고, 문제 해결 및 구성에 도움이 될 수 있습니다.

AD DS를 배포하는 방법은 여러 가지가 있습니다.

1. 테넌트의 가상 네트워킹 환경에서 Azure Active Directory Domain Services를 사용하도록 설정합니다. 그러면 Azure AD에 존재하는 사용자와 그룹에 따라 테넌트의 관리형 AD DS 인스턴스가 생성됩니다.
2. 테넌트의 가상 네트워킹 환경에 독립 실행형 AD DS 서버를 설정합니다. 이렇게 하면 가상 머신에서 실행 중인 모든 AD DS 인스턴스를 완벽하게 제어할 수 있습니다.
3. 테넌트의 프레미스에 있는 AD DS 서버에 대한 사이트 간 VPN 연결을 만듭니다. 이렇게 하면 테넌트가 기존 AD DS 인스턴스에 연결하고, 사용자, 그룹, 조직 단위 등의 중복을 줄일 수 있습니다.

자세한 내용은 다음 문서를 참조하세요.

* [Azure Active Directory Domain Services 설명서](https://docs.microsoft.com/azure/active-directory-domain-services/)
* [Windows Server 2012 R2 데스크톱 호스팅 참조 아키텍처 가이드](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)
* [Azure Portal에서 사이트 간 연결 만들기](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)

## <a name="sql-database"></a>SQL Database

원격 데스크톱 연결 브로커는 고가용성 SQL Database를 사용하여 현재 사용자의 호스트 서버 연결 매핑과 같은 배포 정보를 저장합니다.

SQL Database를 배포하는 방법은 여러 가지가 있습니다.

1. 테넌트의 환경에서 Azure SQL Database를 만듭니다. 이렇게 하면 서버 자체를 관리할 필요 없이 중복 SQL Database의 기능을 사용할 수 있습니다. 또한 인프라에 투자하는 대신 사용하는 만큼만 요금을 지불할 수 있습니다.
2. SQL Server AlwaysOn 클러스터를 만듭니다. 그러면 기존 SQL Server 인프라를 활용할 수 있으며 SQL Server 인스턴스를 완전히 제어할 수 있습니다.

고가용성 SQL Database 인프라를 설정하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

* [Azure SQL Database 서비스란?](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview)
* [가용성 그룹(SQL Server) 생성 및 구성](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server?view=sql-server-2017)
* [배포에 RD 연결 브로커 서버 추가 및 고가용성 구성](rds-connection-broker-cluster.md)

## <a name="file-server"></a>파일 서버

파일 서버는 SMB(서버 메시지 블록) 3.0 프로토콜을 사용하여 공유 폴더를 제공합니다. 이러한 공유 폴더는 사용자 프로필 디스크 파일(.vhdx)을 만들고 저장하여 데이터를 백업하는 데 사용되며, 사용자가 테넌트의 클라우드 서비스 내에서 데이터를 서로 공유할 수 있게 해줍니다.

파일 서버를 배포하는 가상 머신에는 Azure 데이터 디스크가 연결되어 있고 공유 폴더가 구성되어 있어야 합니다. Azure 데이터 디스크는 동시 쓰기 캐싱을 사용하므로 가상 머신이 다시 시작될 때마다 디스크에 기록된 데이터가 지워지지 않습니다.

소규모 테넌트는 파일 서버와 [RD 라이선싱 역할](rds-roles.md#remote-desktop-licensing)을 테넌트 환경의 단일 가상 머신에 결합하여 비용을 줄일 수 있습니다.

자세한 내용은 다음 문서를 참조하세요.

* [Windows Server의 스토리지](../../storage/storage.md)
* [Azure Portal에서 Windows VM에 관리형 데이터 디스크를 연결하는 방법](https://docs.microsoft.com/azure/virtual-machines/windows/attach-managed-disk-portal?toc=%2Fazure%2Fvirtual-machines%2Fwindows%2Fclassic%2Ftoc.json)

### <a name="user-profile-disks"></a>사용자 프로필 디스크

사용자 프로필 디스크는 사용자가 한 컬렉션에 있는 RD 세션 호스트 서버의 세션에 로그인된 경우 개인 설정 및 파일을 저장한 후 해당 컬렉션의 다른 [RD 세션 호스트](rds-roles.md#remote-desktop-session-host) 서버에 로그인할 때 동일한 설정 및 파일에 액세스할 수 있게 해줍니다. 사용자가 처음 로그인하면 테넌트의 파일 서버가 사용자가 현재 연결된 RD 세션 호스트 서버에 탑재되는 사용자 프로필 디스크를 만듭니다. 이후 로그인할 때마다 사용자 프로필 디스크가 적절한 RD 세션 호스트 서버에 마운트되고, 로그아웃할 때마다 탑재 해제됩니다. 해당 사용자만 프로필 디스크의 콘텐츠에 액세스할 수 있습니다.