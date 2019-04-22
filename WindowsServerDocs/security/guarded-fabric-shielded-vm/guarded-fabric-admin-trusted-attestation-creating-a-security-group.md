---
title: 보호 된 호스트에 대 한 보안 그룹을 만들고 그룹 HGS 등록
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: a12c8494-388c-4523-8d70-df9400bbc2c0
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: ba547dff862a283b68ff105a14b14ed367891745
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816344"
---
# <a name="create-a-security-group-for-guarded-hosts-and-register-the-group-with-hgs"></a>보호 된 호스트에 대 한 보안 그룹을 만들고 그룹 HGS 등록

>적용 대상: Windows Server (반기 채널), Windows Server 2016

>[!IMPORTANT]
>AD 모드는 Windows Server 2019로 시작 하는 사용 되지 않습니다. TPM 증명 수 없는 환경에 대 한 구성 [호스트 키 증명](guarded-fabric-initialize-hgs-key-mode.md)합니다. 호스트 키 증명 AD 모드에 유사한 보증을 제공 하며 간단 하 게 설정 합니다. 


이 항목에서는 관리자-신뢰할 수 있는 증명 (AD 모드)를 사용 하 여 보호 된 호스트를 Hyper-v 호스트를 준비 하는 중간 단계를 설명 합니다. 이 단계를 수행 하기 전에 단계를 완료 [보호 된 호스트 될 호스트에 대 한 DNS 패브릭 구성](guarded-fabric-configuring-fabric-dns-ad.md)합니다.


## <a name="create-a-security-group-and-add-hosts"></a>보안 그룹을 만들고 호스트를 추가 합니다.

1. 새 **GLOBAL** 보안 fabric 도메인의 그룹 및 보호 된 Vm을 실행 하는 Hyper-v 호스트를 추가 합니다. 해당 그룹 멤버 자격을 업데이트할 호스트를 다시 시작 합니다.

2. Get-ADGroup를 사용 하 여 보안 그룹의 보안 식별자 (SID)를 가져올를 HGS 관리자에 게 제공 합니다. 

    ```powershell
    Get-ADGroup "Guarded Hosts"
    ```

    ![출력을 사용 하 여 get AdGroup 명령](../media/Guarded-Fabric-Shielded-VM/guarded-host-get-adgroup.png)

## <a name="register-the-sid-of-the-security-group-with-hgs"></a>보안 그룹의 SID를 HGS에 등록  

1. HGS 서버에서 HGS를 사용 하 여 보안 그룹을 등록 하려면 다음 명령을 실행 합니다. 
   추가 그룹에 대해 필요한 경우 명령을 다시 실행 합니다. 
   그룹의 이름을 제공 합니다. 
   Active Directory 보안 그룹 이름과 일치 하지 않아도 됩니다. 

   ```powershell
   Add-HgsAttestationHostGroup -Name "<GuardedHostGroup>" -Identifier "<SID>"
   ```

2. 추가 된 그룹을 확인 하려면 [Get HgsAttestationHostGroup](https://technet.microsoft.com/library/mt652172.aspx)합니다. 

## <a name="next-step"></a>다음 단계

>[!div class="nextstepaction"]
[증명 확인](guarded-fabric-confirm-hosts-can-attest-successfully.md)


## <a name="see-also"></a>참조

- [보호 된 호스트 및 차폐 Vm에 대 한 호스트 보호 서비스 배포](guarded-fabric-deploying-hgs-overview.md)
