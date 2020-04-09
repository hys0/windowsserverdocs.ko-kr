---
ms.assetid: 16a344a9-f9a6-4ae2-9bea-c79a0075fd04
title: TPM 키 증명
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: de5a38ff6f811046d06c52a1ca4598f9650b3cfe
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823016"
---
# <a name="tpm-key-attestation"></a>TPM 키 증명

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**작성자**: Justin Turner, Windows 그룹이 포함 된 선임 지원 에스컬레이션 엔지니어  
  
> [!NOTE]  
> 이 콘텐츠는 Microsoft 고객 지원 엔지니어에 의해 작성되었으며 Windows Server 2012 R2의 기능 및 솔루션에 대해 TechNet에서 일반적으로 제공하는 항목보다 더 자세한 기술적 설명을 찾고 있는 숙련된 관리자 및 시스템 설계자를 대상으로 합니다. 그러나 동일한 편집 과정을 수행하지 않았으므로 일부 언어는 일반적으로 TechNet에서 찾을 수 있는 것보다 완벽하지 않을 수 있습니다.  
  
## <a name="overview"></a>개요  
지원 하는 동안 TPM으로 보호 된 키가 Windows 8부터 존재 했던에 대 한 없었습니다 암호화 인증서 요청자 프라이빗 키의 여는 모듈 TPM(Trusted Platform)을 보호 하 고 실제로 설명 하는 Ca에 대 한 메커니즘 없습니다. 이 업데이트에는 해당 증명을 수행 하 고 해당 증명 발급된 된 인증서에 반영 하는 CA 수 있도록 합니다.  
  
