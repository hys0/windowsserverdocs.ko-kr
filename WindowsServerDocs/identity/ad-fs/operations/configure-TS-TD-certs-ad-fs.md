---
title: AD FS에 대 한 토큰 서명 및 토큰 암호 해독 인증서 가져오기 및 구성
description: 이 문서에서는 AD FS에 대 한 TS 및 TD 인증서를 가져오고 구성 하는 방법을 설명 합니다.
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 10/23/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: c544f956983357bdcaaaf2e5ee5b4ab5f80abb6e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407487"
---
# <a name="obtain-and-configure-ts-and-td-certificates-for-ad-fs"></a>AD FS에 대 한 TS 및 TD 인증서 가져오기 및 구성

이 항목에서는 AD FS 토큰 서명 및 토큰 암호 해독 인증서가 최신 상태 인지 확인 하기 위해 수행할 수 있는 작업 및 절차를 설명 합니다.

토큰 서명 인증서는 페더레이션 서버에서 발급 하는 모든 토큰을 안전 하 게 서명 하는 데 사용 되는 표준 X509 인증서입니다. 토큰 암호 해독 인증서는 들어오는 토큰의 암호를 해독 하는 데 사용 되는 표준 X509 인증서입니다. 페더레이션 메타 데이터에도 게시 됩니다.

자세한 내용은 [인증서 요구 사항](../design/ad-fs-requirements.md#BKMK_1) 을 참조 하세요.

## <a name="determine-whether-ad-fs-renews-the-certificates-automatically"></a>AD FS에서 인증서를 자동으로 갱신할 지 여부 결정
기본적으로 AD FS는 초기 구성 시 및 인증서가 만료 날짜에 근접 하는 경우 토큰 서명 및 토큰 암호 해독 인증서를 자동으로 생성 하도록 구성 됩니다.

다음 Windows PowerShell 명령을 `Get-AdfsProperties`실행할 수 있습니다.
  
  ![Set-adfsproperties](media/configure-TS-TD-certs-ad-fs/ts1.png)
  
AutoCertificateRollover 속성은 AD FS가 토큰 서명 및 토큰 암호 해독 인증서를 자동으로 갱신 하도록 구성 되었는지 여부를 설명 합니다.

AutoCertificateRollover를 TRUE로 설정 하면 AD FS 인증서가 자동으로 갱신 되 고 AD FS에서 구성 됩니다. 새 인증서가 구성 되 면 가동 중단을 방지 하기 위해 각 페더레이션 파트너 (신뢰 당사자 트러스트 또는 클레임 공급자 트러스트를 통해 AD FS 팜에 표시)가이 새 인증서로 업데이트 되었는지 확인 해야 합니다.
    
토큰 서명 및 토큰 암호 해독 인증서를 자동으로 갱신 하도록 AD FS 구성 되지 않은 경우 (AutoCertificateRollover가 False로 설정 된 경우) AD FS 새 토큰 서명 또는 토큰 암호 해독 인증서를 자동으로 생성 하거나 시작 하지 않습니다. 이러한 작업은 수동으로 수행 해야 합니다.
    
토큰 서명 및 토큰 암호 해독 인증서를 자동으로 갱신 하도록 AD FS 구성 되어 있으면 (AutoCertificateRollover가 TRUE로 설정 됨) 갱신 되는 시기를 결정할 수 있습니다.

CertificateGenerationThreshold는 새 인증서가 생성 될 때까지 남은 일 수를 미리 설명 합니다.

CertificatePromotionThreshold은 기본 인증서로 승격 될 새 인증서를 생성 한 후의 일 수를 결정 합니다. 즉 AD FS,이 인증서를 사용 하 여 토큰을 발급 하는 토큰에 서명 하 고 id 공급자에서 토큰을 해독 하는 데 사용 됩니다.

![Set-adfsproperties](media/configure-TS-TD-certs-ad-fs/ts2.png)
  
토큰 서명 및 토큰 암호 해독 인증서를 자동으로 갱신 하도록 AD FS 구성 되어 있으면 (AutoCertificateRollover가 TRUE로 설정 됨) 갱신 되는 시기를 결정할 수 있습니다.

 - **CertificateGenerationThreshold** 는 새 인증서가 생성 될 때까지 남은 일 수를 미리 설명 합니다.
 - **CertificatePromotionThreshold** 는 새 인증서가 생성 된 후의 일 수를 결정 합니다. 즉 AD FS, 기본 인증서로 승격 됩니다. 즉, 발급 하는 토큰에 서명 하는 데 사용 하 고 id에서 토큰의 암호를 해독 하기 시작 합니다. 공급자).

