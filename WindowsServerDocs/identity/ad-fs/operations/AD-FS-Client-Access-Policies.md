---
ms.assetid: 
title: "Adfs의 클라이언트 액세스 제어 정책"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5e1e1b907e6fccbf2b9906106d3360bd9a6fd69d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="controlling-access-to-organizational-data-with-active-directory-federation-services"></a>조직 Active Directory Federation Services 데이터에 대 한 액세스를 제어

이 문서에서는 온-프레미스를 통해 Adfs로 액세스 제어 간략하게 하이브리드 하 고 구름 시나리오 합니다.  

## <a name="ad-fs-and-conditional-access-to-on-premises-resources"></a>ADFS 및 프레미스 리소스에 대 한 조건 액세스 
Active Directory Federation Services, 출시 이후 인증 정책 제한 하거나 사용자가 특성 요청에 따라 리소스와에서 리소스에 액세스할 수 있도록 수 있게 되었습니다.  Adfs의 버전은 움직일이 정책이 어떻게 구현는 변경 되었습니다.  버전 액세스 제어 기능에 대 한 자세한 내용은 참조:
- [Windows Server 2016에서 adfs에서 액세스 제어 정책](Access-Control-Policies-in-AD-FS.md)
- [Windows Server 2012 r 2에서 adfs에서 액세스 제어](Manage-Risk-with-Conditional-Access-Control.md)


## <a name="ad-fs-and-conditional-access-in-a-hybrid-organization"></a>ADFS 및 하이브리드 조직에서 조건부 액세스  

Adfs에 프레미스 구성 조건부 액세스 정책 하이브리드 시나리오에서 제공합니다. AD 기반 FS 인증 규칙을 사용 해야 비 Azure AD 리소스와 같은 온-프레미스 Adfs에 직접 연결 된 응용 프로그램입니다.  제공 하는 클라우드 구성 요소 [Azure AD 조건부 액세스](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access)합니다.  Azure AD 연결 두 연결 제어 비행기를 제공 합니다.

예를 들어, Azure AD에 대 한 조건 액세스 클라우드 리소스도 장치를 등록할 때 Azure AD 연결 디바이스 다시 기록 기능을 사용 하면 디바이스 등록 정보 제공 온-프레미스 ADFS 정책을 사용 하 고 적용 해야 합니다.  이런 방법이으로 수 있는 온-프레미스 둘 다에 대 한 액세스를 제어 정책 및 리소스 클라우드 하는 일관 된 방법입니다.  

![조건부 액세스](../deployment/media/Plan-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  


### <a name="the-evolution-of-client-access-policies-for-office-365"></a>Office 365에 대 한 클라이언트 액세스 정책을 발전
Office 365와의 위치는 클라이언트와 사용 중인 클라이언트 응용 프로그램 유형 같은 요인에 따라 다른 Microsoft Online services에 대 한 액세스를 제한 하려면 ADFS 클라이언트 액세스 정책의 사용 하 고 여러분 중 상당수.  
- [Windows Server 2012 r 2 adfs에서 클라이언트 액세스 정책](Access-Control-Policies-W2K12.md)
- [ADFS 2.0에에서 대 한 액세스 정책 클라이언트](Access-Control-Policies-in-AD-FS-2.md)

이 정책 중 몇 가지 예는 다음과 같습니다.
- Office 365에 대 한 모든 엑스트라넷 클라이언트 액세스 차단
- Office 365, Exchange Online Exchange Activesync에 대 한 액세스 하는 디바이스를 제외 하 고 모든 엑스트라넷 클라이언트 액세스 차단

이 정책 뒤 기본 필요만 공인된 클라이언트 응용 프로그램에 데이터를 캐시 하지 않는 수 있도록 하 여 데이터 누수 위험을 완화 하는 자주 또는 원격으로 해제할 수는 장치 리소스에 액세스할 수 있습니다.

Adfs의 위의 문서화 정책을 설명 하는 특정 상황에서 작동 하는 동안은 제한이 일관 되 게 사용할 수 있는 클라이언트 데이터에 의존 때문에 있습니다.  예를 들어, 클라이언트 응용 프로그램의 id 에서만 사용할 수 있었던 Exchange Online 기반 서비스에 대 한 및 하지 리소스 등 SharePoint Online 브라우저나 두꺼운 클라이언트 Word 또는 Excel 등을 통해 동일한 데이터에 액세스할 수 있습니다.  또한 ADFS SharePoint Online 또는 Exchange Online 등 액세스 하 고 Office 365 내 리소스를 인식 하지 않습니다.

Microsoft Azure AD 조건부 액세스를 소개 했습니다을 비즈니스 데이터 Office 365 또는 기타 기반 Azure AD 리소스에 액세스를 관리 하려면 정책을 이러한 제한을 주소를 사용 하는 강력한 방법 제공 합니다.  Azure AD 조건부 액세스 정책은 Azure AD에 특정 리소스에 대 한 또는 Office 365, SaaS 또는 사용자 지정 응용 프로그램 내의 일부 또는 전혀 리소스에 대 한 구성할 수 있습니다.  이 정책 장치 보안, 위치 및 기타 요인에 피벗 합니다.

Azure AD 조건부 액세스에 대해 자세히 알아보려면 [Azure Active Directory에 조건부 액세스](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access)

이러한 시나리오 활성화 주요 변경 내용은 [최신 인증](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/), 인증 사용자와 디바이스의 Office 클라이언트, Skype, Outlook 및 브라우저에서 동일한 방식으로 작동 하는 새로운 방법입니다.

## <a name="next-steps"></a>다음 단계
자세한 내용은 클라우드에서에서 액세스 제어 켜고 온-프레미스 참조 하십시오.

- [Azure Active Directory에 조건부 액세스](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access)
- [ADFS 2016에에서 액세스 제어 정책](Access-Control-Policies-in-AD-FS.md)
