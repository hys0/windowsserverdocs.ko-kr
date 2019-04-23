---
ms.assetid: a3f50046-5d48-43d3-b0f8-ac2346b15285
title: Windows Server 2016의 AD FS 및 WAP의 SSL 인증서 관리
description: Windows Server 2016의 AD FS 및 WAP의 SSL 인증서 관리
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 10/02/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: abcff8632bc8a3a75af4eee30c3aed046ca0ccc9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877344"
---
# <a name="managing-ssl-certificates-in-ad-fs-and-wap-in-windows-server-2016"></a>Windows Server 2016의 AD FS 및 WAP의 SSL 인증서 관리

>적용 대상: Windows Server 2016

이 문서에서는 AD FS 및 WAP 서버에 새 SSL 인증서를 배포 하는 방법을 설명 합니다.

>[!NOTE]
>앞으로 AD FS 팜에 대 한 SSL 인증서를 바꾸려면 Azure AD Connect를 사용 하는 것이 좋습니다.  자세한 내용은 참조 하세요. [Active Directory Federation Services (AD FS) 팜에 대 한 SSL 인증서 업데이트](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectfed-ssl-update)

## <a name="obtaining-your-ssl-certificates"></a>SSL 인증서 가져오기
프로덕션 AD FS 팜의 SSL 인증서를 공개적으로 신뢰할 수 있는 것이 좋습니다. 이 문제는 일반적으로 인증서 서명 요청 (CSR) 제 3 자, 공용 인증서 공급자를 제출 하 여 가져옵니다. Windows 7 또는 더 높은 PC에서 포함 하 여 CSR을 생성 하는 방법의 여러 가지가 있습니다. 공급 업체 설명서를이 있어야 합니다.

