---
ms.assetid: a33bd54c-e6db-4b58-8264-c0f34bd8ba39
title: 연습-Android 장치에 작업 공간 연결
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 73dbe4d62d460f9487467c7d4198d62b3b6af539
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188933"
---
# <a name="walkthrough-workplace-join-to-an-android-device"></a>연습: Android 장치에 작업 공간 연결



## <a name="join-your-device-with-workplace-join"></a>작업 공간 연결을 사용하여 장치를 연결합니다.

> [!NOTE]
> Android 작업 공간 연결에는 Azure Active Directory Device Registration Service에 필요합니다. 조건부 장치 정책을 온-프레미스에 적용 하기 위해 디렉터리 동기화 도구 (DirSync)를 사용 하도록 설정 하는 장치 개체 쓰기 저장 옵션을 사용 하 여 배포 되어야 합니다. 현재, 장치 쓰기 저장 Active Directory에 Azure Active Directory에서은 3 시간 동안 최대 걸릴 수 있습니다. 따라서 사용자가 회사 계정을 만든 후 온-프레미스 웹 응용 프로그램에 액세스 하는 데 3 시간이 대기 해야 합니다. Azure Active Directory Device Registration을 배포 하는 방법에 대 한 자세한 내용은 서비스, 참조, [Azure Active Directory 장치 등록 서비스 개요](https://msdn.microsoft.com/library/azure/dn788908.aspx)

#### <a name="create-a-work-account-that-joins-your-device-with-workplace-join"></a>작업 공간 조인 사용 하 여 장치를 조인 하는 작업 계정 만들기

1.  장치의 작업 공간 연결을 사용 하 여 장치를 조인 하는 작업 계정을 만들려면 Azure Authenticator 응용 프로그램을 설치 해야 합니다. 다음 URL을 Android 장치에서 Azure authenticator 앱을 설치 하 고 회사 계정을 추가 하는 방법 대 한 지침이 있습니다. 회사 계정을 신뢰할 수 있는 장치에 Android 장치를 만들고 장치에서 응용 프로그램에 Single Sign-on (SSO)을 제공 합니다. IT 관리자가 권장 한 대로 액세스 웹 응용 프로그램 및 최신 기간 업무 응용 프로그램에 신뢰할 수 있는 장치를 사용할 수 있습니다. 자세한 내용은 [Android 용 Azure Authenticator](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to)합니다.

## <a name="see-also"></a>관련 항목
[SSO 및 원활한 두 번째 단계 인증에서 회사 응용 프로그램에 대 한 모든 장치에서 작업 공간 가입](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
[Azure Active Directory Device Registration Service를 사용 하 여 온-프레미스 조건부 액세스 설정](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup)


