---
title: AD DS(Active Directory Domain Services)를 안전하게 가상화
description: Active Directory의 USN 롤백 및 안전한 가상화
ms.topic: article
ms.prod: windows-server
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 03/22/2019
ms.technology: identity-adds
ms.assetid: 7a3114c8-bda8-49bb-83a8-4e04340ab221
ms.openlocfilehash: 67e35a47467b1f5f66bfd073c6f9db06094ea3f9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71391032"
---
# <a name="safely-virtualizing-active-directory-domain-services-ad-ds"></a>AD DS(Active Directory Domain Services)를 안전하게 가상화

>적용 대상: Windows Server

Windows Server 2012부터 AD DS는 가상화 안전 기능을 도입하여 도메인 컨트롤러를 가상화하기 위한 뛰어난 지원 기능을 제공합니다. 이 문서에서는 도메인 컨트롤러 복제에서 USNs 및 InvocationIDs의 역할을 설명하고 발생 가능한 몇 가지 문제에 대해 설명합니다.

## <a name="update-sequence-number-and-invocationid"></a>시퀀스 번호 및 InvocationID 업데이트

가상 환경에는 논리적 클록 기반 복제 스키마에 종속된 분산 워크로드와 관련된 고유한 해결 과제가 있습니다. 예를 들어 AD DS 복제에서는 각 도메인 컨트롤러의 트랜잭션에 할당된 일정하게 증가하는 값(USN 또는 업데이트 시퀀스 번호라고 함)을 사용합니다. 각 도메인 컨트롤러의 데이터베이스 인스턴스에 invocationid 라는 id가 지정 됩니다. 도메인 컨트롤러의 InvocationID는 해당 USN과 함께 각 도메인 컨트롤러에서 수행되는 모든 쓰기 트랜잭션과 관련된 고유 식별자의 역할을 하므로 포리스트 내에서 고유해야 합니다.

AD DS 복제에서는 각 도메인 컨트롤러에서 InvocationID 및 USN을 사용하여 다른 도메인 컨트롤러에 복제해야 하는 변경 내용을 확인합니다. 도메인 컨트롤러에서 도메인 컨트롤러의 인식 시간에 롤백되고 USN이 완전히 다른 트랜잭션에 다시 사용 됩니다, 다른 도메인 컨트롤러가 해당 InvocationID의 컨텍스트에서 재사용된 USN와 관련 된 업데이트 이미 받은 생각 됩니다 때문에 복제는 수렴 되지 않습니다.

예를 들어 다음 그림에서는 VDC2, 즉 가상 컴퓨터에서 실행되는 대상 도메인 컨트롤러에서 USN 롤백이 감지된 경우 Windows Server 2008 R2 이하 운영 체제에서 발생하는 이벤트의 순서를 보여 줍니다. 이 그림에서는 VDC2 VDC2의 데이터베이스에 롤백되는 시간에 부적절 하 게 나타내는 복제 파트너에 게 이전에 표시 하는 최신 USN 값을 전송한는 복제 파트너를 감지할 때 VDC2에서 USN 롤백이 감지 발생 합니다.

![USN 롤백이 감지될 때의 이벤트 순서](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_Exampleofhowreplicationcanbecomeinconsistent.png)

