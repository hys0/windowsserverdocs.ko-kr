---
ms.assetid: 16a344a9-f9a6-4ae2-9bea-c79a0075fd04
title: "TPM 키 대"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9d08efe825e10d526763a1654c7e090427719c51
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="tpm-key-attestation"></a>TPM 키 대

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**작성자**: Windows 그룹과 조자룡 Turner, 선임 지원 엔지니어로  
  
> [!NOTE]  
> 이 콘텐츠는 Microsoft 고객 지원 담당자가 작성 하며 경험이 관리자와 technet 항목 일반적으로 제공 하는 것 보다에 대 한 보다 긴밀 기술 설명은 기능 및 Windows Server 2012 r 2에 대 한 해결 방법을 찾는 누가 시스템 개발자를 위한 것입니다. 그러나 받지 않았습니다 동일한 편집 가공 일부 언어 일반적으로 technet 찾을 수 보다 세련 된 적게 보일 수 있도록 합니다.  
  
## <a name="overview"></a>개요  
지원 동안 Windows 8, 이후 키 TPM 암호로 보호 된 했음을 대 한 발생 없는 장치에 대 한 암호화 인증서 요청 자가 개인 키도를 신뢰할 수 있는 TPM (플랫폼 모듈) 보호 실제로 설명 CAs 했습니다. 이 업데이트에는 해당 대를 수행 하 고 해당 증명 발급된 된 인증서에 반영 하기 위해 캘리포니아 수 있도록 합니다.  
  
