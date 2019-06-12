---
ms.assetid: c5eb3fa0-550c-4a2f-a0bc-698b690c4199
title: 온-프레미스 장치 기반 조건부 액세스 계획
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3a78334f64d9e51515757b01f2d788bf87f67a35
ms.sourcegitcommit: cd12ace92e7251daaa4e9fabf1d8418632879d38
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66501613"
---
# <a name="plan-device-based-conditional-access-on-premises"></a>온-프레미스 장치 기반 조건부 액세스 계획


이 문서에서는 온-프레미스 디렉터리를 Azure AD Connect를 사용 하 여 Azure AD에 연결 되어 있는 하이브리드 시나리오에서 장치 기반 조건부 액세스 정책을 설명 합니다.     

## <a name="ad-fs-and-hybrid-conditional-access"></a>AD FS 및 하이브리드 조건부 액세스  

AD FS는 하이브리드 시나리오에서 조건부 액세스 정책의 온-프레미스 구성 요소를 제공합니다.  클라우드 리소스에 대 한 조건부 액세스에 대 한 Azure AD를 사용 하 여 장치를 등록할 때 Azure AD Connect 장치 쓰기 저장 기능을 사용 하면 장치 등록 정보가 사용할 수 있는 온-프레미스 AD FS 정책을 사용 하 고 적용 하려면.  이 이렇게 하면 온-프레미스 둘 다에 대 한 액세스 제어 정책 및 클라우드 리소스에 일관 된 접근을 해야 합니다.  