가상 컴퓨터 (VM) 쉽게 롤백할 수는 도메인 컨트롤러의 Usn (논리적 클록), 여 하이퍼바이저 관리자에 대 한 예를 들어, 도메인 컨트롤러의 인식 스냅샷을 적용 합니다. USN 및 USN 하는 방법에 대 한 자세한 내용은 롤백, USN 롤백이 감지 되지 않은 인스턴스를 설명 하기 위해 다른 그림을 포함 하 여 참조 [USN 및 USN 롤백](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(WS.10).aspx#usn_and_usn_rollback)합니다.

Windows Server 2012부터, Vm-generation ID 라는 식별자를 노출하는 하이퍼바이저 플랫폼에서 호스트 되는 AD DS 가상 도메인 컨트롤러 수 감지 하고 적용할 롤백되는 경우 가상 머신은 시간에 VM 스냅샷의 애플리케이션에서 AD DS 환경을 보호하는데 필요한 안전 조치합니다. VM-생성 ID 설계에서는 하이퍼바이저 공급업체에 독립적인 메커니즘을 사용하여 이 식별자를 게스트 가상 컴퓨터의 주소 공간에 표시하므로 VM-생성 ID를 지원하는 모든 하이퍼바이저에서 안전한 가상화 환경을 일관되게 사용할 수 있습니다. 가상 컴퓨터 내에서 실행되는 서비스 및 응용 프로그램을 통해 이 식별자를 샘플링하여 가상 컴퓨터가 제시간에 롤백되었는지 감지할 수 있습니다.

## <a name="effects-of-usn-rollback"></a>USN 롤백 효과

USN 롤백이 발생할 때 개체 및 속성에 대한 수정 사항은 USN에서 이전에 확인된 대상 도메인 컨트롤러에 의해 복제된 것으로 바인딩되지 않습니다.

이러한 대상 도메인 컨트롤러는 최신 상태로 간주되기 때문에 디렉터리 서비스 이벤트 로그에 또는 모니터링 및 진단 도구에 의해 복제 오류가 보고되지 않습니다.

USN 롤백은 모든 패턴에 있는 모든 개체 또는 속성의 복제에 영향을 줄 수 있습니다. 가장 자주 발견되는 부작용은 롤백 도메인 컨트롤러에 생성된 사용자 계정 및 컴퓨터 계정이 하나 이상의 복제 파트너에 존재하지 않는 것입니다. 또는 롤백 도메인 컨트롤러에서 시작된 암호 업데이트가 복제 파트너에 존재하지 않을 수 있습니다.

USN 롤백은 모든 Active Directory 파티션에 있는 어떠한 개체 유형도 복제되지 않도록 방지할 수 있습니다. 이러한 개체 유형에는 다음이 포함됩니다.

* Active Directory 복제 토폴로지 및 일정
* 포리스트에 있는 도메인 컨트롤러의 존재 유무 및 이러한 도메인 컨트롤러에 지정된 역할
* 포리스트에 있는 도메인 및 애플리케이션 파티션의 존재 유무
* 보안 그룹의 존재 유무 및 보안 그룹의 현재 그룹 멤버십
* Active Directory 통합 DNS 영역에 있는 DNS 레코드 등록

USN 구멍 크기는 사용자, 컴퓨터, 트러스트 및 보안 그룹에 대한 수백, 수천 또는 수만 개의 변경 사항을 나타낼 수 있습니다. USN 구멍은 복원된 시스템 상태 백업이 생성되었을 때 존재하던 가장 높은 USN 번호와 오프라인으로 전환되기 전 롤백된 도메인 컨트롤러에서 생성되었던 원래 변경 사항 수 사이의 차이로 정의됩니다.

## <a name="detecting-a-usn-rollback"></a>USN 롤백 감지

USN 롤백은 감지하기 어렵기 때문에 호출 ID에 포함된 해당 변경 사항 없이 소스 도메인 컨트롤러가 대상 도메인 컨트롤러에 이전에 인식된 USN 번호를 전송할 때 도메인 컨트롤러가 이벤트 2095를 기록합니다.

Active Directory에 대한 고유한 원래 업데이트가 잘못 복원된 도메인 컨트롤러에서 생성되지 않도록 방지하기 위해 Net Logon 서비스가 일시 중지됩니다. Net Logon 서비스가 일시 중지되면 사용자 및 컴퓨터 계정이 그러한 변경 사항을 와부에 복제하지 않는 도메인 컨트롤러에서 암호를 변경할 수 없습니다. 마찬가지로 Active Directory 관리 도구는 Active Directory에서 개체를 업데이트할 때 상태가 양호한 도메인 컨트롤러를 선호합니다.

도메인 컨트롤러에서 다음 조건이 일치하면 다음과 비슷한 이벤트 메시지가 기록됩니다.

* 소스 도메인 컨트롤러는 이전에 인식된 USN 번호를 대상 도메인 컨트롤러로 전송합니다.
* 호출 ID에는 해당 변경 사항이 없습니다.

이러한 이벤트는 Directory Service 이벤트 로그에서 캡처될 수 있습니다. 하지만 관리자에 의해 관측되기 전에 겹쳐 쓰여질 수 있습니다.

USN 롤백이 발생했다고 의심되지만, 이벤트 로그에서 해당 이벤트를 찾을 수 없으면 레지스트리에서 DSA Not Writable 항목을 확인하세요. 이 항목은 USN 롤백이 발생했음을 보여주는 포렌식 증거를 제공합니다.

```
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\NTDS\Parameters
Registry entry: Dsa Not Writable
Value: 0x4
```

> [!WARNING]
> Dsa Not Writable 레지스트리 항목 값을 삭제하거나 수동으로 변경하면 롤백 도메인 컨트롤러가 영구적으로 지원되지 않는 상태가 됩니다. 따라서 이러한 변경은 지원되지 않습니다. 특히 값을 수정하면 USN 롤백 검색 코드로 추가되는 격리 행동이 제거됩니다. 롤백 도메인 컨트롤러의 Active Directory 파티션은 동일한 Active Directory 포리스트에 있는 직접 및 임시 복제 파트너와 영구적으로 일치하지 않습니다.

이 레지스트리 키 및 해결 단계에 대한 자세한 내용은 지원 문서 [Active Directory 복제 오류 8456 또는 8457: "원본 | 대상 서버가 현재 복제 요청을 거부함"](https://support.microsoft.com/help/2023007/active-directory-replication-error-8456-or-8457-the-source-destination)을 참조하세요.

## <a name="virtualization-based-safeguards"></a>가상화 기반 보안

도메인 컨트롤러를 설치 하는 동안 AD DS 도메인 컨트롤러의 컴퓨터 개체 (디렉터리 정보 트리 또는 DIT 라고도 함)는 데이터베이스에 대 한 Msds-generationid 특성의 일부로 VM 생성 Id 식별자 처음 저장 합니다. VM 생성 ID는 가상 컴퓨터 내 Windows 드라이버를 통해 독립적으로 추적됩니다.

관리자가 이전 스냅샷에서 가상 머신을 복원하면 가상 머신 드라이버의 현재 VM 생성 ID 값이 DIT의 값과 비교됩니다.

두 값이 다르면 invocationID가 다시 설정되고 RID 풀이 삭제되므로 USN을 다시 사용할 수 없습니다. 값이 같으면 트랜잭션이 정상적으로 커밋됩니다.

또한 AD DS에서는 도메인 컨트롤러가 다시 부팅될 때마다 가상 머신의 현재 VM 생성 ID 값을 DIT의 값과 비교하며, 값이 다른 경우 invocationID를 다시 설정하고, RID 풀을 삭제하고, DIT를 새 값으로 업데이트합니다. 뿐만 아니라 안전한 복원을 완료하기 위해 SYSVOL 폴더를 비정식으로 동기화합니다. 이를 통해 종료된 VM에서의 스냅샷 적용으로 보호 기능을 확장할 수 있습니다. Windows Server 2012에 도입 된 이러한 보호 기능 배포 및 관리 가상화 된 환경에서 도메인 컨트롤러의 고유한 이점을 제대로 활용 하려면 AD DS 관리자를 사용 합니다.

다음 그림은 VM-GenerationID를 지원하는 하이퍼바이저에서 Windows Server 2012를 실행하는 가상화된 도메인 컨트롤러에서 동일한 USN 롤백이 검색될 때 가상화 보안이 적용되는 방법을 보여줍니다.

![동일한 USN 롤백이 검색되었을 때 적용되는 보안](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_VDC_Exampleofhowsafeguardswork.gif)

이 예에서 하이퍼바이저가 VM-생성 ID 값의 변경을 감지한 경우, 가상화 DC(이전 예의 A~B)에 대한 InvocationID를 다시 설정하고, 하이퍼바이저에서 저장한 새 값(G2)과 일치하도록 VM에 저장된 VM-생성 ID 값을 업데이트하는 등 가상화 보호 기능이 트리거됩니다. 이러한 보호 기능은 두 도메인 컨트롤러 모두에 대해 복제가 수렴되도록 합니다.

Windows Server 2012에서 AD DS는 VM-GenerationID 인식 하이퍼바이저에서 호스팅되는 가상 도메인 컨트롤러에 보안을 적용하고 실수로 인한 스냅샷 적용 또는 가상 머신 상태를 롤백할 수 있는 이러한 하이퍼바이저 지원 메커니즘이 AD DS 환경을 중단하지 않도록 합니다(USN 버블 또는 느린 개체와 같은 복제 문제 방지).

그러나 가상 머신 스냅샷을 적용하여 도메인 컨트롤러를 복원하는 것은 도메인 컨트롤러 백업의 대체 메커니즘으로 권장되지 않습니다. Windows Server 백업 또는 기타 VSS 기록기 기반 백업 솔루션을 계속 사용하는 것이 좋습니다.

> [!CAUTION]
> 프로덕션 환경에서 도메인 컨트롤러가 실수로 스냅샷으로 되돌려진 애플리케이션 공급 업체에 문의 하고 스냅샷 이후에 이러한 프로그램의 상태를 확인에 대한 지침은 해당 가상 머신에서 호스팅되는 서비스 복원 것이 좋습니다.

자세한 내용은 참조 [도메인 컨트롤러 안전 복원 아키텍처를 가상화](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch)합니다.

## <a name="recovering-from-a-usn-rollback"></a>USN 롤백에서 복구

USN에서 복구를 위해서는 두 가지 접근 방식이 있습니다.

* 도메인에서 도메인 컨트롤러 제거
* 올바른 백업의 시스템 상태 복원

### <a name="remove-the-domain-controller-from-the-domain"></a>도메인에서 도메인 컨트롤러 제거

1. 도메인 컨트롤러에서 Active Directory를 제거하여 독립형 서버가 되도록 강제 적용합니다.
2. 강등된 서버를 종료합니다.
3. 정상 상태의 도메인 컨트롤러에서 강등된 도메인 컨트롤러의 메타데이터를 정리합니다.
4. 잘못 복원된 도메인 컨트롤러가 작업 마스터 역할을 호스팅할 경우, 이러한 역할을 올바른 상태의 도메인 컨트롤러로 전송합니다.
5. 강등된 서버를 다시 시작합니다.
6. 필요한 경우 독립형 서버에 다시 Active Directory를 설치합니다.
7. 도메인 컨트롤러가 이전에 글로벌 카탈로그인 경우, 도메인 컨트롤러를 글로벌 컨트롤러로 구성합니다.
8. 도메인 컨트롤러가 이전에 작업 마스터 역할을 호스팅한 경우 작업 마스터 역할을 다시 도메인 컨트롤러로 전송합니다.

### <a name="restore-the-system-state-of-a-good-backup"></a>올바른 백업의 시스템 상태 복원

이 도메인 컨트롤러에 대해 유효한 시스템 상태 백업이 존재하는지 확인합니다. 롤백 도메인 컨트롤러가 잘못 복원되기 전에 유효한 시스템 상태 백업이 수행되었고 도메인 컨트롤러에서 수행된 최근 변경 사항이 백업에 포함된 경우, 최근 백업으로부터 시스템 상태를 복원합니다.

또한 스냅샷을 백업 원본으로 사용할 수도 있습니다. 또는 [적절한 시스템 상태 데이터 백업을 사용할 수 없을 때 가상 도메인 컨트롤러 복원](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd363553%28v%3dws.10%29#restoring-a-virtual-domain-controller-when-an-appropriate-system-state-data-backup-is-not-available) 섹션의 절차를 사용해서 새로운 호출 ID를 제공하도록 데이터베이스를 설정할 수 있습니다.

## <a name="next-steps"></a>다음 단계

* 가상화된 도메인 컨트롤러에 대한 추가 문제 해결 정보는 [가상화된 도메인 컨트롤러 문제 해결](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md)을 참조하십시오.
* [Windows 시간 서비스(W32Time)에 대한 세부 정보](../../networking/windows-time-service/windows-time-service-top.md)
