---
ms.assetid: a3f50046-5d48-43d3-b0f8-ac2346b15285
title: "Adfs의 인증서를 SSL 및 Windows Server 2016에에서 WAP 관리"
description: "Adfs의 인증서를 SSL 및 Windows Server 2016에에서 WAP 관리"
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 10/02/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5156b3ad357ab8edb5e08a89a459beaf9b8c9b1a
ms.sourcegitcommit: ca7dc3d56a33924ae5fe0e9ffb1274da6dc4e54d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2017
---
# <a name="managing-ssl-certificates-in-ad-fs-and-wap-in-windows-server-2016"></a>Adfs의 인증서를 SSL 및 Windows Server 2016에에서 WAP 관리

>Windows Server 2016 적용 됩니다.

이 문서에서는 새로운 SSL 인증서 Adfs와 WAP 서버에 배포 하는 방법을 설명 합니다.

>[!NOTE]
>Azure AD 연결을 사용 하 여 ADFS 농장 용 향후 SSL 인증서를 교체 하는 권장된 방법이입니다.  자세한 내용은 참조 [SSL 인증서 AD FS(Active Directory Federation Services) 팜에 대 한 업데이트](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectfed-ssl-update)

## <a name="obtaining-your-ssl-certificates"></a>SSL 인증서를 얻는
프로덕션 ADFS 농장 공개적으로 신뢰할 수 있는 SSL 인증 하는 것이 좋습니다. 이 정보는 일반적으로 제 3 자 인증서 서명 요청 (CSR), 공용 인증서 공급자 제출 하 여 얻을 합니다. 다양 한 방법으로 높은 PC 또는 Windows 7에서 등 CSR 생성할 수 있습니다. 공급 업체는이 대 한 설명서가 있어야 합니다.