## <a name="determine-when-the-current-certificates-expire"></a>현재 인증서가 만료 되는 시점 결정
다음 절차를 사용 하 여 기본 토큰 서명 및 토큰 암호 해독 인증서를 식별 하 고 현재 인증서가 만료 되는 시점을 확인할 수 있습니다.

다음 Windows PowerShell 명령을 실행할 수 있습니다. `Get-AdfsCertificate –CertificateType token-signing` (또는) `Get-AdfsCertificate –CertificateType token-decrypting ` 또는 MMC에서 현재 인증서를 검사할 수 있습니다. 서비스 > 인증서.

![ADFSCertificate](media/configure-TS-TD-certs-ad-fs/ts3.png)

**IsPrimary** 값이 **True** 로 설정 된 인증서는 AD FS 현재 사용 하 고 있는 인증서입니다.

**다음 시간 이후에** 표시 되는 날짜는 새 기본 토큰 서명 또는 암호 해독 인증서를 구성 해야 하는 날짜입니다.

서비스 연속성을 보장 하기 위해 모든 페더레이션 파트너 (신뢰 당사자 트러스트 또는 클레임 공급자 트러스트를 통해 AD FS 팜에 표시 됨)가 만료 되기 전에 새 토큰 서명 및 토큰 암호 해독 인증서를 사용 해야 합니다. 이 프로세스에 대 한 계획을 최소 60 일 이상 미리 시작 하는 것이 좋습니다.

## <a name="generating-a-new-self-signed-certificate-manually-prior-to-the-end-of-the-grace-period"></a>유예 기간이 끝나기 전에 수동으로 자체 서명 된 새 인증서 생성
다음 단계를 사용 하 여 유예 기간이 끝나기 전에 새 자체 서명 된 인증서를 수동으로 생성할 수 있습니다.

1. 기본 AD FS 서버에 로그온 했는지 확인 합니다.
2. Windows PowerShell을 열고 다음 명령을 실행 합니다.`Add-PSSnapin "microsoft.adfs.powershell"`
3. 필요에 따라 AD FS에서 현재 서명 인증서를 확인할 수 있습니다. 이렇게 하려면 다음 명령을 `Get-ADFSCertificate –CertificateType token-signing`실행 합니다. 명령 출력을 확인 하 여 나열 된 인증서의 이후 날짜를 확인 합니다.
4. 새 인증서를 생성 하려면 다음 명령을 실행 하 여 AD FS 서버 `Update-ADFSCertificate –CertificateType token-signing`에서 인증서를 갱신 하 고 업데이트 합니다.
5. 다음 명령을 다시 실행 하 여 업데이트를 확인 합니다.`Get-ADFSCertificate –CertificateType token-signing`
6. 이제 두 개의 인증서가 나열 됩니다. 그 중 하나는 나중에 약 1 년 **이후** 날짜이 고 **IsPrimary** 값은 **False**입니다.

>[!IMPORTANT]
>서비스 중단을 방지 하려면 유효한 토큰 서명 인증서로 Azure AD를 업데이트 하는 방법의 단계를 실행 하 여 Azure AD에서 인증서 정보를 업데이트 합니다.

## <a name="if-youre-not-using-self-signed-certificates"></a>자체 서명 된 인증서를 사용 하 고 있지 않은 경우 ...
자동으로 생성 된 기본 자체 서명 된 토큰 서명 및 토큰 암호 해독 인증서를 사용 하지 않는 경우 이러한 인증서를 수동으로 갱신 하 고 구성 해야 합니다.

