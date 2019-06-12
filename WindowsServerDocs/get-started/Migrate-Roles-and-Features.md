---
title: 역할 및 기능 마이그레이션
description: ''
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.date: 04/03/2017
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0f78ef4c-dd12-4b1b-8c6e-251dd803c5d1
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 486c11ebd46c6fd23b3bd16cd90463f8d607287e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443542"
---
# <a name="migrating-roles-and-features-in-windows-server"></a>Windows Server에서 역할 및 기능 마이그레이션

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 페이지에는 역할 및 기능을 Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012로 마이그레이션하는 과정에 도움이 되는 정보와 도구에 대한 링크가 들어 있습니다. 역할 및 기능 요소와 데이터를 쉽게 마이그레이션할 수 있도록 Windows Server 2008 R2에서 처음 도입된 다섯 가지 Windows PowerShell cmdlets 모음인 Windows Server Migration Tools를 이용해서 많은 역할과 기능을 마이그레이션할 수 있습니다.

마이그레이션 가이드는 특정한 역할과 기능을 한 서버에서 다른 서버로 마이그레이션하는 기능을 지원합니다(현재 위치 업그레이드일 경우에는 해당 없음). 가이드에서 달리 설명한 경우 외에는, 마이그레이션은 물리적 컴퓨터와 가상 컴퓨터 사이, 그리고 Windows Server 전체 설치 옵션과 Server Core 설치 옵션 실행 서버 사이에서 지원됩니다.  

## <a name="before-you-begin"></a>시작하기 전 주의 사항

