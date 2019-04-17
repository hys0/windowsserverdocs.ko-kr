---
ms.assetid: a33bd54c-e6db-4b58-8264-c0f34bd8ba39
title: "연습-Android 디바이스를 회사 가입"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cfe26947b6b0de28ea50367f82d52815fff8f323
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="walkthrough-workplace-join-to-an-android-device"></a>Android 디바이스를 회사 가입 연습:

>적용 대상: Windows Server 2016, Windows Server 2012 r 2


## <a name="join-your-device-with-workplace-join"></a>회사 계정에 연결 된 디바이스에 참여

> [!NOTE]
> Android 회사 가입 Azure Active Directory 디바이스 등록 서비스 필요합니다. 조건부 디바이스 정책 온-프레미스를 적용 하기 위해 디바이스 개체 다시 쓰기 옵션을 사용 하도록 설정 동기화 도구 디렉터리 (디렉터리 동기화)를 배포 합니다. 현재 시간에 디바이스 다시 쓰기 Active Directory를 Azure Active directory에서은 3 시간 최대 걸릴 수 있습니다. 따라서 사용자가 온-프레미스 웹 응용 프로그램, 회사 계정을 만든 후에 액세스 하는 3 시간에 대 한 기다려야. Azure Active Directory 장치 등록 배포에 대 한 자세한 내용은 대 한 서비스를 참조 하세요 [Azure Active Directory 디바이스 등록 서비스 개요](https://msdn.microsoft.com/library/azure/dn788908.aspx)

#### <a name="create-a-work-account-that-joins-your-device-with-workplace-join"></a>회사 가입와 사용자 디바이스를 연결 하는 회사 계정 만들기

1.  장치에 가입 회사와 디바이스를 연결 하는 회사 계정 만들기를 Azure 인증 응용 프로그램을 설치 해야 합니다. 다음 URL Android 디바이스에서 Azure 인증 앱을 설치 하 고 회사 계정을 추가 하는 방법에 지침입니다. 회사 계정을 Android 디바이스를 신뢰할 수 있는 장치에는 디바이스에서 응용 프로그램을 Single Sign-on (SSO)를 제공 합니다. IT 관리자가 권장 액세스 웹 응용 프로그램 및 최신 온라인 비즈니스 응용 프로그램에 신뢰할 수 있는 디바이스를 사용할 수 있습니다. 자세한 내용은 참조 [Android 용 Azure 인증](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to)합니다.

## <a name="see-also"></a>참조 하십시오
[회사에 SSO와 원활 하 게 두 번째 요소 인증 간에 회사 응용 프로그램에 모든 디바이스에서 참여](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
[온-프레미스 조건부 액세스 Azure Active Directory 디바이스 등록 서비스를 사용 하 여 설정](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup)


