---
title: 데스크톱 호스팅 서비스
description: 데스크톱 호스팅 서비스의 구성 요소를 설명 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 07/06/2018
ms.tgt_pltfrm: na
ms.topic: article
author: heidilohr
manager: dougkim
ms.openlocfilehash: adbb9fd69bc61d2e877cadb0484a4e42093f262a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840474"
---
# <a name="desktop-hosting-service"></a>데스크톱 호스팅 서비스

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 문서에서는 자세히 알려줍니다는 데스크톱 호스팅 서비스의 구성 요소에 대 한 합니다.

## <a name="tenant-environment"></a>테 넌 트 환경

에 설명 된 대로 [원격 데스크톱 서비스 역할](rds-roles.md), 테 넌 트 환경에서 고유한 부분을 수행 하는 각 역할입니다.

데스크톱 호스팅 서비스 공급자의 격리 된 테 넌 트 환경 집합으로 구현 됩니다. 각 테 넌 트 환경 저장소 컨테이너, 가상 머신 집합 및 격리 된 virtual network를 통해 모든 통신 Azure 서비스의 조합으로 구성 됩니다. 각 가상 컴퓨터에는 테 넌 트의 호스 티 드 데스크톱 환경을 구성 하는 구성 요소 중 하나 이상을 포함 합니다. 다음 하위 섹션에서는 각 테 넌 트의 호스 티 드 데스크톱 환경을 구성 하는 구성 요소를 설명 합니다.

## <a name="active-directory-domain-services"></a>Active Directory 도메인 서비스

테 넌 트의 사용자가 응용 프로그램 워크 로드를 수행 하 고 데스크톱에 로그인 할 수 있도록 active Directory Domain Services (AD DS) 도메인 및 포리스트 정보를 제공 합니다. 이렇게 할 수를 설정 하거나 필요한 파일 공유 및 Windows 응용 프로그램에 필요할 수 있는 데이터베이스에 연결 합니다.

테 넌 트의 포리스트 공급자의 관리 포리스트 트러스트 관계가 필요 하지 않습니다. 도메인 관리자 계정이 설정할 수 있습니다 테 넌 트의 도메인 공급자의 기술 담당자 (예: 시스템 상태를 모니터링 하 고 소프트웨어 업데이트를 적용) 테 넌 트의 환경에서 관리 작업을 수행 하는 데 도움이 수 있도록 문제 해결 및 구성 합니다.

여러 가지 방법으로 AD DS를 배포할 수 있습니다.

1. 테 넌 트의 가상 네트워킹 환경에서 Azure Active Directory Domain Services를 사용 하도록 설정 합니다. 이 사용자와 Azure AD에 존재 하는 그룹에 따라 테 넌 트를 관리 되는 AD DS 인스턴스를 만듭니다.
2. 테 넌 트의 가상 네트워킹 환경에서 독립 실행형 AD DS 서버를 설정 합니다. 이렇게 하면 모든 가상 머신에서 실행 되는 AD DS 인스턴스의 전체 제어 합니다.
3. 테 넌 트의 온-프레미스에 있는 AD DS 서버에 사이트 간 VPN 연결을 만듭니다. 따라서 테 넌 트를에 기존 AD DS 인스턴스에 연결 하 고 사용자, 그룹, 조직 구성 단위 및 등의 중복을 줄일 수 있습니다.

자세한 내용은 다음 문서를 참조하세요.

* [Azure Active Directory Domain Services 설명서](https://docs.microsoft.com/azure/active-directory-domain-services/)
* [데스크톱 호스팅 참조 아키텍처 가이드 Windows Server 2012 r2](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)
* [Azure portal에서 사이트 간 연결 만들기](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)

## <a name="sql-database"></a>SQL 데이터베이스(SQL database)

항상 사용 가능한 SQL database는 현재 사용자가 호스트 서버에 연결의 매핑 같은 배포 정보를 저장 하 원격 데스크톱 연결 브로커에서 사용 됩니다.

SQL 데이터베이스를 배포 하는 방법은 여러 가지 있습니다.

1. 테 넌 트의 환경에서 Azure SQL Database를 만듭니다. 이렇게 하면 중복 SQL database의 기능을 사용 하 여 서버 자체를 관리 하지 않아도 됩니다. 또한 인프라에 투자 하는 대신 사용 하는 것에 대 한 요금을 지불 수도 있습니다.
2. SQL Server AlwaysOn 클러스터를 만듭니다. 기존 SQL Server 인프라를 활용할 수 있습니다 하 고 SQL Server 인스턴스를 완전히 제어를 제공 합니다.

항상 사용 가능한 SQL 데이터베이스 인프라를 설정 하는 방법에 대 한 자세한 내용은 다음 문서를 참조 합니다.

* [Azure SQL Database 서비스란 무엇입니까?](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview)
* [가용성 그룹 (SQL Server)의 생성 및 구성](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server?view=sql-server-2017)합니다.
* [배포에 RD 연결 브로커 서버를 추가 하 고 고가용성 구성](rds-connection-broker-cluster.md)합니다.

## <a name="file-server"></a>파일 서버

파일 서버가 서버 메시지 블록 (SMB) 3.0 프로토콜을 사용 하 여 공유 폴더를 제공 합니다. 이러한 공유 폴더 만들기 및 사용자 프로필 디스크 파일 (.vhdx)에 데이터를 백업 하 고 사용자가 테 넌 트의 클라우드 서비스 내에서 데이터를 서로 공유할 수 있도록 저장에 사용 됩니다.

파일 서버를 배포 하는 가상 컴퓨터를 Azure 데이터 디스크 연결 및 공유 폴더를 사용 하 여 구성 있어야 합니다. Azure 데이터 디스크는 write-through 캐싱을, 가상 컴퓨터를 다시 시작할 때마다 디스크에 쓰기 지워지지는 보장을 사용 합니다.

작은 테 넌 트 파일 서버를 결합 하 여 비용을 줄일 수 있습니다 하 고 [RD 라이선싱 역할](rds-roles.md#remote-desktop-licensing) 테 넌 트의 환경에서 단일 가상 머신에서 합니다.

자세한 내용은 다음 문서를 참조하세요.

* [Windows Server에서 저장소](../../storage/storage.md)
* [Azure portal에서 Windows VM에 관리 되는 데이터 디스크를 연결 하는 방법](https://docs.microsoft.com/azure/virtual-machines/windows/attach-managed-disk-portal?toc=%2Fazure%2Fvirtual-machines%2Fwindows%2Fclassic%2Ftoc.json)

### <a name="user-profile-disks"></a>사용자 프로필 디스크

사용자 프로필 디스크를 하나의 컬렉션의 RD 세션 호스트 서버의 세션에 로그인 하는 경우 개인 설정 및 파일을 저장 하는 작업을 할 수 있습니다. 한 후 다른 로그인 할 때 동일한 설정 및 파일에 액세스할 [RD 세션 호스트](rds-roles.md#remote-desktop-session-host) 컬렉션의 서버입니다. 사용자 처음 로그인 하면 테 넌 트의 파일 서버에 현재 연결 된 사용자는 RD 세션 호스트 서버에 탑재 되는 사용자 프로필 디스크를 만듭니다. 각 후속 로그인에서 사용자 프로필 디스크를 적절 한 RD 세션 호스트 서버에 마운트되어 이므로 각를 사용 하 여 탑재 된 로그 아웃 합니다. 만 사용자 프로필 디스크의 콘텐츠를 액세스할 수 있습니다.