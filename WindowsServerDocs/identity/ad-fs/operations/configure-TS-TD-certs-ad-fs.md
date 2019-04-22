---
title: 가져오고 있는 AD fs 토큰 서명 및 토큰 암호 해독 인증서 구성
description: 이 문서에서는 TD 고 TS를 구성 하는 방법 설명. AD FS에 대 한 인증서
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 10/23/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d16a886c9fb8f88748ffe732a75f0fd6a32c3702
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820214"
---
# <a name="obtain-and-configure-ts-and-td-certificates-for-ad-fs"></a>가져오고 AD FS에 대 한 TS 및 TD 인증서 구성

이 항목에서는 작업 및 AD FS 토큰 서명 및 토큰 암호 해독 인증서 최신 인지 확인을 수행할 수 있는 절차를 설명 합니다.

토큰 서명 인증서는 표준 X509 페더레이션 서버에서 발급 하는 모든 토큰을 안전 하 게 로그인 하는 데 사용 되는 인증서입니다. 토큰 암호 해독 인증서는 표준 X509 들어오는 토큰의 암호를 해독 하는 데 사용 되는 인증서입니다. 이러한 페더레이션 메타 데이터에도 게시 됩니다.

추가 정보를 참조 하세요. [인증서 요구 사항](../design/ad-fs-requirements.md#BKMK_1)

## <a name="determine-whether-ad-fs-renews-the-certificates-automatically"></a>AD FS 인증서를 자동으로 갱신 여부를 결정 합니다.
기본적으로 초기 구성 시와 인증서 만료 날짜에 도달 하는 경우 토큰 서명 및 토큰 암호 해독 인증서를 자동으로 생성 하려면 AD FS가 구성 됩니다.

다음 Windows PowerShell 명령을 실행할 수 있습니다: `Get-AdfsProperties`합니다.
  
  ![Get-ADFSProperties](media/configure-TS-TD-certs-ad-fs/ts1.png)
  
AutoCertificateRollover 속성 AD FS 토큰 서명 및 인증서를 자동으로 암호 해독 하는 토큰을 갱신 하도록 구성 되어 있는지 설명 합니다.

AutoCertificateRollover를 TRUE로 설정 하는 경우 AD FS 인증서를 갱신 하 고 AD FS에서 자동으로 구성 됩니다. 새 인증서가 구성 되 면 중단을 방지 하기 위해 확인 해야 합니다 (클레임 공급자 트러스트 또는 신뢰 당사자 트러스트에서 AD FS 팜의 표시 됨)는 각 페더레이션 파트너가 새 인증서로 업데이트 되도록 합니다.
    
AD FS 토큰 서명 갱신 하도록 구성 되지 않으며 토큰 경우 자동으로 (AutoCertificateRollover가 False로 설정) 인증서를 암호 해독, AD FS를 자동으로 생성 하거나 새 토큰 서명 또는 인증서를 암호 해독 하는 토큰을 사용 하 여 시작 합니다. 이러한 작업을 수동으로 수행 해야 합니다.
    
AD FS 토큰 서명 및 인증서를 자동으로 암호 해독 하는 토큰을 갱신 하도록 구성 된 경우 (AutoCertificateRollover를 TRUE로 설정 됨), 갱신 때 확인할 수 있습니다.

CertificateGenerationThreshold 기간 (일) 인증서의 이후가 아님 날짜 전에 새 인증서를 생성할 것을 설명 합니다.

CertificatePromotionThreshold 기간 (일) 후 새 인증서를 생성 하는 결정 기본 인증서를 승격할 수는 (즉, AD FS 시작 합니다. 사용 하 여 발급 된 토큰에 서명 하 고 id 공급자의에서 토큰을 해독 하).

![Get-ADFSProperties](media/configure-TS-TD-certs-ad-fs/ts2.png)
  
AD FS 토큰 서명 및 인증서를 자동으로 암호 해독 하는 토큰을 갱신 하도록 구성 된 경우 (AutoCertificateRollover를 TRUE로 설정 됨), 갱신 때 확인할 수 있습니다.

 - **CertificateGenerationThreshold** 기간 (일) 인증서의 이후가 아님 날짜 전에 새 인증서를 생성할에 대해 설명 합니다.
 - **CertificatePromotionThreshold** 기간 (일) 후 새 인증서를 생성 하는 결정 기본 인증서를 승격할 수는 (즉, AD FS 시작 합니다. 사용 하 여 발급 되는 토큰 서명 및 토큰 id의 암호를 해독 하려면 공급자)입니다.

## <a name="determine-when-the-current-certificates-expire"></a>현재 인증서의 만료 시기 결정
기본 토큰 서명 및 인증서를 암호 해독 하는 토큰을 확인 하 고 현재 인증서의 만료 시기를 결정 하려면 다음 절차를 사용할 수 있습니다.

다음 Windows PowerShell 명령을 실행할 수 있습니다: `Get-AdfsCertificate –CertificateType token-signing` (또는 `Get-AdfsCertificate –CertificateType token-decrypting `). 또는 MMC에서 현재 인증서를 검사할 수 있습니다. 서비스 인증서-> 합니다.

![Get-ADFSCertificate](media/configure-TS-TD-certs-ad-fs/ts3.png)

인증서를 **IsPrimary** 값으로 설정 됩니다 **True** AD FS는 현재 사용 중인 인증서입니다.

날짜에 대해 표시 되는 **뒤** 새 기본 토큰 서명 인증서를 암호 해독 또는 구성할 수 있는 날짜입니다.

서비스 연속성을 보장 하기 (클레임 공급자 트러스트 또는 신뢰 당사자 트러스트에서 AD FS 팜의 표시 됨) 하는 모든 페더레이션 파트너는 새 토큰 서명 및 토큰 암호 해독 인증서를이 만료 되기 전에 사용 해야 합니다. 이 프로세스에 대 한 최소 60 일 미리 계획을 시작 하는 것이 좋습니다.

## <a name="generating-a-new-self-signed-certificate-manually-prior-to-the-end-of-the-grace-period"></a>유예 기간 종료 전에 수동으로 새 자체 서명 된 인증서를 생성합니다.
유예 기간 종료 전에 수동으로 새 자체 서명 된 인증서를 생성 하려면 다음 단계를 사용할 수 있습니다.

1. 기본 AD FS 서버에 로그온 확인 합니다.
2. Windows PowerShell을 열고 다음 명령을 실행 합니다. `Add-PSSnapin "microsoft.adfs.powershell"`
3. 필요에 따라 AD FS에서 현재 서명 인증서를 확인할 수 있습니다. 이렇게 하려면 다음 명령을 실행: `Get-ADFSCertificate –CertificateType token-signing`합니다. 뒤의 날짜를 나열 된 모든 인증서를 확인 하려면 명령 출력을 살펴봅니다.
4. 새 인증서를 생성 하려면 갱신 하 고 AD FS 서버에서 인증서를 업데이트 하려면 다음 명령을 실행: `Update-ADFSCertificate –CertificateType token-signing`합니다.
5. 다음 명령을 다시 실행 하 여 업데이트를 확인 합니다. `Get-ADFSCertificate –CertificateType token-signing`
6. 이제 두 개의 인증서 야,이 **이후가 아님** 날짜가 약 1 년 나중에 **IsPrimary** 값이 **False**합니다.

>[!IMPORTANT]
>서비스 중단을 방지 하려면 유효한 토큰 서명 인증서를 사용 하 여 Azure AD 업데이트 하는 방법의 단계를 실행 하 여 Azure AD에서 인증서 정보를 업데이트 합니다.

## <a name="if-youre-not-using-self-signed-certificates"></a>자체 서명 된 인증서를 사용 하지 않는 경우...
자동으로 생성 된 기본을 사용 하지, 자체 서명 된 토큰 서명 및 토큰 암호 해독 인증서 인 경우 갱신 하 고 이러한 인증서를 수동으로 구성 해야 합니다.

먼저 기관에서 새 인증서를 받아야 하며 각 페더레이션 서버의 로컬 컴퓨터 개인 인증서 저장소로 가져옵니다. 지침은 합니다 [인증서를 가져오려면](https://technet.microsoft.com/library/cc754489.aspx) 문서.

그런 다음이 보조 AD FS 토큰 서명 인증서 또는 암호 해독 인증서를 구성 해야 합니다. (구성한 페더레이션 파트너 기본 인증서로 수준을 올리기 전에 새 인증서를 사용 하도록 충분 한 시간을 허용 하도록 보조 인증서로).

### <a name="to-configure-a-new-certificate-as-a-secondary-certificate"></a>보조 인증서로 새 인증서를 구성 하려면
1. PowerShell을 열고 다음을 실행 합니다. `Set-ADFSProperties -AutoCertificateRollover $false`
2. 한 번 인증서를 가져왔습니다. 엽니다는 **AD FS 관리** 콘솔.
3. 확장 **서비스** 선택한 후 **인증서**합니다.
4. 작업 창에서 클릭 **추가 토큰 서명 인증서**합니다.
![Get-ADFSCertificate](media/configure-TS-TD-certs-ad-fs/ts4.png)</br>
5. 표시 된 인증서 목록에서 새 인증서를 선택한 다음 확인을 클릭 합니다.
6.  PowerShell을 열고 다음을 실행 합니다. `Set-ADFSProperties -AutoCertificateRollover $true`

>[!WARNING]
>새 인증서에 연결 된 개인 키를 확인 하 고 개인 키에 대 한 읽기 AD FS 서비스 계정이 부여 됩니다. 각 페더레이션 서버에서이 확인 합니다. 인증서 스냅인에서를 위해 새 인증서를 마우스 오른쪽 단추로 클릭 하 고 모든 작업을 개인 키 관리를 클릭 합니다.

새 인증서 (페더레이션 메타 데이터를 가져올 때 또는 새 인증서의 공개 키를 송신)를 사용 하 여 페더레이션 파트너를 위한 충분 한 시간을 허용한 후 기본 인증서를 보조 인증서를 승격 해야 합니다.

### <a name="to-promote-the-new-certificate-from-secondary-to-primary"></a>보조에서 주로 새 인증서를 승격 하려면

1. 엽니다는 **AD FS 관리** 콘솔.
2. 확장 **서비스** 선택한 후 **인증서**합니다.
3. 보조 토큰 서명 인증서를 클릭 합니다.
4. 에 **동작** 창 클릭 **기본으로 설정**합니다. 확인 프롬프트에서 예를 클릭 합니다.
![Get-ADFSCertificate](media/configure-TS-TD-certs-ad-fs/ts5.png)</br>


## <a name="updating-federation-partners"></a>페더레이션 파트너를 업데이트 하는 중

### <a name="partners-who-can-consume-federation-metadata"></a>페더레이션 메타 데이터를 사용할 수 있는 파트너
갱신 해야 하는 새 토큰 서명 또는 토큰 암호 해독 인증서를 구성 해야 하는 모든 페더레이션 파트너 (당사자 트러스트를 사용 하 여 AD FS에서 표현 되는 리소스 조직 또는 계정 조직의 파트너와 클레임 공급자 트러스트)가 새 인증서를 선택 합니다.

### <a name="partners-who-can-not-consume-federation-metadata"></a>페더레이션 메타 데이터를 사용할 수 있는 파트너
페더레이션 파트너 페더레이션 메타 데이터를 사용할 수 없는, 하는 경우 수동으로 보내야 하 새 토큰 서명 / 토큰 암호 해독 인증서의 공개 키. 모든 리소스 조직에 새 인증서 공개 키 (.cer 파일 또는 전체 체인 포함 하려는 경우. p7b)를 보내거나 계정 조직 파트너 (신뢰 당사자 트러스트와 클레임 공급자 트러스트에서 AD fs에서 표시 됨). 파트너가 새 인증서를 신뢰 하도록 해당 하는 쪽에서 변경 내용을 구현 했습니다.

### <a name="promote-to-primary-if-autocertificaterollover-is-false"></a>기본 수준으로 올리기 (AutoCertificateRollover False 이면)
하는 경우 **AutoCertificateRollover** 로 설정 된 **False**, AD FS를 자동으로 만들지 것입니다 또는 시작을 사용 하 여 새 토큰 서명 또는 토큰 암호 해독 인증서입니다. 이러한 작업을 수동으로 수행 해야 합니다.
모든 새 보조 인증서를 사용 하 여 페더레이션 파트너에 대 한 충분 한 시간 동안 허용, 후 (의 주 클릭 보조 토큰 서명 인증서 및 작업 창에서 MMC 스냅인이 보조 인증서를 승격 **를 주 데이터베이스로 설정**.)

## <a name="updating-azure-ad"></a>Azure AD를 업데이트 하는 중
AD FS는 기존 AD DS 자격 증명을 통해 사용자를 인증 하 여 Office 365와 같은 Microsoft 클라우드 서비스에 single sign-on 액세스를 제공 합니다.  인증서를 사용 하 여 추가 정보를 참조 하세요. [Office 365 및 Azure AD에 대 한 페더레이션 인증서 갱신](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-o365-certs)합니다.