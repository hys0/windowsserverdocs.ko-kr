---
title: 관리자가 신뢰할 수 있는 증명에 대 한 호스트 정보 추가
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 87089ebc-b953-4aa3-96b5-966cf91acb02
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 946f91d05063475ae45fb334c67f8d5081d3984d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403720"
---
>적용 대상: Windows Server(반기 채널), Windows Server 2016

# <a name="authorize-hyper-v-hosts-using-admin-trusted-attestation"></a>관리자가 신뢰할 수 있는 증명을 사용 하 여 Hyper-v 호스트에 권한 부여

>[!IMPORTANT]
>관리자가 신뢰할 수 있는 증명 (AD 모드)은 Windows Server 2019부터 사용 되지 않습니다. TPM 증명을 사용할 수 없는 환경의 경우 [호스트 키 증명](guarded-fabric-initialize-hgs-key-mode.md)을 구성 합니다. 호스트 키 증명은 AD 모드와 비슷한 보증을 제공 하 고 설정 하는 것이 더 간단 합니다. 


AD 모드에서 보호 된 호스트에 권한을 부여 하려면: 

1. 패브릭 도메인에서 보안 그룹에 Hyper-v 호스트를 추가 합니다.
2. HGS 도메인에서 보안 그룹의 SID를 HGS에 등록 합니다. 

## <a name="add-the-hyper-v-host-to-a-security-group-and-reboot-the-host"></a>Hyper-v 호스트를 보안 그룹에 추가 하 고 호스트를 다시 부팅 합니다.

1. 패브릭 도메인에서 **전역** 보안 그룹을 만들고 보호 된 vm을 실행할 hyper-v 호스트를 추가 합니다. 
   호스트를 다시 시작 하 여 그룹 멤버 자격을 업데이트 합니다.

2. New-adgroup를 사용 하 여 보안 그룹의 SID (보안 식별자)를 가져오고이를 HGS 관리자에 게 제공 합니다. 

   ```powershell
   Get-ADGroup "Guarded Hosts"
   ```

   ![출력을 포함 하는 New-adgroup 명령](../media/Guarded-Fabric-Shielded-VM/guarded-host-get-adgroup.png)

## <a name="register-the-sid-of-the-security-group-with-hgs"></a>HGS를 사용 하 여 보안 그룹의 SID 등록  

1. 패브릭 관리자에서 보호 된 호스트에 대 한 보안 그룹의 SID를 가져오고 다음 명령을 실행 하 여 HGS에 보안 그룹을 등록 합니다. 
   추가 그룹에 필요한 경우 명령을 다시 실행 합니다. 
   그룹에 대 한 친숙 한 이름을 입력 합니다. 
   Active Directory 보안 그룹 이름과 일치할 필요는 없습니다. 

   ```powershell
   Add-HgsAttestationHostGroup -Name "<GuardedHostGroup>" -Identifier "<SID>"
   ```

2. 그룹이 추가 되었는지 확인 하려면 [HgsAttestationHostGroup](https://technet.microsoft.com/library/mt652172.aspx)를 실행 합니다. 


