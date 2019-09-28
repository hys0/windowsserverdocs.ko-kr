---
ms.assetid: ''
title: AD FS의 클라이언트 Access Control 정책
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: c00a13076b3c3cf28f9efa0a5127f50e34219c84
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358630"
---
# <a name="controlling-access-to-organizational-data-with-active-directory-federation-services"></a>Active Directory Federation Services를 사용 하 여 조직 데이터에 대 한 액세스 제어

이 문서에서는 온-프레미스, 하이브리드 및 클라우드 시나리오에서 AD FS 사용 하는 액세스 제어의 개요를 제공 합니다.  

## <a name="ad-fs-and-conditional-access-to-on-premises-resources"></a>온-프레미스 리소스에 대 한 AD FS 및 조건부 액세스 
Active Directory Federation Services 도입 후에는 권한 부여 정책을 사용 하 여 요청 및 리소스의 특성에 따라 리소스에 대 한 사용자 액세스를 제한 하거나 허용할 수 있었습니다.  AD FS 버전에서 버전으로 이동 했으므로 이러한 정책을 구현 하는 방법이 변경 되었습니다.  버전별 액세스 제어 기능에 대 한 자세한 내용은 다음을 참조 하세요.
- [Windows Server 2016의 AD FS Access Control 정책](Access-Control-Policies-in-AD-FS.md)
- [Windows Server 2012 r 2에서 AD FS의 액세스 제어](Manage-Risk-with-Conditional-Access-Control.md)


## <a name="ad-fs-and-conditional-access-in-a-hybrid-organization"></a>하이브리드 조직의 AD FS 및 조건부 액세스  

AD FS는 하이브리드 시나리오에서 조건부 액세스 정책의 온-프레미스 구성 요소를 제공 합니다. AD FS 기반 권한 부여 규칙은 AD FS에 직접 페더레이션된 온-프레미스 응용 프로그램과 같은 비 Azure AD 리소스에 사용 해야 합니다.  클라우드 구성 요소는 [AZURE AD 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)에서 제공 됩니다.  Azure AD Connect는 두 가지를 연결 하는 제어 평면을 제공 합니다.

예를 들어 클라우드 리소스에 대 한 조건부 액세스를 위해 Azure AD에 장치를 등록 하는 경우 Azure AD Connect 장치 쓰기 복구 기능을 사용 하면 온-프레미스에서 장치 등록 정보를 사용 하 여 AD FS 정책을 사용 하 고 적용할 수 있습니다.  이러한 방식으로 온-프레미스 및 클라우드 리소스 모두에 대 한 액세스 제어 정책에 대 한 일관 된 접근 방식을 사용할 수 있습니다.  

![조건부 액세스](../deployment/media/Plan-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  


### <a name="the-evolution-of-client-access-policies-for-office-365"></a>Office 365에 대 한 클라이언트 액세스 정책의 진화
클라이언트의 위치 및 사용 중인 클라이언트 응용 프로그램의 유형과 같은 요소에 따라 Office 365 및 기타 Microsoft Online services에 대 한 액세스를 제한 하기 위해 AD FS와 함께 클라이언트 액세스 정책을 사용 하는 경우가 많습니다.  
- [Windows Server 2012 R2 AD FS의 클라이언트 액세스 정책](Access-Control-Policies-W2K12.md)
- [AD FS 2.0의 클라이언트 액세스 정책](Access-Control-Policies-in-AD-FS-2.md)

이러한 정책의 몇 가지 예는 다음과 같습니다.
- Office 365에 대 한 모든 엑스트라넷 클라이언트 액세스 차단
- Exchange Active Sync에 대해 Exchange Online에 액세스 하는 장치를 제외 하 고 Office 365에 대 한 모든 엑스트라넷 클라이언트 액세스 차단

이러한 정책에 대 한 기본 요구는 인증 된 클라이언트, 데이터를 캐시 하지 않는 응용 프로그램 또는 원격으로 사용 하지 않도록 설정할 수 있는 장치에서 리소스에 액세스할 수 있도록 하 여 데이터 누출 위험을 완화 하는 것입니다.

위에서 설명한 특정 시나리오에서 AD FS에 대 한 위의 설명 된 정책은 일관 되 게 사용할 수 없는 클라이언트 데이터에 의존 하기 때문에 제한 사항이 있습니다.  예를 들어 클라이언트 응용 프로그램의 id는 SharePoint Online과 같은 리소스에 대해서만 사용할 수 있으며, 브라우저를 통해 동일한 데이터에 액세스 하거나 Word 또는 Excel과 같은 ' 굵은 클라이언트 '를 통해 액세스할 수 있습니다.  AD FS 또한 SharePoint Online 또는 Exchange Online과 같이 액세스 되는 Office 365 내의 리소스를 인식 하지 못합니다.

이러한 제한을 해결 하 고 정책을 사용 하 여 Office 365 또는 기타 Azure AD 기반 리소스의 비즈니스 데이터에 대 한 액세스를 관리 하는 보다 강력한 방법을 제공 하기 위해 Microsoft는 Azure AD 조건부 액세스를 도입 했습니다.  Azure ad 조건부 액세스 정책은 특정 리소스에 대해 구성 하거나 Azure AD의 Office 365, SaaS 또는 사용자 지정 응용 프로그램 내에서 또는 모든 리소스에 대해 구성할 수 있습니다.  이러한 정책은 장치 신뢰, 위치 및 기타 요소에 대해 피벗 됩니다.

Azure AD 조건부 액세스에 대해 자세히 알아보려면 [Azure Active Directory의 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) 를 참조 하세요.

이러한 시나리오를 사용 하도록 설정 하는 주요 변경 내용은 Office 클라이언트, Skype, Outlook 및 브라우저에서 동일 하 게 작동 하는 사용자 및 장치를 인증 하는 새로운 방법인 [최신 인증](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)입니다.

## <a name="next-steps"></a>다음 단계
클라우드 및 온-프레미스에서 액세스를 제어 하는 방법에 대 한 자세한 내용은 다음을 참조 하세요.

- [Azure Active Directory의 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)
- [AD FS 2016의 Access Control 정책](Access-Control-Policies-in-AD-FS.md)
