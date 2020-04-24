---
title: 역할 및 기능 마이그레이션
description: 역할 및 기능을 최신 버전의 Windows Server로 마이그레이션하는 방법에 대한 정보입니다.
ms.prod: windows-server
ms.date: 08/28/2019
ms.technology: server-general
ms.topic: article
ms.assetid: 0f78ef4c-dd12-4b1b-8c6e-251dd803c5d1
author: jasongerend
ms.author: jgerend
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 33c1aa654e4c660b4fe2f3305bfaf78b5191220a
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "70119197"
---
# <a name="migrating-roles-and-features-in-windows-server"></a>Windows Server에서 역할 및 기능 마이그레이션

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 페이지에는 역할 및 기능을 최신 버전의 Windows Server로 마이그레이션하는 프로세스를 안내하는 데 도움이 되는 정보 및 도구에 대한 링크가 포함되어 있습니다. [스토리지 마이그레이션 서비스](../storage/storage-migration-service/overview.md)를 사용하여 파일 서버와 스토리지를 마이그레이션할 수 있으며, 역할과 기능을 마이그레이션하기 위해 Windows Server 2008 R2에 도입된 PowerShell cmdlet 세트인 Windows Server 마이그레이션 도구를 사용하여 다른 많은 역할과 기능을 마이그레이션할 수 있습니다.

마이그레이션 가이드는 특정한 역할과 기능을 한 서버에서 다른 서버로 마이그레이션하는 기능을 지원합니다(현재 위치 업그레이드일 경우에는 해당 없음). 가이드에서 달리 설명한 경우 외에는, 마이그레이션은 물리적 컴퓨터와 가상 머신 사이, 그리고 Windows Server 전체 설치 옵션과 Server Core 설치 옵션 실행 서버 사이에서 지원됩니다.

## <a name="before-you-begin"></a>시작하기 전에

역할 및 기능의 마이그레이션을 시작하기 전에 원본 서버와 대상 서버 모두 해당 운영 체제에 제공되는 최신 서비스 팩을 실행 중인지 확인해야 합니다. 

