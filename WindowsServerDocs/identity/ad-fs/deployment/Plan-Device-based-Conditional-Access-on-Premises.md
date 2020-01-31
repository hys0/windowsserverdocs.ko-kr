---
ms.assetid: c5eb3fa0-550c-4a2f-a0bc-698b690c4199
title: 온-프레미스 디바이스 기반 조건부 액세스 계획
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 00a7edf9529e1f116d951fd69d3bfa381d6d413a
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822756"
---
# <a name="plan-device-based-conditional-access-on-premises"></a>온-프레미스 디바이스 기반 조건부 액세스 계획


이 문서에서는 온-프레미스 디렉터리가 Azure AD Connect를 사용 하 여 Azure AD에 연결 되는 하이브리드 시나리오의 장치를 기반으로 하는 조건부 액세스 정책에 대해 설명 합니다.     

## <a name="ad-fs-and-hybrid-conditional-access"></a>AD FS 및 하이브리드 조건부 액세스  

AD FS는 하이브리드 시나리오에서 조건부 액세스 정책의 온-프레미스 구성 요소를 제공합니다.  클라우드 리소스에 대 한 조건부 액세스를 위해 Azure AD에 장치를 등록 하는 경우 Azure AD Connect 장치 쓰기 백 기능을 사용 하 여 온-프레미스에서 장치 등록 정보를 사용 하 여 AD FS 정책을 사용 하 고 적용 합니다.  이러한 방식으로 온-프레미스 및 클라우드 리소스 모두에 대 한 액세스 제어 정책에 대 한 일관 된 접근 방식을 사용할 수 있습니다.  

