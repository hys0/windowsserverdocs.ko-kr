---
ms.assetid: e22d84a5-113d-4bec-b484-036ed29f0c28
title: SSO 및 원활 하 게 초에 대 한 모든 디바이스에서 회사에 가입 인증 회사 응용 프로그램에서 요인
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 12/05/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4926eb32a0bbffb092ec02ca2508fe97d52d1466
ms.sourcegitcommit: 46439194e5deb0fa5f338b428f95dd6b5b799337
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/21/2018
---
# <a name="join-to-workplace-from-any-device-for-sso-and-seamless-second-factor-authentication-across-company-applications"></a>SSO 및 원활 하 게 초에 대 한 모든 디바이스에서 회사에 가입 인증 회사 응용 프로그램에서 요인

>Windows Server 2012 r 2에 적용 됩니다.

소비자 디바이스 및 보편적 정보 액세스 수가 증가 하 여 신속 하 게 사람들이 기술을 요소임는 방식으로 변경 됩니다. 일정 정보를 쉽게 액세스할 수 있도록 함께 하루 종일 정보 기술 사용 업무와 홈 번체 경계 흐림이입니다. 하면 경계 이동 이러한 동반 기술 선택 하 고 사용자의 개성도, 활동 및 일정에 맞게 사용자 지정이 개인-직장으로 확장 됩니다. 엔터프라이즈 네트워크에 연결 되어 개인 소비자 디바이스 데스크톱이 요구 사항에 맞게, 다음과 같은 가치 제안 소개:

-   관리자는 응용 프로그램, 사용자, 디바이스 및 위치를 기반으로 하는 회사 리소스에 액세스할 수 있는 사람을 제어할 수 있습니다.

-   직원이 응용 프로그램 및 데이터를 어디서 나 모든 장치에서 액세스할 수 있습니다. 직원이 Single Sign-on 브라우저 응용 프로그램이 나 엔터프라이즈 응용 프로그램에서 사용할 수 있습니다.

## <a name="key-concepts-introduced-in-the-solution"></a>솔루션의 개념을 키

### <a name="workplace-join"></a>Workplace Join
Workplace Join를 사용 하 여 정보 작업자 회사 리소스 및 서비스에 액세스 하려면 해당 회사의 회사 컴퓨터와 개인 디바이스에 연결할 수 있습니다. 회사 계정에 개인 디바이스를 연결할 때 되는 알려진된 디바이스 및 원활 하 게 초 제공 인증과 Single Sign-on 회사 리소스와 응용 프로그램을 고려 합니다. 디바이스는 Workplace Join로 결합, 경우 디바이스의 특성 디렉터리에서 발급 응용 프로그램에 대 한 보안 토큰를 승인 하기 위해 드라이브 조건부 액세스 검색할 수 있습니다. Windows 8.1 및 iOS 6.0 + Android 및 4.0 + 장치 Workplace Join 사용 하 여 결합 될 수 있습니다.

### <a name="BKMK_DRS"></a>Azure Active Directory 디바이스 등록 서비스
Workplace Join Azure Active Directory 디바이스 등록 서비스에 의해 수 있게 됩니다. 하는 디바이스에 Workplace Join 하 여 참여 서비스에서 Azure Active Directory 개체를 장치를 제공 하 고 디바이스 id를 나타내는 데 사용 되는 로컬 디바이스에는 키를 설정 합니다. 이 디바이스 id 클라우드 및 온-프레미스 호스트 된 응용 프로그램에 대 한 액세스를 제어 규칙과 함께 사용할 수 있습니다.

Azure Active Directory 디바이스 등록 서비스 사용에 대 한 자세한 내용은 참조 [Azure Active Directory 디바이스 등록 서비스 개요](https://msdn.microsoft.com/6a14cb1f-a058-4453-8ede-d9f4a66a7073.aspx)합니다.

### <a name="workplace-join-as-a-seamless-second-factor-authentication"></a>원활 하 게 번째도 Workplace Join 단계 인증
회사 정보 액세스 및 관리 드라이브 준수 소비자 디바이스 기업 리소스에 대 한 액세스 권한을 부여 하는 동안와 관련 된 위험을 관리할 수 있습니다. 디바이스에서 Workplace Join 다음과 같은 기능을 관리자에 게 제공합니다.

-   장치 인증 알려진된 장치를 식별합니다. 관리자는 리소스에 조건부 액세스 및 제어 액세스를 생성 하려면이 정보를 사용할 수 있습니다.

-   사용자가 신뢰할 수 있는 디바이스를 회사 리소스에 액세스를 더욱 원활 하 게 로그인 환경을 제공 합니다.

### <a name="single-sign-on"></a>Single Sign-on
Single Sign-on (SSO)이이 시나리오의 컨텍스트에서 암호를 확인 알려진된 디바이스에서 회사 리소스에 액세스할 수를 입력 하는 최종 사용자의 수를 줄일 수 있는 기능입니다. 이 기능은 사용자가이 디바이스에서 액세스 회사 응용 프로그램 및 리소스에 SSO 수명 동안 한 번 메시지가 표시 되는 의미입니다. 디바이스를 사용 하는 Workplace Join 하는 경우이 디바이스를 사용 하 여 등록 한 사용자가 영구 SSO를 7 일 동안 기본적으로 가져옵니다. 이 사용자가 원활 하 게 로그인 환경이 같은 세션 또는 새 세션에 있습니다.

## <a name="solution-overview"></a>해결 방법 개요
이 솔루션의 일환으로, Workplace Join 지원 되는 디바이스에서 사용 하 고 Single Sign-on 회사 리소스에 발생 하는 방법을 알아보세요.

> [!NOTE]
> Windows 8.1, iOS 6.0 + Android 및 4.0 + 장치를 지원 하기 위해 다시 쓰기 장치 개체 함께 Azure Active Directory 장치 등록 구성, 참조 해야 [온-프레미스 조건부 액세스를 사용 하 여 Azure Active Directory 디바이스 등록 서비스에 대 한 단계별 가이드](https://msdn.microsoft.com/library/azure/dn788908.aspx)

이 해결 방법 안내 걸리는 연습 다음 단계를 안내 합니다.

1.  [연습: Workplace Join 사용 하 여 Windows 장치](../../ad-fs/operations/Walkthrough--Workplace-Join-with-a-Windows-Device.md)

2.  [연습: Workplace Join는 iOS 디바이스와](../../ad-fs/operations/Walkthrough--Workplace-Join-with-an-iOS-Device.md)

3.  [연습: Workplace Join Android 디바이스를](../../ad-fs/operations/walkthrough--workplace-join-to-an-android-device.md)

## <a name="see-also"></a>참조 하십시오
[디바이스 등록 서비스에 federation 서버를 구성 합니다.](../deployment/configure-a-federation-server-with-device-registration-service.md)