먼저 인증 기관에서 새 인증서를 받아서 각 페더레이션 서버의 로컬 컴퓨터 개인 인증서 저장소로 가져와야 합니다. 자세한 내용은 [인증서 가져오기](https://technet.microsoft.com/library/cc754489.aspx) 문서를 참조 하세요.

그런 다음이 인증서를 보조 AD FS 토큰 서명 또는 암호 해독 인증서로 구성 해야 합니다. (기본 인증서로 수준을 올리기 전에 페더레이션 파트너가이 새 인증서를 사용할 충분 한 시간을 가질 수 있도록 보조 인증서로 구성 합니다.)

### <a name="to-configure-a-new-certificate-as-a-secondary-certificate"></a>보조 인증서로 새 인증서를 구성 하려면
1. PowerShell을 열고 다음을 실행 합니다.`Set-ADFSProperties -AutoCertificateRollover $false`
2. 인증서를 가져온 후 **AD FS Management** console을 엽니다.
3. **서비스** 를 확장 하 고 **인증서**를 선택 합니다.
4. 작업 창에서 **토큰 서명 인증서 추가**를 클릭 합니다.
![ADFSCertificate](media/configure-TS-TD-certs-ad-fs/ts4.png)</br>
5. 표시 된 인증서 목록에서 새 인증서를 선택 하 고 확인을 클릭 합니다.
6.  PowerShell을 열고 다음을 실행 합니다.`Set-ADFSProperties -AutoCertificateRollover $true`

>[!WARNING]
>새 인증서에 연결 된 개인 키가 있고 AD FS 서비스 계정에 개인 키에 대 한 읽기 권한이 부여 되어 있는지 확인 하십시오. 각 페더레이션 서버에서이를 확인 합니다. 이렇게 하려면 인증서 스냅인에서 새 인증서를 마우스 오른쪽 단추로 클릭 하 고 모든 작업을 클릭 한 다음 개인 키 관리를 클릭 합니다.

페더레이션 파트너가 새 인증서를 사용 하는 데 충분 한 시간을 허용 하면 (페더레이션 메타 데이터를 끌어오거나 새 인증서의 공개 키를 보내는 경우) 보조 인증서를 기본 인증서로 승격 해야 합니다.

### <a name="to-promote-the-new-certificate-from-secondary-to-primary"></a>새 인증서를 보조에서 기본으로 승격 하려면

1. **AD FS Management** console을 엽니다.
2. **서비스** 를 확장 하 고 **인증서**를 선택 합니다.
3. 보조 토큰 서명 인증서를 클릭 합니다.
4. **작업** 창에서 **기본으로 설정**을 클릭 합니다. 확인 프롬프트에서 예를 클릭 합니다.
![ADFSCertificate](media/configure-TS-TD-certs-ad-fs/ts5.png)</br>


## <a name="updating-federation-partners"></a>페더레이션 파트너 업데이트

### <a name="partners-who-can-consume-federation-metadata"></a>페더레이션 메타 데이터를 사용할 수 있는 파트너
새 토큰 서명 또는 토큰 암호 해독 인증서를 갱신 하 고 구성한 경우 신뢰 당사자 트러스트를 통해 AD FS에 표시 되는 모든 페더레이션 파트너 (리소스 조직 또는 계정 조직 파트너)를 확인 해야 합니다. 클레임 공급자 트러스트)에서 새 인증서를 선택 했습니다.

### <a name="partners-who-can-not-consume-federation-metadata"></a>페더레이션 메타 데이터를 사용할 수 없는 파트너
페더레이션 파트너가 페더레이션 메타 데이터를 사용할 수 없는 경우 새 토큰 서명/토큰 암호 해독 인증서의 공개 키를 수동으로 전송 해야 합니다. 모든 리소스 조직 또는 계정 조직 파트너 (신뢰 당사자 트러스트와 클레임 공급자 트러스트를 통해 AD FS에 표시)에 새 인증서 공개 키 (.cer 파일 또는 전체 체인을 포함 하려는 경우 p7b)를 보냅니다. 파트너가 새 인증서를 신뢰 하기 위해 그 쪽에서 변경 내용을 구현 하도록 합니다.

### <a name="promote-to-primary-if-autocertificaterollover-is-false"></a>주로 승격 (AutoCertificateRollover가 False 인 경우)
**AutoCertificateRollover** 가 **False**로 설정 된 경우 AD FS는 새 토큰 서명 또는 토큰 암호 해독 인증서를 자동으로 생성 하거나 사용 하지 않습니다. 이러한 작업은 수동으로 수행 해야 합니다.
모든 페더레이션 파트너가 새 보조 인증서를 사용할 수 있는 충분 한 기간을 허용한 후이 보조 인증서를 주 복제본으로 승격 합니다. MMC 스냅인에서 보조 토큰 서명 인증서를 클릭 하 고 작업 창에서 다음을 클릭 합니다. **기본으로 설정**합니다.)

## <a name="updating-azure-ad"></a>Azure AD 업데이트 중
AD FS는 기존 AD DS 자격 증명을 통해 사용자를 인증 하 여 Office 365와 같은 Microsoft 클라우드 서비스에 대 한 Single Sign-On 액세스를 제공 합니다.  인증서 사용에 대 한 자세한 내용은 [Office 365 및 AZURE AD에 대 한 페더레이션 인증서 갱신](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-o365-certs)을 참조 하세요.