> [!NOTE]  
> 이 문서에서는 뷰어가 인증서 서식 개념 익숙한 가정 (참조를 위해 표시 [인증서 템플릿](https://technet.microsoft.com/library/cc730705.aspx)). 또한 뷰어가 엔터프라이즈 CAs 인증서 템플릿에 따라 문제 인증서를 구성 하는 방법에 잘 알고 가정 (참조를 위해 표시 [검사: 구성 CAs 인증서 발급 및 관리 하](https://technet.microsoft.com/library/cc771533.aspx)) 합니다.  
  
### <a name="terminology"></a>용어  
  
|용어|정의|  
|--------|--------------|  
|EK|보증 키입니다. TPM (제조 시간에 삽입)에 포함 비대칭 키입니다. EK 모든 TPM에 대 한 고유 하며 식별할 수 있습니다. EK 변경 또는 제거할 수 없습니다.|  
|EKpub|EK의 공개 키를 의미 합니다.|  
|EKPriv|EK의 개인 키를 의미 합니다.|  
|EKCert|EK 인증서 합니다. TPM 제조업체 발급 된 인증서를 EKPub 합니다. 모든 Tpm EKCert 했습니다.|  
|TPM|신뢰할 수 있는 플랫폼 모듈 합니다. 하드웨어 보안 관련 기능을 제공 하도록 TPM 설계 되었습니다. TPM 칩 암호화 작업을 수행 하도록 설계 된는 보안 암호화 프로세서입니다. 칩 변조을 위해 여러 물리적 보안 메커니즘 포함 되어 있으며 악성 소프트웨어 tpm 보안 기능을 조작할 수 없습니다.|  
  
### <a name="background"></a>배경  
Windows 8 부터는 신뢰할 수 있는 플랫폼 모듈 TPM () 보안 인증서의 개인 키를 사용할 수 있습니다. Microsoft 플랫폼 암호화 공급자 키 저장소 공급자 (KSP)이이 기능을 사용할 수 있습니다. 두 개의 관심사 구현 했습니다.  

-   키를는 TPM (사람이 수 쉽게 위장 소프트웨어 KSP TPM KSP 로컬 관리자 자격 증명으로)으로 보호 되 실제로 되지는 했습니다.

-   엔터프라이즈 (에 PKI 관리자 종류의 환경에서 인증서를 얻는 데 사용할 수 있는 장치를 제어 하려는) 발급 된 인증서를 보호할 수 있는 Tpm 목록이 제한 하지 못했습니다.  

### <a name="tpm-key-attestation"></a>TPM 키 대  
TPM 주요 대는 한 캘리포니아에 증명 암호화 인증서 요청에서 RSA 키는 캘리포니아 신뢰 하는 "a" 또는 "에서" TPM에 의해 보호 되 인증서를 요청 엔터티의 기능입니다. TPM 신뢰 모델에서 자세히 설명는 [배포 개요](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentOverview) 이 항목 뒷부분.  
  
### <a name="why-is-tpm-key-attestation-important"></a>TPM 키 증명 중요 한 이유는?  
TPM attested 키와 함께 사용자 인증서 비 내보내기, 해머링-및 격리 키 TPM에서 제공 하 여 백업 높은 보안 보증을 제공 합니다.  
  
TPM 주요 대와는 새로운 관리 방식은 이제 가능한: 관리자 수 있습니다 (예: VPN 또는 무선 액세스 포인트)에 회사 리소스에 액세스 하는 사용자가 사용할 수 있는 장치를 정의할 **강력한** 에 액세스할 수 없는 다른 디바이스를 사용할 수 있도록 보장 합니다. 이 새로운 액세스 제어 방식은 **강력한** 는 연결 하기 때문에 *하드웨어 바인딩된* 소프트웨어 기반 자격 증명을 보다 강력한 사용자 id를 합니다.
  
### <a name="how-does-tpm-key-attestation-work"></a>TPM 주요 대는 어떻게 작동 하나요?  
일반적으로 TPM 키 증명 다음 기둥에 따라는 다음과 같습니다.  
  
1.  고유한 비대칭 키를 함께 제공 된 모든 TPM 라는 *인증 키* 제조업체가 구울 (EK). 참조 하이 키를의 공개 부분 *EKPub* 와 관련 된 개인 키로 *EKPriv*합니다. 일부 TPM 칩은 EKPub에 대 한 제조업체에서 발급 한 EK 인증서를 수도 있습니다. 이 인증서 부름 *EKCert*합니다.  
  
2.  캘리포니아는 TPM EKPub 또는 EKCert 통해의 보안을 설정합니다.  
  
3.  사용자 요청 되는 인증서 RSA 키는 EKPub 관련이 암호화 하 고 사용자는 EKpriv 소유 하 고 하 고 캘리포니아 증명 합니다.  
  
4.  인증서를 발급 특수 발급 정책을 OID 키가는 TPM에 의해 보호 attested 이제는 나타내기 위해 사용 하 여 합니다.  
  
## <a name="BKMK_DeploymentOverview"></a>배포 개요  
이 배포 Windows Server 2012 R2 enterprise 캘리포니아 설정 간주 됩니다. (Windows 8.1) 클라이언트가 해당 엔터프라이즈 캘리포니아에 등록 하도록 구성 된 또한 템플릿 인증서를 사용 합니다. 

TPM 키 증명을 구축 하는 세 단계는 다음과 같습니다.  
  
1.  **TPM 신뢰 모델 계획:** 첫 번째 단계는 어떤 TPM 신뢰 모델을 사용할지를 결정 합니다. 이 위해 지원 되는 3 가지 방법은 다음과 같습니다.  
  
    -   **신뢰 사용자 자격 증명에 따라:** 엔터프라이즈 캘리포니아 인증서 요청의 일부로 서 사용자가 제공한 EKPub 신뢰 하 고 없는 유효성 검사가 수행 사용자 도메인 자격 이외의 합니다.  
  
    -   **신뢰 EKCert에 따라:** 캘리포니아 엔터프라이즈의 관리자가 관리할 목록과 인증서 요청의 일부로 제공 되는 EKCert 체인의 유효성을 검사 *도 괜찮나요 EK 인증서 체인*합니다. 허용 체인 정의 제조업체 되며 (중간에 대 한 개 저장소)와 캐나다 루트 인증서에 대 한 발급 캐나다에서 두 개의 인증서 사용자 지정 상점을 통해 표시 됩니다. 이 보안 모드는 것을 의미 **모든** 신뢰할 수 있는 Tpm 해당된 제조업체의 합니다. 노트는이 모드에서는 Tpm 환경에서 사용에서이 포함 되도록 EKCerts 합니다.
  
    -   **신뢰 EKPub에 따라:** 캘리포니아 엔터프라이즈의 프로그램 관리자가 관리할 목록에 나타나는 인증서 요청의 일부로 제공 EKPub EKPubs 수 있는지 확인 합니다. 이 목록은 각 파일의이 디렉터리의 이름을 허용된 EKPub의 SHA-2 해시 파일의 디렉터리로 표시 됩니다. 이 옵션은 보증 최상위 제공 하지만 각 디바이스를 개별적으로 식별 때문에 많은 노력이 필요한 합니다. 이 보안 모델 자신의 TPM EKPub EKPubs 허용된 목록에 추가 된 장치만 TPM attested 인증서를 등록할 수 허용 됩니다.  
  
    사용 되는 방법을 따라는 캘리포니아 발급된 된 인증서를 여러 발급 정책을 OID 적용 됩니다. 발급 Oid 정책에 대 한 자세한 내용은 발급 정책 Oid 표를 참조 하세요.는 [인증서 템플릿 구성](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_ConfigCertTemplate) 이 항목의 합니다.  
  
    메모 TPM 신뢰 모델을 조합해 선택할 수 있다는 것입니다. 이 경우에 캘리포니아 증명 방법 및 Oid 실패 하는 모든 증명 메서드를 반영 합니다 발급 정책 중 하나를 허용 합니다.  
  
2.  **인증서 템플릿을 구성:** 에 명시 된 인증서 템플릿 구성는 [배포 세부 정보](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentDetails) 이 항목의 합니다. 이 문서가 인증서 템플릿을 캘리포니아 엔터프라이즈에 할당 되어 어떻게 커버 되지 않거나 등록 하려면 어떻게 액세스는 사용자에 게 제공 됩니다. 자세한 내용은 참조 [검사: 인증서 발급 및 관리를 구성 CAs](https://technet.microsoft.com/library/cc771533.aspx)합니다.  
  
3.  **캘리포니아 TPM 신뢰 모델에 대 한 구성**  
  
    1.  **신뢰 사용자 자격 증명에 따라:** 특정 구성이 필요 하지 않습니다.  
  
    2.  **신뢰 EKCert에 따라:** 관리자 TPM 제조업체에서 EKCert 체인 인증서를 얻는 하 고 캘리포니아 TPM 키 증명을 수행 하는에서 관리자 만든 새 두 인증서 저장소를 가져오는 해야 합니다. 자세한 내용은 참조는 [캘리포니아 구성](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) 이 항목의 합니다.  
  
    3.  **신뢰 EKPub에 따라:** 관리자 EKPub TPM attested 인증서가 필요 되며 EKPubs 허용된 목록에 추가 하는 각 디바이스에 대해 구입 해야 합니다. 자세한 내용은 참조는 [캘리포니아 구성](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) 이 항목의 합니다.  
  
    > [!NOTE]  
    > -   이 기능을 사용 하려면.1 Windows 8 / Windows Server 2012 r 2.  
    > -   제 3 자 스마트 카드 KSPs TPM 주요 증명 지원 되지 않습니다. Microsoft 플랫폼 암호화 공급자 KSP 사용 해야 합니다.  
    > -   TPM 주요 대만 RSA 키에 대해 작동합니다.  
    > -   TPM 키 증명 독립 실행형 캘리포니아 지원 되지 않습니다.  
    > -   TPM 키 증명을 지원 하지 않는 [영구 인증서 처리](https://technet.microsoft.com/library/ff934598)합니다.  
  
## <a name="BKMK_DeploymentDetails"></a>배포 세부 정보  
  
### <a name="BKMK_ConfigCertTemplate"></a>인증서 템플릿을 구성합니다  
TPM 주요 대는 인증서 템플릿을 구성 하려면 다음과 같이 구성:  
  
1.  **호환성** 탭  
  
    에 **호환성 설정을** 섹션.  
  
    -   확인 **Windows Server 2012 r 2** 선택 되어 있는 **인증 기관**합니다.  
  
    -   확인 **.1 Windows 8 / Windows Server 2012 r 2** 선택 되어 있는 **인증서 받는**합니다.  
  
    ![TPM 키 대](media/TPM-Key-Attestation/GTR_ADDS_CompatibilityTab.gif)  
  
2.  **암호화** 탭  
  
    확인 **키 저장소 공급자** 에 대해 선택한는 **공급자 범주** 및 **RSA** 에 대해 선택한는 **알고리즘 이름**합니다. 확인 **요청 공급자 다음 중 하나를 사용 해야** 선택 및 **Microsoft 플랫폼 암호화 공급자** 옵션을 선택 **공급자**합니다.  
  
    ![TPM 키 대](media/TPM-Key-Attestation/GTR_ADDS_CryptoTab.gif)  
  
3.  **키 증명** 탭  
  
    다음은 Windows Server 2012 r 2에 대 한 새 탭을입니다.  
  
    ![TPM 키 대](media/TPM-Key-Attestation/GTR_ADDS_ConfigCertTemplate.gif)  
  
    증명 모드 세 가능한 옵션 중에서 선택 합니다.  
  
    ![TPM 키 대](media/TPM-Key-Attestation/GTR_ADDS_KeyModes.gif)  
  
    -   **없음:** 주요 대를 사용할 수 있어야 의미  
  
    -   **필요한 클라이언트 수 있는 경우:** TPM를 지원 하지 않는 디바이스에서 사용자가 허용 키 증명 해당 인증서에 대 한 등록을 계속 합니다. 증명 수행할 수 있는 사용자에 게 OID 특수 발급 정책으로 구분 됩니다. 일부 장치 핵심 증명 또는 전혀 TPM를가지고 있지 않은 경우 디바이스를 지원 하지 않는 이전 TPM으로 인해 증명을 수행할 수 수 있습니다.
  
    -   **필요한:** 클라이언트 *해야* TPM 키 증명 수행, 그렇지 않으면 인증서 요청이 실패 합니다.  
  
    TPM 신뢰 모델을 선택 합니다. 다시 세 가지 옵션은 다음과 같습니다.  
  
    ![TPM 키 대](media/TPM-Key-Attestation/GTR_ADDS_KeyTypeToEnforce.gif)  
  
    -   **사용자 자격 증명:** 인증 사용자 도메인 자격 증명 지정 하 여 유효한 TPM 보장할 수 있도록 합니다.  
  
    -   **보증 인증서:** 디바이스의 The EKCert 인증서를 통해 관리자 관리 TPM 중간 캘리포니아 관리자 관리 루트 캘리포니아 인증서를 확인 해야 합니다. EKCA 및 EKRoot를 설정 해야 하는 경우이 옵션을 선택 하면 인증서에 설명 된 대로에서 발급 캘리포니아 저장소는 [캘리포니아 구성](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) 이 항목의 합니다.  
  
    -   **보증 키:** 디바이스의 EKPub PKI 관리자 관리 목록에 표시 되어야 합니다. 이 옵션은 보증 최상위 제공 하지만 관리 더 많은 작업이 필요 합니다. 에 설명 된 대로에서 발급 캘리포니아 EKPub 목록을 설정 해야 하는 경우이 옵션을 선택 하면는 [캘리포니아 구성](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) 이 항목의 합니다.  
  
    마지막으로, 발급된 된 인증서에 표시 하는 발급 정책을 결정 합니다. 기본적으로 각 집행 유형에 관련된 OID 개체 식별자 ()은 아래에 설명 된 대로 해당 집행 종류를 통과 하면 인증서에 삽입 됩니다. 메모 적용 방법 조합을 선택 수 있다는 것입니다. 이 경우 대 방법 중 하나는 캘리포니아 수락할 고 발급 정책을 OID 성공 모든 증명 방법 반영 됩니다.  
  
    **정책 Oid 발급**  
  
    |OID|주요 증명 유형|설명|보증 수준|  
    |-------|------------------------|---------------|-------------------|  
    |1.3.6.1.4.1.311.21.30|EK|"EK 확인": EK의 목록을 보려면 관리자 관리|높은|  
    |1.3.6.1.4.1.311.21.31|보증 인증서|"EK 인증서 확인": EK 인증서 체인의 유효성을 검사 하는 경우|보통|  
    |1.3.6.1.4.1.311.21.32|사용자 자격 증명|"EK 신뢰할 수 있는 사용": 사용자 attested EK에 대 한|낮은|  
  
    하는 경우는 Oid 발급된 된 인증서에 삽입 됩니다 **발급 정책 포함** 됩니다 (기본 구성)를 선택 합니다.  
  
    ![TPM 키 대](media/TPM-Key-Attestation/GTR_ADDS_IssuancePolicies.gif)  
  
    > [!TIP]  
    > 인증서에 있는 OID 하는 데 사용할 VPN에 대 한 액세스를 제한 하거나 무선 네트워킹 특정 디바이스입니다. 예를 들어, OID 1.3.6.1.4.1.311.21.30 인증서에 있는 경우 연결 (또는 다른 VLAN에 대 한 액세스) 액세스 정책 허용할 수 있습니다. 해당 TPM EK EKPUB 목록에 있으면 장치에 대 한 액세스를 제한할 수 있습니다.  
  
### <a name="BKMK_CAConfig"></a>캘리포니아 구성  
  
1.  **발급 캘리포니아 EKCA 및 EKROOT 인증서 저장소 설정**  
  
    선택한 경우 **보증 인증서** 템플릿 설정을 다음과 같은 구성 단계를 수행 합니다.  
  
    1.  Windows PowerShell를 사용 하 여 TPM 키 증명을 수행 하는 인증 기관 서버에 두 가지 새로운 인증서 저장소를 만들 수 있습니다.  
  
    2.  중간 받아서 루트 인증서 엔터프라이즈 환경에서 허용 하 시겠습니까 제조업체를 캘리포니아 합니다. 해당 인증서를 적절 하 게 이전에 만든 인증서 저장소 (EKCA 및 EKROOT)로 가져와야 합니다.  
  
    다음 Windows PowerShell 스크립트 이러한 단계를 모두를 수행합니다. 다음 예제에서 TPM 제조업체 Fabrikam 루트 인증서 제공 *FabrikamRoot.cer* 및는 발급 된 인증서 *Fabrikamca.cer*합니다.  
  
    ```powershell  
    PS C:>\cd cert:  
    PS Cert:\>cd .\\LocalMachine  
    PS Cert:\LocalMachine> new-item EKROOT  
    PS Cert:\ LocalMachine> new-item EKCA  
    PS Cert:\EKCA\copy FabrikamCa.cer .\EKCA  
    PS Cert:\EKROOT\copy FabrikamRoot.cer .\EKROOT  
    ```  
  
2.  **EKPUB 목록 EK 증명 유형을 사용 하는 경우 설정**  
  
    선택한 경우 **인증 키** 템플릿 설정을 다음 구성 단계 만들고에 0 바이트 파일을 포함 하 여 발급 캐나다 폴더를 구성할 수는, 허용된 EK SHA-2 콘텐츠의 해시 이름을 각 합니다. 이 폴더는 "허용 목록" 장치를 허용 하도록 TPM 키 attested 인증서를 얻는 역할도 합니다. Attested 인증서가 필요한 각 디바이스에 대 한 EKPUB을 수동으로 추가 해야 하기 때문에 엔터프라이즈 보장 TPM 키 attested 인증서를 얻는 실시 권 자는 장치를 제공 합니다. 이 모드에 대 한 캘리포니아 구성 두 단계가 필요 합니다.  
  
    1.  **만들기 EndorsementKeyListDirectories 레지스트리 항목이 활성화 된:** Certutil 명령줄 도구를 사용 하 여 다음 표에 설명 된 바와 같이 신뢰할 수 있는 EKpubs 정의 되어 있는 폴더 위치가 구성할 수 있습니다.  
  
        |작업|명령 구문|  
        |-------------|------------------|  
        |폴더 위치를 추가|Certutil.exe-setreg CA\EndorsementKeyListDirectories + "<folder>"|  
        |제거 폴더 위치|Certutil.exe-setreg CA\EndorsementKeyListDirectories-"<folder>"|  
  
        Certutil 명령에 EndorsementKeyListDirectories은 아래에 설명 된 대로 레지스트리 설정입니다.  
  
        |이름 값|입력|데이터|  
        |--------------|--------|--------|  
        |EndorsementKeyListDirectories|REG_MULTI_SZ|< 로컬 또는 UNC EKPUB 경로 허용 목록 ><br /><br />예:<br /><br />*\\\blueCA.contoso.com\ekpub*<br /><br />*\\\bluecluster1.contoso.com\ekpub*<br /><br />D:\ekpub|  
  
        HKLM\SYSTEM\CurrentControlSet\Services\CertSvc\Configuration\\<CA Sanitized Name>  
  
        *EndorsementKeyListDirectories* 는 캘리포니아 읽기 액세스할 수 있는 폴더를 가리키도록 각 UNC 또는 로컬 파일 시스템 경로 목록이 포함 됩니다. 각 폴더 0 포함 되어 있거나 더 허용 목록 항목 각 항목은는 SHA-2 이름 파일 콘텐츠의 해시 신뢰할 수 있는 EKpub 없이 파일 확장명을 가진 합니다. 
        만들기 또는 편집이 레지스트리 키 구성 기존 캘리포니아 레지스트리 구성 설정 처럼 캐나다의 다시 시작을 해야 합니다. 그러나 구성 설정에 대 한 편집 즉시 적용 고 캐나다를 다시 시작 하지 않아도 됩니다.  
  
        > [!IMPORTANT]  
        > 폴더 훼손 목록에서 보안 및 무단된 액세스 권한을 관리자 권한이 있는를 구성 하 여 읽고 쓰기 액세스 합니다. 고 캐나다의 컴퓨터 계정 읽기 액세스만 필요합니다.  
  
    2.  **EKPUB 목록을 채웁니다:** 다음과 같은 Windows PowerShell cmdlet 사용 하 여 각 디바이스에서 Windows PowerShell를 사용 하 여 TPM EK 공개 키 콘텐츠의 해시 얻을 보내고 다음이 공개 하 고 캐나다 해시 키 및 EKPubList 폴더에 저장 합니다.  
  
        ```powershell  
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256  
        PS C:>$b=new-item $a.PublickKeyHash -ItemType file  
        ```  
  
## <a name="troubleshooting"></a>문제 해결  
  
### <a name="key-attestation-fields-are-unavailable-on-a-certificate-template"></a>주요 증명 필드 인증서 템플릿에서 사용할 수 없는 경우  
키 증명 필드는 템플릿 설정 대의 요구 사항을 충족 하지 않으면 사용할 수 없습니다. 일반적인 이유는 다음과 같습니다.  
  
1.  호환성 설정은 올바르게 구성 되지 않습니다. 다음과 같이 구성 되어 있는지 확인 합니다.  
  
    1.  **인증 기관**: **Windows Server 2012 r 2**  
  
    2.  **받는 사람에 게 인증서**: **.1 Windows 8 / Windows Server 2012 r 2**  
  
2.  암호화 설정은 올바르게 구성 되지 않습니다. 다음과 같이 구성 되어 있는지 확인 합니다.  
  
    1.  **공급자 범주**: **저장소 공급자 키**  
  
    2.  **알고리즘 이름을**: **RSA**  
  
    3.  **공급자**: **Microsoft 플랫폼 암호화 공급자**  
  
3.  요청 처리 설정은 올바르게 구성 되지 않습니다. 다음과 같이 구성 되어 있는지 확인 합니다.  
  
    1.  **허용 개인 키를 내보낼 수** 옵션을 선택 해야 합니다.  
  
    2.  **개인 주체 암호화 키 보관** 옵션을 선택 해야 합니다.  
  
### <a name="verification-of-tpm-device-for-attestation"></a>TPM 장치에 대 한 확인  
Windows PowerShell cmdlet, 사용 하 여 **확인 CAEndorsementKeyInfo**, CAs 하 여 대를 신뢰할 수 있는 특정 TPM 디바이스 인지 확인 합니다. 다음 두 가지 옵션이: EKCert, 하 고 있는 EKPub 확인 하기 위해 다른 확인 하기 위한 하나입니다. Cmdlet는 되거나 로컬로 원격 CAs 또는 캐나다에 사용 하 여 실행 Windows PowerShell 원격 합니다.  
  
1.  다음 두 단계를 수행는 EKPub에서 보안 확인을.  
  
    1.  **클라이언트 컴퓨터에서는 EKPub 추출:** The EKPub 통해 클라이언트 컴퓨터에서 추출 수 **Get TpmEndorsementKeyInfo**합니다. 관리자 권한 명령 프롬프트에서 다음을 실행 합니다.  
  
        ```  
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256  
        ```  
  
    2.  **캘리포니아 컴퓨터에서 EKCert에서 보안 확인:** 추출된 문자열이 (은 EKPub SHA-2 해시) (예: 메일) 통해 서버에 복사한 확인 CAEndorsementKeyInfo cmdlet에 전달 됩니다. 참고가이 매개 64 문자를 여야 합니다.  
  
        ```  
        Confirm-CAEndorsementKeyInfo [-PublicKeyHash] <string>  
        ```  
  
2.  다음 두 단계를 수행는 EKCert에서 보안 확인을.  
  
    1.  **클라이언트 컴퓨터에서는 EKCert 추출:** The EKCert 통해 클라이언트 컴퓨터에서 추출 수 **Get TpmEndorsementKeyInfo**합니다. 관리자 권한 명령 프롬프트에서 다음을 실행 합니다.  
  
        ```  
        PS C:>\$a= Get- TpmEndorsementKeyInfo  
        PS C:>\$a.manufacturerCertificates|Export-Certificate c:\myEkcert.cer  
        ```  
  
    2.  **캘리포니아 컴퓨터에서 KCert에서 보안 확인:** 압축 푼된 EKCert (EkCert.cer) (예를 들어, 메일 또는 통해 xcopy) 캘리포니아에 복사 합니다. 예를 들어, 캐나다 서버의 인증서 "c:\diagnose" 폴더 파일을 복사 인증을 완료 하려면 다음을 실행 합니다.  
  
        ```  
        PS C:>new-object System.Security.Cryptography.X509Certificates.X509Certificate2 "c:\diagnose\myEKcert.cer" | Confirm-CAEndorsementKeyInfo  
        ```  
  
## <a name="see-also"></a>참조 하십시오  
[신뢰할 수 있는 플랫폼 모듈 기술 개요](https://technet.microsoft.com/library/jj131725.aspx)  
[신뢰할 수 있는 플랫폼 모듈 외부 리소스의 경우:](http://www.cs.unh.edu/~it666/reading_list/Hardware/tpm_fundamentals.pdf)  
  


