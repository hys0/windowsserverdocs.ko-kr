---
title: 보호 된 호스트에 대 한 보안 그룹을 만들고 HGS로 그룹 등록
ms.prod: windows-server
ms.topic: article
ms.assetid: a12c8494-388c-4523-8d70-df9400bbc2c0
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 84bf134ac5224f224339cc1ec216bded8cbcc792
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475680"
---
# <a name="create-a-security-group-for-guarded-hosts-and-register-the-group-with-hgs"></a>보호 된 호스트에 대 한 보안 그룹을 만들고 HGS로 그룹 등록

> 적용 대상: Windows Server(반기 채널), Windows Server 2016

> [!IMPORTANT]
> AD 모드는 Windows Server 2019부터 사용 되지 않습니다. TPM 증명을 사용할 수 없는 환경의 경우 [호스트 키 증명](guarded-fabric-initialize-hgs-key-mode.md)을 구성 합니다. 호스트 키 증명은 AD 모드와 비슷한 보증을 제공 하 고 설정 하는 것이 더 간단 합니다.

이 항목에서는 관리자가 신뢰할 수 있는 증명 (AD 모드)을 사용 하 여 보호 된 호스트가 되도록 Hyper-v 호스트를 준비 하는 중간 단계에 대해 설명 합니다. 이러한 단계를 수행 하기 전에 [보호 된 호스트가 될 호스트에 대 한 패브릭 DNS 구성](guarded-fabric-configuring-fabric-dns-ad.md)의 단계를 완료 합니다.


## <a name="create-a-security-group-and-add-hosts"></a>보안 그룹을 만들고 호스트 추가

1. 패브릭 도메인에 새 **글로벌** 보안 그룹을 만들고 보호 된 vm을 실행할 hyper-v 호스트를 추가 합니다. 호스트를 다시 시작 하 여 그룹 멤버 자격을 업데이트 합니다.

2. New-adgroup를 사용 하 여 보안 그룹의 SID (보안 식별자)를 가져오고이를 HGS 관리자에 게 제공 합니다.

    ```powershell
    Get-ADGroup "Guarded Hosts"
    ```

    ![출력을 포함 하는 New-adgroup 명령](../media/Guarded-Fabric-Shielded-VM/guarded-host-get-adgroup.png)

## <a name="register-the-sid-of-the-security-group-with-hgs"></a>HGS를 사용 하 여 보안 그룹의 SID 등록

1. HGS 서버에서 다음 명령을 실행 하 여 HGS로 보안 그룹을 등록 합니다.
   추가 그룹에 필요한 경우 명령을 다시 실행 합니다.
   그룹에 대 한 친숙 한 이름을 입력 합니다.
   Active Directory 보안 그룹 이름과 일치할 필요는 없습니다.

   ```powershell
   Add-HgsAttestationHostGroup -Name "<GuardedHostGroup>" -Identifier "<SID>"
   ```

2. 그룹이 추가 되었는지 확인 하려면 [HgsAttestationHostGroup](https://technet.microsoft.com/library/mt652172.aspx)를 실행 합니다.

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [증명 확인](guarded-fabric-confirm-hosts-can-attest-successfully.md)


## <a name="additional-references"></a>추가 참조

- [보호된 호스트 및 보호된 VM에 대해 호스트 보호 서비스 배포](guarded-fabric-deploying-hgs-overview.md)