> [!NOTE]
> 어느 버전의 Windows Server로든 마이그레이션 또는 업그레이드할 때마다 반드시 해당 버전의 [지원 주기 정책](https://support.microsoft.com/lifecycle)과 지원 기간을 검토 및 파악하여 그에 따라 계획을 수립해야 합니다. 관심 있는 특정 Windows Server 릴리스에 대한 [수명 주기 정보](https://support.microsoft.com/lifecycle)를 검색할 수 있습니다.

## <a name="windows-server-2019"></a>시작

파일 서버와 스토리지를 Windows Server 2019 또는 Windows Server 2016으로 마이그레이션하려면 [스토리지 마이그레이션 서비스](../storage/storage-migration-service/overview.md)를 사용하는 것이 좋습니다. 다른 역할을 마이그레이션하려면 Windows Server 2016 및 Windows Server 2012 R2에 대한 지침을 참조하세요.

## <a name="windows-server-2016"></a>Windows Server 2016

Windows Server 2016에 대한 마이그레이션 가이드는 다음과 같습니다. 대부분의 경우 Windows Server 2012 R2 마이그레이션 가이드를 사용할 수도 있습니다.

- [원격 데스크톱 서비스](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/migrate-rds-role-services)
- [웹 서버(IIS)](https://www.iis.net/downloads/microsoft/web-deploy)
- [Windows Server Update Services](https://technet.microsoft.com/library/hh852339.aspx)
- [MultiPoint 서비스](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/multipoint-services/multipoint-services-migrate)

파일 서버를 Windows Server 2019 또는 Windows Server 2016으로 마이그레이션하려면 [스토리지 마이그레이션 서비스](../storage/storage-migration-service/overview.md)를 사용하는 것이 좋습니다.

## <a name="windows-server-2012-r2"></a>Windows Server 2012 R2

이 가이드에 제시된 단계적 절차를 따르면 Windows Server 2003, Windows Server 2008, Windows Server 2008 R2, Windows Server 2012 또는 Windows Server 2012 R2를 실행하는 서버로부터 Windows Server 2012 R2로 역할과 기능을 마이그레이션할 수 있습니다. Windows Server 2012 R2의 Windows Server 마이그레이션 도구는 서브넷 간 마이그레이션을 지원합니다.

- [Windows Server 마이그레이션 도구 설치, 사용 및 제거](https://technet.microsoft.com/library/jj134202.aspx)
- [Windows Server 2012 R2용 Active Directory 인증서 서비스 마이그레이션 가이드](https://technet.microsoft.com/library/dn486797.aspx)
- [Windows Server 2012 R2로 Active Directory Federation Services 역할 서비스 마이그레이션](https://technet.microsoft.com/library/dn486815.aspx)
- [Active Directory Rights Management Services 마이그레이션 및 업그레이드 가이드](https://technet.microsoft.com/library/cc754277.aspx)
- [Windows Server 2012 R2로 파일 및 스토리지 서비스 마이그레이션](https://technet.microsoft.com/library/dn479292.aspx)
- [Windows Server 2012에서 Windows Server 2012 R2로 Hyper-V 마이그레이션](https://technet.microsoft.com/library/dn486799.aspx)
- [Windows Server 2012로 네트워크 정책 서버 마이그레이션](https://technet.microsoft.com/library/hh831652)
- [Windows Server 2012 R2로 원격 데스크톱 서비스 마이그레이션](https://technet.microsoft.com/library/dn479239.aspx)
- [Windows Server Update Services를 Windows Server 2012 R2로 마이그레이션](https://technet.microsoft.com/library/hh852339.aspx)
- [Windows Server 2012 R2로 클러스터 역할 마이그레이션](https://technet.microsoft.com/library/dn530779.aspx)
- [Windows Server 2012 R2로 DHCP 서버 마이그레이션](https://technet.microsoft.com/library/dn495425.aspx)

이제 Windows Server 2012 R2 및 Windows Server 2012 마이그레이션 가이드가 eBook으로 제공됩니다. 더 자세한 내용 또는 eBook 다운로드는 [Microsoft 기술 eBook 갤러리](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#MigrateRoles)를 참조하시기 바랍니다.

## <a name="windows-server-2012"></a>Windows Server 2012

이 가이드에 제시된 단계적 절차를 따르면 Windows Server 2003, Windows Server 2008, Windows Server 2008 R2 또는 Windows Server 2012를 실행하는 서버로부터 Windows Server 2012로 역할 및 기능을 마이그레이션할 수 있습니다. Windows Server 2012의 Windows Server 마이그레이션 도구는 서브넷 간 마이그레이션을 지원합니다.

- [Windows Server 마이그레이션 도구 설치, 사용 및 제거](https://technet.microsoft.com/library/jj134202)
- [Windows Server 2012로 Active Directory Federation Services 역할 서비스 마이그레이션](https://technet.microsoft.com/library/jj647765)
- [Windows Server 2012로 상태 등록 기관 마이그레이션](https://technet.microsoft.com/library/hh831513)
- [Windows Server 2008 R2에서 Windows Server 2012로 Hyper-V 마이그레이션](https://technet.microsoft.com/library/jj574113)
- [Windows Server 2012로 IP 구성 마이그레이션](https://technet.microsoft.com/library/jj574133)
- [Windows Server 2012로 네트워크 정책 서버 마이그레이션](https://technet.microsoft.com/library/hh831652)
- [Windows Server 2012로 인쇄 및 문서 서비스 마이그레이션](https://technet.microsoft.com/library/jj134150)
- [Windows Server 2012로 원격 액세스 마이그레이션](https://technet.microsoft.com/library/hh831423)
- [Windows Server Update Services를 Windows Server 2012로 마이그레이션](https://technet.microsoft.com/library/hh852339)
- [Active Directory 도메인 컨트롤러를 Windows Server 2012로 업그레이드](https://technet.microsoft.com/library/hh994618.aspx)
- [Windows Server 2012로 클러스터링된 서비스 및 애플리케이션 마이그레이션](https://technet.microsoft.com/library/dn486790.aspx)
 

마이그레이션 자료가 더 필요하시면 [Windows Server 2012로 역할 및 기능 마이그레이션](https://technet.microsoft.com/library/jj134039)을 방문하시기 바랍니다.

## <a name="windows-server-2008-r2"></a>Windows Server 2008 R2

이 가이드에 제시된 단계적 절차를 따르면 Windows Server 2003, Windows Server 2008 또는 Windows Server 2008 R2를 실행하는 서버로부터 Windows Server 2008 R2로 역할 및 기능을 마이그레이션할 수 있습니다. Windows Server 2008 R2의 Windows Server 마이그레이션 도구는 서브넷 간 마이그레이션을 지원하지 않습니다.

- [Windows Server 마이그레이션 도구 설치, 액세스 및 제거](https://technet.microsoft.com/library/dd379545)
- [Active Directory 인증서 서비스 마이그레이션 가이드](https://technet.microsoft.com/library/ee126170)
- [Active Directory Domain Services 및 DNS(Domain Name System) 서버 마이그레이션 가이드](https://technet.microsoft.com/library/dd379558)
- [BranchCache 마이그레이션 가이드](https://technet.microsoft.com/library/dd548365)
- [DHCP(Dynamic Host Configuration Protocol) 서버 마이그레이션 가이드](https://technet.microsoft.com/library/dd379535)
- [파일 서비스 마이그레이션 가이드](https://technet.microsoft.com/library/dd379487)
- [HRA 마이그레이션 가이드](https://technet.microsoft.com/library/ee791829)
- [Hyper-V 마이그레이션 가이드](https://technet.microsoft.com/library/ee849855)
- [IP 구성 마이그레이션 가이드](https://technet.microsoft.com/library/dd379537)
- [로컬 사용자 및 그룹 마이그레이션 가이드](https://technet.microsoft.com/library/dd379531)
- [NPS 마이그레이션 가이드](https://technet.microsoft.com/library/ee791849)
- [인쇄 서비스 마이그레이션 가이드](https://technet.microsoft.com/library/dd379488)
- [원격 데스크톱 서비스 마이그레이션 가이드](https://technet.microsoft.com/library/ff849223)
- [RRAS 마이그레이션 가이드](https://technet.microsoft.com/library/ee822825)
- [Windows Server 마이그레이션의 일반적인 작업 및 정보](https://technet.microsoft.com/library/ff400258)
- [Windows Server Update Services 3.0 SP2 마이그레이션 가이드](https://technet.microsoft.com/library/ee822826)
 
마이그레이션 자료가 더 필요하시면 [Windows Server 2008 R2로 역할 및 기능 마이그레이션](https://technet.microsoft.com/library/dd365353)을 방문하시기 바랍니다.