- 인증서를 충족 하는지 확인 합니다 [AD FS 및 웹 응용 프로그램 프록시 SSL 인증서 요구 사항](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

### <a name="how-many-certificates-are-needed"></a>얼마나 많은 인증서가 필요
모든 AD FS 및 웹 응용 프로그램 프록시 서버에서 공용 SSL 인증서를 사용 하는 것이 좋습니다. 문서를 참조 하는 자세한 요구 사항에 대 한 [AD FS 및 웹 응용 프로그램 프록시 SSL 인증서 요구 사항](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

### <a name="ssl-certificate-requirements"></a>SSL 인증서 요구 사항
이름 지정을 포함 하 여 요구 사항에 대 한 신뢰 및 확장의 루트 문서를 참조 [AD FS 및 웹 응용 프로그램 프록시 SSL 인증서 요구 사항](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

## <a name="replacing-the-ssl-certificate-for-ad-fs"></a>AD FS에 대 한 SSL 인증서를 교체
> [!NOTE]
> AD FS SSL 인증서는 AD FS 관리 스냅인에 AD FS 서비스 통신 인증서로 같지는 않습니다. AD FS SSL 인증서를 변경 하려면 PowerShell을 사용 해야 합니다.

먼저, AD FS 서버가 실행 되는 바인딩 모드는 인증서를 확인 합니다: 기본 인증서 인증 바인딩 또는 대체 클라이언트 TLS 바인딩 모드입니다.

### <a name="replacing-the-ssl-certificate-for-ad-fs-running-in-default-certificate-authentication-binding-mode"></a>기본 바인딩 모드를 인증 하는 인증서를 실행 하는 AD FS 용 SSL 인증서를 교체
AD FS 기본적으로 포트 443 장치 인증서 인증 및 포트 49443에서 사용자 인증서 인증 (또는 구성할 수 없는 포트를 443)를 수행 합니다.
이 모드에서는 Set-adfssslcertificate powershell cmdlet을 사용 하 여 SSL 인증서를 관리 합니다.

아래의 단계를 수행합니다.

1. 먼저 새 인증서를 얻을 수 해야 합니다. 일반적으로 인증서 서명 요청 (CSR) 제 3 자, 공용 인증서 공급자를 제출 하면 됩니다. Windows 7 또는 더 높은 PC에서 포함 하 여 CSR을 생성 하는 방법의 여러 가지가 있습니다. 공급 업체 설명서를이 있어야 합니다.

    * 인증서를 충족 하는지 확인 합니다 [AD FS 및 웹 응용 프로그램 프록시 SSL 인증서 요구 사항](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

1. 인증서 공급자 로부터 응답을 받은 후 각 AD FS 및 웹 응용 프로그램 프록시 서버에서 로컬 컴퓨터 저장소로 가져옵니다.

1. 에 **기본** AD FS 서버에서 새 SSL 인증서를 설치 하려면 다음 cmdlet을 사용 합니다.

```powershell
Set-AdfsSslCertificate -Thumbprint '<thumbprint of new cert>'
```

이 명령을 실행 하 여 인증서 지문을 찾을 수 있습니다.

```powershell
dir Cert:\LocalMachine\My\
```

#### <a name="additional-notes"></a>추가 정보

* Set-adfssslcertificate cmdlet은 다중 노드 cmdlet; 즉,만 주 노드에서 실행 해야 하 고 팜의 모든 노드가 업데이트 됩니다. 이것이 Server 2016의 새로운 기능입니다. Server 2012 R2에서 Set-adfssslcertificate 각 서버에서 실행 해야 합니다.
* Set-adfssslcertificate cmdlet은 주 서버 에서만 실행 해야 합니다. Server 2016을 실행 하려면 주 서버에 및 팜 동작 수준 2016 발생 합니다.
* Set-adfssslcertificate cmdlet은 다른 AD FS 서버를 구성, 포트 5985 TCP ()이 다른 노드에서 열려 있는지 확인 하려면 PowerShell 원격을 사용 합니다.
* Set-adfssslcertificate cmdlet은 SSL 인증서의 읽기 권한을 개인 키에 adfssrv 주 부여 됩니다. 이 보안 주체는 AD FS 서비스를 나타냅니다. SSL 인증서의 개인 키를 AD FS 서비스 계정 읽기 액세스 권한을 부여 하는 데 필요한 것입니다.

### <a name="replacing-the-ssl-certificate-for-ad-fs-running-in-alternate-tls-binding-mode"></a>대체 TLS 바인딩 모드에서 실행 되는 AD FS에 대 한 SSL 인증서를 교체
대체 클라이언트에서 TLS 바인딩 모드를 구성 하는 경우 AD FS 포트 443 장치 인증서 인증 및 사용자 인증서 인증도 포트 443에서 다른 호스트에서 수행 합니다. 사용자 인증서 호스트 이름은 AD FS 호스트 이름 앞에 "certauth", "certauth.fs.contoso.com" 예입니다.
이 모드에서는 AdfsAlternateTlsClientBinding powershell cmdlet을 사용 하 여 SSL 인증서를 관리 합니다. 이 다른 클라이언트 TLS 바인딩 뿐만 아니라 AD FS SSL 인증서도 설정 하는 다른 모든 바인딩을 관리 합니다.

아래의 단계를 수행합니다.

1. 먼저 새 인증서를 얻을 수 해야 합니다. 일반적으로 인증서 서명 요청 (CSR) 제 3 자, 공용 인증서 공급자를 제출 하면 됩니다. Windows 7 또는 더 높은 PC에서 포함 하 여 CSR을 생성 하는 방법의 여러 가지가 있습니다. 공급 업체 설명서를이 있어야 합니다.

    * 인증서를 충족 하는지 확인 합니다 [AD FS 및 웹 응용 프로그램 프록시 SSL 인증서 요구 사항](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

1. 인증서 공급자 로부터 응답을 받은 후 각 AD FS 및 웹 응용 프로그램 프록시 서버에서 로컬 컴퓨터 저장소로 가져옵니다.

1. 에 **기본** AD FS 서버에서 새 SSL 인증서를 설치 하려면 다음 cmdlet을 사용 합니다.

```powershell
Set-AdfsAlternateTlsClientBinding -Thumbprint '<thumbprint of new cert>'
```

이 명령을 실행 하 여 인증서 지문을 찾을 수 있습니다.

```powershell
dir Cert:\LocalMachine\My\
```

#### <a name="additional-notes"></a>추가 정보

* AdfsAlternateTlsClientBinding cmdlet은 다중 노드 cmdlet; 즉,만 주 노드에서 실행 해야 하 고 팜의 모든 노드가 업데이트 됩니다.
* AdfsAlternateTlsClientBinding cmdlet은 주 서버 에서만 실행 해야 합니다. Server 2016을 실행 하려면 주 서버에 및 팜 동작 수준 2016 발생 합니다.
* AdfsAlternateTlsClientBinding cmdlet은 다른 AD FS 서버를 구성, 포트 5985 TCP ()이 다른 노드에서 열려 있는지 확인 하려면 PowerShell 원격을 사용 합니다.
* AdfsAlternateTlsClientBinding cmdlet은 SSL 인증서의 읽기 권한을 개인 키에 adfssrv 주 부여 됩니다. 이 보안 주체는 AD FS 서비스를 나타냅니다. SSL 인증서의 개인 키를 AD FS 서비스 계정 읽기 액세스 권한을 부여 하는 데 필요한 것입니다.

## <a name="replacing-the-ssl-certificate-for-the-web-application-proxy"></a>웹 응용 프로그램 프록시에 대 한 SSL 인증서를 교체
WAP에서 기본 인증서 인증 바인딩 또는 대체 클라이언트 TLS 바인딩 모드 모두를 구성 하기 위한 집합 WebApplicationProxySslCertificate cmdlet을 사용할 수 있습니다.
웹 응용 프로그램 프록시 SSL 인증서를 바꾸려면 **각** 새 SSL 인증서를 설치 하려면 다음 cmdlet을 사용 하는 웹 응용 프로그램 프록시 서버:

```powershell
Set-WebApplicationProxySslCertificate '<thumbprint of new cert>'
```

위의 cmdlet은 이전 인증서가 이미 만료 되어 실패 하는 경우 다음 cmdlet을 사용 하 여 프록시를 다시 구성 합니다.

```powershell
$cred = Get-Credential
```

AD FS 서버의 로컬 관리자 인 도메인 사용자의 자격 증명 입력

```powershell
Install-WebApplicationProxy -FederationServiceTrustCredential $cred -CertificateThumbprint '<thumbprint of new cert>' -FederationServiceName 'fs.contoso.com'
```

## <a name="additional-references"></a>추가 참조  
* [AD FS 인증서 인증에 대 한 대체 호스트 이름 바인딩에 대 한 지원](../operations/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication.md)
* [AD FS 및 인증서 KeySpec 속성 정보](../technical-reference/AD-FS-and-KeySpec-Property.md)
