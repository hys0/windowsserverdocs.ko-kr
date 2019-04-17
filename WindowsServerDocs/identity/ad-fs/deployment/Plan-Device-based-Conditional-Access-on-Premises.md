---
ms.assetid: c5eb3fa0-550c-4a2f-a0bc-698b690c4199
title: "장치 기반 조건부 액세스 온-프레미스 계획"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6303bba92ce4f4f99ae8e5095060b06885e427d6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="plan-device-based-conditional-access-on-premises"></a>장치 기반 조건부 액세스 온-프레미스 계획

>Windows Server 2016 적용 됩니다.

이 문서는 온-프레미스 디렉터리 Azure AD 연결을 사용 하 여 Azure AD에 연결 되어 있는 하이브리드 시나리오에서 디바이스에 따라 조건부 액세스 정책을 설명 합니다.     

## <a name="ad-fs-and-hybrid-conditional-access"></a>ADFS 및 하이브리드 조건부 액세스  

Adfs에 프레미스 구성 조건부 액세스 정책을 하이브리드 시나리오에서 제공합니다.  Azure AD에 대 한 조건 액세스 클라우드 리소스도 장치를 등록할 때 Azure AD 연결 디바이스 다시 기록 기능을 사용 하면 디바이스 등록 정보 제공 온-프레미스 ADFS 정책을 사용 하 고 적용 해야 합니다.  이런 방법이으로 수 있는 온-프레미스 둘 다에 대 한 액세스를 제어 정책 및 리소스 클라우드 하는 일관 된 방법입니다.  

![조건부 액세스](media/Plan-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  

### <a name="types-of-registered-devices"></a>종류의 등록 된 디바이스  
등록 된 디바이스를 Azure AD에 장치 개체도 표시 되 고 조건부 온-프레미스도 ADFS 액세스에 사용할 수 있는 모든 데이터의 세 종류 가지가 있습니다.  

| |추가 직장 또는 학교 계정  |Azure AD 가입  |Windows 10 Domian 가입    
| --- | --- |--- | --- |
|설명    |  사용자가 작품 추가 또는 학교 계정을 BYOD 디바이스에 대화형 합니다.  **참고:** 회사에 Windows 8/8.1 참여에 대 한 대체 하는 추가 회사 또는 학교 계정       | 사용자에 게 Azure ad 자녀가 Windows 10 작업 디바이스에 참여 합니다.|Windows 10 도메인에 가입 장치 Azure AD에 자동으로 등록합니다.|           
|사용자가 얼마나 디바이스에 로그인     |  직장 또는 학교 계정으로 Windows에 로그인 합니다.  Microsoft 계정을 사용 하 여 로그인 합니다.       |   장치를 등록 하는 계정 (회사 또는 학교)으로 Windows에 로그인 합니다.      |     광고 계정을 사용 하 여 로그인 합니다.|      
|디바이스 관리    |      MDM 정책 (와 추가 Intune 등록)   | MDM 정책 (와 추가 Intune 등록)        |   그룹 정책, System Center Configuration Manager SCCM) |
|Azure AD 보안 유형|회사 가입|Azure AD 가입|도메인 가입  |     
|위치 W10 설정    | 설정 > 계정 > 계정 > 회사 또는 학교 계정 추가        | 설정 > 시스템 > 정보 > Azure AD에 참여       |   설정 > 시스템 > 정보 > 도메인 가입 |       
|또한 iOS 및 Android 디바이스에서 사용할 수 있나요?   |    예     |       아니요  |   아니요   |   

  

