---
title: 배스 천 포리스트의 키 모드를 사용 하 여 HGS 클러스터를 초기화 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: e785ee17bf68c07d965816480baa0d59062fc434
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447422"
---
# <a name="initialize-the-hgs-cluster-using-key-mode-in-an-existing-bastion-forest"></a>키 모드를 사용 하 여 기존 배스 천 포리스트의 HGS 클러스터를 초기화 합니다.

> 적용 대상: Windows Server 2019
> 
> [!div class="step-by-step"]
> [«HGS 새 포리스트 설치](guarded-fabric-install-hgs-in-a-bastion-forest.md)
> [호스트 키 만들기»](guarded-fabric-create-host-key.md)

Active Directory Domain Services가 컴퓨터에 설치 되지만 구성 되지 않은 상태로 유지 해야 합니다.

[!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)] 

계속 하기 전에 호스트 보호 서비스에 대 한 클러스터 개체를 사전 준비 된 하 고 로그온 한 사용자에 부여 했는지 확인 **전면적인** Active Directory에서 VCO 및 CNO 개체입니다.
가상 컴퓨터 개체 이름에 전달 해야 합니다 `-HgsServiceName` 매개 변수 및 클러스터 이름을 `-ClusterName` 매개 변수입니다.

> [!TIP]
> 이중 확인 AD 도메인 컨트롤러가 클러스터 개체를 확인 하려면 계속 하기 전에 모든 Dc에 복제 않았습니다.

PFX 기반 인증서를 사용 하는 경우에 HGS 서버에 다음 명령을 실행 합니다.

```powershell
$signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
$encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

Install-ADServiceAccount -Identity 'HGSgMSA'

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -ClusterName 'HgsCluster' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustHostKey
```

(예: HSM 지원 인증서 및 인증서를 내보낼 수 없는) 로컬 컴퓨터에 설치 된 인증서를 사용 하는 경우 사용 합니다 `-SigningCertificateThumbprint` 및 `-EncryptionCertificateThumbprint` 매개 변수 대신 합니다.

