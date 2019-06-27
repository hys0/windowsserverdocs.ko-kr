---
title: 신뢰할 수 있는 TPM 루트 인증서를 설치 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 06/21/2019
ms.openlocfilehash: 211d2f24b01d1e308f012df681f9e16a2190449f
ms.sourcegitcommit: 260b1d78cb28b88b876579e1ac9a41a74e8752fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2019
ms.locfileid: "67398807"
---
# <a name="install-trusted-tpm-root-certificates"></a>신뢰할 수 있는 TPM 루트 인증서를 설치 합니다.

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

TPM 증명을 사용 하도록 HGS를 구성한 경우 또한 HGS 서버에 Tpm의 공급 업체를 신뢰 하도록 구성 해야 합니다.
추가 인증 하면 인증, 신뢰할 수 있는 Tpm만 HGS를 사용 하 여 증명할 수 있습니다.
사용 하 여 신뢰할 수 없는 TPM 등록 하려는 경우 `Add-HgsAttestationTpmHost`, TPM 공급 업체를 신뢰할 수 있는 아님을 나타내는 오류가 표시 됩니다.

에 Tpm를 신뢰 하려면 루트 및 서버 Tpm 인증 키를 로그인 하는 데 사용 되는 중간 서명 인증서를 HGS에 설치 해야 합니다.
데이터 센터에 둘 이상의 TPM 모델을 사용 하는 경우 각 모델에 대 한 다른 인증서를 설치 해야 합니다.
HGS에서 "TrustedTPM_RootCA"와 "TrustedTPM_IntermediateCA" 인증서 저장소 공급 업체 인증서에 대 한 합니다.

> [!NOTE]
> TPM 공급 업체 인증서를 Windows에 기본적으로 설치 하는 것과 다른 되며 특정 루트 및 TPM 공급 업체에 의해 사용 되는 중간 인증서를 나타냅니다.

신뢰할 수 있는 TPM 루트 및 중간 인증서의 컬렉션은 사용자 편의 위해 Microsoft에서 게시 됩니다.
이러한 인증서를 설치 하려면 다음 단계를 사용할 수 있습니다.
TPM 인증서 아래 패키지에 포함 되지 않은, 경우에 TPM 공급 업체 또는 OEM 서버 루트와 특정 TPM 모델에 대 한 중간 인증서를 가져오려면에 문의 합니다.

다음 단계를 반복 **모든 HGS 서버**:

1.  최신 패키지를 다운로드 [ https://tpmsec.microsoft.com/TPMCerts/TrustedTPM.cab ](https://tpmsec.microsoft.com/TPMCerts/TrustedTPM.cab)합니다.

2.  Cab 파일을 확장 합니다.

    ```
    mkdir .\TrustedTPM
    expand.exe -F:* <Path-To-TrustedTpm.cab> .\TrustedTPM
    ```

3.  구성 스크립트는 기본적으로 모든 TPM 공급 업체에 대 한 인증서 설치 됩니다. 특정 TPM 공급 업체에 대 한 인증서를 가져올 하려는 경우 조직에서 신뢰할 수 없는 TPM 공급 업체 폴더를 삭제 합니다.

4.  확장 된 폴더에서 설치 스크립트를 실행 하 여 신뢰할 수 있는 인증서 패키지를 설치 합니다.

    ```
    cd .\TrustedTPM
    .\setup.cmd
    ```

새 인증서 또는 이전 설치를 의도적으로 건너뛰었습니다 추가할 HGS 클러스터의 모든 노드에 대해 위의 단계를 반복 하면 됩니다.
기존 인증서 신뢰할 수 있는 상태로 유지 되지만 신뢰할 수 있는 TPM에 추가할 확장 된 cab 파일에 새 인증서를 저장 합니다.

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [패브릭 DNS 구성](guarded-fabric-configuring-fabric-dns-tpm.md)



