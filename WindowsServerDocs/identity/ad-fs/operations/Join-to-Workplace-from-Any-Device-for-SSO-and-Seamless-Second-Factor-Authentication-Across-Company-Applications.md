---
ms.assetid: e22d84a5-113d-4bec-b484-036ed29f0c28
title: 회사 응용 프로그램 전반에 SSO 및 연속된 두 번째 단계 인증을 위한 모든 장치의 작업 공간 연결
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 12/05/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e9d6161666be89673cff6ef1a975d3205fa4b5c9
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189090"
---
# <a name="join-to-workplace-from-any-device-for-sso-and-seamless-second-factor-authentication-across-company-applications"></a>회사 응용 프로그램 전반에 SSO 및 연속된 두 번째 단계 인증을 위한 모든 장치의 작업 공간 연결



소비자 장치와 유비쿼터스 정보 액세스의 급증으로 사용자가 기술을 인식하는 방식이 바뀌고 있습니다. 정보 기술의 지속적인 사용은 정보의 간편한 액세스와 함께 업무와 개인 생활 간의 기존 경계를 무너뜨리고 있습니다. 믿음이 수반 됩니다 변화 하는 경계 이러한 기술을 선택 하 고 사용자의 개성, 활동 및 일정에 맞게 사용자 지정 하는 개인-작업 공간으로 확장 되어야 합니다. 엔터프라이즈 네트워크에 연결해야 하는 개인 소비자 장치의 증가하는 요구 사항을 수용하기 위해 다음과 같은 가치 제안을 도입했습니다.

-   관리자는 응용 프로그램, 사용자, 장치 및 위치를 기반으로 하는 회사 리소스에 액세스할 수 있는 사람을 제어할 수 있습니다.

-   직원은 위치에 관계없이 모든 장치에서 응용 프로그램 및 데이터에 액세스할 수 있습니다. 직원은 브라우저 응용 프로그램 또는 엔터프라이즈 응용 프로그램에서 Single Sign-On을 사용할 수 있습니다.

## <a name="key-concepts-introduced-in-the-solution"></a>솔루션에 도입된 주요 개념

### <a name="workplace-join"></a>작업 공간 연결
작업 공간 연결을 사용하면 정보 작업자가 개인 장치를 회사의 작업 공간 컴퓨터에 연결하여 회사 리소스 및 서비스에 액세스할 수 있습니다. 개인 장치를 작업 공간에 연결한 경우 해당 장치는 알려진 장치가 되며, 작업 공간 리소스 및 응용 프로그램에 연속된 두 번째 단계 인증과 Single Sign-On을 제공합니다. 작업 공간 연결을 통해 장치를 연결하면 디렉터리에서 장치의 특성을 검색하여 응용 프로그램의 보안 토큰 발급 권한을 부여하기 위한 조건부 액세스를 유도할 수 있습니다. 작업 공간 연결을 사용하여 Windows 8.1 및 iOS 6.0+, Android 4.0+ 장치를 연결할 수 있습니다.

### <a name="BKMK_DRS"></a>Azure Active Directory Device Registration 서비스
작업 공간 연결은 Azure Active Directory 장치 등록 서비스에서 가능합니다. 작업 공간 연결을 통해 장치가 연결되면 서비스에서 Azure Active Directory에 장치 개체를 프로비전하고 장치 ID를 나타내는 데 사용되는 키를 로컬 장치에 설정합니다. 그러면 클라우드 및 온-프레미스에서 호스트되는 응용 프로그램에 대한 액세스 제어 규칙에서 이 장치 ID를 사용할 수 있습니다.

자세한 내용은 참조 하세요. [Azure Active Directory의 장치 관리 소개](https://docs.microsoft.com/azure/active-directory/device-management-introduction)합니다.

### <a name="workplace-join-as-a-seamless-second-factor-authentication"></a>연속된 두 번째 단계 인증으로서의 작업 공간 연결
회사에서는 소비자 장치에 회사 리소스에 대한 액세스 권한을 부여하는 동시에 정보 액세스와 관련된 위험을 관리하고 관리 방식 및 규정 준수를 유도할 수 있습니다. 장치의 작업 공간 연결을 통해 관리자는 다음을 할 수 있습니다.

-   장치 인증을 사용하여 알려진 장치 식별. 관리자는 이 정보를 사용하여 조건부 액세스를 유도하고 리소스 액세스를 제어할 수 있습니다.

-   사용자가 신뢰할 수 있는 장치에서 회사 리소스에 액세스할 수 있는 보다 원활한 로그인 환경 제공

### <a name="single-sign-on"></a>Single Sign-On
이 시나리오의 컨텍스트에서 SSO(Single Sign-On)는 최종 사용자가 알려진 장치에서 회사 리소스에 액세스하기 위해 입력해야 하는 암호 프롬프트 수를 줄이는 기능입니다. 이 기능은 사용자가 SSO 수명 동안 단 한 번 표시되는 프롬프트를 통해 이 장치에서 회사 응용 프로그램 및 리소스에 액세스할 수 있음을 의미합니다. 장치에서 작업 공간 연결을 사용하는 경우 이 장치를 사용하도록 등록된 사용자에게는 기본적으로 7일간의 영구 SSO가 제공됩니다. 따라서 같은 세션 또는 새 세션에서 원활한 로그인 환경을 경험할 수 있습니다.

## <a name="solution-overview"></a>솔루션 개요
이 솔루션의 일부로, 지원되는 장치에서 작업 공간 연결을 사용하고 Single Sign-On을 통해 회사 리소스에 액세스하는 방법을 배웁니다.

> [!NOTE]
> Windows 8.1, iOS 6.0+ 및 Android 4.0+ 장치를 지원하려면 장치 개체 나중 쓰기와 함께 Azure Active Directory 장치 등록을 구성해야 합니다. [Azure Active Directory 장치 등록 서비스를 사용하여 온-프레미스 조건부 액세스를 위한 단계별 가이드](https://msdn.microsoft.com/library/azure/dn788908.aspx)를 참조하세요.

이 솔루션에서는 다음 연습 단계를 안내합니다.

1.  [연습: Windows 디바이스를 사용하여 작업 공간 연결](../../ad-fs/operations/Walkthrough--Workplace-Join-with-a-Windows-Device.md)

2.  [연습: iOS 디바이스를 사용하여 작업 공간 연결](../../ad-fs/operations/Walkthrough--Workplace-Join-with-an-iOS-Device.md)

3.  [연습: Android 디바이스를 사용하여 작업 공간 연결](../../ad-fs/operations/walkthrough--workplace-join-to-an-android-device.md)

## <a name="see-also"></a>관련 항목
[Device Registration Service를 사용 하 여 페더레이션 서버 구성](../deployment/configure-a-federation-server-with-device-registration-service.md)