- 인증서 만족 하는지 확인는 [ADFS 및 웹 응용 프로그램 프록시 SSL 인증서 요구 사항](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

### <a name="how-many-certificates-are-needed"></a>개수 인증서가 필요
모든 ADFS 및 웹 응용 프로그램 프록시 서버에 걸쳐 일반 SSL 인증서를 사용 하는 것이 좋습니다. 자세한 요구 사항을 문서를 참조 [ADFS 및 웹 응용 프로그램 프록시 SSL 인증서 요구 사항](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

### <a name="ssl-certificate-requirements"></a>SSL 인증서 요구 사항
보안 및 확장 프로그램의 루트 이름을 포함 하 여 요구 사항에 대 한 문서를 참조 [ADFS 및 웹 응용 프로그램 프록시 SSL 인증서 요구 사항](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

## <a name="replacing-the-ssl-certificate-for-ad-fs"></a>Adfs SSL 인증서 교체
> [!NOTE]
> 광고 FS SSL 인증서가 FS 관리 AD 스냅인에서 찾을 수 있는 ADFS 서비스 통신 인증서와 동일 합니다. AD FS SSL 인증서를 변경 하려면 PowerShell 사용 해야 합니다.

먼저, 모드 구속력 있는 인증서 ADFS 서버를 실행 하는 확인: 기본 인증서 인증 구속력 또는 다른 클라이언트 TLS 구속력 모드입니다.

### <a name="replacing-the-ssl-certificate-for-ad-fs-running-in-default-certificate-authentication-binding-mode"></a>ADFS 실행 기본 인증서 인증 구속력 모드에 대 한 ssl 교체
ADFS 기본적으로 443 포트 인증서 인증 디바이스와 사용자 인증서 인증 49443 포트에서 (또는 443 하지 않은 구성 가능한 포트)를 수행 합니다.
이 모드에서는 powershell cmdlet 설정 AdfsSslCertificate SSL 인증서 관리 하기 위해 사용 합니다.

다음 단계를 따르세요.

1. 먼저, 새 인증서를 얻는 해야 합니다. 일반적으로 제 3 자 인증서 서명 요청 (CSR), 공용 인증서 공급자 제출 하면 됩니다. 다양 한 방법으로 높은 PC 또는 Windows 7에서 등 CSR 생성할 수 있습니다. 공급 업체는이 대 한 설명서가 있어야 합니다.

    * 인증서 만족 하는지 확인는 [ADFS 및 웹 응용 프로그램 프록시 SSL 인증서 요구 사항](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

1. 인증서 공급자의 응답을 다운로드 한 후 로컬 컴퓨터 저장소 각 ADFS 및 웹 응용 프로그램 프록시 서버로 가져옵니다.

1. 에 **기본** ADFS 서버 새로운 SSL 인증서를 설치 하려면 다음 cmdlet 사용

```powershell
Set-AdfsSslCertificate -Thumbprint '<thumbprint of new cert>'
```

이 명령을 실행 하 여 인증서 지문 찾을 수 있습니다.

```powershell
dir Cert:\LocalMachine\My\
```

#### <a name="additional-notes"></a>추가 참고 사항

* 여러 노드 cmdlet; 설정 AdfsSslCertificate cmdlet이 즉,만 주에서 실행 하는 그룹의 모든 노드 업데이트 됩니다. 서버 2016의 새로운 기능입니다. Server 2012 r 2 각 서버 설정 AdfsSslCertificate 실행 해야 했습니다.
* 설정 AdfsSslCertificate cmdlet에 주 서버에만 실행 합니다. 주 서버 Server 2016을 실행 중 이어야 있고 팜 동작 수준 2016 발생 합니다.
* 설정 AdfsSslCertificate cmdlet 사용 하 여 PowerShell 원격 다른 ADFS 서버 구성 포트 5985가 열립니다 (TCP)가 다른 노드에서 열려 있는지 확인 합니다.
* 설정 AdfsSslCertificate cmdlet SSL 인증서의 읽기 사용 개인 키에 adfssrv 주 권한을 부여 됩니다. 이 주 ADFS 서비스를 나타냅니다. ADFS 서비스 계정 읽기 액세스 SSL 인증서의 개인 키를 허용 하는 데 필요한 것은 아닙니다.

### <a name="replacing-the-ssl-certificate-for-ad-fs-running-in-alternate-tls-binding-mode"></a>암호 확인용 TLS 구속력 모드에서 실행 adfs SSL 인증서 교체
TLS 구속력 모드 대체 클라이언트에서 구성한 경우 ADFS 포트 443 인증서 인증 장치 및 사용자도 443 포트 인증서 인증 다른 호스트에서 수행 합니다. 사용자 인증서 호스트는 ADFS 호스트 레이블이 앞에 "certauth.fs.contoso.com" 예 "certauth"입니다.
이 모드에서는 powershell cmdlet 설정 AdfsAlternateTlsClientBinding SSL 인증서 관리 하기 위해 사용 합니다. 대체 클라이언트 TLS 구속력 뿐 아니라 ADFS 설정에서 SSL 인증서에 대 한 모든 바인딩에 관리 합니다.

다음 단계를 따르세요.

1. 먼저, 새 인증서를 얻는 해야 합니다. 일반적으로 제 3 자 인증서 서명 요청 (CSR), 공용 인증서 공급자 제출 하면 됩니다. 다양 한 방법으로 높은 PC 또는 Windows 7에서 등 CSR 생성할 수 있습니다. 공급 업체는이 대 한 설명서가 있어야 합니다.

    * 인증서 만족 하는지 확인는 [ADFS 및 웹 응용 프로그램 프록시 SSL 인증서 요구 사항](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

1. 인증서 공급자의 응답을 다운로드 한 후 로컬 컴퓨터 저장소 각 ADFS 및 웹 응용 프로그램 프록시 서버로 가져옵니다.

1. 에 **기본** ADFS 서버 새로운 SSL 인증서를 설치 하려면 다음 cmdlet 사용

```powershell
Set-AdfsAlternateTlsClientBinding -Thumbprint '<thumbprint of new cert>'
```

이 명령을 실행 하 여 인증서 지문 찾을 수 있습니다.

```powershell
dir Cert:\LocalMachine\My\
```

#### <a name="additional-notes"></a>추가 참고 사항

* 여러 노드 cmdlet; 설정 AdfsAlternateTlsClientBinding cmdlet이 즉,만 주에서 실행 하는 그룹의 모든 노드 업데이트 됩니다.
* 설정 AdfsAlternateTlsClientBinding cmdlet에 주 서버에만 실행 합니다. 주 서버 Server 2016을 실행 중 이어야 있고 팜 동작 수준 2016 발생 합니다.
* 설정 AdfsAlternateTlsClientBinding cmdlet 사용 하 여 PowerShell 원격 다른 ADFS 서버 구성 포트 5985가 열립니다 (TCP)가 다른 노드에서 열려 있는지 확인 합니다.
* 설정 AdfsAlternateTlsClientBinding cmdlet SSL 인증서의 읽기 사용 개인 키에 adfssrv 주 권한을 부여 됩니다. 이 주 ADFS 서비스를 나타냅니다. ADFS 서비스 계정 읽기 액세스 SSL 인증서의 개인 키를 허용 하는 데 필요한 것은 아닙니다.

## <a name="replacing-the-ssl-certificate-for-the-web-application-proxy"></a>웹 응용 프로그램 프록시 SSL 인증서 교체
WAP는에 기본 인증서 인증 구속력 또는 암호 확인용 클라이언트 TLS 구속력 모드 구성에 대 한 설정 WebApplicationProxySslCertificate cmdlet을 사용할 수 있습니다.
웹 응용 프로그램 프록시 SSL 인증서에 바꾸려면 **각** 웹 응용 프로그램 프록시 서버 새로운 SSL 인증서를 설치 하려면 다음 cmdlet 사용:

```powershell
Set-WebApplicationProxySslCertificate '<thumbprint of new cert>'
```

위의 cmdlet 이전 인증서가 만료 이미 때문에 오류가 발생 하면 다음 cmdlet를 사용 하 여 프록시 다시 구성 합니다.

```powershell
$cred = Get-Credential
```

도메인이 사용자가 ADFS 서버의 로컬 관리자 자격 증명을 입력

```powershell
Install-WebApplicationProxy -FederationServiceTrustCredential $cred -CertificateThumbprint '<thumbprint of new cert>' -FederationServiceName 'fs.contoso.com'
```

## <a name="additional-references"></a>추가 참조  
* [Adfs는 인증서를 인증에 대 한 암호 확인용 호스트 구속력에 대 한 지원](../operations/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication.md)
* [ADFS 및 인증서 KeySpec 속성 정보](../technical-reference/AD-FS-and-KeySpec-Property.md)
