---
ms.assetid: e22d84a5-113d-4bec-b484-036ed29f0c28
title: 회사 응용 프로그램 전반에 SSO 및 연속된 두 번째 단계 인증을 위한 모든 장치의 작업 공간 연결
author: billmath
ms.author: billmath
manager: femila
ms.date: 12/05/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 82c94adadb9241e2b7cd8d75ea1693957aaffc61
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816266"
---
# <a name="join-to-workplace-from-any-device-for-sso-and-seamless-second-factor-authentication-across-company-applications"></a>회사 응용 프로그램 전반에 SSO 및 연속된 두 번째 단계 인증을 위한 모든 장치의 작업 공간 연결



소비자 디바이스와 유비쿼터스 정보 액세스의 급증으로 사용자가 기술을 인식하는 방식이 바뀌고 있습니다. 정보 기술의 지속적인 사용은 정보의 간편한 액세스와 함께 업무와 개인 생활 간의 기존 경계를 무너뜨리고 있습니다. 이러한 변화 하는 경계는 사용자의 개성, 활동 및 일정에 맞게 개인 기술이 선택 하 고 사용자 지정 하는 하다 신념으로와 함께 작업 공간으로 확장 되어야 합니다. 엔터프라이즈 네트워크에 연결해야 하는 개인 소비자 디바이스의 증가하는 요구 사항을 수용하기 위해 다음과 같은 가치 제안을 도입했습니다.

-   관리자는 응용 프로그램, 사용자, 디바이스 및 위치를 기반으로 하는 회사 리소스에 액세스할 수 있는 사람을 제어할 수 있습니다.

-   직원은 위치에 관계없이 모든 디바이스에서 응용 프로그램 및 데이터에 액세스할 수 있습니다. 직원은 브라우저 애플리케이션 또는 엔터프라이즈 애플리케이션에서 Single Sign-On을 사용할 수 있습니다.

## <a name="key-concepts-introduced-in-the-solution"></a>솔루션에 도입된 주요 개념

### <a name="workplace-join"></a>작업 공간 연결
작업 공간 연결을 사용하면 정보 작업자가 개인 디바이스를 회사의 작업 공간 컴퓨터에 연결하여 회사 리소스 및 서비스에 액세스할 수 있습니다. 개인 디바이스를 작업 공간에 연결한 경우 해당 디바이스는 알려진 디바이스가 되며, 작업 공간 리소스 및 응용 프로그램에 연속된 두 번째 단계 인증과 Single Sign-On을 제공합니다. 작업 공간 연결을 통해 디바이스를 연결하면 디렉터리에서 디바이스의 특성을 검색하여 응용 프로그램의 보안 토큰 발급 권한을 부여하기 위한 조건부 액세스를 유도할 수 있습니다. 작업 공간 연결을 사용하여 Windows 8.1 및 iOS 6.0+, Android 4.0+ 디바이스를 연결할 수 있습니다.

### <a name="azure-active-directory-device-registration-service"></a><a name="BKMK_DRS"></a>Azure Active Directory Device Registration 서비스
작업 공간 연결은 Azure Active Directory 장치 등록 서비스에서 가능합니다. 작업 공간 연결을 통해 디바이스가 연결되면 서비스에서 Azure Active Directory에 디바이스 개체를 프로비전하고 디바이스 ID를 나타내는 데 사용되는 키를 로컬 디바이스에 설정합니다. 그러면 클라우드 및 온-프레미스에서 호스트되는 응용 프로그램에 대한 액세스 제어 규칙에서 이 디바이스 ID를 사용할 수 있습니다.

자세한 내용은 [Azure Active Directory의 장치 관리 소개](https://docs.microsoft.com/azure/active-directory/device-management-introduction)를 참조 하세요.

### <a name="workplace-join-as-a-seamless-second-factor-authentication"></a>연속된 두 번째 단계 인증으로서의 작업 공간 연결
회사에서는 소비자 디바이스에 회사 리소스에 대한 액세스 권한을 부여하는 동시에 정보 액세스와 관련된 위험을 관리하고 관리 방식 및 규정 준수를 유도할 수 있습니다. 디바이스의 작업 공간 연결을 통해 관리자는 다음을 할 수 있습니다.

-   디바이스 인증을 사용하여 알려진 디바이스 식별. 관리자는 이 정보를 사용하여 조건부 액세스를 유도하고 리소스 액세스를 제어할 수 있습니다.

-   사용자가 신뢰할 수 있는 디바이스에서 회사 리소스에 액세스할 수 있는 보다 원활한 로그인 환경 제공

### <a name="single-sign-on"></a>Single Sign-On
이 시나리오의 컨텍스트에서 SSO(Single Sign-On)는 최종 사용자가 알려진 디바이스에서 회사 리소스에 액세스하기 위해 입력해야 하는 암호 프롬프트 수를 줄이는 기능입니다. 이 기능은 사용자가 SSO 수명 동안 단 한 번 표시되는 프롬프트를 통해 이 디바이스에서 회사 응용 프로그램 및 리소스에 액세스할 수 있음을 의미합니다. 디바이스에서 작업 공간 연결을 사용하는 경우 이 디바이스를 사용하도록 등록된 사용자에게는 기본적으로 7일간의 영구 SSO가 제공됩니다. 따라서 같은 세션 또는 새 세션에서 원활한 로그인 환경을 경험할 수 있습니다.

## <a name="solution-overview"></a>솔루션 개요
이 솔루션의 일부로, 지원되는 디바이스에서 작업 공간 연결을 사용하고 Single Sign-On을 통해 회사 리소스에 액세스하는 방법을 배웁니다.

> [!NOTE]
> Windows 8.1, iOS 6.0+ 및 Android 4.0+ 장치를 지원하려면 장치 개체 나중 쓰기와 함께 Azure Active Directory 장치 등록을 구성해야 합니다. [Azure Active Directory 장치 등록 서비스를 사용하여 온-프레미스 조건부 액세스를 위한 단계별 가이드](https://msdn.microsoft.com/library/azure/dn788908.aspx)를 참조하세요.

이 솔루션에서는 다음 연습 단계를 안내합니다.

1.  [연습: Windows 장치를 사용 하 여 Workplace Join](../../ad-fs/operations/Walkthrough--Workplace-Join-with-a-Windows-Device.md)

2.  [연습: iOS 장치를 사용 하 여 Workplace Join](../../ad-fs/operations/Walkthrough--Workplace-Join-with-an-iOS-Device.md)

3.  [연습: Android 장치를 사용 하 여 Workplace Join](../../ad-fs/operations/walkthrough--workplace-join-to-an-android-device.md)

## <a name="see-also"></a>관련 항목
[장치 등록 서비스를 사용 하 여 페더레이션 서버 구성](../deployment/configure-a-federation-server-with-device-registration-service.md)



