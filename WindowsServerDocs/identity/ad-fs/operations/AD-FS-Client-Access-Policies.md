---
ms.assetid: ''
title: AD FS에서 클라이언트 액세스 제어 정책
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cc91cd9a446c8ca30471b65374ca99a7bd49d369
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882374"
---
# <a name="controlling-access-to-organizational-data-with-active-directory-federation-services"></a>Active Directory Federation Services 사용 하 여 조직 데이터에 대 한 액세스를 제어합니다.

이 문서에서는 온-프레미스에서 AD FS 사용 하 여 액세스 제어 개요를 제공 하 고 하이브리드 클라우드 시나리오입니다.  

## <a name="ad-fs-and-conditional-access-to-on-premises-resources"></a>AD FS 및 온-프레미스 리소스에 대 한 조건부 액세스 
Active Directory Federation Services가 도입 된 이후 권한 부여 정책 요청의 특성을 기반으로 하는 리소스 및 리소스에 대 한 사용자 액세스를 허용 하거나 제한 하기 위해 제공 되었습니다.  AD FS 버전 간에 이동에, 이러한 정책을 구현 하는 방법 변경 되었습니다.  버전에서 액세스 제어 기능에 대 한 자세한 내용은 다음을 참조 하세요.
- [Windows Server 2016에서에서 AD FS에서 액세스 제어 정책](Access-Control-Policies-in-AD-FS.md)
- [Windows Server 2012 R2의 AD FS에서 액세스 제어](Manage-Risk-with-Conditional-Access-Control.md)


## <a name="ad-fs-and-conditional-access-in-a-hybrid-organization"></a>AD FS 및 하이브리드 조직에서 조건부 액세스  

AD FS는 하이브리드 시나리오에서 조건부 액세스 정책의 온-프레미스 구성 요소를 제공합니다. AD FS 기반 권한 부여 규칙에 사용할 비 Azure AD 리소스와 같은 온-프레미스 AD FS에 직접 페더레이션 응용 프로그램입니다.  클라우드 구성 요소에서 제공 하는 [Azure AD 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)합니다.  Azure AD Connect는 둘을 연결 하는 제어 평면을 제공 합니다.

예를 들어, 클라우드 리소스에 대 한 조건부 액세스에 대 한 Azure AD를 사용 하 여 장치를 등록할 때 Azure AD Connect 장치 쓰기 저장 기능을 사용 하면 장치 등록 정보가 사용할 수 있는 온-프레미스 AD FS 정책을 사용 하 고 적용 하려면.  이 이렇게 하면 온-프레미스 둘 다에 대 한 액세스 제어 정책 및 클라우드 리소스에 일관 된 접근을 해야 합니다.  

![조건부 액세스](../deployment/media/Plan-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  


### <a name="the-evolution-of-client-access-policies-for-office-365"></a>Office 365에 대 한 클라이언트 액세스 정책의 진화
Office 365 및 클라이언트와 사용 중인 클라이언트 응용 프로그램 종류의 위치 등의 요인에 따라 다른 Microsoft Online services에 대 한 액세스를 제한 하려면 AD FS를 사용 하 여 클라이언트 액세스 정책을 사용 하는 많은.  
- [Windows Server 2012 R2 AD FS의 클라이언트 액세스 정책](Access-Control-Policies-W2K12.md)
- [AD FS 2.0에서에서 클라이언트 액세스 정책](Access-Control-Policies-in-AD-FS-2.md)

이러한 정책의 예는 다음과 같습니다.
- Office 365에 대 한 모든 엑스트라넷 클라이언트 액세스를 차단 합니다.
- Office 365, Exchange Active Sync에 대 한 Exchange Online에 액세스 하는 장치를 제외 하 고 모든 엑스트라넷 클라이언트 액세스 차단

종종 권한이 있는 클라이언트만, 데이터를 캐시 하지 않습니다 하는 응용 프로그램을 확인 하 여 데이터 누출의 위험을 완화 하는 이러한 정책의 기본 원본으로 사용 해야 하거나 원격으로 사용할 수 있는 장치 리소스에 대 한 액세스를 가져올 수 있습니다.

AD FS에 대 한 문서화 된 위의 정책 문서화 된 특정 시나리오에서 작동 하는 동안 이러한 일관 되 게 사용할 수 없는 클라이언트 데이터에 의존 하므로 제한 사항이 있습니다.  예를 들어, 클라이언트 응용 프로그램의 id만 사용할 수 있었던 브라우저 또는 Word 또는 Excel 같은 씩 클라이언트를 통해 동일한 데이터에 액세스할 수 있습니다는 SharePoint Online과 같은 리소스 아닌에 따라 Exchange Online 서비스에 대 한 합니다.  또한 AD FS 액세스 하는 SharePoint Online 또는 Exchange Online 같은 Office 365 내에서 리소스를 인식 하지 않습니다.

이러한 제한 사항을 해결 하 고 사용 하는 보다 강력한 방법을 제공 Office 365 또는 다른 Azure AD 기반 리소스에서 비즈니스 데이터에 대 한 액세스를 관리 하려면을 정책을 Microsoft는 Azure AD 조건부 액세스를 도입 했습니다.  Azure AD 조건부 액세스 정책은 Azure AD에서 Office 365, SaaS 또는 사용자 지정 응용 프로그램 내에서 모든 리소스 또는 특정 리소스에 대해 구성할 수 있습니다.  이러한 정책은 장치 신뢰, 위치 및 기타 요인에 피벗 합니다.

Azure AD 조건부 액세스에 대 한 자세한 참조 [Azure Active Directory의 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)

이러한 시나리오를 사용 하도록 설정 하는 키 변경 [최신 인증](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/), Office 클라이언트, Skype, Outlook 및 브라우저에서 동일한 방식으로 작동 하는 사용자 및 장치를 인증 하는 새로운 방법입니다.

## <a name="next-steps"></a>다음 단계
온-프레미스 및 클라우드 전체에 대 한 액세스 제어에 자세한 내용은 다음을 참조 하세요.

- [Azure Active Directory에서 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)
- [AD FS 2016에서에서 액세스 제어 정책](Access-Control-Policies-in-AD-FS.md)