![조건부 액세스](media/Plan-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  

### <a name="types-of-registered-devices"></a>등록 된 장치의 유형  
등록 된 장치에는 세 가지 종류가 있습니다. 이러한 장치는 모두 Azure AD에서 장치 개체로 표시 되며 온-프레미스 AD FS를 사용 하는 조건부 액세스에도 사용할 수 있습니다.  

| |회사 또는 학교 계정 추가  |Azure AD 조인  |Windows 10 도메인 가입    
| --- | --- |--- | --- |
|설명    |  사용자는 회사 또는 학교 계정을 BYOD 장치에 대화형으로 추가 합니다.  **참고:** 회사 또는 학교 계정 추가는 Windows 8/8.1의 Workplace Join에 대 한 대체 항목입니다.       | 사용자는 Windows 10 작업 장치를 Azure AD에 연결 합니다.|Windows 10 도메인 가입 장치는 Azure AD에 자동으로 등록 됩니다.|           
|사용자가 장치에 로그인 하는 방법     |  회사 또는 학교 계정으로 Windows에 로그인 하지 않습니다.  Microsoft 계정를 사용 하 여 로그인 합니다.       |   장치를 등록 한 (회사 또는 학교) 계정으로 Windows에 로그인 합니다.      |     AD 계정을 사용 하 여 로그인 합니다.|      
|장치를 관리 하는 방법    |      MDM 정책 (추가 Intune 등록 포함)   | MDM 정책 (추가 Intune 등록 포함)        |   그룹 정책, Configuration Manager |
|Azure AD 트러스트 유형|작업 공간 연결 됨|Azure AD 조인 됨|도메인 가입  |     
|W10 설정 위치    | 계정 > 계정 > 회사 또는 학교 계정을 추가 하 > 설정        | 설정 > 시스템 > Azure AD 가입 >       |   도메인 >에 대 한 > 시스템 > 설정 |       
|또한 iOS 및 Android 디바이스에서 사용할 수 있습니까?   |    예     |       아니요  |   아니요   |   

  

장치를 등록 하는 다양 한 방법에 대 한 자세한 내용은 다음을 참조 하세요.  
* [작업 공간에서 Windows 10 장치 사용](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-windows10-devices/)  
* [회사에 대 한 Windows 10 장치 설정](https://jairocadena.com/2016/01/18/setting-up-windows-10-devices-for-work-domain-join-azure-ad-join-and-add-work-or-school-account/)  
[Azure Active Directory에 Windows 10 Mobile 연결](https://technet.microsoft.com/itpro/windows/manage/join-windows-10-mobile-to-azure-active-directory)  

### <a name="how-windows-10-user-and-device-sign-on-is-different-from-previous-versions"></a>Windows 10 사용자 및 디바이스 Sign on와 다른 점은 이전 버전  
Windows 10 및 AD FS 2016의 경우 사용자가 알아야 하는 장치 등록 및 인증에는 몇 가지 새로운 측면이 있습니다 (특히, 이전 릴리스의 장치 등록과 "작업 공간 연결"에 대해 잘 알고 있는 경우).  

첫째, Windows 10 및 Windows Server 2016에서 AD FS에서 디바이스 등록 및 인증 더 이상 오로지 기반는 X509 인증서 사용자입니다.  더 나은 보안과 보다 원활한 사용자 환경을 제공 하는 새롭고 강력한 프로토콜이 있습니다.  중요 한 차이점은 Windows 10 도메인 조인과 Azure AD 조인의 경우 X509 컴퓨터 인증서와 PRT 라는 새 자격 증명이 있습니다.  [여기 및](https://jairocadena.com/2016/01/18/how-domain-join-is-different-in-windows-10-with-azure-ad/) [여기](https://jairocadena.com/2016/02/01/azure-ad-join-what-happens-behind-the-scenes/)에서 모든 정보를 읽을 수 있습니다.  

둘째로, Windows 10 및 AD FS 2016는 [여기](https://jairocadena.com/2016/03/09/azure-ad-and-microsoft-passport-for-work-in-windows-10/) 와 [여기](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)에서 읽을 수 있는 Microsoft Passport for Work를 사용 하 여 사용자 인증을 지원 합니다.  

AD FS 2016는 PRT와 Passport 자격 증명을 기반으로 원활한 장치 및 사용자 SSO를 제공 합니다.  이 문서의 단계를 사용 하 여 이러한 기능을 사용 하도록 설정 하 고 작동 하는지 확인할 수 있습니다.  

### <a name="device-access-control-policies"></a>장치 Access Control 정책  
장치는 다음과 같은 간단한 AD FS 액세스 제어 규칙에서 사용할 수 있습니다.  

- 등록 된 장치 에서만 액세스 허용   
- 장치가 등록 되지 않은 경우 multi-factor authentication 필요  

그런 다음 이러한 규칙을 네트워크 액세스 위치 및 multi-factor authentication과 같은 다른 요소와 결합 하 여 다음과 같은 다양 한 조건부 액세스 정책을 만들 수 있습니다.  


- 등록 되지 않은 장치에 대해 특정 그룹의 구성원을 제외 하 고 회사 네트워크 외부에서 액세스 하는 multi-factor authentication 필요  

AD FS 2016를 사용 하면 특정 장치 신뢰 수준 ( **인증**됨, **관리**됨 또는 **규정 준수**)을 요구 하도록 특별히 이러한 정책을 구성할 수 있습니다.  

AD FS 액세스 제어 정책 구성에 대 한 자세한 내용은 [AD FS의 액세스 제어 정책](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)을 참조 하세요.  

#### <a name="authenticated-devices"></a>인증 된 장치  
인증 된 장치는 MDM에 등록 되지 않은 등록 된 장치 (Windows 10 용 Intune 및 타사 MDMs, iOS 및 Android 용 Intune에만 해당)입니다.   

인증 된 장치에는 값이 **FALSE**인 **isManaged** AD FS 클레임이 있습니다. (등록 되지 않은 장치는이 클레임을 받지 않습니다.)  인증 된 장치 및 등록 된 모든 장치에는 값이 **TRUE**인 isknown AD FS 클레임이 포함 됩니다.  

#### <a name="managed-devices"></a>관리 되는 장치:   

관리 되는 장치는 MDM에 등록 된 장치를 등록 합니다.  

관리 되는 장치에는 값이 **TRUE**인 isManaged AD FS 클레임이 있습니다.  

#### <a name="devices-compliant-with-mdm-or-group-policies"></a>장치 호환 (MDM 또는 그룹 정책 사용)  
규격 장치는 MDM에 등록 되었지만 MDM 정책과 호환 되는 등록 된 장치입니다. 준수 정보는 MDM을 사용 하 여 시작 되며 Azure AD에 기록 됩니다.  

호환 디바이스 갖습니다는 **isCompliant** AD FS 클레임 값을 가진 **TRUE**합니다.    

AD FS 2016 장치 및 조건부 액세스 클레임의 전체 목록은 [참조](#reference)를 참조 하세요.  


## <a name="reference"></a>참고자료  
#### <a name="complete-list-of-new-ad-fs-2016-and-device-claims"></a>새 AD FS 2016 및 장치 클레임의 전체 목록  

* https://schemas.microsoft.com/ws/2014/01/identity/claims/anchorclaimtype  
* http://schemas.xmlsoap.org/ws/2005/05/identity/claims/implicitupn  
* https://schemas.microsoft.com/2014/03/psso  
* https://schemas.microsoft.com/2015/09/prt  
* http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn  
* https://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid  
* https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid  
* http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name  
* https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname  
* https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/registrationid  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/displayname  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/identifier  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/ostype  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/osversion  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged  
* https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser  
* https://schemas.microsoft.com/2014/02/devicecontext/claims/isknown  
* https://schemas.microsoft.com/2014/02/deviceusagetime  
* https://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant  
* https://schemas.microsoft.com/2014/09/devicecontext/claims/trusttype  
* https://schemas.microsoft.com/claims/authnmethodsreferences  
* https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent  
* https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path  
* https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork  
* https://schemas.microsoft.com/2012/01/requestcontext/claims/client-request-id  
* https://schemas.microsoft.com/2012/01/requestcontext/claims/relyingpartytrustid  
* https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-ip  
* https://schemas.microsoft.com/2014/09/requestcontext/claims/userip  
* https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod  
