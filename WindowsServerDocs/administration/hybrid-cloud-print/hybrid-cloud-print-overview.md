---
title: Windows Server 하이브리드 클라우드 인쇄 개요
description: 하이브리드 클라우드 인쇄를 통해 IT 전문가는 BYOD 또는 도메인 가입 장치에 대 한 인쇄 요구 사항을 지원할 수 있습니다.
ms.prod: windows-server
ms.technology: server-general
author: trudyha
ms.author: trudyha
ms.date: 10/16/2017
ms.openlocfilehash: f448e8709f9e73165ba1a477c59567fcff4a2008
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852006"
---
# <a name="windows-server-hybrid-cloud-print-overview"></a>Windows Server 하이브리드 클라우드 인쇄 개요

**적용 대상**
-   Windows Server 2016

## <a name="what-is-hybrid-cloud-print"></a>하이브리드 클라우드 인쇄 란?
**하이브리드 클라우드 인쇄** 는 **주문형 기능**을 통해 제공 되는 Windows Server 2016에 대 한 새로운 기능입니다. It 전문가는 자신의 장치를 가져오거나 Azure Active Directory에 가입 된 장치를 사용 하는 사용자에 게 인쇄 요구 사항을 지원할 수 있습니다. 여기에는 windows 10 또는 Windows Mobile을 실행 하는 Windows phone, 노트북, 태블릿 등의 모바일 장치가 포함 됩니다. 사용자가 인터넷에 액세스할 수 있는 모든 곳에서 인쇄 지원을 제공 합니다.

IT 관리자의 경우 **하이브리드 클라우드 인쇄** 는 사용자 액세스의 유효성을 검사 하기 위해 Azure의 multi-factor authentication을 사용 하 여 온-프레미스 프린터에 대 한 보안 사용자 액세스를 제공 합니다. SSO (Single sign-on) 기능은 사용자 환경을 단순화 합니다. **하이브리드 클라우드 인쇄** 는 Windows **인쇄 서버** 역할을 기반으로 하며, IT 전문가에 게 프린터 및 사용자 액세스 보안을 관리 하는 것과 비슷한 환경을 제공 합니다.

**하이브리드 클라우드 인쇄** 를 사용 하면 조직의 사용자가 책상 이나 작업 공간에서 떨어져 있는 경우에도 작업을 완료 하는 데 사용 하는 장치에서 인쇄할 수 있습니다.

**하이브리드 클라우드 인쇄** 는 Windows 10 크리에이터 업데이트 및 Windows 10 S에서 지원 됩니다.
 
## <a name="feature-summary"></a>기능 요약
**하이브리드 클라우드 인쇄** 는 두 가지 주요 서버 쪽 구성 요소인 **검색** 서비스 및 **Windows 인쇄** 서비스로 구성 됩니다.
- Moto를 지 원하는 IIS 서비스에서 실행 되는 **검색** 서비스 끝점은 클라우드의 프린터 검색용 동맹 업계 표준입니다.
- 업계 표준 IPP (인터넷 인쇄 프로토콜)를 지 원하는 IIS 서비스에서 실행 되는 **Windows 인쇄** 서비스 끝점으로, 가장 광범위 한 클라이언트 OS 지원을 보장 합니다.

## <a name="deployment"></a>배포
**하이브리드 클라우드 인쇄** 는 조직에서 사용자 인증을 요구 하는 위치에 따라 몇 가지 배포 옵션을 지원 합니다. 배포의 모양은 다음과 같습니다.

![하이브리드 클라우드 인쇄 솔루션의 그래픽 표시를 보여 주는 다이어그램](../media/hybrid-cloud-print/wshcp-deployment-options.png)

*하이브리드 클라우드 인쇄 솔루션 다이어그램*

다이어그램은 다음을 보여 줍니다.
- **하이브리드 클라우드** 는 Azure Active Directory를 사용자 id 공급자로 사용 하 여 인쇄 합니다. 
- **Windows 인쇄** 서비스 및 **검색** 서비스 끝점은 Azure Active Directory에 등록 되어 클라이언트 장치에서 이러한 서비스에 대해 사용할 필수 사용자 인증 토큰을 검색할 수 있도록 합니다. 
- **Microsoft Intune**와 같은 MDM 서비스는 **Windows 인쇄** 서비스 및 **검색** 서비스에 Azure Active Directory 연결 하는 데 필요한 정책을 사용 하 여 클라이언트 장치를 프로 비전 합니다.

이 표에는 다이어그램의 요소에 대 한 자세한 정보가 있습니다.  

| 요소 | 설명 |
| ------- | ----------- |
| Azure Active Directory  | 사용자 id 및 권한 부여 기능을 제공 하 고 제어 합니다. |
| Active Directory        | 사용자 id 및 권한 부여 기능을 제공 하 고 제어 합니다. |
| Azure AD 연결  | Azure AD와 온-프레미스 AD 간에 사용자 자격 증명을 동기화 합니다. |
| MDM 서비스 (Intune) | 클라이언트 장치 (BYOD 장치)가 회사 정책을 준수 하는지 확인 하는 장치 정책 프로 비전 기능을 제공 합니다. |
| Azure AD 프록시 | 방화벽 뒤에서 Azure로 설정 된 수명이 긴 연결을 제공 하 여 특정 구성 응용 프로그램 트래픽이 인터넷에서 회사 네트워크로 전달 될 수 있도록 합니다. |
| Azure 웹앱 | 하이브리드 클라우드 인쇄 솔루션의 핵심입니다. 프린터를 검색 하 고 도메인에 가입 되지 않은 장치에 대 한 인쇄 콘텐츠를 전송 하는 데 필요한 웹 끝점을 제공 합니다. |
| BYOD 장치/Windows 인쇄 서버 스풀러/프린터 | 이는 그대로 있습니다. 배포의 기능은 변경 되지 않습니다. |

**하이브리드 클라우드 인쇄**를 설치 하는 방법에는 다음 두 가지가 있습니다.
- \* * 주문형 기능- [Windows Server에서 주문형 기능 구성](https://docs.microsoft.com/windows-server/administration/server-manager/configure-features-on-demand-in-windows-server) 을 참조 하 여 역할 및 기능 파일을 추가 하 고 제거 하는 방법에 대해 자세히 알아보세요. 
- \* * Windows Server 2016 설정-관리자는 **설정** -> **앱** -> **선택적 -> 기능을 관리** 하 고 **기능을 추가** 하 고 주문형 기능 패키지를 검색할 수 있습니다. 
- PowerShell 명령-PowerShell 관리자 창에서 다음 명령을 실행 합니다.

```PowerShell
    Install-Module -Name PublishCloudPrinter
    Import-Module PublishCloudPrinter
    ```