역할 및 기능의 마이그레이션을 시작하기 전에 원본 서버와 대상 서버 모두 해당 운영 체제에 제공되는 최신 서비스 팩을 실행 중인지 확인해야 합니다.
Windows Server 2012 R2 및 Windows Server 2012 마이그레이션 가이드는 전자책이 나와 있습니다. 더 자세한 내용 또는 전자책 다운로드는 [E-Book Gallery for Microsoft Technologies(Microsoft 기술 전자책 갤러리)](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#MigrateRoles)를 참조하시기 바랍니다. 

>[!NOTE]
>어느 버전의 Windows Server로든 마이그레이션 또는 업그레이드할 때마다 반드시 해당 버전의 [지원 주기 정책](https://support.microsoft.com/lifecycle)과 지원 기간을 검토 및 파악하여 그에 따라 계획을 수립해야 합니다. 관심 있는 특정 Windows Server 릴리스에 대한 [수명 주기 정보](https://support.microsoft.com/lifecycle)를 검색할 수 있습니다.
 
## <a name="windows-server-2016"></a>Windows Server 2016

### <a name="migration-guides"></a>마이그레이션 가이드
Windows Server 2016에 맞춰 업데이트된 마이그레이션 가이드를 현재 제작 중입니다. 업데이트가 나오는 대로 이곳에서 다시 확인해보시기 바랍니다. 대부분의 경우 Windows Server 2012 R2 마이그레이션 가이드에 제시된 단계가 Windows Server 2016에도 적용됩니다.

- [원격 데스크톱 서비스](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/migrate-rds-role-services)
- [웹 서버 (IIS)](https://www.iis.net/downloads/microsoft/web-deploy)
- [Windows Server Update Services](https://technet.microsoft.com/library/hh852339.aspx)
- [MultiPoint 서비스](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/multipoint-services/multipoint-services-migrate)
 
## <a name="windows-server-2012-r2"></a>Windows Server 2012 R2

### <a name="migration-guides"></a>마이그레이션 가이드
이 가이드에 제시된 단계적 절차를 따르면 Windows Server 2003, Windows Server 2008, Windows Server 2008 R2, Windows Server 2012 또는 Windows Server 2012 R2를 실행하는 서버로부터 Windows Server 2012 R2로 역할과 기능을 마이그레이션할 수 있습니다. Windows Server 2012 R2의 Windows Server 마이그레이션 도구는 서브넷 간 마이그레이션을 지원합니다.

- [설치, 사용 및 Windows Server 마이그레이션 도구를 제거 합니다.](https://technet.microsoft.com/library/jj134202.aspx)
- [Windows Server 2012 R2 용 active Directory 인증서 서비스 마이그레이션 가이드](https://technet.microsoft.com/library/dn486797.aspx)
- [Windows Server 2012 R2로 Active Directory Federation Services 역할 서비스 마이그레이션](https://technet.microsoft.com/library/dn486815.aspx)
- [Active Directory Rights Management Services 마이그레이션 및 업그레이드 가이드](https://technet.microsoft.com/library/cc754277.aspx)
- [Windows Server 2012 R2로 File and Storage Services 마이그레이션](https://technet.microsoft.com/library/dn479292.aspx)
- [Windows Server 2012에서 Windows Server 2012 R2로 Hyper-V 마이그레이션](https://technet.microsoft.com/library/dn486799.aspx)
- [Windows Server 2012로 네트워크 정책 서버 마이그레이션](https://technet.microsoft.com/library/hh831652)
- [Windows Server 2012 R2로 원격 데스크톱 서비스 마이그레이션](https://technet.microsoft.com/library/dn479239.aspx)
- [Windows Server 2012 R2로 Windows Server Update Services로 마이그레이션](https://technet.microsoft.com/library/hh852339.aspx)
- [Windows Server 2012 R2로 클러스터 역할 마이그레이션](https://technet.microsoft.com/library/dn530779.aspx)
- [Windows Server 2012 R2로 DHCP 서버 마이그레이션](https://technet.microsoft.com/library/dn495425.aspx)
 
## <a name="windows-server-2012"></a>Windows Server 2012

### <a name="migration-guides"></a>마이그레이션 가이드
이 가이드에 제시된 단계적 절차를 따르면 Windows Server 2003, Windows Server 2008, Windows Server 2008 R2 또는 Windows Server 2012를 실행하는 서버로부터 Windows Server 2012로 역할 및 기능을 마이그레이션할 수 있습니다. Windows Server 2012의 Windows Server 마이그레이션 도구는 서브넷 간 마이그레이션을 지원합니다.

- [설치, 사용 및 Windows Server 마이그레이션 도구를 제거 합니다.](https://technet.microsoft.com/library/jj134202)
- [Windows Server 2012로 Active Directory Federation Services 역할 서비스 마이그레이션](https://technet.microsoft.com/library/jj647765)
- [Windows Server 2012로 상태 등록 기관 마이그레이션](https://technet.microsoft.com/library/hh831513)
- [Windows Server 2008 R2에서 Windows Server 2012로 Hyper-v 마이그레이션](https://technet.microsoft.com/library/jj574113)
- [Windows Server 2012로 IP 구성 마이그레이션](https://technet.microsoft.com/library/jj574133)
- [Windows Server 2012로 네트워크 정책 서버 마이그레이션](https://technet.microsoft.com/library/hh831652)
- [인쇄 마이그레이션 및 문서 서비스를 Windows Server 2012](https://technet.microsoft.com/library/jj134150)
- [Windows Server 2012로 원격 액세스 마이그레이션](https://technet.microsoft.com/library/hh831423)
- [Windows Server 2012로 Windows Server Update Services로 마이그레이션](https://technet.microsoft.com/library/hh852339)
- [Active Directory 도메인 컨트롤러를 Windows Server 2012로 업그레이드](https://technet.microsoft.com/library/hh994618.aspx)
- [클러스터 된 서비스 및 응용 프로그램 Windows Server 2012로 마이그레이션](https://technet.microsoft.com/library/dn486790.aspx)
 

마이그레이션 자료가 더 필요하시면 [Windows Server 2012로 역할 및 기능 마이그레이션](https://technet.microsoft.com/library/jj134039)을 방문하시기 바랍니다.

## <a name="windows-server-2008-r2"></a>Windows Server 2008 R2

### <a name="migration-guides"></a>마이그레이션 가이드
이 가이드에 제시된 단계적 절차를 따르면 Windows Server 2003, Windows Server 2008 또는 Windows Server 2008 R2를 실행하는 서버로부터 Windows Server 2008 R2로 역할 및 기능을 마이그레이션할 수 있습니다. Windows Server 2008 R2의 Windows Server 마이그레이션 도구는 서브넷 간 마이그레이션을 지원하지 않습니다.

- [Windows Server 마이그레이션 도구 설치, 액세스 및 제거](https://technet.microsoft.com/library/dd379545)
- [Active Directory 인증서 서비스 마이그레이션 가이드](https://technet.microsoft.com/library/ee126170)
- [Active Directory Domain Services 및 도메인 이름 시스템 (DNS) 서버 마이그레이션 가이드](https://technet.microsoft.com/library/dd379558)
- [BranchCache 마이그레이션 가이드](https://technet.microsoft.com/library/dd548365)
- [동적 호스트 구성 프로토콜 (DHCP) 서버 마이그레이션 가이드](https://technet.microsoft.com/library/dd379535)
- [파일 서비스 마이그레이션 가이드](https://technet.microsoft.com/library/dd379487)
- [HRA 마이그레이션 가이드](https://technet.microsoft.com/library/ee791829)
- [Hyper-v 마이그레이션 가이드](https://technet.microsoft.com/library/ee849855)
- [IP 구성 마이그레이션 가이드](https://technet.microsoft.com/library/dd379537)
- [로컬 사용자 및 그룹 마이그레이션 가이드](https://technet.microsoft.com/library/dd379531)
- [NPS 마이그레이션 가이드](https://technet.microsoft.com/library/ee791849)
- [인쇄 서비스 마이그레이션 가이드](https://technet.microsoft.com/library/dd379488)
- [원격 데스크톱 서비스 마이그레이션 가이드](https://technet.microsoft.com/library/ff849223)
- [RRAS 마이그레이션 가이드](https://technet.microsoft.com/library/ee822825)
- [Windows Server 마이그레이션에 대 한 일반적인 정보 및 정보](https://technet.microsoft.com/library/ff400258)
- [Windows Server Update Services 3.0 SP2 마이그레이션 가이드](https://technet.microsoft.com/library/ee822826)
 
마이그레이션 자료가 더 필요하시면 [Windows Server 2008 R2로 역할 및 기능 마이그레이션](https://technet.microsoft.com/library/dd365353)을 방문하시기 바랍니다.
