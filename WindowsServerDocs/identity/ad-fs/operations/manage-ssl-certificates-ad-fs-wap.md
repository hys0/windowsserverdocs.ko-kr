---
ms.assetid: a3f50046-5d48-43d3-b0f8-ac2346b15285
title: Windows Server 2016의 AD FS 및 WAP의 SSL 인증서 관리
description: Windows Server 2016의 AD FS 및 WAP의 SSL 인증서 관리
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 10/02/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b832756e123bee0223738ee804ac3a4db2371e84
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855296"
---
# <a name="managing-ssl-certificates-in-ad-fs-and-wap-in-windows-server-2016"></a>Windows Server 2016의 AD FS 및 WAP의 SSL 인증서 관리



이 문서에서는 AD FS 및 WAP 서버에 새 SSL 인증서를 배포 하는 방법을 설명 합니다.

>[!NOTE]
>AD FS 팜에 대해 전달 되는 SSL 인증서를 대체 하는 권장 방법은 Azure AD Connect를 사용 하는 것입니다.  자세한 내용은 [Active Directory Federation Services (AD FS) 팜에 대 한 SSL 인증서 업데이트](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectfed-ssl-update) 를 참조 하세요.

## <a name="obtaining-your-ssl-certificates"></a>SSL 인증서 가져오기
프로덕션 AD FS 팜의 경우 공개적으로 신뢰할 수 있는 SSL 인증서를 권장 합니다. 이는 일반적으로 타사 공용 인증서 공급자에 CSR (인증서 서명 요청)을 제출 하 여 가져옵니다. Windows 7 이상의 PC에서 비롯 하 여 CSR을 생성 하는 다양 한 방법이 있습니다. 공급 업체에이에 대 한 설명서가 있어야 합니다.

- 인증서가 [AD FS 및 웹 응용 프로그램 프록시 SSL 인증서 요구 사항을](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1) 충족 하는지 확인 합니다.

### <a name="how-many-certificates-are-needed"></a>필요한 인증서 수
모든 AD FS 및 웹 응용 프로그램 프록시 서버에서 일반적인 SSL 인증서를 사용 하는 것이 좋습니다. 자세한 요구 사항은 문서 [AD FS 및 웹 응용 프로그램 프록시 SSL 인증서 요구 사항](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1) 을 참조 하세요.

### <a name="ssl-certificate-requirements"></a>SSL 인증서 요구 사항
명명, 신뢰 및 확장의 루트를 포함 한 요구 사항은 문서 [AD FS 및 웹 응용 프로그램 프록시 SSL 인증서 요구 사항](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1) 을 참조 하세요.

## <a name="replacing-the-ssl-certificate-for-ad-fs"></a>AD FS에 대 한 SSL 인증서 바꾸기
> [!NOTE]
> AD FS SSL 인증서는 AD FS 관리 스냅인에 있는 AD FS 서비스 통신 인증서와 다릅니다. AD FS SSL 인증서를 변경 하려면 PowerShell을 사용 해야 합니다.

먼저, AD FS 서버가 실행 중인 인증서 바인딩 모드 (기본 인증서 인증 바인딩 또는 대체 클라이언트 TLS 바인딩 모드)를 확인 합니다.

### <a name="replacing-the-ssl-certificate-for-ad-fs-running-in-default-certificate-authentication-binding-mode"></a>기본 인증서 인증 바인딩 모드에서 실행 되는 AD FS에 대 한 SSL 인증서 바꾸기
기본적으로 AD FS는 포트 443에서 장치 인증서 인증을 수행 하 고 포트 49443 (또는 443이 아닌 구성 가능한 포트)에서 사용자 인증서 인증을 수행 합니다.
이 모드에서 powershell cmdlet Set-adfssslcertificate을 사용 하 여 SSL 인증서를 관리 합니다.

아래의 단계를 수행합니다.

1. 먼저 새 인증서를 가져와야 합니다. 이는 일반적으로 타사 공용 인증서 공급자에 CSR (인증서 서명 요청)을 제출 하 여 수행 됩니다. Windows 7 이상의 PC에서 비롯 하 여 CSR을 생성 하는 다양 한 방법이 있습니다. 공급 업체에이에 대 한 설명서가 있어야 합니다.

    * 인증서가 [AD FS 및 웹 응용 프로그램 프록시 SSL 인증서 요구 사항을](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1) 충족 하는지 확인 합니다.

1. 인증서 공급자 로부터 응답을 받은 후 각 AD FS 및 웹 응용 프로그램 프록시 서버에서 로컬 컴퓨터 저장소로 가져옵니다.

1. **주** AD FS 서버에서 다음 cmdlet을 사용 하 여 새 SSL 인증서를 설치 합니다.

```powershell
Set-AdfsSslCertificate -Thumbprint '<thumbprint of new cert>'
```

다음 명령을 실행 하 여 인증서 지문을 찾을 수 있습니다.

```powershell
dir Cert:\LocalMachine\My\
```

#### <a name="additional-notes"></a>추가 참고 사항