장치를 등록 하는 다양 한 방법에 대 한 자세한 내용은 참조:  
* [회사에서 Windows 10 디바이스를 사용 하 여](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-windows10-devices/)  
* [회사에 대 한 Windows 10 디바이스를 설정](https://jairocadena.com/2016/01/18/setting-up-windows-10-devices-for-work-domain-join-azure-ad-join-and-add-work-or-school-account/)  
[Windows 10 Mobile에는 Azure Active Directory 가입](https://technet.microsoft.com/itpro/windows/manage/join-windows-10-mobile-to-azure-active-directory)  

### <a name="how-windows-10-user-and-device-sign-on-is-different-from-previous-versions"></a>Windows 10 사용자와 디바이스 기호에는 이전 버전에서 다른 방법  
Windows 10 및 광고 FS 2016 있는 몇 가지 새 디바이스 등록 및 인증에 대해 알아야 할 (특히 경우 이전 버전의에서 장치를 등록 하 고 "회사 가입"를 잘 알고).  

먼저 Windows 10 및 Windows Server 2016에 Adfs의 장치를 등록 하 고 인증 더 이상 삼고는 X509에만 사용자 인증서 합니다.  더 나은 보안 및 더욱 원활 하 게 사용자 경험을 제공 하는 새로운 기능과 더 강력한 프로토콜이 있습니다.  있는 주요 차이 Azure AD에 연결할 및 Windows 10 도메인 가입는 X509는 인증서 컴퓨터와 새로운 자격 증명을 PRT 이라고 합니다.  모든 것을 읽을 수 있습니다 [여기](https://jairocadena.com/2016/01/18/how-domain-join-is-different-in-windows-10-with-azure-ad/) 및 [여기](https://jairocadena.com/2016/02/01/azure-ad-join-what-happens-behind-the-scenes/)합니다.  

Windows 10 및 광고 FS 2016 Microsoft Passport을 사용 하 여 자세한 내용을 확인할 수 있는 작업에 대 한 사용자 인증을 지원 두 번째로, [여기](https://jairocadena.com/2016/03/09/azure-ad-and-microsoft-passport-for-work-in-windows-10/) 및 [여기](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-passport-deployment/)합니다.  

원활 하 게 디바이스와 사용자 SSO PRT 및 Passport 자격 증명을 기반 FS 2016 광고를 제공 합니다.  이 문서에 있는 단계에 따라, 이러한 기능을 사용할 수을 작동 하 게 확인할 수 있습니다.  

### <a name="device-access-control-policies"></a>디바이스 액세스 제어 정책  
디바이스와 같은 간단한 ADFS 액세스 제어 규칙에서 사용할 수 있습니다.  

- 등록 된 디바이스로 액세스 허용   
- 장치를 등록 되지 않은 경우 다중 요소 인증 필요  

이 규칙와 같은 네트워크 위치 액세스 하 고 만드는 풍부한 조건부 액세스 정책을와 같은 다중 요소 인증을 다른 요인 결합 다음 수 있습니다.  


- 회사 네트워크 특정 그룹의 회원 제외 하 고 외부에서 액세스 등록 되지 않은 디바이스에 대 한 다중 요소 인증 필요  

FS 2016 AD 이러한 정책을 구성할 수는 특정 디바이스 보안 수준 필요 전문으로: 두 **인증**, **관리**, 또는 **준수**합니다.  

액세스 제어 정책을 ADFS 구성 대 한 자세한 내용은 참조 하십시오 [adfs에서 액세스 제어 정책을](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)합니다.  

#### <a name="authenticated-devices"></a>인증 된 디바이스  
인증 된 디바이스는 등록 된 디바이스에서 MDM (Intune 및 제 3 자 Windows 10에 대 한 MDMs을 Android 및 iOS에 대해서만 Intune) 등록 하지 않은입니다.   

인증 된 디바이스는는 **isManaged** ADFS 값으로 주장 **FALSE**합니다. (반면 전혀 등록 된 디바이스는 부족이 클레임 합니다.) 인증 된 디바이스 (와 등록 된 모든 디바이스)는 광고 isKnown FS 값으로 주장 **진정한**합니다.  

#### <a name="managed-devices"></a>디바이스 관리 되는 다음과 같습니다.   

관리 되는 장치는 MDM.로 등록 된 디바이스 등록된  

디바이스 관리 되는 광고 isManaged는 FS 값으로 주장 **진정한**합니다.  

#### <a name="devices-compliant-with-mdm-or-group-policies"></a>디바이스 그룹 정책 또는 MDM) (와 호환  
호환 장치는 등록 된 MDM 정책을 준수 있지만 mdm 등록만 하지 합니다. (준수 정보는 MDM와 시작 및 Azure AD에 기록 됩니다.)  

호환 디바이스가는 **isCompliant** ADFS 주장 값으로 **진정한**합니다.    

광고 FS 2016 디바이스 및 조건부 액세스 클레임의 전체 목록을 참조 [참조](#reference)합니다.  


## <a name="reference"></a>참조  
#### <a name="complete-list-of-new-ad-fs-2016-and-device-claims"></a>새 광고 FS 2016 및 장치 클레임의 전체 목록  

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
