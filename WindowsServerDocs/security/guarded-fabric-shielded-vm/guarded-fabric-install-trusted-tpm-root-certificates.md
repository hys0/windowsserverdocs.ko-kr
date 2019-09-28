---
title: 신뢰할 수 있는 TPM 루트 인증서 설치
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 06/27/2019
ms.openlocfilehash: 15614ce1065170bc557fad10a168b3dda6a5b05a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386554"
---
# <a name="install-trusted-tpm-root-certificates"></a>신뢰할 수 있는 TPM 루트 인증서 설치

>적용 대상: Windows server 2019, Windows Server (반기 채널), Windows Server 2016

TPM 증명을 사용 하도록 HGS를 구성 하는 경우 서버에서 Tpm 공급 업체를 신뢰 하도록 HGS를 구성 해야 합니다.
이 추가 확인 프로세스를 통해 인증 된 신뢰할 수 있는 Tpm만 HGS로 증명할 수 있습니다.
@No__t-0을 사용 하 여 신뢰할 수 없는 TPM을 등록 하려고 하면 TPM 공급 업체를 신뢰할 수 없다는 오류가 표시 됩니다.

Tpm을 신뢰 하려면 서버 Tpm의 인증 키에 서명 하는 데 사용 되는 루트 및 중간 서명 인증서를 HGS에 설치 해야 합니다.
데이터 센터에서 TPM 모델을 둘 이상 사용 하는 경우 각 모델에 대해 서로 다른 인증서를 설치 해야 할 수 있습니다.
HGS는 공급 업체 인증서에 대 한 "TrustedTPM_RootCA" 및 "TrustedTPM_IntermediateCA" 인증서 저장소를 확인 합니다.

> [!NOTE]
> TPM 공급 업체 인증서는 기본적으로 Windows에 설치 된 인증서와 다르며 TPM 공급 업체에서 사용 하는 특정 루트 및 중간 인증서를 나타냅니다.

사용자 편의를 위해 신뢰할 수 있는 TPM 루트 및 중간 인증서 컬렉션은 Microsoft에서 게시 합니다.
아래 단계를 사용 하 여 이러한 인증서를 설치할 수 있습니다.
아래 패키지에 TPM 인증서가 포함 되지 않은 경우 tpm 공급 업체 또는 서버 OEM에 문의 하 여 특정 TPM 모델에 대 한 루트 및 중간 인증서를 가져옵니다.

**모든 HGS 서버**에서 다음 단계를 반복 합니다.

1.  [@No__t-1](https://go.microsoft.com/fwlink/?linkid=2097925)에서 최신 패키지를 다운로드 합니다.

2.  Cab 파일의 서명을 확인 하 여 정품 인증을 확인 하십시오. 서명이 유효 하지 않은 경우에는 진행 하지 마십시오.

    ```powershell
    Get-AuthenticodeSignature .\TrustedTpm.cab
    ```
    
    다음은 몇 가지 출력 예제입니다.
    
    ```
    Directory: C:\Users\Administrator\Downloads
        
    SignerCertificate                         Status                                 Path
    -----------------                         ------                                 ----
    0DD6D4D4F46C0C7C2671962C4D361D607E370940  Valid                                  TrustedTpm.cab
    ```

2.  Cab 파일을 확장 합니다.

    ```
    mkdir .\TrustedTPM
    expand.exe -F:* <Path-To-TrustedTpm.cab> .\TrustedTPM
    ```

3.  기본적으로 구성 스크립트는 모든 TPM 공급 업체에 대 한 인증서를 설치 합니다. 특정 TPM 공급 업체에 대 한 인증서를 가져오려면 조직에서 신뢰 하지 않는 TPM 공급 업체에 대 한 폴더를 삭제 합니다.

4.  확장 된 폴더에서 설치 스크립트를 실행 하 여 신뢰할 수 있는 인증서 패키지를 설치 합니다.

    ```
    cd .\TrustedTPM
    .\setup.cmd
    ```

이전 설치 중에 새 인증서 또는 의도적으로 건너뛴 인증서를 추가 하려면 HGS 클러스터의 모든 노드에서 위의 단계를 반복 하면 됩니다.
기존 인증서는 신뢰할 수 있는 상태로 유지 되지만 확장 된 cab 파일에 있는 새 인증서는 신뢰할 수 있는 TPM 저장소에 추가 됩니다.

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [패브릭 DNS 구성](guarded-fabric-configuring-fabric-dns-tpm.md)