![조건부 액세스](media/Plan-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  

### <a name="types-of-registered-devices"></a>등록 된 장치 유형  
세 가지 종류의 등록 된 장치를 모두 Azure AD에서 장치 개체로 표현 됩니다 하 고도 온-프레미스에서 AD FS 사용 하 여 조건부 액세스에 사용할 수 있습니다.  

| |작업 추가 회사 또는 학교 계정  |Azure AD 조인  |Windows 10 Domain Join    
| --- | --- |--- | --- |
|설명    |  사용자가 회사를 추가 또는 학교는 BYOD 장치에는 계정에 대화형으로 합니다.  **참고:** 작업 공간 연결에 Windows 8/8.1에 대 한 대체 회사 또는 학교 계정 추가       | 사용자가 Azure AD에는 Windows 10 작업 장치를 연결 합니다.|Windows 10 도메인 가입 장치는 자동으로 Azure AD에 등록 합니다.|           
|장치에 사용자에 로그인 하는 방법     |  회사 또는 학교 계정으로 Windows에 로그인 합니다.  Microsoft 계정을 사용 하 여 로그인 합니다.       |   장치를 등록 (회사 또는 학교) 계정으로 Windows에 로그인 합니다.      |     AD 계정을 사용 하 여 로그인 합니다.|      
|장치를 관리 하는 방법    |      MDM 정책 (Intune 등록 추가)   | MDM 정책 (Intune 등록 추가)        |   그룹 정책, System Center Configuration Manager (SCCM) |
|Azure AD 트러스트 종류|작업 공간 연결|Azure AD 조인 됨|도메인 가입  |     
|W10 설정 위치    | 설정 > 계정 > 계정 > 회사 또는 학교 계정 추가        | 설정 > 시스템 > 정보 > Azure AD에 가입       |   설정 > 시스템 > 정보 > 도메인에 가입 |       
|또한 iOS 및 Android 장치에서 사용할 수 있습니까?   |    예     |       아니오  |   아니오   |   

  

장치 등록에 대 한 다양 한 방법에 대 한 자세한 내용은 참고 항목:  
* [작업 공간에서 Windows 10 장치 사용](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-windows10-devices/)  
* [작업에 대 한 Windows 10 장치 설정](https://jairocadena.com/2016/01/18/setting-up-windows-10-devices-for-work-domain-join-azure-ad-join-and-add-work-or-school-account/)  
[Windows 10 Mobile Azure Active Directory에 조인](https://technet.microsoft.com/itpro/windows/manage/join-windows-10-mobile-to-azure-active-directory)  

### <a name="how-windows-10-user-and-device-sign-on-is-different-from-previous-versions"></a>Windows 10 사용자 및 장치 Sign on와 다른 점은 이전 버전  
Windows 10 및 AD FS 2016 장치 등록 및 인증의 새로운 측면이 일부에 대해 알아야 할 (특히 경우 이전 릴리스에서 장치 등록 및 "공간"에 매우 잘 알고 있다면).  

첫째, Windows 10 및 Windows Server 2016에서 AD FS에서 장치 등록 및 인증 더 이상 오로지 기반는 X509 인증서 사용자입니다.  향상 된 보안 및 더 원활한 사용자 환경을 제공 하는 새롭고 더욱 강력한 프로토콜이 있습니다.  주요 차이점은, Windows 10 도메인 가입 및 Azure AD 조인에 X509 컴퓨터 인증서와 새 자격 증명을 PRT를 호출 합니다.  내용은 읽어보세요 [여기](https://jairocadena.com/2016/01/18/how-domain-join-is-different-in-windows-10-with-azure-ad/) 하 고 [여기](https://jairocadena.com/2016/02/01/azure-ad-join-what-happens-behind-the-scenes/)합니다.  

둘째, Windows 10 및 AD FS 2016 지원에 대 한 읽을 수 있는 작업에 대 한 Microsoft Passport를 사용 하 여 사용자 인증 [같습니다](https://jairocadena.com/2016/03/09/azure-ad-and-microsoft-passport-for-work-in-windows-10/) 하 고 [여기](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)합니다.  

AD FS 2016 원활 하 게 장치 및 사용자 PRT 및 Passport 자격 증명에 따라 SSO 제공 합니다.  이 문서의 단계를 사용 하 여, 이러한 기능을 사용 하도록 설정 하 고 작동 하 게 볼 수 있습니다.  

### <a name="device-access-control-policies"></a>장치 액세스 제어 정책  
장치는 같은 간단한 AD FS 액세스 제어 규칙에서 사용할 수 있습니다.  

- 등록된 된 장치에만 액세스를 허용 합니다.   
- 장치가 등록 되지 않은 경우 다단계 인증 필요  

그런 다음 네트워크 위치 및 다단계 인증와 같은 다양 한 조건부 액세스 정책 만들기와 같은 다른 요소를 사용 하 여 이러한 규칙을 결합할 수 있습니다.  


- 특정 그룹 또는 그룹의 구성원 제외 하 고 회사 네트워크 외부에서 액세스 하는 등록 되지 않은 장치에 대 한 다단계 인증 필요  

AD FS 2016에서는 이러한 정책은 특정 장치 신뢰 수준 에서도 필요에 맞게 구성할 수 있습니다: 어느 **인증**, **관리**, 또는 **규격**합니다.  

자세한 내용은 AD FS를 구성 하는 방법에 대 한 액세스 제어 정책을 참조 하세요 [AD FS에서 액세스 제어 정책](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)합니다.  

#### <a name="authenticated-devices"></a>인증 된 장치  
인증 된 장치는 MDM (Intune 및 타사 MDMs Windows 10, iOS 용만 Intune 및 Android)에 등록 되지 않은 등록 된 장치.   

인증 된 장치 갖습니다는 **isManaged** 값을 사용 하 여 AD FS 클레임 **FALSE**합니다. (반면에 등록 되지 않은 장치 부족 하 게이 클레임입니다.)  인증 된 장치 (모든 등록 된 장치)가 있고 isKnown AD FS 클레임 값을 가진 **TRUE**합니다.  

#### <a name="managed-devices"></a>관리 되는 장치의 경우:   

관리 되는 장치는 등록 된 MDM. 등록 된 장치  

관리 되는 장치에는 AD isManaged 갖습니다 FS 클레임 값을 가진 **TRUE**합니다.  

#### <a name="devices-compliant-with-mdm-or-group-policies"></a>장치 준수 (MDM 또는 그룹 정책)  
규격 장치는 등록 되지 않은 MDM을 사용 하 여 MDM 정책을 준수 하지만 등록 된 장치입니다. (호환성 정보는 MDM을 사용 하 여 시작 되 고 Azure AD에 기록 됩니다.)  

호환 장치 갖습니다는 **isCompliant** AD FS 클레임 값을 가진 **TRUE**합니다.    

AD FS 2016 장치 및 조건부 액세스 클레임의 전체 목록은 참조 하세요 [참조](#reference)합니다.  


## <a name="reference"></a>참조  
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