> [!NOTE]  
> 이 문서에서는 판독기가 인증서 템플릿 개념을 알고 있다고 가정 (참조를 참조 하십시오. [인증서 템플릿](https://technet.microsoft.com/library/cc730705.aspx)). 가 잘 인증서 템플릿을 기반으로 인증서를 발급 하는 엔터프라이즈 Ca를 구성 하는 방법에 잘 알고 있다고 가정 합니다 (참조를 참조 하십시오. [검사 목록: 구성 Ca가 인증서 발급 및 관리](https://technet.microsoft.com/library/cc771533.aspx)).  
  
### <a name="terminology"></a>용어  
  
|용어|정의|  
|--------|--------------|  
|EK|인증 키입니다. TPM (제조 과정에 주입) 내에 포함 하는 비대칭 키입니다. EK 모든 TPM에 대 한 고유 하며이 지정할 수 있습니다. EK 변경 하거나 제거할 수 없습니다.|  
|EKpub|EK의 공개 키를 참조합니다.|  
|EKPriv|EK의 프라이빗 키를 참조하세요.|  
|EKCert|EK 인증서입니다. EKPub에 대 한 TPM 제조업체에서 발급 한 인증서입니다. 모든 Tpm EKCert 있으며|  
|TPM|신뢰할 수 있는 플랫폼 모듈입니다. TPM은 하드웨어 기반의 보안 관련 기능을 제공 하도록 설계 되었습니다. TPM 칩은 암호화 작업을 수행하도록 설계된 보안 암호화 프로세서입니다. 칩에는 변조를 방지하는 여러 가지 실제 보안 메커니즘이 포함되어 있으며, 악성 소프트웨어가 TPM의 보안 기능을 변조할 수 없습니다.|  
  
### <a name="background"></a>배경  
Windows 8 부터는 신뢰할 수 있는 플랫폼 모듈 (TPM) 데 사용할 수는 인증서의 프라이빗 키 보호 합니다. Microsoft 플랫폼 암호화 공급자 키 저장소 공급자 KSP ()는이 기능을 활성화합니다. 구현으로 두 가지 문제가 있었습니다.  

-   실제로 TPM에서 키를 보호 하는 것이 보장 되지 않았습니다. 누군가가 로컬 관리자 자격 증명을 사용 하 여 소프트웨어 KSP를 TPM KSP로 쉽게 스푸핑할 수 있습니다.

-   목록이 허용 되는 엔터프라이즈 발급 된 인증서 (하는 경우 PKI 관리자가 제어 환경에서 인증서를 가져올 때 사용할 수 있는 장치 유형을 하려는)를 보호 하기 위해 Tpm 제한할 수 없습니다.  

### <a name="tpm-key-attestation"></a>TPM 키 증명  
TPM 키 증명은 인증서 요청에서 RSA 키가 CA가 신뢰 하는 "a" 또는 "the" TPM으로 보호 됨을 CA에 증명 하는 인증서를 요청 하는 엔터티의 기능입니다. TPM 트러스트 모델에 대해서는이 항목의 뒷부분에 나오는 [배포 개요](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentOverview) 섹션에서 자세히 설명 합니다.  
  
### <a name="why-is-tpm-key-attestation-important"></a>TPM 키 증명 중요 한 이유는 무엇입니까?  
TPM-증명 된 키를 사용 하는 사용자 인증서는 내보내기, 공세 및 TPM에서 제공 하는 키 격리에 의해 백업 되는 더 높은 보안 보증을 제공 합니다.  
  
TPM 키 증명을 사용 하 여 새로운 관리 패러다임을 사용할 수 있습니다. 관리자는 사용자가 회사 리소스에 액세스 하는 데 사용할 수 있는 장치 집합 (예: VPN 또는 무선 액세스 지점)을 정의 하 고 다른 장치를 사용 하 여 액세스할 수 없도록 **강력** 하 게 보장할 수 있습니다. 이 새로운 액세스 제어 패러다임은 소프트웨어 기반 자격 증명 보다 강력한 *하드웨어 바인딩된* 사용자 id에 연결 되기 때문에 **강력** 합니다.
  
### <a name="how-does-tpm-key-attestation-work"></a>TPM 키 증명 어떻게 작동 합니까?  
일반적으로 TPM 키 증명은 다음 핵심 요소을 기반으로 합니다.  
  
1.  모든 TPM에는 제조업체에서 구운 EK ( *인증 키* ) 라고 하는 고유한 비대칭 키가 제공 됩니다. 이 키의 공개 부분을 *EKPub* 으로, 연결 된 개인 키를 *EKPriv*로 지칭 합니다. 일부 TPM 칩에는 또한는 EKPub에 대 한 제조업체에서 발급 된 EK 인증서가 있으며 *EKCert*로이 인증서를 참조 합니다.  
  
2.  CA는 EKPub 또는 EKCert을 통해 TPM에서 트러스트를 설정 합니다.  
  
3.  사용자는 인증서 요청 되는 RSA 키 암호화와 관련 되어 있다고는 EKPub는 EKpriv을 소유 하는 CA에 게 증명 합니다.  
  
4.  CA는 OID 나타내는 키를 TPM으로 보호 증명 된 이제는 특별 한 발급 정책을 사용 하 여 인증서를 발급 합니다.  
  
## <a name="deployment-overview"></a><a name="BKMK_DeploymentOverview"></a>배포 개요  
이 배포에서는 Windows Server 2012 R2 엔터프라이즈 CA가 설정 되어 있는지 가정 합니다. 또한 클라이언트 (Windows 8.1)는 인증서 템플릿을 사용 하 여 해당 엔터프라이즈 CA에 등록 하도록 구성 됩니다. 

TPM 키 증명을 배포 하는 방법은 세 가지 단계가 있습니다.  
  
1.  **TPM 트러스트 모델 계획:** 사용 하 여 TPM 트러스트 모델을 결정 하는 첫 번째 단계입니다. 이 위해 지원 되는 3 가지가 있습니다.  
  
    -   **사용자 자격 증명을 기반으로 하는 신뢰:** 엔터프라이즈 CA 인증서 요청의 일부로 사용자가 제공한 EKPub를 트러스트 하 고 유효성 검사는 수행 하지는 사용자의 도메인 자격 증명 이외의 합니다.  
  
    -   **EKCert를 기반으로 신뢰:** 엔터프라이즈 CA는 관리자가 관리 되는 목록에 대 한 인증서 요청의 일부로 제공 되는 EKCert 체인의 유효성을 검사 *허용 EK 인증서 체인*합니다. 허용 되는 체인은 제조업체 별로 정의 되며 발급 CA에서 두 개의 사용자 지정 인증서 저장소를 통해 표현 됩니다 (중간에 대해 하나의 저장소 및 루트 CA 인증서 용 저장소). 이 신뢰 모드 즉 **모든** 특정된 제조업체의 Tpm은 신뢰 합니다. 이 모드에서는 환경에서 사용 중인 Tpm이 포함 되도록 EKCerts 참고 합니다.
  
    -   **EKPub를 기반으로 신뢰:** 엔터프라이즈 CA는 관리자가 관리 되는 목록에 표시 된 인증서 요청의 일부로으로 제공 된 EKPub EKPubs 수 있는지 확인 합니다. 이 목록은이 디렉터리에 있는 각 파일의 이름이 허용된 EKPub의 sha-2 해시 인 파일의 디렉터리로 표현 됩니다. 이 옵션은 최고 보증 수준을 제공 하지만 각 장치를 개별적으로 식별 하기 때문에 더 많은 관리 작업이 필요 합니다. 이 신뢰 모델에서는 허용 되는 EKPubs 목록에 해당 TPM의 EKPub 추가 된 장치만 TPM 증명 된 인증서를 등록할 수 있습니다.  
  
    사용 되는 방법에 따라 CA는 발급 된 인증서에 다른 발급 정책 OID를 적용 합니다. 발급 정책 Oid에 대 한 자세한 내용은 발급 정책 Oid 표를 참조는 [인증서 템플릿 구성](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_ConfigCertTemplate) 섹션을이 참조 합니다.  
  
    TPM 트러스트 모델의 조합을 선택할 수 있다는 것을 참고 합니다. 이 경우 CA는 증명 메서드를 모두 수락 하 고 발급 정책 Oid는 성공 하는 모든 증명 메서드를 반영 합니다.  
  
2.  **인증서 템플릿을 구성:** 에 설명 된 인증서 템플릿을 구성의 [배포 세부 정보](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentDetails) 섹션을이 참조 합니다. 이 문서는 엔터프라이즈 CA에이 인증서 템플릿에 할당 되는 방법을 설명 하지 않거나 등록 하는 방법은 사용자의 그룹에 대 한 액세스 제공 됩니다. 자세한 내용은 참조 [검사 목록: 구성 Ca가 인증서 발급 및 관리](https://technet.microsoft.com/library/cc771533.aspx)합니다.  
  
3.  **TPM 트러스트 모델용 CA 구성**  
  
    1.  **사용자 자격 증명을 기반으로 하는 신뢰:** 특정 구성이 필요 하지 않습니다.  
  
    2.  **EKCert 기반 신뢰:** 관리자는 tpm 제조업체에서 EKCert 체인 인증서를 가져온 다음 TPM 키 증명을 수행 하는 CA에서 관리자가 만든 두 개의 새 인증서 저장소로 가져와야 합니다. 자세한 내용은 참조는 [CA 구성을](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) 섹션을이 참조 합니다.  
  
    3.  **EKPub를 기반으로 신뢰:** 관리자가 TPM 증명 된 인증서가 필요 하 EKPubs 허용된 목록에 추가할 각 장치에 대 한 EKPub를 얻어야 합니다. 자세한 내용은 참조는 [CA 구성을](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) 섹션을이 참조 합니다.  
  
    > [!NOTE]  
    > -   이 기능은 Windows 8.1/Windows Server 2012 r 2 필요로 합니다.  
    > -   TPM 키 증명 타사 스마트 카드 Ksp에 대 한 지원 되지 않습니다. Microsoft 플랫폼 암호화 공급자 KSP은 사용 해야 합니다.  
    > -   RSA 키에 대 한 TPM 키 증명 에서만 작동합니다.  
    > -   TPM 키 증명 독립 실행형 CA에 대 한 지원 되지 않습니다.  
    > -   TPM 키 증명을 지원 하지 않습니다 [비영구적 인증서 처리](https://technet.microsoft.com/library/ff934598)합니다.  
  
## <a name="deployment-details"></a><a name="BKMK_DeploymentDetails"></a>배포 세부 정보  
  
### <a name="configure-a-certificate-template"></a><a name="BKMK_ConfigCertTemplate"></a>인증서 템플릿 구성  
TPM 키 증명에 대 한 인증서 템플릿을 구성 하려면 다음 구성 단계를 수행 합니다.  
  
1.  **호환성** 탭  
  
    에 **호환성 설정** 섹션:  
  
    -   확인 **Windows Server 2012 R2** 에 대 한 선택은 **인증 기관**합니다.  
  
    -   확인 **Windows 8.1 / Windows Server 2012 R2** 에 대 한 선택은 **인증서 받는 사람**합니다.  
  
    ![TPM 키 증명](media/TPM-Key-Attestation/GTR_ADDS_CompatibilityTab.gif)  
  
2.  **암호화** 탭  
  
    확인 **키 저장소 공급자** 에 대해 선택한는 **공급자 범주** 및 **RSA** 에 대해 선택한는 **알고리즘 이름**합니다. **요청에서 다음 공급자 중 하나를 사용 해야** 하는지 확인 하 고 **공급자**아래에서 **Microsoft 플랫폼 암호화 공급자** 옵션을 선택 합니다.  
  
    ![TPM 키 증명](media/TPM-Key-Attestation/GTR_ADDS_CryptoTab.gif)  
  
3.  **키 증명** 탭  
  
    다음은 Windows Server 2012 r 2에 대 한 새 탭입니다.  
  
    ![TPM 키 증명](media/TPM-Key-Attestation/GTR_ADDS_ConfigCertTemplate.gif)  
  
    세 가지 가능한 옵션에서 증명 모드를 선택 합니다.  
  
    ![TPM 키 증명](media/TPM-Key-Attestation/GTR_ADDS_KeyModes.gif)  
  
    -   **None:** 키 증명 해야 사용 되지 않음을 의미 합니다.  
  
    -   **클라이언트를 사용할 수 있는 경우 필수:** TPM 키 증명을 지원 하지 않는 장치의 사용자가 해당 인증서를 계속 등록할 수 있도록 허용 합니다. 증명을 수행할 수 있는 사용자는 OID 특수 발급 정책으로 구분 됩니다. 일부 장치는 키 증명을 지원 하지 않는 이전 TPM 또는 TPM이 없는 장치에 대 한 증명을 수행 하지 못할 수 있습니다.
  
    -   **필수:** 클라이언트에서 TPM 키 증명을 수행 *해야* 합니다. 그렇지 않으면 인증서 요청이 실패 합니다.  
  
    TPM 트러스트 모델을 선택 합니다. 다음 세 가지 옵션이 있습니다.  
  
    ![TPM 키 증명](media/TPM-Key-Attestation/GTR_ADDS_KeyTypeToEnforce.gif)  
  
    -   **사용자 자격 증명:** 는 인증 사용자가 해당 도메인 자격 증명을 지정 하 여 유효한 TPM에 대 한 신뢰성을 보증 하도록 허용 합니다.  
  
    -   **보증 인증서:** The EKCert 장치 관리자에서 관리 되는 TPM 중간 CA 인증서 관리자에서 관리 하는 루트 CA 인증서를 통해 유효성을 검사 해야 합니다. EKCA 및 EKRoot를 설정 해야이 옵션을 선택 하는 경우에 설명 된 대로 인증서 발급 CA에는 저장소는  [CA 구성을](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) 섹션을이 참조 합니다.  
  
    -   **인증 키:** 장치의 EKPub는 PKI 관리자 관리 목록에 나타나야 합니다. 이 옵션은 가장 높은 보증 수준을 제공 하는 하지만 많은 노력이 필요 합니다. 에 설명 된 대로 EKPub 목록을 발급 ca를 설정 해야이 옵션을 선택 하는 경우는 [CA 구성을](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) 섹션을이 참조 합니다.  
  
    마지막으로, 발급된 된 인증서에 표시 하는 발급 정책을 결정 합니다. 기본적으로 각 적용 유형에는 다음 표에 설명 된 대로 해당 적용 유형을 통과 하는 경우 인증서에 삽입 되는 연결 된 OID (개체 식별자)가 있습니다. 적용 방법의 조합을 선택할 수 있다는 것을 참고 합니다. 이 경우 CA는 증명 메서드를 모두 수락 하 고 발급 정책 OID는 성공한 모든 증명 메서드를 반영 합니다.  
  
    **발급 정책 Oid**  
  
    |OID|키 증명 유형|설명|보증 수준|  
    |-------|------------------------|---------------|-------------------|  
    |1.3.6.1.4.1.311.21.30|EK|"EK Verified": EK의 목록은 관리자 관리|높음|  
    |1.3.6.1.4.1.311.21.31|보증 인증서|"EK 인증서 확인 됨": EK 인증서 체인의 유효성을 검사 하는 경우|중간|  
    |1.3.6.1.4.1.311.21.32|사용자 자격 증명|"EK 신뢰할 수 있는 사용 시": EK 사용자 입증에 대 한|낮음|  
  
    Oid 경우 발급된 된 인증서에 삽입 됩니다 **발급 정책 포함** 됩니다 (기본 구성)를 선택 합니다.  
  
    ![TPM 키 증명](media/TPM-Key-Attestation/GTR_ADDS_IssuancePolicies.gif)  
  
    > [!TIP]  
    > 인증서에 OID를 사용 하는 한 가지 잠재적인 사용은 특정 장치로 VPN 또는 무선 네트워킹에 대 한 액세스를 제한 하는 것입니다. 예를 들어 인증서에 OID 1.3.6.1.4.1.311.21.30가 있는 경우 액세스 정책에서 연결을 허용 하거나 다른 VLAN에 대 한 액세스를 허용할 수 있습니다. 이 옵션을 사용 하면 해당 TPM EK EKPUB 목록에는 장치에 대 한 액세스를 제한할 수 있습니다.  
  
### <a name="ca-configuration"></a><a name="BKMK_CAConfig"></a>CA 구성  
  
1.  **발급 CA에 EKCA 및 EKROOT 인증서 저장소 설정**  
  
    선택한 경우 **보증 인증서** 템플릿 설정에 대해 다음 구성 단계를 수행 합니다.  
  
    1.  TPM 키 증명을 수행 하는 인증 기관 (CA) 서버에 두 개의 새 인증서 저장소를 만들려면 Windows PowerShell을 사용 합니다.  
  
    2.  엔터프라이즈 환경에서 허용 하려는 제조업체에서 중간 및 루트 CA 인증서를 가져옵니다. 이러한 인증서는 이전에 만든 인증서 저장소 (EKCA 및 EKROOT)로 적절 하 게 가져와야 합니다.  
  
    다음 Windows PowerShell 스크립트는 두이 단계를 수행합니다. 다음 예제에서는 Fabrikam TPM 제조업체는 루트 인증서를 제공 했습니다 *FabrikamRoot.cer* 및 발급 CA 인증서 *Fabrikamca.cer*합니다.  
  
    ```powershell  
    PS C:>\cd cert:  
    PS Cert:\>cd .\\LocalMachine  
    PS Cert:\LocalMachine> new-item EKROOT  
    PS Cert:\ LocalMachine> new-item EKCA  
    PS Cert:\EKCA\copy FabrikamCa.cer .\EKCA  
    PS Cert:\EKROOT\copy FabrikamRoot.cer .\EKROOT  
    ```  
  
2.  **EK 증명 유형을 사용 하는 경우 Setup EKPUB List**  
  
    템플릿 설정에서 **인증 키** 를 선택한 경우 다음 구성 단계는 허용 되는 EK의 SHA-2 해시로 명명 된 0 바이트 파일을 포함 하 여 발급 CA에서 폴더를 만들고 구성 하는 것입니다. 이 폴더는 TPM 키-증명 된 인증서를 가져올 수 있는 장치의 "허용 목록"으로 사용 됩니다. Attested는 인증서가 필요한 각 장치에 대 한 EKPUB를 수동으로 추가 해야 하기 때문에 기업 TPM 키 증명 된 인증서를 얻을 수 있는 권한이 있는 장치를 보장 하는 것으로 제공 합니다. 이 모드에 대 한 CA를 구성 하려면 두 단계가 필요 합니다.  
  
    1.  **EndorsementKeyListDirectories 레지스트리 항목을 만듭니다.** Certutil 명령줄 도구를 사용 하 여 다음 표에 설명 된 대로 신뢰할 수 있는 EKpubs가 정의 된 폴더 위치를 구성 합니다.  
  
        |연산|명령 구문|  
        |-------------|------------------|  
        |폴더 위치를 추가 합니다.|certutil.exe-setreg CA\EndorsementKeyListDirectories + "<folder>"|  
        |폴더 위치를 제거 합니다.|certutil.exe-setreg CA\EndorsementKeyListDirectories-"<folder>"|  
  
        Certutil의 EndorsementKeyListDirectories 명령은 다음 표에 설명 된 대로 레지스트리 설정입니다.  
  
        |값 이름|형식|데이터|  
        |--------------|--------|--------|  
        |EndorsementKeyListDirectories|REG_MULTI_SZ|< EKPUB 로컬 또는 UNC 경로 목록을 허용 ><p>예:<p>*\\\blueCA.contoso.com\ekpub*<p>*\\\bluecluster1.contoso.com\ekpub*<p>D:\ekpub|  
  
        HKLM\SYSTEM\CurrentControlSet\Services\CertSvc\Configuration\\<CA Sanitized Name>  
  
        *EndorsementKeyListDirectories* 에는 CA에 대 한 읽기 액세스 권한이 있는 폴더를 가리키는 UNC 또는 로컬 파일 시스템 경로 목록이 포함 됩니다. 각 폴더에는 0 개 이상의 허용 목록 항목이 포함 될 수 있으며, 각 항목은 파일 확장명이 없는 신뢰할 수 있는 EKpub의 SHA-2 해시로 이름이 있는 파일입니다. 
        이 레지스트리 키 구성을 만들거나 편집 하려면 기존 CA 레지스트리 구성 설정과 마찬가지로 CA를 다시 시작 해야 합니다. 그러나 구성 설정에 대 한 편집 즉시 적용 됩니다 및 다시 시작 해야 하는 CA를 필요 하지 않습니다.  
  
        > [!IMPORTANT]  
        > 변조 목록에서 폴더를 보호 하 고 관리자 권한이 있는 있도록 권한을 구성 하 여 무단된 액세스에 대 한 읽기 및 쓰기 액세스 합니다. CA의 컴퓨터 계정에는 읽기 액세스만 필요 합니다.  
  
    2.  **EKPUB 목록을 채우는:** 각 장치에서 Windows PowerShell을 사용 하 여 TPM EK의 공개 키 해시를 가져오려면 다음 Windows PowerShell cmdlet을 사용 하 고 다음 보내고이 공용 CA에 대 한 해시를 키 EKPubList 폴더에 저장 합니다.  
  
        ```powershell  
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256  
        PS C:>$b=new-item $a.PublicKeyHash -ItemType file  
        ```  
  
## <a name="troubleshooting"></a>문제 해결  
  
### <a name="key-attestation-fields-are-unavailable-on-a-certificate-template"></a>키 증명 필드에서 사용할 수 없는 인증서 템플릿  
키 증명 필드 템플릿 설정 증명에 대 한 요구 사항을 충족 하지 않는 경우에 사용할 수 있습니다. 일반적인 원인은 다음과 같습니다.  
  
1.  호환성 설정은 올바르게 구성 되지 않습니다. 다음과 같이 구성 되어 있는지 확인 합니다.  
  
    1.  **인증 기관**: **Windows Server 2012 R2**  
  
    2.  **받는 사람 인증서**: **Windows 8.1 또는 Windows Server 2012 R2**  
  
2.  암호화 설정은 올바르게 구성 되지 않습니다. 다음과 같이 구성 되어 있는지 확인 합니다.  
  
    1.  **공급자 범주**: **키 저장소 공급자**  
  
    2.  **알고리즘 이름**: **RSA**  
  
    3.  **공급자**: **Microsoft 플랫폼 암호화 공급자**  
  
3.  요청 처리 설정이 올바르게 구성 되지 않습니다. 다음과 같이 구성 되어 있는지 확인 합니다.  
  
    1.  **프라이빗 키를 내보낼 수 있음** 옵션을 선택하지 않아야 합니다.  
  
    2.  **주체의 암호화 프라이빗 키를 보관할** 옵션을 선택하지 않아야 합니다.  
  
### <a name="verification-of-tpm-device-for-attestation"></a>TPM에 대 한 장치 증명 확인  
Windows PowerShell cmdlet을 사용 하 여 **확인 CAEndorsementKeyInfo**, Ca가 증명에 대해 신뢰할 수 있는 특정 TPM 장치 인지 확인 합니다. 두 가지 옵션이 있습니다: EKCert, 및는 EKPub 확인 하기 위한 기타 확인 하기 위한 하나입니다. Cmdlet은 실행 로컬로 또는 원격 Ca는 CA에서 Windows PowerShell 원격을 사용 하 여.  
  
1.  EKPub에 신뢰를 확인 하기 위한 다음 두 단계를 수행 합니다.  
  
    1.  **클라이언트 컴퓨터에서의 EKPub 추출:** The EKPub를 통해 클라이언트 컴퓨터에서 추출할 수 **Get TpmEndorsementKeyInfo**합니다. 상승된 된 명령 프롬프트에서 다음을 실행 합니다.  
  
        ```  
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256  
        ```  
  
    2.  **CA 컴퓨터에는 EKCert에 트러스트 확인:** 예를 들어 (전자 메일)를 통해 서버에 압축 푼된 문자열 (EKPub는 sha-2 해시)을 복사 하 고 확인 CAEndorsementKeyInfo cmdlet에 전달 합니다. 이 매개 변수 이름은 64 자 이어야 하는 참고 합니다.  
  
        ```  
        Confirm-CAEndorsementKeyInfo [-PublicKeyHash] <string>  
        ```  
  
2.  EKCert에 신뢰를 확인 하기 위한 다음 두 단계를 수행 합니다.  
  
    1.  **클라이언트 컴퓨터에서의 EKCert 추출:** The EKCert를 통해 클라이언트 컴퓨터에서 추출할 수 **Get TpmEndorsementKeyInfo**합니다. 상승된 된 명령 프롬프트에서 다음을 실행 합니다.  
  
        ```  
        PS C:>\$a=Get-TpmEndorsementKeyInfo
        PS C:>\$a.manufacturerCertificates|Export-Certificate -filepath c:\myEkcert.cer
        ```  
  
    2.  **CA 컴퓨터에서 EKCert에 대 한 트러스트 확인:** 추출 된 EKCert (EkCert)를 CA에 복사 합니다 (예: 전자 메일 또는 xcopy를 통해). 예를 들어, CA 서버에 인증서 파일의 "c:\diagnose" 폴더를 복사 하는 경우 확인을 완료 하려면 다음을 실행 합니다.  
  
        ```  
        PS C:>new-object System.Security.Cryptography.X509Certificates.X509Certificate2 "c:\diagnose\myEKcert.cer" | Confirm-CAEndorsementKeyInfo  
        ```  
  
## <a name="see-also"></a>관련 항목  
[신뢰할 수 있는 플랫폼 모듈 기술 개요](https://technet.microsoft.com/library/jj131725.aspx)  
[외부 리소스: 신뢰할 수 있는 플랫폼 모듈](http://www.cs.unh.edu/~it666/reading_list/Hardware/tpm_fundamentals.pdf)  
