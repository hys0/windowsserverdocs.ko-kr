---
title: "가져올 및 하 고 구성 토큰 서명 인증서 토큰 암호 해독 adfs"
description: "이 문서에서는 TS 및 TD 구성 하는 방법에 설명 adfs 인증서"
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 10/23/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0d7f8ba4efb74a377f9f9d748949a934398ebefc
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="obtain-and-configure-ts-and-td-certificates-for-ad-fs"></a>가져올 및 하 고 구성 TS TD 인증서 adfs

이 항목에서는 작업 및 ADFS 토큰 서명 및 토큰 해독 인증서가 최신 상태를 유지 하도록 수행할 수 있는 방법을 설명 합니다.

토큰 서명 인증서는 표준 X509 모든 토큰 연합 서버 발급을 안전 하 게 서명 하는 데 사용 되는 인증서를 합니다. 토큰 해독 인증서가 표준 X509 모든 들어오는 토큰 암호를 해독 하는 데 사용 되는 인증서를 합니다. 이러한도 federation 메타 데이터에 게시 됩니다.

자세한 내용은 참조 [인증서 요구 사항](../design/ad-fs-requirements.md#BKMK_1)

## <a name="determine-whether-ad-fs-renews-the-certificates-automatically"></a>ADFS 인증서를 자동으로 갱신 있는지 여부를 결정 합니다.
기본적으로 ADFS 초기 구성 당시와 인증서가 만료 날짜에 도달 하는 경우 토큰 서명 및 토큰 해독 인증서를 자동으로 생성 구성 됩니다.

다음 Windows PowerShell 명령을 실행: `Get-AdfsProperties`합니다.
  
  ![Get-ADFSProperties](media/configure-TS-TD-certs-ad-fs/ts1.png)
  
AutoCertificateRollover 속성 ADFS 토큰 서명 인증서를 자동으로 해독 토큰 갱신 구성 되어 있는지 여부에 대해 설명 합니다.

AutoCertificateRollover 참 설정 되어 ADFS 인증서 갱신 고 Adfs에서 자동으로 구성 됩니다. 새 인증서를 구성 중단을 방지 하기 위해 해야 (신뢰 파티 신뢰 또는 클레임 제공자 신뢰 ADFS 농장의 표시 됨) 각 federation 파트너 새 인증서도 업데이트 됩니다.
    
ADFS 구성 토큰 서명 갱신 되 고 토큰는 자동으로 (AutoCertificateRollover로 설정 된 경우 False) 인증서를 암호를 해독, Adfs은 자동으로 생성 하거나 새 토큰 서명 또는 토큰 해독 인증서를 사용 하 여 시작 합니다. 이러한 작업을 수동으로 수행 해야 합니다.
    
ADFS 토큰 서명 하 고 토큰 해독 인증서 자동으로 갱신 하도록 구성 된 경우 (AutoCertificateRollover 참으로 설정)을 갱신 시기를 확인할 수 있습니다.

CertificateGenerationThreshold 설명 인증서의 하지 후 날짜에 앞서 며칠이 새 인증서를 생성 됩니다.

CertificatePromotionThreshold 며칠 후 새 인증서 생성 되는 것은 될 수준을 올린 주 인증서를 결정 (즉, ADFS 시작 합니다. 사용 하 여 발급 토큰 서명 하 고 id 공급자 로부터 토큰 암호 해독).

![Get-ADFSProperties](media/configure-TS-TD-certs-ad-fs/ts2.png)
  
ADFS 토큰 서명 하 고 토큰 해독 인증서 자동으로 갱신 하도록 구성 된 경우 (AutoCertificateRollover 참으로 설정)을 갱신 시기를 확인할 수 있습니다.

 - **CertificateGenerationThreshold** 설명 인증서의 하지 후 날짜에 앞서 며칠이 새 인증서를 생성 됩니다.
 - **CertificatePromotionThreshold** 며칠 후 새 인증서 생성 되는 것은 될 수준을 올린 주 인증서를 결정 (즉, ADFS 시작 합니다. 발급 토큰 서명 하 고 id에서 토큰 해독를 사용 하 여 공급자)입니다.

## <a name="determine-when-the-current-certificates-expire"></a>있는 현재 인증서가 만료 될 때를 결정 합니다.
다음 절차 기본 토큰 서명 및 토큰 인증서의 암호를 해독 식별 하 고 있는 현재 인증서가 만료 될 때를 결정을 사용할 수 있습니다.

다음 Windows PowerShell 명령을 실행: `Get-AdfsCertificate –CertificateType token-signing` (또는 `Get-AdfsCertificate –CertificateType token-decrypting `). 또는 MMC에 있는 현재 인증서 검사할 수 있습니다: 서비스 인증서-> 합니다.

![Get-ADFSCertificate](media/configure-TS-TD-certs-ad-fs/ts3.png)

인증서의 **IsPrimary** 값으로 설정 되어 **진정한** ADFS 현재 사용 중인 인증서가 있습니다.

에 대 한 표시 된 날짜는 **하지 후** 새로운 기본 토큰 서명 인증서의 암호를 해독 또는 구성할 수 있는 날짜 합니다.

서비스 연속성 되도록 (신뢰 파티 신뢰 또는 클레임 제공자 신뢰 ADFS 농장의 표시 됨) 하는 모든 federation 파트너 새로운 토큰 서명 및이 만료 되기 전에 토큰 해독 인증서를 사용 해야 합니다. 최소 60 일이이 프로세스에 대 한 계획을 시작 하는 것이 좋습니다.

## <a name="generating-a-new-self-signed-certificate-manually-prior-to-the-end-of-the-grace-period"></a>이 유예 기간이 종료 하기 전에 수동으로 새로운 자체 서명된 인증서를 생성
이 유예 기간이 종료 하기 전에 수동으로 새로운 자체 서명된 인증서를 생성 하려면 다음 단계를 사용할 수 있습니다.

1. 기본 ADFS 서버에 로그온 확인 합니다.
2. Windows PowerShell 열고 다음 명령을 실행 합니다. `Add-PSSnapin "microsoft.adfs.powershell"`
3. 필요에 따라 adfs에서 현재 서명 인증서를 확인할 수 있습니다. 이렇게 하려면 다음 명령을 실행: `Get-ADFSCertificate –CertificateType token-signing`합니다. 나열 된 어떤 인증서의 하지 후 날짜를 보려면 명령 출력 확인 합니다.
4. 새 인증서를 생성 하려면 갱신 ADFS 서버의 인증서를 업데이트 하 고 다음 명령을 실행: `Update-ADFSCertificate –CertificateType token-signing`합니다.
5. 다음 명령을 다시 실행 하 여 업데이트를 확인 합니다. `Get-ADFSCertificate –CertificateType token-signing`
6. 두 개의 인증서 이제 나타납니다, 있고이 중 한는 **후 하지** 약 1 년 앞으로 및 된 날짜는 **IsPrimary** 값이 **False**합니다.

>[!IMPORTANT]
>서비스 중단을 방지 하려면 Azure AD 유효한 토큰 서명 인증서를 업데이트 하는 방법에 단계를 실행 하 여 Azure AD 인증서 정보를 업데이트 합니다.

## <a name="if-youre-not-using-self-signed-certificates"></a>자체 서명된 인증서를 사용 하지 않는 경우...
자동으로 생성 기본값 사용 하지, 서명한 토큰 서명 및 토큰 해독 인증서를 사용 중인 경우 갱신 하 고 이러한 인증서를 수동으로 구성 해야 합니다.

먼저, 인증 기관에서 새 인증서를 얻는 하 고 각 federation 서버에서 로컬 컴퓨터 개인 인증서 스토어를 가져오려면 해야 합니다. 자세한 내용은 [인증서 가져오기](https://technet.microsoft.com/library/cc754489.aspx) 문서 합니다.

그런 다음이 되었거나 암호 해독으로 보조 ADFS 토큰 서명 인증서 구성 해야 합니다. (하면 구성 federation 파트너 주 인증서를 홍보 하기 전에이 새로운 인증서를 사용 하기에 충분 한 시간 수 있도록 보조 인증서로).

### <a name="to-configure-a-new-certificate-as-a-secondary-certificate"></a>새 인증서 보조 인증서 구성 하려면
1. PowerShell을 열고 다음을 실행 합니다. `Set-ADFSProperties -AutoCertificateRollover $false`
2. 인증서 가져온 후. 열려 있는 **AD FS 관리** 콘솔 합니다.
3. 확장 **서비스** 선택한 다음 **인증서**합니다.
4. 작업 창 클릭 **추가 토큰 서명 인증서**합니다.
![Get-ADFSCertificate](media/configure-TS-TD-certs-ad-fs/ts4.png)</br>
5. 새 인증서 표시 된 인증서를 목록에서 선택한 다음 확인을 클릭 합니다.
6.  PowerShell을 열고 다음을 실행 합니다. `Set-ADFSProperties -AutoCertificateRollover $true`

>[!WARNING]
>새 인증서에 관련 된 개인 키를 확인 하 고 개인 키에 대 한 읽기 ADFS 서비스 계정이 부여 됩니다. 각 federation 서버에서이 확인 합니다. 이렇게 하려면 스냅인 인증서를 새 인증서를 마우스 오른쪽 단추로 클릭 하 고 모든 작업을, 관리 개인 키를 클릭 한 다음 합니다.

새 (federation 메타 데이터를 꺼냅니다 또는 새 인증서의 공개 키를 보내는) 인증서를 사용 하 여 federation 파트너에 대 한 충분 한 시간 허용한, 되 면 보조 인증서 기본 인증서를 공유 해야 합니다.

### <a name="to-promote-the-new-certificate-from-secondary-to-primary"></a>기본 주소로 보조에서 새 인증서 올리려면

1. 열려 있는 **AD FS 관리** 콘솔 합니다.
2. 확장 **서비스** 선택한 다음 **인증서**합니다.
3. 보조 토큰 서명 인증서를 클릭 합니다.
4. 에 **작업** 창 클릭 **기본으로 설정**합니다. 명령 프롬프트에 예를 클릭 합니다.
![Get-ADFSCertificate](media/configure-TS-TD-certs-ad-fs/ts5.png)</br>


## <a name="updating-federation-partners"></a>Federation 파트너 업데이트

### <a name="partners-who-can-consume-federation-metadata"></a>파트너에 게 Federation 메타 데이터를 사용할 수 있습니다
갱신 해야 하 고 새로운 토큰 서명 또는 토큰 암호 해독 인증서를 구성할 경우 있는지 확인 해야 하는 모든 사용자 federation 파트너 (사용 함으로써 ADFS 사용자에서 나타나는 리소스 조직 또는 계정 조직 파트너 파티 신뢰 하 고 클레임 제공자 신뢰)는 새로운 인증서 연주 했습니다.

### <a name="partners-who-can-not-consume-federation-metadata"></a>파트너에 게 Federation 메타 데이터를 사용할 수 없습니다
Federation 파트너 federation 메타 데이터를 사용 수 없는 경우 수동으로 보내야을 새 토큰 암호를 해독 / 토큰 서명 인증서의 공개 키. 새 인증서 공개 키 보내기 (.cer 파일 또는.p7b 포함 전체 연결 하려는 경우) 모든 리소스 조직 또는 계정 조직 파트너에 게 (에 표시 되며 사용자 ADFS 의존 파티 신뢰 하 고 공급자 주장 신뢰) 합니다. 새 인증서를 신뢰 편인 변경을 구현 파트너 했습니다.

### <a name="promote-to-primary-if-autocertificaterollover-is-false"></a>기본 홍보 (AutoCertificateRollover False 경우)
하는 경우 **AutoCertificateRollover** 로 설정 되어 **False**, ADFS 자동으로 생성 하지 것입니다 이나 시작을 사용 하 여 새로운 토큰 서명 인증서 암호를 해독 토큰 합니다. 이러한 작업을 수동으로 수행 해야 합니다.
새 보조 인증서를 사용 하 여 federation 파트너의 모든에 대 한 충분 한 시간 동안을 허용 후 홍보이 보조 인증서를 (에서 클릭 보조 토큰 서명 인증서 및 클릭 동작 창에서 MMC 스냅인 기본으로 만들기 **기본 언어로 설정**.)

## <a name="updating-azure-ad"></a>Azure AD 업데이트
Adfs의 기존 AD DS 자격 증명을 통해 사용자가 인증 함으로써 단일 로그인에 액세스 Office 365 같은 Microsoft 클라우드 서비스 제공 합니다.  에 대 한 자세한 내용은 인증서를 사용 하 여 [federation 인증서를 Azure AD 및 Office 365에 대 한 갱신](https://docs.microsoft.com/en-us/azure/active-directory/connect/active-directory-aadconnect-o365-certs)합니다.