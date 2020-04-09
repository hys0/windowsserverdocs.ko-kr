---
ms.assetid: a33bd54c-e6db-4b58-8264-c0f34bd8ba39
title: 연습-Android 장치로 Workplace Join
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a52c5b6e808094e1ef31c800e8a724dd0a37f3d3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816086"
---
# <a name="walkthrough-workplace-join-to-an-android-device"></a>연습: Android 장치에 Workplace Join



## <a name="join-your-device-with-workplace-join"></a>작업 공간 연결을 사용하여 디바이스를 연결합니다.

> [!NOTE]
> Android 작업 공간 연결에는 Azure Active Directory Device Registration 서비스가 필요 합니다. 온-프레미스에서 조건부 장치 정책을 적용 하려면 장치 개체 쓰기-뒤로 옵션을 사용 하도록 설정 하 여 디렉터리 동기화 도구 (DirSync)를 배포 해야 합니다. 현재 Azure Active Directory에서 Active Directory에 대 한 장치 쓰기 복구는 최대 3 시간이 걸릴 수 있습니다. 따라서 사용자는 회사 계정을 만든 후 3 시간 동안 대기 하 여 온-프레미스 웹 응용 프로그램에 액세스 해야 합니다. Azure Active Directory Device Registration 서비스를 배포 하는 방법에 대 한 자세한 내용은 [Azure Active Directory Device Registration 서비스 개요](https://msdn.microsoft.com/library/azure/dn788908.aspx) 를 참조 하세요.

#### <a name="create-a-work-account-that-joins-your-device-with-workplace-join"></a>작업 공간 연결을 사용 하 여 장치를 연결 하는 회사 계정 만들기

1.  장치에 작업 공간 연결을 사용 하 여 장치를 연결 하는 회사 계정을 만들려면 장치에 Azure Authenticator 응용 프로그램을 설치 해야 합니다. 다음 URL에는 Android 장치에 Azure authenticator 앱을 설치 하 고 회사 계정을 추가 하는 방법에 대 한 지침이 포함 되어 있습니다. 회사 계정은 Android 장치를 신뢰할 수 있는 장치로 만들고 장치의 응용 프로그램에 SSO (Single Sign-on)를 제공 합니다. 신뢰할 수 있는 장치를 사용 하 여 IT 관리자가 권장 하는 대로 웹 응용 프로그램 및 최신 lob (기간 업무) 응용 프로그램에 액세스할 수 있습니다. 자세한 내용은 [Android 용 Azure Authenticator](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to)를 참조 하세요.

## <a name="see-also"></a>관련 항목
[회사 응용 프로그램 전체에서 SSO 및 원활한 두 번째 단계 인증을 위해 모든 장치에서 작업 공간에 연결](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
[Azure Active Directory Device Registration 서비스를 사용 하 여 온-프레미스 조건부 액세스 설정](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup)


