---
title: 관리자-신뢰할 수 있는 증명에 대 한 호스트 정보를 추가 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 87089ebc-b953-4aa3-96b5-966cf91acb02
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 7949711dbb0f89f5404b491d60938985bfa98c22
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849464"
---
>적용 대상: Windows Server (반기 채널), Windows Server 2016

# <a name="authorize-hyper-v-hosts-using-admin-trusted-attestation"></a>관리자-신뢰할 수 있는 증명을 사용 하 여 Hyper-v 호스트를 권한 부여

>[!IMPORTANT]
>관리자-신뢰할 수 있는 증명 (AD 모드)는 Windows Server 2019로 시작 하는 사용 되지 않습니다. TPM 증명 수 없는 환경에 대 한 구성 [호스트 키 증명](guarded-fabric-initialize-hgs-key-mode.md)합니다. 호스트 키 증명 AD 모드에 유사한 보증을 제공 하며 간단 하 게 설정 합니다. 


AD 모드에서 보호 된 호스트에 권한을 부여 합니다. 

1. Fabric 도메인에서 보안 그룹에 Hyper-v 호스트를 추가 합니다.
2. HGS 도메인에서 HGS를 사용 하 여 보안 그룹의 SID를 등록 합니다. 

## <a name="add-the-hyper-v-host-to-a-security-group-and-reboot-the-host"></a>보안 그룹에 Hyper-v 호스트를 추가 하 고 호스트를 다시 부팅

1. 만들기는 **GLOBAL** 보안 fabric 도메인의 그룹 및 보호 된 Vm을 실행 하는 Hyper-v 호스트를 추가 합니다. 
   해당 그룹 멤버 자격을 업데이트할 호스트를 다시 시작 합니다.

2. Get-ADGroup를 사용 하 여 보안 그룹의 보안 식별자 (SID)를 가져올를 HGS 관리자에 게 제공 합니다. 

   ```powershell
   Get-ADGroup "Guarded Hosts"
   ```

   ![출력을 사용 하 여 get AdGroup 명령](../media/Guarded-Fabric-Shielded-VM/guarded-host-get-adgroup.png)

## <a name="register-the-sid-of-the-security-group-with-hgs"></a>보안 그룹의 SID를 HGS에 등록  

1. 패브릭 관리자에서 보호 된 호스트에 대 한 보안 그룹의 SID를 가져오고 HGS를 사용 하 여 보안 그룹을 등록 하려면 다음 명령을 실행 합니다. 
   추가 그룹에 대해 필요한 경우 명령을 다시 실행 합니다. 
   그룹의 이름을 제공 합니다. 
   Active Directory 보안 그룹 이름과 일치 하지 않아도 됩니다. 

   ```powershell
   Add-HgsAttestationHostGroup -Name "<GuardedHostGroup>" -Identifier "<SID>"
   ```

2. 추가 된 그룹을 확인 하려면 [Get HgsAttestationHostGroup](https://technet.microsoft.com/library/mt652172.aspx)합니다. 


