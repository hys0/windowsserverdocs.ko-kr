---
title: Windows Server 하이브리드 클라우드 인쇄 개요
description: BYOD 또는 도메인에 대 한 인쇄 요구를 지원 하기 위해 IT 전문가 사용 하면 하이브리드 클라우드 인쇄 장치를 조인 합니다.
ms.prod: w10
ms.mktglfcycl: manage
ms.sitesec: library
ms.pagetype: store
ms.technology: server-general
author: TrudyHa
ms.author: TrudyHa
ms.date: 10/16/2017
ms.openlocfilehash: faa9fde857a9a4ee3f7c03f682b3dbced0340417
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878834"
---
# <a name="windows-server-hybrid-cloud-print-overview"></a>Windows Server 하이브리드 클라우드 인쇄 개요

**적용 대상**
-   Windows Server 2016

## <a name="what-is-hybrid-cloud-print"></a>하이브리드 클라우드 인쇄 란?
**하이브리드 클라우드 인쇄** Windows Server 2016의 새로운 기능을 통해 제공 됩니다 **주문형 기능**합니다. IT 전문가가 자신의 장치 또는 Azure Active Directory에 가입 된 장치를 사용 하 여 사용자를 위해 인쇄 요구 사항을 지원할 수 있습니다. Windows phone, 랩톱 또는 Windows 10 또는 Windows Mobile을 실행 하는 태블릿과 같은 모바일 장치 포함 됩니다. 인쇄 지원을 제공 어디에서 나 사용자가 인터넷에 액세스 합니다.

IT 관리자에 대 한 **하이브리드 클라우드 인쇄** 사용자 액세스의 유효성을 검사 하려면 Azure multi-factor authentication을 사용 하 여 온-프레미스 프린터에 대 한 보안 사용자 액세스를 제공 합니다. 단일 로그온 (SSO) 기능에는 사용자 환경을 간소화합니다. **하이브리드 클라우드 인쇄** Windows에 빌드되어 **인쇄 서버** 역할, IT 전문가 프린터 및 사용자 액세스 보안 관리와 비슷한 환경을 제공 합니다.

**하이브리드 클라우드 인쇄** 책상에 있든 workplace와 멀리 떨어져 있을 경우에 작업-완료를 사용 하 여 장치에서 인쇄 하기 위해 조직에서 사용자를 허용 합니다.

**하이브리드 클라우드 인쇄** S. Windows 10 및 Windows 10 크리에이터 스 업데이트에서 지원 됩니다
 
## <a name="feature-summary"></a>기능 요약
**하이브리드 클라우드 인쇄** 두 주 서버 쪽 구성 요소로 구성 됩니다. **검색** 서비스와 **Windows 인쇄** 서비스입니다.
- **검색** 클라우드에서 프린터 검색 Mopria Alliance 업계 표준을 지 원하는 IIS 서비스를 실행 하는 서비스 끝점입니다.
- **Windows 인쇄** 업계를 지 원하는 IIS 서비스를 실행 하는 서비스 끝점 표준 인쇄 IPP (인터넷 프로토콜) 가장 광범위 한 클라이언트 OS 되도록 지원 합니다.

## <a name="deployment"></a>배포
**하이브리드 클라우드 인쇄** 는 두 가지 조직에서 사용자 인증을 해야 하는 위치에 따라 다양 한 배포 옵션을 지원 합니다. 배포를 다음과 같을 수 있습니다 다음과 같습니다.

![하이브리드 클라우드 인쇄 솔루션에 대 한 그래픽 설명을 보여 주는 다이어그램](../media/hybrid-cloud-print/wshcp-deployment-options.png)

*하이브리드 클라우드 인쇄 솔루션 다이어그램*

다이어그램을 보여 줍니다.
- **하이브리드 클라우드 인쇄** 사용자 id 공급자로 Azure Active Directory를 사용 합니다. 
- **Windows 인쇄** 서비스와 **검색** 클라이언트 장치에 이러한 서비스에 대해 사용 하 여 필요한 사용자 인증 토큰을 검색할 수 있도록 Azure Active Directory를 사용 하 여 서비스 끝점 등록 됩니다. 
- MDM 서비스와 같은 **Microsoft Intune**, Azure Active Directory를 연결 하는 데 필요한 정책을 사용 하 여 클라이언트 장치를 프로 비전 **Windows 인쇄** 서비스 및 **검색**서비스입니다.

이 테이블에는 다이어그램의 요소에 자세한 정보.  

| 요소 | 설명 |
| ------- | ----------- |
| Azure Active Directory  | 제공 하 고 사용자 id 및 권한 부여 기능을 제어 합니다. |
| Active Directory        | 제공 하 고 사용자 id 및 권한 부여 기능을 제어 합니다. |
| Azure AD 연결  | Azure AD 간에 사용자 자격 증명을 동기화 하 고 온-프레미스 AD입니다. |
| MDM 서비스 (Intune) | 클라이언트 장치 (BYOD 장치)를 확인 하려면 장치 정책을 프로 비전 기능을 회사 정책 준수를 제공 합니다. |
| Azure AD Proxy | 회사 네트워크에 인터넷에서 특정 구성 된 응용 프로그램 트래픽 흐름을 허용 하기 위해 Azure 방화벽 뒤에서 설정 되는 수명이 긴 연결을 제공 합니다. |
| Azure 웹 앱 | 하이브리드 클라우드 인쇄 솔루션의 핵심입니다. 프린터를 검색 하 고 비-도메인 가입된 장치에 대 한 인쇄 콘텐츠를 보낼 필요한 웹 끝점을 제공 합니다. |
| BYOD 장치 Windows 인쇄 서버 스풀러 / / 프린터 | 이러한-됩니다. 배포의 기능은 변경 되지 않았습니다. |

설치 하는 방법은 두 가지가 **하이브리드 클라우드 인쇄**:
- **주문형 기능** -참조 [Windows Server에서 주문형 기능 구성](https://docs.microsoft.com/windows-server/administration/server-manager/configure-features-on-demand-in-windows-server) 역할 및 기능 파일 추가 및 제거 하는 방법에 대 한 자세한 내용을 보려면. 
- **Windows Server 2016 설정** -관리자 이동할 수 있습니다 **설정** -> **앱** -> **선택적 기능 관리**  ->  **기능을 추가할** 및 요청 시 패키지에 기능에 대 한 검색 
- PowerShell 명령-PowerShell에서 관리자 창 다음이 명령을 실행:

```PowerShell
    Install-Module -Name PublishCloudPrinter
    Import-Module PublishCloudPrinter
    ```
