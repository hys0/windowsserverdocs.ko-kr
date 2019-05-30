---
title: Active Directory Domain Services (AD DS)를 안전 하 게 가상화
description: USN 롤백 및 Active Directory의 안전한 가상화
ms.topic: article
ms.prod: windows-server-threshold
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 03/22/2019
ms.technology: identity-adds
ms.assetid: 7a3114c8-bda8-49bb-83a8-4e04340ab221
ms.openlocfilehash: aa84e09e8a958193fee82c7b9c03cd1dca910c55
ms.sourcegitcommit: 2977c707a299929c6ab0d1e0adab2e1c644b8306
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63684174"
---
# <a name="safely-virtualizing-active-directory-domain-services-ad-ds"></a>Active Directory Domain Services (AD DS)를 안전 하 게 가상화

>적용 대상: Windows Server

Windows Server 2012부터, AD DS는 가상화 안전 기능을 도입 함으로써 도메인 컨트롤러 가상화에 대 한 향상 된 지원을 제공 합니다. 이 문서는 도메인 컨트롤러 복제에 Usn과 InvocationIDs의 역할에 설명 하 고 발생할 수 있는 일부 잠재적인 문제를 설명 합니다.

## <a name="update-sequence-number-and-invocationid"></a>업데이트 시퀀스 번호 및 InvocationID

가상 환경에는 논리적 클록 기반 복제 스키마에 종속된 분산 워크로드와 관련된 고유한 해결 과제가 있습니다. 예를 들어 AD DS 복제에서는 각 도메인 컨트롤러의 트랜잭션에 할당된 일정하게 증가하는 값(USN 또는 업데이트 시퀀스 번호라고 함)을 사용합니다. 각 도메인 컨트롤러의 데이터베이스 인스턴스에 invocationid 라는 id가 지정 됩니다. 도메인 컨트롤러의 InvocationID는 해당 USN과 함께 각 도메인 컨트롤러에서 수행되는 모든 쓰기 트랜잭션과 관련된 고유 식별자의 역할을 하므로 포리스트 내에서 고유해야 합니다.

AD DS 복제에서는 각 도메인 컨트롤러에서 InvocationID 및 USN을 사용하여 다른 도메인 컨트롤러에 복제해야 하는 변경 내용을 확인합니다. 도메인 컨트롤러에서 도메인 컨트롤러의 인식 시간에 롤백되고 USN이 완전히 다른 트랜잭션에 다시 사용 됩니다, 다른 도메인 컨트롤러가 해당 InvocationID의 컨텍스트에서 재사용된 USN와 관련 된 업데이트 이미 받은 생각 됩니다 때문에 복제는 수렴 되지 않습니다.

예를 들어 다음 그림에서는 VDC2, 즉 가상 컴퓨터에서 실행되는 대상 도메인 컨트롤러에서 USN 롤백이 감지된 경우 Windows Server 2008 R2 이하 운영 체제에서 발생하는 이벤트의 순서를 보여 줍니다. 이 그림에서는 VDC2 VDC2의 데이터베이스에 롤백되는 시간에 부적절 하 게 나타내는 복제 파트너에 게 이전에 표시 하는 최신 USN 값을 전송한는 복제 파트너를 감지할 때 VDC2에서 USN 롤백이 감지 발생 합니다.

![USN 롤백이 감지 된 때의 이벤트 순서](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_Exampleofhowreplicationcanbecomeinconsistent.png)