* Set-adfssslcertificate cmdlet은 다중 노드 cmdlet입니다. 즉, 주 복제본에서 실행 해야 하 고 팜의 모든 노드가 업데이트 됩니다. 서버 2016의 새로운 기능은입니다. 2012 R2 서버에서 각 서버에 대해 Set-adfssslcertificate를 실행 해야 했습니다.
* Set-adfssslcertificate cmdlet은 주 서버 에서만 실행 해야 합니다. 주 서버에서 서버 2016을 실행 해야 하 고 팜 동작 수준을 2016로 올려야 합니다.
* Set-adfssslcertificate cmdlet은 PowerShell 원격을 사용 하 여 다른 AD FS 서버를 구성 하 고, 다른 노드에서 포트 5985 (TCP)이 열려 있는지 확인 합니다.
* Set-adfssslcertificate cmdlet은 SSL 인증서의 개인 키에 대 한 읽기 권한을 adfssrv 보안 주체에 게 부여 합니다. 이 보안 주체는 AD FS 서비스를 나타냅니다. AD FS 서비스 계정에 SSL 인증서의 개인 키에 대 한 읽기 액세스 권한을 부여 하는 것은 필요 하지 않습니다.

### <a name="replacing-the-ssl-certificate-for-ad-fs-running-in-alternate-tls-binding-mode"></a>대체 TLS 바인딩 모드에서 실행 되는 AD FS에 대 한 SSL 인증서 바꾸기
대체 클라이언트 TLS 바인딩 모드에서 구성 된 경우 AD FS는 포트 443에서 장치 인증서 인증을 수행 하 고 다른 호스트 이름에도 포트 443에서 사용자 인증서 인증을 수행 합니다. 사용자 인증서 호스트 이름은 "certauth" (예: "certauth.fs.contoso.com")를 사용 하 여 사전 준비 된 AD FS 호스트 이름입니다.
이 모드에서 powershell cmdlet AdfsAlternateTlsClientBinding을 사용 하 여 SSL 인증서를 관리 합니다. 이는 대체 클라이언트 TLS 바인딩 뿐만 아니라 AD FS도 SSL 인증서를 설정 하는 다른 모든 바인딩을 관리 합니다.

아래의 단계를 수행합니다.

1. 먼저 새 인증서를 가져와야 합니다. 이는 일반적으로 타사 공용 인증서 공급자에 CSR (인증서 서명 요청)을 제출 하 여 수행 됩니다. Windows 7 이상의 PC에서 비롯 하 여 CSR을 생성 하는 다양 한 방법이 있습니다. 공급 업체에이에 대 한 설명서가 있어야 합니다.

    * 인증서가 [AD FS 및 웹 응용 프로그램 프록시 SSL 인증서 요구 사항을](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1) 충족 하는지 확인 합니다.

1. 인증서 공급자 로부터 응답을 받은 후 각 AD FS 및 웹 응용 프로그램 프록시 서버에서 로컬 컴퓨터 저장소로 가져옵니다.

1. **주** AD FS 서버에서 다음 cmdlet을 사용 하 여 새 SSL 인증서를 설치 합니다.

```powershell
Set-AdfsAlternateTlsClientBinding -Thumbprint '<thumbprint of new cert>'
```

다음 명령을 실행 하 여 인증서 지문을 찾을 수 있습니다.

```powershell
dir Cert:\LocalMachine\My\
```

#### <a name="additional-notes"></a>추가 참고 사항

* AdfsAlternateTlsClientBinding cmdlet은 다중 노드 cmdlet입니다. 즉, 주 복제본에서 실행 해야 하 고 팜의 모든 노드가 업데이트 됩니다.
* AdfsAlternateTlsClientBinding cmdlet은 주 서버 에서만 실행 해야 합니다. 주 서버에서 서버 2016을 실행 해야 하 고 팜 동작 수준을 2016로 올려야 합니다.
* AdfsAlternateTlsClientBinding cmdlet은 PowerShell 원격을 사용 하 여 다른 AD FS 서버를 구성 하 고, 다른 노드에서 포트 5985 (TCP)이 열려 있는지 확인 합니다.
* AdfsAlternateTlsClientBinding cmdlet은 SSL 인증서의 개인 키에 대 한 읽기 권한을 adfssrv 보안 주체에 게 부여 합니다. 이 보안 주체는 AD FS 서비스를 나타냅니다. AD FS 서비스 계정에 SSL 인증서의 개인 키에 대 한 읽기 액세스 권한을 부여 하는 것은 필요 하지 않습니다.

## <a name="replacing-the-ssl-certificate-for-the-web-application-proxy"></a>웹 응용 프로그램 프록시에 대 한 SSL 인증서 바꾸기
WAP에서 기본 인증서 인증 바인딩 또는 대체 클라이언트 TLS 바인딩 모드를 모두 구성 하는 경우 WebApplicationProxySslCertificate cmdlet을 사용할 수 있습니다.
웹 응용 프로그램 프록시 SSL 인증서를 바꾸려면 **각** 웹 응용 프로그램 프록시 서버에서 다음 cmdlet을 사용 하 여 새 SSL 인증서를 설치 합니다.

```powershell
Set-WebApplicationProxySslCertificate -Thumbprint '<thumbprint of new cert>'
```

이전 인증서가 이미 만료 되어 위의 cmdlet이 실패 한 경우 다음 cmdlet을 사용 하 여 프록시를 다시 구성 합니다.

```powershell
$cred = Get-Credential
```

AD FS 서버의 로컬 관리자 인 도메인 사용자의 자격 증명을 입력 합니다.

```powershell
Install-WebApplicationProxy -FederationServiceTrustCredential $cred -CertificateThumbprint '<thumbprint of new cert>' -FederationServiceName 'fs.contoso.com'
```

## <a name="additional-references"></a>추가 참조  
* [인증서 인증의 대체 호스트 이름 바인딩에 대한 AD FS 지원](../operations/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication.md)
* [AD FS 및 certificate KeySpec 속성 정보](../technical-reference/AD-FS-and-KeySpec-Property.md)