가상 컴퓨터 (VM) 쉽게 롤백할 수는 도메인 컨트롤러의 Usn (논리적 클록), 여 하이퍼바이저 관리자에 대 한 예를 들어, 도메인 컨트롤러의 인식 스냅숏을 적용 합니다. USN 및 USN 하는 방법에 대 한 자세한 내용은 롤백, USN 롤백이 감지 되지 않은 인스턴스를 설명 하기 위해 다른 그림을 포함 하 여 참조 [USN 및 USN 롤백](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(WS.10).aspx#usn_and_usn_rollback)합니다.

Windows Server 2012부터, Vm-generation ID 라는 식별자를 노출 하는 하이퍼바이저 플랫폼에서 호스트 되는 AD DS 가상 도메인 컨트롤러 수 감지 하 고 적용할 롤백되는 경우 가상 컴퓨터는 시간에 VM 스냅숏의 응용 프로그램에서 AD DS 환경을 보호 하는 데 필요한 안전 조치 합니다. VM-생성 ID 설계에서는 하이퍼바이저 공급업체에 독립적인 메커니즘을 사용하여 이 식별자를 게스트 가상 컴퓨터의 주소 공간에 표시하므로 VM-생성 ID를 지원하는 모든 하이퍼바이저에서 안전한 가상화 환경을 일관되게 사용할 수 있습니다. 가상 컴퓨터 내에서 실행되는 서비스 및 응용 프로그램을 통해 이 식별자를 샘플링하여 가상 컴퓨터가 제시간에 롤백되었는지 감지할 수 있습니다.

## <a name="effects-of-usn-rollback"></a>USN 롤백의 효과

USN 롤백 발생 개체 및 특성에 대 한 수정 내용을 인바운드 복제 하지 않습니다 USN 이전에 살펴보았습니다는 대상 도메인 컨트롤러에 의해.

이러한 대상 도메인 컨트롤러는 최신을 판단 하므로 디렉터리 서비스 이벤트 로그 또는 모니터링 및 진단 도구에서 복제 오류가 보고 됩니다.

USN 롤백 개체 또는 모든 파티션에 대 한 특성의 복제에 영향을 줄 수 있습니다. 가장 자주 관찰 된 부작용이 롤백 도메인 컨트롤러에서 생성 된 컴퓨터 계정과 사용자 계정을 하나 이상의 복제 파트너에 존재 하지 않도록 합니다. 또는 롤백 도메인 컨트롤러에서 시작 된 암호 업데이트가 복제 파트너 인스턴스에 존재 하지 않습니다.

USN 롤백 복제에서 파티션의 Active Directory에서 해당 개체 유형을 방지할 수 있습니다. 이러한 개체 유형은 다음과 같습니다.

* Active Directory 복제 토폴로지 및 일정
* 이러한 도메인 컨트롤러를 보유 하는 역할과 포리스트에 있는 도메인 컨트롤러의 존재 여부
* 포리스트의 도메인 및 응용 프로그램 파티션의 존재 여부
* 보안 그룹과 현재 그룹 구성원의 존재 여부
* DNS는 Active Directory 통합 DNS 영역에서 등록 레코드

USN 구멍의 크기는 수백, 수천 또는 심지어 수천 개의 변경 내용 사용자, 컴퓨터, 트러스트, 암호 및 보안 그룹을 나타낼 수 있습니다. USN 구멍 번호가 가장 높은 USN이 복원 된 시스템 상태 백업 되 고 발생 수가 변경 될 때 있던 것 오프 라인 상태 였던 전에 롤백된 도메인 컨트롤러에서 생성 된 간의 차이로 정의 됩니다.

## <a name="detecting-a-usn-rollback"></a>USN 롤백이 감지

도메인 컨트롤러 2095 원본 도메인 컨트롤러를 해당 호출 ID 변경 하지 않고 대상 도메인 컨트롤러로 이전에 승인된 USN 번호를 전송 하는 경우 이벤트를 기록 하면 USN 롤백이 감지 하기가 어려울 이기 때문에

방지 하기 위해 Active Directory에 업데이트를 시작 하 되 잘못 복원 된 도메인 컨트롤러에서 만들어지는 고유 Net Logon 서비스가 일시 중지 됩니다. Net Logon 서비스가 일시 중지 하는 경우 사용자 및 컴퓨터 계정 암호는 하지 아웃 바운드 복제 변경 하는 도메인 컨트롤러를 변경할 수 없습니다. 마찬가지로, Active Directory 관리 도구는 Active Directory의 개체에 업데이트를 할 때 정상적인 도메인 컨트롤러를 선호 합니다.

도메인 컨트롤러에서 다음 조건이 true 인 경우 다음과 같이 표시 되는 이벤트 메시지가 기록 됩니다.

* 대상 도메인 컨트롤러를 이전에 승인된 USN 번호를 전송 하는 원본 도메인 컨트롤러.
* 호출 ID에 해당 변경 사항이 없습니다

디렉터리 서비스 이벤트 로그에서 이러한 이벤트를 캡처할 수 있습니다. 그러나 이러한 관리자에 의해 알림이 전에 덮어쓸 수 있습니다.

의심 되는 경우 USN 롤백이 발생 했습니다 하지만 DSA 없거나 쓸 수 없습니다 레지스트리 항목에 대 한 로그를 확인 이벤트에 해당 이벤트가 나타나지 않습니다. 이 항목 USN 롤백 되었음을 법정 증거를 제공 합니다.

```
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\NTDS\Parameters
Registry entry: Dsa Not Writable
Value: 0x4
```

> [!WARNING]
> Dsa 없거나 쓸 수 없습니다 레지스트리 항목 값을 수동으로 변경 또는 삭제를 영구적으로 지원 되지 않는 상태에서 롤백 도메인 컨트롤러를 배치 합니다. 따라서 이러한 변경은 지원 되지 않습니다. 특히, 값을 수정 USN 롤백이 감지 코드에서 추가 격리 동작을 제거 합니다. 롤백 도메인 컨트롤러에 있는 Active Directory 파티션이 동일한 Active Directory 포리스트에서 직접 및 전이적 복제 파트너와 함께 영구적으로 일관 되지 것입니다.

이 레지스트리 키 및 해결 단계에 대 한 자세한 내용은 지원 문서에서 찾을 수 있습니다 [Active Directory 복제 오류 8456 또는 8457: "원본 | 대상 서버가 현재 복제 요청을 거부 하 고"](https://support.microsoft.com/help/2023007/active-directory-replication-error-8456-or-8457-the-source-destination)합니다.

## <a name="virtualization-based-safeguards"></a>기반 가상화 세이프 가드

도메인 컨트롤러를 설치 하는 동안 AD DS 도메인 컨트롤러의 컴퓨터 개체 (디렉터리 정보 트리 또는 DIT 라고도 함)는 데이터베이스에 대 한 Msds-generationid 특성의 일부로 VM 생성 Id 식별자 처음 저장 합니다. VM 생성 ID는 가상 컴퓨터 내 Windows 드라이버를 통해 독립적으로 추적됩니다.

관리자가 이전 스냅숏에서 가상 컴퓨터를 복원하면 가상 컴퓨터 드라이버의 현재 VM 생성 ID 값이 DIT의 값과 비교됩니다.

두 값이 다르면 invocationID가 다시 설정되고 RID 풀이 삭제되므로 USN을 다시 사용할 수 없습니다. 값이 같으면 트랜잭션이 정상적으로 커밋됩니다.

또한 AD DS에서는 도메인 컨트롤러가 다시 부팅될 때마다 가상 컴퓨터의 현재 VM 생성 ID 값을 DIT의 값과 비교하며, 값이 다른 경우 invocationID를 다시 설정하고, RID 풀을 삭제하고, DIT를 새 값으로 업데이트합니다. 뿐만 아니라 안전한 복원을 완료하기 위해 SYSVOL 폴더를 비정식으로 동기화합니다. 이를 통해 종료된 VM에서의 스냅숏 적용으로 보호 기능을 확장할 수 있습니다. Windows Server 2012에 도입 된 이러한 보호 기능 배포 및 관리 가상화 된 환경에서 도메인 컨트롤러의 고유한 이점을 제대로 활용 하려면 AD DS 관리자를 사용 합니다.

다음 그림에서는 Vm-generationid를 지 원하는 하이퍼바이저에서 Windows Server 2012를 실행 하는 가상화 된 도메인 컨트롤러에서 동일한 USN 롤백이 감지 된 경우 가상화 보호 기능이 적용 되는 방법을 보여 줍니다.

![동일한 USN 롤백이 감지 된 경우 적용 된 보호](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_VDC_Exampleofhowsafeguardswork.gif)

이 예에서 하이퍼바이저가 VM-생성 ID 값의 변경을 감지한 경우, 가상화 DC(이전 예의 A~B)에 대한 InvocationID를 다시 설정하고, 하이퍼바이저에서 저장한 새 값(G2)과 일치하도록 VM에 저장된 VM-생성 ID 값을 업데이트하는 등 가상화 보호 기능이 트리거됩니다. 이러한 보호 기능은 두 도메인 컨트롤러 모두에 대해 복제가 수렴되도록 합니다.

Windows Server 2012를 사용 하 여 AD DS VM-생성 Id 인식 하이퍼바이저에서 호스트 되는 가상 도메인 컨트롤러에 보호를 사용 하 고 되도록 실수로 응용 프로그램의 스냅숏 또는 다른 이러한 하이퍼바이저 지원 메커니즘이 롤백 할 수는 가상 컴퓨터의 상태 (USN 버블 같은 복제 문제를 방지 또는 느린 개체가)에서 AD DS 환경을 방해 하지 않도록 합니다.

도메인 컨트롤러를 복원 하는 가상 머신 스냅숏을 적용 하 여 도메인 컨트롤러를 백업 하는 대체 메커니즘으로 권장 되지 않습니다. Windows Server 백업 또는 기타 VSS 기록기 기반 백업 솔루션을 계속 사용하는 것이 좋습니다.

> [!CAUTION]
> 프로덕션 환경에서 도메인 컨트롤러가 실수로 스냅숏으로 되돌려 진 응용 프로그램 공급 업체에 문의 하 고 스냅숏 이후에 이러한 프로그램의 상태를 확인에 대 한 지침은 해당 가상 컴퓨터에서 호스팅되는 서비스 복원 것이 좋습니다.

자세한 내용은 참조 [도메인 컨트롤러 안전 복원 아키텍처를 가상화](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch)합니다.

## <a name="recovering-from-a-usn-rollback"></a>USN 롤백에서 복구

USN 롤백에서 복구 하는 방법은 두 가지가 있습니다.

* 도메인에서 도메인 컨트롤러를 제거 합니다.
* 양호한 백업의 시스템 상태 복원

### <a name="remove-the-domain-controller-from-the-domain"></a>도메인에서 도메인 컨트롤러를 제거 합니다.

1. 독립 실행형 서버로 하도록 도메인 컨트롤러에서 Active Directory를 제거 합니다.
2. 강등된 된 서버를 종료 합니다.
3. 정상적인 도메인 컨트롤러에서 강등된 된 도메인 컨트롤러의 메타 데이터를 정리 합니다.
4. 잘못 복원 된 도메인 컨트롤러 호스트 작업 마스터 역할을 하는 경우 이러한 역할을 정상적인 도메인 컨트롤러에 전송 합니다.
5. 강등된 된 서버를 다시 시작 합니다.
6. 해야 하는 경우 Active Directory를 다시 독립 실행형 서버에 설치 합니다.
7. 도메인 컨트롤러를 글로벌 카탈로그를 이전 하는 경우 글로벌 카탈로그 도메인 컨트롤러를 구성 합니다.
8. 도메인 컨트롤러를 이전에 작업 마스터 역할을 호스트 하는 경우에 작업 마스터 역할을 도메인 컨트롤러로 다시 전송 합니다.

### <a name="restore-the-system-state-of-a-good-backup"></a>양호한 백업의 시스템 상태 복원

이 도메인 컨트롤러에 대 한 유효한 시스템 상태 백업이 있는지 여부를 평가 합니다. 롤백된 도메인 컨트롤러가 잘못 복원 되기, 및 백업 도메인 컨트롤러에서 수행한 최근 변경 내용을 포함 하기 전에 유효한 시스템 상태 백업을 수행한 경우 가장 최근의 백업에서 시스템 상태를 복원 합니다.

또한 백업 원본으로 스냅숏을 사용할 수 있습니다. 섹션의 절차를 사용 하는 새 호출 ID를 부여 하는 데이터베이스를 설정할 수 있습니다 또는 [는 적절 한 시스템 상태 데이터 백업을 사용할 수 없을 때 가상 도메인 컨트롤러 복원](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd363553%28v%3dws.10%29#restoring-a-virtual-domain-controller-when-an-appropriate-system-state-data-backup-is-not-available)

## <a name="next-steps"></a>다음 단계

* 가상화된 도메인 컨트롤러에 대한 추가 문제 해결 정보는 [가상화된 도메인 컨트롤러 문제 해결](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md)을 참조하십시오.
* [Windows 시간 서비스 (w32time))에 대 한 자세한 정보](../../networking/windows-time-service/windows-time-service-top.md)
