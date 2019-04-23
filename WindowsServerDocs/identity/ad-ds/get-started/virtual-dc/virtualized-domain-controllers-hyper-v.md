---
Title: Hyper-v를 사용 하 여 도메인 컨트롤러 가상화
description: Windows Server Active Directory 도메인 컨트롤러에서 하이퍼-V를 가상화 할 때 고려 사항
author: MicrosoftGuyJFlo
ms.author: joflore
ms.date: 04/19/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.openlocfilehash: 684f3418bf336af4959282e7a8c2088d22a8c8dc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865134"
---
# <a name="virtualizing-domain-controllers-using-hyper-v"></a>Hyper-v를 사용 하 여 도메인 컨트롤러 가상화

> 적용 대상: Windows Server 2016

이 항목에서는 Windows Server 2016에 적용 가능한 지침을 확인 하기 위해 업데이트 됩니다. Windows Server 2012 가상 Dc를 복제 하는 기능과 가상 Dc에 USN 롤백이 방지 하기 위해 보호를 포함 하 여 가상화 된 도메인 컨트롤러 (Dc)를 위한 많은 개선 사항이 도입 되었습니다. 이러한 향상 된이 기능에 대 한 자세한 내용은 참조 하세요. [Introduction to Active Directory Domain Services (AD DS) Virtualization (Level 100)](../../introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100.md)합니다.

Hyper-v가 하나의 물리적 컴퓨터를 다른 서버 역할을 통합합니다. 이 가이드에서는 32 비트 또는 64 비트 게스트 운영 체제로 실행 중인 도메인 컨트롤러를 설명 합니다.

## <a name="planning-to-virtualize-domain-controllers"></a>도메인 컨트롤러 가상화 계획

이 섹션에서는 hyper-v 서버에 대 한 하드웨어 요구 사항 설명 단일 지점의 적절 한 유형의 Hyper-v 서버 및 virtual machines 및 보안 및 성능을 결정에 대 한 구성 선택 하면 오류를 방지 하는 방법입니다.

## <a name="hyper-v-requirements"></a>Hyper-v 요구 사항

를 설치 및 Hyper-v 역할을 사용 하려면 다음이 필요 합니다.

   - **X64 프로세서**
      - Hyper-v는 x64 기반 버전의 Windows Server 2008 이상에서 사용할 수 있습니다.  
   - **하드웨어 기반 가상화**
      - 이 기능은 가상화 옵션, 특히 Intel Virtualization Technology (Intel VT) 또는 AMD 가상화 (Amd-v)을 포함 하는 프로세서에서 사용할 수 있습니다.  
   - **하드웨어 데이터 실행 방지 (DEP)**
      - 하드웨어 DEP 사용 가능 하 고 사용 하도록 설정 해야 합니다. 특히 Intel XD 비트 설정 해야 합니다 (execute disable bit) 또는 AMD NX 비트 (no execute bit).  

## <a name="avoid-creating-single-points-of-failure"></a>단일 실패 지점을 방지합니다

가상 도메인 컨트롤러 배포를 계획할 때 잠재적인 단일 실패 지점을 만들지 않아야 합니다. 시스템 중복성을 구현 하 여 잠재적인 단일 실패 지점을 도입을 피할 수 있습니다. 예를 들어 관리 비용을 증가 가능성을 염두 하면서 다음 권장 사항을 따릅니다.

1. 각 도메인의 단일 가상화 호스트가 실패 하는 경우 모든 도메인 컨트롤러를 손실 위험을 줄일 수 있는 다른 가상화 호스트에 두 개 이상의 가상화 된 도메인 컨트롤러를 실행 합니다.  
2. 다른 기술에 대 한 권장 한 대로에서 도메인 컨트롤러에서 실행 됩니다 (다른 Cpu, 마더보드, 네트워크 어댑터 또는 다른 하드웨어 사용)는 하드웨어를 다양화 합니다. 다양성 하드웨어 공급 업체 구성, 드라이버를 하나의 또는 유형의 하드웨어에 관련 된 오작동 하 여 발생할 수 있는 피해를 제한 합니다.  
3. 가능 하면 도메인 컨트롤러는 전 세계의 서로 다른 지역에 있는 하드웨어에서 실행 되어야 합니다. 이 오류 도메인 컨트롤러의 호스트 되는 사이트에 영향을 주는 재해의 영향을 줄일 수는 있습니다.  
4. 각 도메인의 실제 도메인 컨트롤러를 유지 합니다. 이 해당 플랫폼을 사용 하는 모든 호스트 시스템에 영향을 주는 가상화 플랫폼 오작동의 위험을 완화 합니다.  

## <a name="security-considerations"></a>보안 고려 사항

컴퓨터가 도메인에 가입 되어 있거나 작업 그룹 컴퓨터만 해당 하는 경우에 가상 도메인 컨트롤러를 실행 하는 호스트 컴퓨터는 쓰기 가능한 도메인 컨트롤러 신중 하 게 관리 되어야 합니다. 중요 한 보안 고려 사항입니다. 유발할된 호스트는 악의적인 사용자가 액세스를 때 발생 하는 권한 상승 공격이 및 권한이 부여 되거나 합법적인 방식으로 할당 된 시스템 권한 공격에 취약 합니다. 악의적인 사용자는 이러한 유형의 공격을 사용 하 여 모든 가상 컴퓨터에서 도메인을 손상 시킬 수 있습니다 하 고 있는 포리스트이 컴퓨터 호스트 합니다.

도메인 컨트롤러를 가상화 하려는 경우 다음 보안 고려 사항을 염두에서에 둡니다 야 합니다.

   - 컨트롤러의 모든 도메인 및 포리스트 도메인 컨트롤러에 속해 있는 기본 도메인 관리자에 게 자격 증명에 해당 하는 고려해 야 하는 virtual, 쓰기 가능한 도메인을 호스팅하는 컴퓨터의 로컬 관리자입니다.  
   - 보안 및 성능 문제를 방지 하려면 권장 구성은 Hyper-v 이외의 응용 프로그램이 없는 이상 또는 Windows Server 2008의 Server Core 설치를 실행 하는 호스트입니다. 이 구성은 응용 프로그램 및 서비스 성능이 향상된 하 고 더 적은 응용 프로그램 및 서비스 악의적으로 컴퓨터 또는 네트워크 공격에 악용 될 수 있는 발생 해야 하는 서버에 설치 된 수를 제한 합니다. 이 구성 유형에 미치는 공격 영역이 감소 이라고 합니다. 지사 또는 만족 스럽게 보안 될 수 없는 다른 위치에서 읽기 전용 도메인 컨트롤러 (RODC)을 사용 하는 것이 좋습니다. 별도 관리 네트워크 있으면 호스트 관리 네트워크만 연결할 수는 것이 좋습니다.  
   - Bitlocker를 사용 하 여 도메인 컨트롤러를 사용 하 여, Windows Server 2016 이후 시스템 볼륨의 잠금을 해제 하려면 게스트 키 자료도 제공 하는 가상 TPM 기능을 사용할 수 있습니다.
   - [보호 패브릭 및 차폐 Vm](/it-server/WindowsServerDocs/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md) 도메인 컨트롤러를 보호 하기 위해 추가 제어를 제공할 수 있습니다.

Rodc에 대 한 자세한 내용은 [읽기 전용 도메인 컨트롤러 계획 및 배포 가이드](../../deploy/rodc/read-only-domain-controller-updates.md)합니다.

도메인 컨트롤러를 보호 하는 방법에 대 한 자세한 내용은 참조 하세요. [Active Directory 설치 보호에 대 한 모범 사례 가이드](../../plan/security-best-practices/best-practices-for-securing-active-directory.md)합니다.

## <a name="security-boundaries-for-different-host-and-guest-configurations"></a>다른 호스트 및 게스트 구성에 대 한 보안 경계

가상 컴퓨터를 사용 하면 다양 한 구성 도메인 컨트롤러를 가질 수 있습니다. 신중 하 게 고려 하는 가상 컴퓨터에 영향을 경계 및 Active Directory 토폴로지 트러스트 방식이 지정 되어야 합니다. 다음 표에서 Active Directory 도메인 컨트롤러를 호스트 (Hyper-v 서버) 및 해당 게스트 컴퓨터 (Hyper-v 서버에서 실행 되는 가상 컴퓨터)에 대 한 가능한 구성은 설명 합니다.

|컴퓨터|구성 1|Configuration 2|
|-------|---------------|---------------|
|Host|작업 그룹 또는 멤버 컴퓨터|작업 그룹 또는 멤버 컴퓨터|
|게스트|도메인 컨트롤러|작업 그룹 또는 멤버 컴퓨터|

![](media/virtualized-domain-controller-architecture/Dd363553.f44706fd-317e-4f0b-9578-4243f4db225f(WS.10).gif)

   - 호스트 컴퓨터의 관리자 쓰기 가능한 도메인 컨트롤러 게스트에 도메인 관리자로 동일한 액세스할 수 있고 따라서 처리 해야 합니다. RODC 게스트의 경우 호스트 컴퓨터의 관리자는 게스트 RODC에 로컬 관리자로 동일한 액세스를 갖습니다.   
   - 통합 문서 호스트는 동일한 도메인에 가입 되어 있으면 가상 컴퓨터에서 도메인 컨트롤러 호스트에 관리 권한이 있습니다. 악의적인 사용자가 악의적인 사용자에는 먼저 가상 컴퓨터 1에 대 한 액세스 권한을 획득 한 경우 모든 가상 컴퓨터를 손상 시킬 수가 있습니다. 이 공격 이라고 합니다. 여러 도메인 또는 포리스트 도메인 컨트롤러의 경우 이러한 도메인에는 하나의 도메인의 관리자가 모든 도메인에서 신뢰할 수 있는 중앙 집중식된 관리를 해야 합니다.  
   - 가상 컴퓨터 1의 공격에 대 한 영업 기회는 RODC로 가상 컴퓨터 1을 설치 하는 경우에 존재 합니다. RODC의 관리자가 도메인 관리자 권한이 명시적으로 제공 하지는 않지만 도구 RODC 호스트 컴퓨터에 정책을 보내는 데 사용할 수 있습니다. 이러한 정책은 시작 스크립트를 포함할 수 있습니다. 이 작업에 성공한 경우 호스트 컴퓨터를 손상 될 수 있습니다 및 호스트 컴퓨터의 다른 가상 컴퓨터를 손상 시킬 다음 사용할 수 있습니다.  

## <a name="security-of-vhd-files"></a>VHD 파일의 보안

가상 도메인 컨트롤러의 VHD 파일을 실제 도메인 컨트롤러의 실제 하드 드라이브 하는 것과 동일합니다. 따라서 동일한 양의 실제 도메인 컨트롤러의 하드 드라이브를 보호 하는 주의 사용 하 여 보호 되어야 합니다. 안정적이 고 신뢰할 수 있는 관리자만 도메인 컨트롤러의 VHD 파일에 대 한 액세스를 허용 되는 있는지 확인 합니다.

## <a name="rodcs"></a>Rodc

Rodc의 이점 중 하나는 없는 물리적 보안을 보장할 수 없는 같은 지점에서 위치에 배치 하는 기능입니다. Windows BitLocker 드라이브 암호화를 사용 하 여 VHD 파일 자체를 보호할 수 있습니다 (파일 시스템이 아닌 여기) 실제 디스크의 도용을 통해 호스트에서 손상 되지 않도록 합니다. 
<!-- Removed link to Windows Server 2008 Hyper-V and BitLocker Drive Encryption (http://go.microsoft.com/fwlink/?linkid=123534). Link is dead. -->

## <a name="performance"></a>성능

새 마이크로 커널 64 비트 아키텍처에서는 이전 가상화 플랫폼에서 하이퍼-V 성능이 크게 향상은 없습니다. 호스트 성능의 호스트 이상 또는 Windows Server 2008의 Server Core 설치 해야 하며 Hyper-v가 아닌 다른 서버 역할 가질 수 없습니다.

가상 머신의 성능 워크 로드에 따라 달라 집니다. Active Directory 성능에 만족을 보장 하기 위해 특정 토폴로지를 테스트 합니다. 안정성 및 성능 모니터 (Perfmon.msc)와 같은 도구를 사용 하 여 기간 동안 현재 워크 로드를 평가 또는 [Microsoft Assessment and Planning (MAP) toolkit](https://go.microsoft.com/fwlink/?linkid=137077)합니다. MAP 도구는 모든 서버 및 네트워크에 현재 존재 하는 서버 역할의 인벤토리를 수행 하려는 경우에 중요 한 수도 있습니다.

가상화 된 도메인 컨트롤러의 성능 파악을 가져오려면 다음 성능 테스트를 사용 하 여 수행할 된 합니다 [Active Directory 성능 테스트 도구 (ADTest.exe)](https://go.microsoft.com/fwlink/?linkid=137088)합니다.

Lightweight Directory Access Protocol (LDAP) 테스트는 실제 도메인 컨트롤러에 동일 하 게 연결 된 서버의 ADTest.exe 사용 하 여 실제 도메인 컨트롤러에서 및 호스트 된 가상 머신입니다 실행 된 합니다. 실제 컴퓨터에 대 한 논리적 프로세서가 하나만 사용한 하 고 CPU 사용률이 100%에 쉽게 연결할 가상 컴퓨터에 대 한 가상 프로세서가 하나 밖에 사용한 키를 누릅니다. 다음 표에 문자와 각 테스트 후 괄호로 수 ADTest.exe에서 특정 테스트를 나타냅니다. 이 데이터에서 알 수 있듯이, 가상화 된 도메인 컨트롤러 성능에는 실제 도메인 컨트롤러 성능의 88에 98% 였습니다.

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>측정</th>
<th>테스트</th>
<th>물리적</th>
<th>가상</th>
<th>델타</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>검색 수/초</p></td>
<td><p>기본 범위 (L1)에서 일반 이름 검색</p></td>
<td><p>11508</p></td>
<td><p>10276</p></td>
<td><p>-10.71%</p></td>
</tr>
<tr class="even">
<td><p>검색 수/초</p></td>
<td><p>기본 범위 (L2)의 특성 집합에 대 한 검색</p></td>
<td><p>10123</p></td>
<td><p>9005</p></td>
<td><p>-11.04%</p></td>
</tr>
<tr class="odd">
<td><p>검색 수/초</p></td>
<td><p>기본 범위 (L3)에 있는 모든 특성에 대 한 검색</p></td>
<td><p>1284</p></td>
<td><p>1242</p></td>
<td><p>-3.27%</p></td>
</tr>
<tr class="even">
<td><p>검색 수/초</p></td>
<td><p>하위 트리 범위 (계층 6)에 일반적인 이름 검색</p></td>
<td><p>8613</p></td>
<td><p>7904</p></td>
<td><p>-8.23%</p></td>
</tr>
<tr class="odd">
<td><p>성공적인 바인딩합니다/sec</p></td>
<td><p>빠른 바인딩합니다 (B1)를 수행 합니다.</p></td>
<td><p>1438</p></td>
<td><p>1374</p></td>
<td><p>-4.45%</p></td>
</tr>
<tr class="even">
<td><p>성공적인 바인딩합니다/sec</p></td>
<td><p>단순 바인딩 (B2)를 수행 합니다.</p></td>
<td><p>611</p></td>
<td><p>550</p></td>
<td><p>-9.98%</p></td>
</tr>
<tr class="odd">
<td><p>성공적인 바인딩합니다/sec</p></td>
<td><p>사용 하는 데 NTLM 바인딩합니다 (B5)</p></td>
<td><p>1068</p></td>
<td><p>1056</p></td>
<td><p>-1.12%</p></td>
</tr>
<tr class="even">
<td><p>Writes/sec</p></td>
<td><p>여러 특성 (W2) 작성</p></td>
<td><p>6467</p></td>
<td><p>5885</p></td>
<td><p>-9.00%</p></td>
</tr>
</tbody>
</table>

만족할 만한 성능을 보장 하기 위해 통합 구성 요소 (IC)는 게스트 운영 체제 "enlightenments," 또는 하이퍼바이저 인식 가상 드라이버를 사용할 수 있도록 설치 않았습니다. 설치 과정에서 에뮬레이트된 Electronics IDE (Integrated Drive) 또는 네트워크 어댑터 드라이버를 사용 해야 할 수도 있습니다. 프로덕션 환경에서는 성능 향상을 위해 가상 드라이버를 사용 하 여 이러한 에뮬레이트된 드라이버 바꿔야 합니다.

가상 컴퓨터의 성능 안정성 및 성능 관리자 (Perfmon.msc)를 모니터링 하면 가상 머신 내에서 CPU 정보가 됩니다 가상 CPU 실제 프로세서에서 예약 된 방식으로 인해 완전히 정확 하 게 합니다. Hyper-v 서버에서 실행 되는 가상 컴퓨터의 CPU 정보를 가져오려는 경우는 호스트 파티션에 Hyper-v 하이퍼바이저 논리 프로세서 카운터를 사용 합니다.

성능에 대 한 자세한 내용은 참조 AD DS와 Hyper-v의 튜닝 [성능 튜닝 지침에 대 한 Windows Server 2016](../../../../administration/performance-tuning/index.md)합니다.
<!-- Updated to 2016 perf guidance -->

또한 않으려는 VHD 차이점 보관용 디스크 성능이 저하 될 수 있으므로 도메인 컨트롤러로 구성 된 가상 머신에서 VHD 차이점 보관용 디스크를 사용 합니다. Hyper-v 디스크 유형, 차이점 보관용 디스크를 포함 하는 방법에 대 한 자세한 내용은 [새 가상 하드 디스크 마법사](http://go.microsoft.com/fwlink/?linkid=137279)합니다.
<!-- Couldn't find an equivalent WS 2016 Hyper-V article. -->

가상 호스팅 환경에서 AD DS에 대 한 자세한 내용은 참조 하세요. [Active Directory 도메인 컨트롤러 가상 호스팅 환경에서 호스트 될 때 고려해 야 할 사항](https://go.microsoft.com/fwlink/?linkid=141292) Microsoft 기술 자료에서 합니다.

## <a name="deployment-considerations-for-virtualized-domain-controllers"></a>가상화 된 도메인 컨트롤러에 대 한 배포 고려 사항

시간 동기화 및 저장소에 대 한 특별 고려 사항 및 도메인 컨트롤러를 배포할 때 하지 않아야 하는 몇 가지 일반적인 가상 머신 사례 있습니다.

## <a name="virtualization-deployment-practices-to-avoid"></a>가상화 배포 예방 방법

Hyper-v 같은 가상화 플랫폼을 다양 한, 유지 관리, 백업, 마이그레이션 및 관리 컴퓨터를 더 쉽게 하는 편리한 기능을 제공 합니다. 그러나 다음과 같은 일반적인 배포 사례 및 기능을 해서는 안 가상 도메인 컨트롤러에 대 한 합니다.

   - Active Directory의 지 속성을 위해 가상 도메인 컨트롤러의 데이터베이스 파일 (Active Directory 데이터베이스 (NTDS 배포 하지 마세요. DIT), 로그 및 SYSVOL) 가상 IDE 디스크에 있습니다. 대신 두 번째 가상 SCSI 컨트롤러에 연결 된 VHD를 만들고 데이터베이스, 로그 및 SYSVOL은에 배치 되도록 가상 컴퓨터의 SCSI 디스크 도메인 컨트롤러를 설치 하는 동안 확인 합니다.  
   - 도메인 컨트롤러로 구성 하는 가상 컴퓨터에서 차이점 보관용 디스크 가상 하드 디스크 (Vhd)를 구현 하지 않습니다. 이렇게 하면 이전 버전으로 되돌리려면 너무 쉽게 및 성능이 줄어듭니다. VHD 형식에 대 한 자세한 내용은 참조 하세요. [새 가상 하드 디스크 마법사](https://go.microsoft.com/fwlink/?linkid=137279)합니다.  
   - 새 Active Directory 도메인 및 포리스트는 복사본을 시스템 준비 도구 (Sysprep)를 사용 하 여 먼저 준비 되지 않았습니다 하는 Windows Server 운영 체제를 배포 하지 않습니다. Sysprep를 실행 하는 방법에 대 한 자세한 내용은 참조 하세요. [Sysprep (시스템 준비) 개요](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview)

      > [!WARNING]
      > 도메인 컨트롤러에서 Sysprep을 실행 하는 것은 지원 되지 않습니다.

   - 잠재적 업데이트 시퀀스 번호 (USN) 롤백 문제를 방지 하려면 추가 도메인 컨트롤러를 배포 하는 이미 배포 된 도메인 컨트롤러를 표시 하는 VHD 파일의 복사본을 사용 하지 마십시오. USN 롤백에 대한 자세한 내용은 [USN 및 USN 롤백](#usn-and-usn-rollback)을 참조하세요.
      - Windows Server 2012 및 최신 추가 도메인 컨트롤러를 배포 하려는 경우 제대로 준비 하는 경우 도메인 컨트롤러 이미지를 복제 하는 작업을 할당할 수 있습니다.
   - 도메인 컨트롤러를 실행 하는 가상 머신을 내보낼 Hyper-v 내보내기 기능을 사용 하지 마세요.
      - Windows Server 2012 이상 버전에서는 내보내기와 가져오기를 게스트 가상 도메인 컨트롤러의 마찬가지로 처리는 신뢰할 수 없는 복원이 생성 ID의 변경을 감지 하 고 복제를 위해 구성 되어 있지 않습니다.
      - 더 이상 내보낸 게스트를 사용 하지 않는 것을 확인 합니다.
  - 도메인 컨트롤러의 두 번째 비활성 복사본을 유지 하려면 Hyper-v 복제를 사용할 수 있습니다. 복제 된 이미지를 시작 하는 경우 해야 하지 소스를 사용 하 여 DC 게스트 이미지를 내보낸 후 동일한 이유로 적절 한 정리를 수행 합니다.

## <a name="physical-to-virtual-migration"></a>물리적 컴퓨터에서 가상 컴퓨터로 마이그레이션

System Center Virtual Machine Manager (VMM) 2008 물리적 컴퓨터 및 virtual machines의 통합된 관리를 제공합니다. 또한 가상 컴퓨터에 물리적 컴퓨터를 마이그레이션하는 기능도 제공 합니다. 이 프로세스는 물리적-가상 컴퓨터로 변환 ((p2v 변환) 이라고 합니다. P2V 변환 과정에서 새 가상 컴퓨터와 마이그레이션하려는 실제 도메인 컨트롤러 실행 하지 않아야 동시 상황을 피하려면 USN 롤백에 설명 된 대로 [USN 및 USN 롤백](#usn-and-usn-rollback)합니다.

도메인 컨트롤러를 다시 설정할 때 디렉터리 데이터를 일관 되도록 오프 라인 모드를 사용 하 여 P2V 변환을 수행 해야 합니다. 오프 라인 모드 옵션을 제공 하는 이며 물리적 서버 변환 마법사에서 권장 됩니다. 온라인 모드와 오프 라인 모드 간의 차이점에 대 한 참조 [P2V: VMM에서 물리적 컴퓨터를 가상 컴퓨터로 변환](https://go.microsoft.com/fwlink/?linkid=155072)을 참조하십시오. P2V 변환 하는 동안 가상 컴퓨터 네트워크에 연결 하지 합니다. 가상 컴퓨터의 네트워크 어댑터는 P2V 변환 프로세스를 완전 하 고 확인 된 후에 설정 되어야 합니다. 이 시점에서 물리적 원본 컴퓨터는 해제 됩니다. 가져오지 않는 물리적 원본 컴퓨터 네트워크 되돌려 다시 하드 디스크를 포맷 하기 전에 합니다.

> [!NOTE]
> 만드는 USN 롤백이 위험을 실행 하지 않는 새 가상 Dc를 만들려면 안전한 옵션이 있습니다. 하나 이상의 가상 DC에 이미 있는 경우 새 가상 DC에서 도메인 컨트롤러 복제를 사용 하며 IfM (미디어)를 설치에서 일반 승격 하 여 설정할 수 있습니다.
이 정보를 통해 하드웨어를 사용 하 여 문제를 방지 또는 플랫폼 관련 문제 가상 게스트 P2V 변환 발생할 수 있습니다.

> [!WARNING]
> Active Directory 복제 관련 문제를 방지 하려면 (실제 또는 가상) 하나의 인스턴스만 확인의 지정된 된 도메인 컨트롤러 네트워크에 있는 지정 된 시점 시간에서입니다.
> 문제가 되 고 이전 클론의 가능성을 낮출 수 있습니다.
> 
> - 새 가상 DC를 실행 하는 경우 두 번 사용 하 여 컴퓨터 계정 암호를 변경 합니다: netdom resetpwd /Server: < 도메인 컨트롤러 >...
> - 새 ID 생성 되는 것으로 새 가상 게스트를 내보내고 데이터베이스 호출 id입니다. 따라서 및
> 

## <a name="using-p2v-migration-to-create-test-environments"></a>P2V 마이그레이션을 사용 하 여 테스트 환경 만들기

VMM 통해 P2V 마이그레이션 테스트 환경을 만드는 데 사용할 수 있습니다. 프로덕션 도메인 컨트롤러를 영구적으로 종료 하지 않고 테스트 환경을 만들려면 가상 컴퓨터에 물리적 컴퓨터에서 프로덕션 도메인 컨트롤러를 마이그레이션할 수 있습니다. 그러나 테스트 환경을 동일한 도메인 컨트롤러의 두 인스턴스가 존재 하는 경우 프로덕션 환경에서 다른 네트워크에 있어야 합니다. 유용한 기울여야 P2V 마이그레이션 사용 하 여 테스트 환경 만드는 테스트 및 프로덕션 환경에 영향을 줄 수 있는 USN 롤백을 방지 하려면. 다음은 P2V를 사용 하 여 테스트 환경을 만드는 데 사용할 수 있는 메서드입니다.

각 도메인에서 프로덕션 도메인 컨트롤러가 하나 P2V를 사용 하 여 물리적 컴퓨터에서 가상 컴퓨터로 마이그레이션 섹션에 명시 된 지침에 따라 테스트 가상 컴퓨터에 마이그레이션됩니다. 실제 프로덕션 시스템 및 테스트 가상 머신을 다시 온라인 상태일 때 서로 다른 네트워크에 이어야 합니다. 테스트 환경에서 USN 롤백을 방지 하려면 가상 컴퓨터에 물리적 컴퓨터에서 마이그레이션할 수 있는 모든 도메인 컨트롤러를 오프 라인입니다. (이렇게 하려면 ntds 서비스가 중지 하거나 컴퓨터에서 디렉터리 서비스 복원 모드 (DSRM)를 다시 시작 합니다.) 도메인 컨트롤러가 오프 라인으로 후 환경에 새로운 업데이트를 도입 해야 합니다. 컴퓨터는 P2V 마이그레이션; 동안 오프 라인으로 유지 해야 합니다. 컴퓨터 하나도 해야 다시 온라인 상태로 만들어야 모든 컴퓨터를 완전히 마이그레이션될 있을 때까지 합니다. USN 롤백에 대 한 자세한 내용은 USN 및 USN 롤백을 참조 하세요.

후속 테스트 도메인 컨트롤러는 테스트 환경에서 복제본으로 승격 되어야 합니다.

## <a name="time-service"></a>시간 서비스

도메인 컨트롤러로 구성 된 virtual machines에 대 한 도메인 컨트롤러 역할을 하는 호스트 시스템 및 게스트 운영 체제 간의 시간 동기화 하지 않도록이 좋습니다. 이 통해 게스트 도메인 컨트롤러를 도메인 계층 구조에서 시간을 동기화 합니다.

Hyper-v 시간 동기화 공급자를 사용 하지 않으려면 VM을 종료 하 고 Integration Services에서 시간 동기화 확인란의 선택을 취소 합니다.

> [!NOTE]
> 이전 권장 부분적으로 호스트 간에 시간 동기화를 사용 하지 않도록 설정 하는 것 보다는 게스트 도메인 컨트롤러는 도메인 계층에서의 시간을 동기화 하기 위한 현재 권장 사항을 반영 하기 위해이 설명서를 최근에 업데이트 했더라도 시스템 및 게스트 도메인 컨트롤러입니다.

## <a name="storage"></a>스토리지

도메인 컨트롤러 가상 컴퓨터의 성능을 최적화 하 고 Active Directory 쓰기 내 구성을 보장 하려면 다음 권장 사항은 운영 체제, Active Directory 및 VHD 파일을 저장 하는 데 사용 합니다.

   - **게스트 저장소**합니다. Active Directory 데이터베이스 (Ntds.dit) 파일, 로그 파일 및 SYSVOL 파일을 운영 체제 파일에서 별도 가상 디스크에 저장 합니다. 두 번째 가상 SCSI 컨트롤러에 연결 된 VHD를 만들고 가상 컴퓨터의 가상 SCSI 디스크에서 데이터베이스, 로그 및 SYSVOL을 저장 합니다. 가상 SCSI 디스크 가상 IDE에 비해 향상 된 성능을 제공 하 고 강제 단위 액세스 (FUA) 지원 합니다. FUA 사용 하면 운영 체제 기록 되며 모든 캐싱 메커니즘을 우회 하는 미디어에서 직접 데이터를 읽습니다.

   > [!NOTE]
   > 가상 DC 게스트에 대 한 Bitlocker를 사용 하려는 경우 "자동 잠금 해제"에 대 한 추가 볼륨 구성 되어 있는지 확인 해야 합니다.
   > 자동 구성에 대 한 자세한 내용은 잠금 해제에서 찾을 수 있습니다 [BitLockerAutoUnlock 사용](https://docs.microsoft.com/powershell/module/bitlocker/enable-bitlockerautounlock)

   - **VHD 파일의 저장소를 호스트**합니다. 권장 사항: VHD 파일의 저장소 권장 사항 주소 저장소를 호스트 합니다. 최상의 성능을 위해 다른 서비스 또는 호스트 Windows 운영 체제가 설치 되어 있는 시스템 디스크 등의 응용 프로그램에서 자주 사용 되는 디스크에 VHD 파일을 저장 하지 마십시오. 호스트 운영 체제에서 별도 파티션에서 각 VHD 파일 및 다른 모든 VHD 파일을 저장 합니다. 이상적인 구성은 별도 실제 드라이브에 있는 각 VHD 파일을 저장 하는 것입니다.  

    호스트 실제 디스크 시스템 충족 해야 합니다 **하나 이상의** 가상화 된 워크 로드 데이터 무결성의 요구 사항을 충족 하기 위해 다음 조건 중:  

      - 서버 클래스 디스크 (SCSI, 파이버 채널)이 사용 됩니다.  
      - 시스템은 디스크는 배터리 백업 캐싱 HBA (호스트 버스 어댑터)에 연결 되어 있는지 있도록 합니다.  
      - 시스템은 저장소 장치로 저장소 컨트롤러 (예를 들어 RAID 시스템)를 사용합니다.  
      - 시스템은 디스크에 대 한 전원 무정전 전원 공급 장치 (UPS)로 보호 되는 게 됩니다.  
      - 시스템은 디스크의 쓰기 캐싱 기능을 해제 하 게 됩니다.  

   - **통과 디스크 및 VHD를 고정**합니다. 가상 머신에 대 한 저장소를 구성 하는 방법은 여러 가지입니다. VHD 파일을 사용 하는 경우 생성 될 때 고정 크기 Vhd에 대 한 메모리 할당 되므로 고정 크기 Vhd는 동적 Vhd 보다 더 효율적입니다. 통과 디스크의 경우 실제 저장소 미디어에 액세스할 사용할 수 있는 가상 컴퓨터에는 더욱 성능을 위해 최적화 됩니다. 통과 디스크는 기본적으로 실제 디스크 또는 가상 머신에 연결 된 논리 단위 번호 (Lun)입니다. 통과 디스크 스냅숏 기능을 지원 하지 않습니다. 따라서 통과 디스크 되므로 기본 하드 디스크 구성을 한 도메인 컨트롤러를 사용 하 여 스냅숏 사용은 권장 되지 않습니다.  

Active Directory 데이터 손상 될 가능성을 줄이기 위해 가상 SCSI 컨트롤러를 사용 합니다.

   - 가상 도메인 컨트롤러를 호스트 하는 Hyper-v 서버에서 SCSI 실제 드라이브 (IDE/ATA 드라이브)를 사용 합니다. SCSI 드라이브를 사용할 수 없는 경우에 가상 도메인 컨트롤러를 호스트 하는 IDE ATA/드라이브에서 쓰기 캐싱을 비활성화를 확인 합니다. 자세한 내용은 [이벤트 ID 1539 – 데이터베이스 무결성](https://go.microsoft.com/fwlink/?linkid=162419)합니다.
   - Active Directory의 내 구성을 보장 하기 위해 쓰기, Active Directory 데이터베이스, 로그 및 SYSVOL 가상 SCSI 디스크에 배치 해야 합니다. 가상 SCSI 디스크 강제 단위 액세스 (FUA)를 지원합니다. FUA 사용 하면 운영 체제 기록 되며 모든 캐싱 메커니즘을 우회 하는 미디어에서 직접 데이터를 읽습니다.  

## <a name="operational-considerations-for-virtualized-domain-controllers"></a>가상화 된 도메인 컨트롤러에 대 한 운영 상의 고려 사항

Virtual machines에서 실행 하는 도메인 컨트롤러에는 물리적 컴퓨터에서 실행 되는 도메인 컨트롤러에 적용 되지 않는 운영 제한 사항이 있습니다. 가상화 된 도메인 컨트롤러를 사용 하면 일부의 가상화 소프트웨어 기능 및 사용 하지 않아야 하는 사례:

   - 수행 하지 일시 중지, 중지 또는 가상 컴퓨터에서 포리스트의 삭제 표시 기간 보다 긴 시간 기간에 대 한 도메인 컨트롤러의 저장된 된 상태를 저장 및 일시 중지 또는 저장 된 상태에서 다시 합니다. 이 복제를 방해할 수 있습니다. 포리스트의 삭제 표시 수명을 결정 하는 방법에 알아보려면 참조 [포리스트의 삭제 표시 수명을 결정](https://go.microsoft.com/fwlink/?linkid=137177)합니다.  
   - 가상 하드 디스크 (Vhd)을 복제 하거나 복사 하지 마십시오. 게스트 VM에 대 한 보호를 사용 하더라도 개별 Vhd도 복사할 수 있습니다 및 USN 롤백 발생 합니다.
   - 가상 도메인 컨트롤러의 스냅숏으로 사용 하거나 사용 하지 마십시오. Windows Server 2012를 사용 하 여 기술적으로 이므로, 적절 한 백업 전략을 대체 합니다. DC 스냅숏을 또는 스냅숏을 복원에 대 한 몇 가지 이유가 있습니다.
   - 도메인 컨트롤러로 구성 된 가상 머신에서 디스크를 차이점 보관용 VHD를 사용 하지 마십시오. 이렇게 하면 너무 쉽다 이전 버전으로 되돌리기 및 성능이 줄어듭니다.  
   - 도메인 컨트롤러를 실행 하는 가상 머신에서 내보내기 기능을 사용 하지 마십시오.  
   - 지원 되는 백업을 사용 하 여 이외의 방법으로 Active Directory 데이터베이스의 내용을 롤백하기 하거나 도메인 컨트롤러를 복원 하지 마십시오. 자세한 내용은 [백업 및 복원 고려 사항 가상화 된 도메인 컨트롤러에 대 한](#backup-and-restore-practices-to-avoid)합니다.  

이러한 모든 권장이 사항은 업데이트 시퀀스 번호 (USN) 롤백 방지 하는 데 도움이 됩니다. USN 롤백에 대 한 자세한 내용은 USN 및 USN 롤백을 참조 하세요.

## <a name="backup-and-restore-considerations-for-virtualized-domain-controllers"></a>백업 및 가상화 된 도메인 컨트롤러에 대 한 복원 고려 사항

도메인 컨트롤러를 백업은 모든 환경에 대 한 중요 한 요구 사항입니다. 백업은 도메인 컨트롤러 실패가 또는 관리 오류가 발생할 경우 데이터 손실을 방지 합니다. 이러한 이벤트가 발생 하는 경우 롤백해야 도메인 컨트롤러의 시스템 상태를 지정 시간에서 전에 실패 또는 오류 것입니다. 도메인 컨트롤러는 정상 상태로 복원 하는 위한 지원 되는 방법은 Active Directory 호환 백업 같은 응용 프로그램을 Windows Server Backup을 사용 하 여 도메인의 현재 설치 된 시스템 상태 백업을 복원할 수 컨트롤러입니다. Active Directory Domain Services (AD DS)를 사용 하 여 Windows Server Backup을 사용 하는 방법에 대 한 자세한 내용은 참조는 [AD DS 백업 및 복구 단계별 가이드](https://go.microsoft.com/fwlink/?LinkId=138501)합니다.

가상 머신 기술을 사용 하 여 Active Directory의 특정 요구 사항을 추가 significance의 작업 수행을 복원합니다. 예를 들어, 가상 하드 디스크 (VHD) 파일의 복사본을 사용 하 여 도메인 컨트롤러를 복원 하는 경우 복원 된 후 도메인 컨트롤러의 데이터베이스 버전을 업데이트는 중요 한 단계를 건너뜁니다. 복제는 도메인 컨트롤러 복제본 간에 일치 하지 않는 데이터베이스에서 결과 부적절 한 추적 번호로 진행 됩니다. 대부분의 경우에서이 문제가 계속 복제 시스템에 의해 감지 되지 않은 하 고 도메인 컨트롤러 간의 불일치 불구 하 고 오류가 보고 됩니다.

가상화 된 도메인 컨트롤러의 백업 및 복원 하는 데 지원 되는 한 가지 방법은 같습니다.

1. 게스트 운영 체제에서 Windows Server Backup을 실행 합니다.  

Windows Server 2012 이상 Hyper-v 호스트 및 게스트, 스냅숏, 게스트 VM 내보내기 및 가져오기 및 Hyper-v 복제를 사용 하 여 도메인 컨트롤러의 지원 되는 백업을 수행할 수 있습니다. 그러나 이러한 모든 되지 게스트 VM 내보내기 약간 예외를 사용 하 여 적절 한 백업 기록을 만들기에 적합 합니다.

사용 하 여 Windows Server 2016 Hyper-v 지원은 "프로덕션 스냅숏"에 있는 Hyper-v 서버 트리거는 게스트 VSS 기반 백업 및 게스트 스냅숏이 완료 되 면, 호스트 된 Vhd를 가져오고 백업 위치에 저장 합니다.

Windows Server 2012 이상에서 작동 하는 동안 Bitlocker 사용 하 여 비 호환성 되어 있습니다.

- VSS 스냅 샷의 수행할 때 AD 데이터베이스 또는 RODC IFM 원본 준비의 경우 백업에서 제공 하는 것으로 표시 하려면 자격 증명 데이터베이스에서 제거 포스트 스냅숏 작업을 수행 하려고 합니다.
- 이 태스크에 대 한 스냅숏 볼륨을 탑재 하는 Hyper-v 때 암호화 되지 않은 액세스에 대 한 볼륨의 잠금을 해제는 기능이 없습니다. 따라서 AD 데이터베이스 엔진 데이터베이스에 액세스 실패 하 고 스냅숏을 결국 실패 합니다.

> [!NOTE]
> 이전에 언급 된 보호 된 VM 프로젝트에는 목표를 비 게스트 VM의 최대 데이터 보호용으로 백업 기반 Hyper-v 호스트에 있습니다.

## <a name="backup-and-restore-practices-to-avoid"></a>예방 백업 및 복원 방법

언급 했 듯이 virtual machines에서 실행 하는 도메인 컨트롤러에는 물리적 컴퓨터에서 실행 되는 도메인 컨트롤러에 적용 되지 않는 제한 사항이 있습니다. 다시 설정 하거나 복원할 때 가상 도메인 컨트롤러에는 특정 가상화 소프트웨어 기능 및 사용 하지 않아야 하는 방법

   - 정기 백업을 수행 하는 대신 도메인 컨트롤러의 VHD 파일을 복제 하거나 복사 하지 마십시오. 그 VHD 파일을 복사 하거나 복제를 하는 경우 만료 됩니다. 그런 다음 VHD 표준 모드에서 시작 된 경우 USN 롤백이 발생 합니다. Windows Server Backup 기능을 사용 하는 등 Active Directory Domain Services (AD DS)에서 지원 되는 적절 한 백업 작업을 수행 해야 합니다.  
   - 도메인 컨트롤러로 구성 된 가상 컴퓨터를 복원 하려면 백업으로 스냅숏 기능을 사용 하지 마세요. Windows Server 2008 r2 및 이전에 이전 상태로 가상 컴퓨터를 되돌릴 때 복제를 사용 하 여 문제가 발생 합니다. 자세한 내용은 [USN 및 USN 롤백](#usn-and-usn-rollback)을 참조하세요. 스냅숏을 사용 하 여 읽기 전용 도메인 컨트롤러 (RODC)를 복원 하는 경우에 복제 문제가 발생 하지는, 있지만 이러한 방식의 복원도 권장 되지 않습니다.  

## <a name="restoring-a-virtual-domain-controller"></a>가상 도메인 컨트롤러 복원

를 실패 한 경우 도메인 컨트롤러를 복원 하려면 시스템 상태를 정기적으로 백업 해야 합니다. 시스템 상태는 Active Directory 데이터 및 로그 파일, 레지스트리, 시스템 볼륨 (SYSVOL 폴더) 및 운영 체제의 다양 한 요소를 포함합니다. 이 요구 사항은 실제 및 가상 도메인 컨트롤러에 대해 동일합니다. Active Directory 호환 백업 응용 프로그램을 수행 하는 시스템 상태 복원 프로시저 복제 알림을 포함 하 여 복원 프로세스를 로컬 및 복제 된 Active Directory 데이터베이스의 일관성을 보장 하기 위한 파트너 호출 ID 다시 설정 합니다. 그러나 관리자는 검사 하지 않으려면 가상 호스팅 환경 및 디스크 또는 운영 체제 이미징 응용 프로그램을 사용 하면 및 도메인 컨트롤러 시스템 상태 때 발생 하는 유효성 검사 복원 합니다.

도메인 컨트롤러 가상 컴퓨터가 실패 하 고 가상 컴퓨터를 복원 하기 위한 두 가지 지원 되는 상황을 가지는 업데이트 시퀀스 번호 (USN) 롤백이 발생 하지 않은 경우.

   - 오류가 발생 하는 유효한 시스템 상태 데이터 백업이 있는 경우에 백업을 만드는 데 사용 되는 백업 유틸리티의 복원 옵션을 사용 하 여 시스템 상태를 복원할 수 있습니다. 시스템 상태 데이터 백업을 만들어야은 기본적으로 최대 180 일 삭제 표시 수명, 범위 내에서 Active Directory 호환 백업 유틸리티를 사용 하 여 합니다. 적어도 매 절반 삭제 표시 수명에는 도메인 컨트롤러를 백업 해야 합니다. 포리스트에 대 한 특정 삭제 표시 수명을 결정 하는 방법에 대 한 지침은 [포리스트의 삭제 표시 수명을 결정](https://go.microsoft.com/fwlink/?linkid=137177)합니다.  
   - VHD 파일의 작업 복사본을 사용할 수 있지만 없는 시스템 상태 백업을 사용할 수 없는 경우에 기존 가상 컴퓨터를 제거할 수 있습니다. 이전 복사본은 VHD 사용 하 여 기존 가상 컴퓨터를 복원 하지만에서 디렉터리 서비스 복원 모드 (DSRM)를 시작 하 고 다음 섹션에 설명 된 대로 제대로 레지스트리를 구성 해야 합니다. 표준 모드에서 다음 도메인 컨트롤러를 다시 시작 합니다.

다음 그림에 가상화 된 도메인 컨트롤러를 복원 하는 최상의 방법을 결정 하는 프로세스를 사용 합니다.

![](media\virtualized-domain-controller-architecture\Dd363553.85c97481-7b95-4705-92a7-006e48bc29d0(WS.10).gif)

Rodc에 대해은 복원 프로세스 및 의사 결정은 간단 합니다.

![](media\virtualized-domain-controller-architecture\Dd363553.4c5c5eda-df95-4c6b-84e0-d84661434e5d(WS.10).gif)

## <a name="restoring-the-system-state-backup-of-a-virtual-domain-controller"></a>가상 도메인 컨트롤러의 시스템 상태 백업 복원

도메인 컨트롤러 가상 머신에 대 한 유효한 시스템 상태 백업이 있는 경우 안전 하 게 백업을 복원할 수 있습니다는 백업에 의해 지정 된 복원 절차를 수행 하 여 VHD 파일을 백업 하는 도구입니다.

> [!IMPORTANT]
> 도메인 컨트롤러를 올바르게 복원 하려면 DSRM에서 시작 해야 합니다. 표준 모드에서 시작 하는 도메인 컨트롤러를 허용 하면 안 됩니다. 시스템 시작 중 DSRM를 입력할 수에도 누락 되 면 도메인 컨트롤러의 가상 컴퓨터 끄기 표준 모드에서 완벽 하 게 시작할 수 있습니다. 도메인 컨트롤러가 DSRM에서 시작 해당 Usn 표준 모드 단위로 도메인 컨트롤러를 시작 하기 때문에 도메인 컨트롤러 네트워크에서 연결이 끊긴 경우에 두는 것이 반드시 합니다. USN 롤백에 대 한 자세한 내용은 USN 및 USN 롤백을 참조 하세요. 

## <a name="to-restore-the-system-state-backup-of-a-virtual-domain-controller"></a>가상 도메인 컨트롤러의 시스템 상태 백업을 복원 하려면

1. 도메인 컨트롤러의 가상 머신을 시작 하 고 f5 키를 눌러 Windows 부팅 관리자 화면에 액세스 합니다. 연결 자격 증명을 입력 해야 하는 경우 즉시 클릭 합니다 **일시 중지** 가상 머신에서 단추를 시작 하는 계속 되지 않습니다. 그런 다음 연결 자격 증명을 입력 하 고 클릭 합니다 **재생** 가상 머신에서 단추입니다. 내 가상 머신 창에서 클릭 하 고 f5 키를 누릅니다.

   시작을 완료 하지 않도록 하려면 가상 컴퓨터를 끄는 Windows 부팅 관리자 화면이 표시 되지 않습니다. 표준 모드로 시작 되는 도메인 컨트롤러를 설정 합니다. Windows 부팅 관리자 화면에 액세스할 수 있을 때까지 필요한 만큼이 단계를 반복 합니다. DSRM Windows 오류 복구 메뉴에서 액세스할 수 없습니다. 따라서 가상 머신을 끄고 Windows 오류 복구 메뉴에 표시 되 면 다시 시도 하세요.

2. Windows 부팅 관리자 화면에서 고급 부팅 옵션에 액세스 하려면 F8 키를 누릅니다.
3. 에 **고급 부팅 옵션** 화면에서 **디렉터리 서비스 복원 모드**, 한 다음 ENTER를 누릅니다. 이 도메인 컨트롤러가 DSRM에서 시작 됩니다.
4. 시스템 상태 백업을 만드는 데 사용한 도구에 대 한 적절 한 restore 메서드를 사용 합니다. Windows Server Backup을 사용 하는 경우 참조 [AD DS의 신뢰할 수 없는 복원 수행](https://go.microsoft.com/fwlink/?linkid=132637)합니다.

## <a name="restoring-a-virtual-domain-controller-when-an-appropriate-system-state-data-backup-is-not-available"></a>가상 도메인 컨트롤러를 복원 하는 적절 한 시스템 상태 데이터 백업을 사용할 수 없는 경우

가상 머신 오류 이전에 실행 되는 시스템 상태 데이터 백업이 없으면 가상 컴퓨터에서 실행 되는 도메인 컨트롤러를 복원 하는 이전 VHD 파일을 사용할 수 있습니다. 가능 하면 절차 중 문제가 발생 하거나 파악, 있습니다 수 있도록 다시 복사한 VHD를 사용 하 여 VHD의 복사본을 만듭니다.

> [!IMPORTANT]
> - 하지 대신 다음 절차를 사용 하 여 정기적으로 계획 된 및 예약 된 백업에 대해 고려해 야 합니다.
> - **다음 절차를 사용 하 여 수행 되는 복원에는 Microsoft에서 지원 되지 않습니다 및 다른 대체 방법이 없는 경우에 사용 해야 합니다.**
> - 복원 하려는 VHD의 복사본을 가상 컴퓨터에서 표준 모드에서 시작 된 경우에이 절차를 사용 하지 마십시오.

## <a name="to-restore-a-previous-version-of-a-virtual-domain-controller-vhd-without-system-state-data-backup"></a>시스템 상태 데이터를 백업 하지 않고 가상 도메인 컨트롤러 VHD의 이전 버전을 복원 하려면

1. 이전 섹션에 설명 된 대로 가상 도메인 컨트롤러를 dsrm에서 시작 이전 VHD를 사용 합니다. 표준 모드에서 시작 하는 도메인 컨트롤러를 허용 하지 않습니다. Windows 부팅 관리자 화면을 놓칠 경우 표준 모드에서가 시작 되는 도메인 컨트롤러 가상 머신을 시작을 완료 하지 못하도록를 해제 합니다. DSRM 입력에 대 한 자세한 지침은 이전 섹션을 참조 하세요.
2. 레지스트리 편집기를 엽니다. 레지스트리 편집기를 열려면 **시작**, 클릭 **실행**, 유형 **regedit**, 확인을 클릭 하 고 합니다. **사용자 계정 컨트롤** 대화 상자가 나타나면 원하는 작업이 표시되었는지 확인한 다음 **예**를 클릭합니다. 레지스트리 편집기에서 다음 경로 확장: **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\NTDS\\Parameters**. 라는 값을 검색할 **DSA 이전 복원 카운트**합니다. 값 있으면 설정을 기록해 둡니다. 값 없는 경우, 설정을 기본값인 0 같습니다. 표시 되지 않으면 하나 있는 경우에 값을 추가 하지 마세요.
3. 마우스 오른쪽 단추로 클릭 합니다 **매개 변수** 키를 클릭 **새로 만들기**를 클릭 하 고 **DWORD (32 비트) 값**합니다.
4. 새 이름을 입력 **백업에서 복원 된 데이터베이스**, 한 다음 ENTER를 누릅니다.
5. 두 번 클릭 하 여 방금 만든 값을 **DWORD 편집 (32 비트) 값** 대화 상자에서 및를 입력 한 후 **1** 에 **값 데이터** 상자. 합니다 **백업 항목에서 복원 된 데이터베이스** 옵션은 Windows 2000 Server sp4(서비스 팩 4 (), Windows Server 2003에 포함 된 업데이트를 실행 하는 도메인 컨트롤러에서 사용할 [검색 하는 방법 및 Windows Server 2003, Windows Server 2008 및 Windows Server 2008 R2에서 USN 롤백에서 복구](https://go.microsoft.com/fwlink/?linkid=137182) Windows Server 2008에 설치 된 Microsoft 기술 자료입니다.
6. 표준 모드에서 도메인 컨트롤러를 다시 시작 합니다.
7. 도메인 컨트롤러를 다시 시작 되 면 이벤트 뷰어를 엽니다. 이벤트 뷰어를 열려면 **시작**, **제어판**을 차례로 클릭하고 **관리 도구**를 두 번 클릭한 다음 **이벤트 뷰어**를 두 번 클릭합니다.
8. 확장 **응용 프로그램 및 서비스 로그**를 클릭 하 고는 **Directory Services** 로그 합니다. 이벤트 세부 정보 창에 표시 되는지 확인 합니다.
9. 마우스 오른쪽 단추로 클릭 합니다 **Directory Services** 로깅하고 클릭 **찾을**합니다. **찾을 내용**, 형식 **1109**를 클릭 하 고 **다음 찾기**합니다.
10. 하나 이상의 이벤트 ID 1109 항목이 표시 됩니다. 이 항목에 표시 되지 않는 경우 다음 단계를 진행 합니다. 그렇지 않으면 항목을 두 번 클릭 하 고 업데이트 InvocationID와 하려고 했음을 확인 하는 텍스트를 검토:

   ```
   Active Directory has been restored from backup media, or has been configured to host an application partition. 
   The invocationID attribute for this directory server has been changed. 
   The highest update sequence number at the time the backup was created is <time>

   InvocationID attribute (old value):<Previous InvocationID value>
   InvocationID attribute (new value):<New InvocationID value>
   Update sequence number:<USN>

   The InvocationID is changed when a directory server is restored from backup media or is configured to host a writeable application directory partition.
   ```

11. 이벤트 뷰어를 닫습니다.
12. 값을 확인 하려면 레지스트리 편집기를 사용 **DSA 이전 복원 개수** 은에 1을 더한 이전 값과 같습니다. 올바른 값이 아니면 이벤트 뷰어에서 이벤트 ID 1109에 대 한 진입점을 찾을 수 없는 경우 도메인 컨트롤러의 서비스 팩 최신 인지 확인 합니다. 동일한 VHD에서 다시이 절차를 시도 수 없습니다. 1 단계부터 다시 시작 하 여 표준 모드에서 시작 되지 않은 다른 VHD 또는 VHD의 복사본에서 다시 시도할 수 있습니다.
13. 레지스트리 편집기를 닫습니다.

## <a name="usn-and-usn-rollback"></a>USN 및 USN 롤백

이 섹션에서는 가상 컴퓨터의 이전 버전을 사용 하 여를 사용 하는 잘못 된 복원 Active Directory 데이터베이스의 결과로 발생할 수 있는 복제 문제를 설명 합니다. Active Directory 복제 프로세스에 대 한 자세한 내용은 참조 하세요. [Active Directory 복제 개념](../replication/active-directory-replication-concepts.md)

<!-- Replaced this link with 2016 article: [How the Active Directory Replication Model Works](http://go.microsoft.com/fwlink/?linkid=27636) (http://go.microsoft.com/fwlink/?LinkID=27636). -->

## <a name="usns"></a>Usn

Active Directory Domain Services (AD DS) 사용 (Usn) 도메인 컨트롤러 간의 데이터 복제를 추적 하기 위해 시퀀스 번호를 업데이트 합니다. 데이터 디렉터리에 변경 될 때마다 변경 된 것을 나타내려면 USN 증가 됩니다.

대상 도메인 컨트롤러를 저장 하는 각 디렉터리 파티션에 대 한 Usn 도메인 컨트롤러의 복제본을 저장 하는 다른 모든 도메인 컨트롤러의 상태 뿐만 아니라 해당 데이터베이스를 소개 하는 원래 최신 업데이트를 추적에 사용 되는 디렉터리 파티션입니다. 서로 변경 내용을 복제 하는 도메인 컨트롤러를 복제 파트너가 변경에 대 한 도메인 컨트롤러는 각 파트너 로부터 받은 마지막 변경의 USN 보다 큰 Usn 사용 하 여 쿼리 합니다.

다음 두 복제 메타 데이터 테이블 Usn을 포함 합니다. 원본 및 대상 도메인 컨트롤러를 사용 하 여 대상 도메인 컨트롤러에서 필요한 업데이트를 필터링 합니다.

1. **최신 벡터가**: 모든 원본 도메인 컨트롤러에서 받은 원래 업데이트를 추적 하는 것에 대 한 대상 도메인 컨트롤러 유지 관리 하는 테이블입니다. 변경 되 면을 대상 도메인 컨트롤러 요청 디렉터리 파티션에 대 한 최신 벡터 원본 도메인 컨트롤러를 제공 합니다. 원본 도메인 컨트롤러는 다음 대상 도메인 컨트롤러에 전송 하는 업데이트를 필터링 하려면이 값을 사용 합니다. 원본 도메인 컨트롤러는 성공적인 복제 주기가 완료 될 때 대상에 대상 도메인 컨트롤러에 모든 도메인 컨트롤러와 동기화 되었음을 알고 있는 보장 하기 위해 최신 벡터를 보냅니다. 원래 업데이트 및 업데이트 소스와 같은 수준에 있습니다.  
2. **상위 워터 마크**: 특정 파티션에 대 한 특정 원본 도메인 컨트롤러 로부터 받은 최근 변경 내용을 추적 하는 대상 도메인 컨트롤러 유지 관리 하는 값입니다. 상위 워터 마크는 대상 도메인 컨트롤러에서 이미 수신 하는 변경 내용을 전송에서 원본 도메인 컨트롤러를 방지 합니다.  

## <a name="directory-database-identity"></a>디렉터리 데이터베이스 id

Usn 외에도 도메인 컨트롤러의 원본 복제 파트너 디렉터리 데이터베이스를 추적 유지 합니다. 서버에서 실행 디렉터리 데이터베이스의 id는 서버 개체 자체의 id에서 별도로 유지 됩니다. 각 도메인 컨트롤러의 데이터베이스 id를 디렉터리에 저장 합니다 **invocationID** 다음 LDAP Lightweight Directory Access Protocol () 경로 아래에 위치한 NTDS 설정 개체의 특성: cn = NTDS 설정, cn = ServerName, cn = Servers, cn =*SiteName*, cn sites, cn = Configuration, dc =*포리스트 루트 도메인*합니다. 서버 개체 id에 저장 합니다 **objectGUID** NTDS 설정 개체의 특성입니다. 서버 개체의 id가 변경 되지 않습니다. 그러나 디렉터리 데이터베이스 변경의 id 시스템 상태 복원 프로시저를 서버에서 발생 하는 경우 응용 프로그램 디렉터리 파티션을 추가 되 면 제거 후 및 나중에 서버에서 다시 추가 합니다. (다른 시나리오: 게스트 자체 VSS 기록기 (백업/복원 위의에서 사용 하는 동일한 메커니즘)를 다시 트리거합니다 HyperV 인스턴스 가상 DC의 VHD를 포함 하는 파티션에 VSS 기록기를 트리거하는 경우 invocationID가 사용 되는 다른 방법의 결과 다시 설정)

따라서 **invocationID** directory 데이터베이스의 특정 버전을 사용 하 여 도메인 컨트롤러에 업데이트 시작 집합을 효과적으로 연결 합니다. 최신 벡터가 및 최대 허용 테이블 사용을 표시 합니다 **invocationID** 및 해당 도메인 컨트롤러에서 Active Directory의 어떤 사본을 알고 데이터베이스 복제 정보를 하므로 각각 DC GUID 제공 될 예정입니다.

합니다 **invocationID** 명령을 실행 한 후 출력의 위쪽에 표시 되는 전역적으로 고유 식별자 (GUID) 값인 **repadmin /showrepl**합니다. 다음 텍스트는 명령의 예제 출력을 나타냅니다.

   ```
   Repadmin: running command /showrepl against full DC local host
   Default-First-Site-Name\VDC1
   DSA Options: IS_GC
   DSA object GUID: 966651f3-a544-461f-9f2c-c30c91d17818
   DSA invocationID: b0d9208b-8eb6-4205-863d-d50801b325a9
   ```

AD DS 도메인 컨트롤러에서 올바르게 복원 되는 **invocationID** 다시 설정 됩니다. 이 변경으로 인해 복제 되 고 파티션의 크기를 기준으로 하는 동안은 복제 트래픽 증가 경험

예를 들어 VDC1 및 DC2는 동일한 도메인에 두 명의 도메인 컨트롤러를 가정 합니다. 다음 그림 VDC1에 대 한 DC2 맞추고 데이터 조작을 invocationID 값 복원 적절 한 상황에서 재설정 될 때입니다.

![](media\virtualized-domain-controller-architecture\Dd363553.ca71fc12-b484-47fb-991c-5a0b7f516366(WS.10).gif)

## <a name="usn-rollback"></a>USN 롤백

Usn의 일반 업데이트는 손상 하 고 도메인 컨트롤러는 최신 업데이트 보다 낮은 USN을 사용 하려고 USN 롤백이 발생 합니다. USN 롤백이 검색 되 고 대부분의 경우에서 포리스트의 확산을 만들기 전에 복제 중지 됩니다. 

USN 롤백이 발생할 수 있습니다 다양 한 방법으로 예를 들어, 기존 가상 하드 디스크 (VHD) 파일을 사용 하거나 물리적-가상 컴퓨터로 변환 ((p2v 변환)는 물리적 컴퓨터에 유지 된다는 오프 라인 영구적으로 변환한 후 확인 하지 않고 수행 됩니다. USN 롤백이 발생 하지 않습니다 수 있도록 다음 예방 조치를 수행 합니다.

   - Windows Server 2012 이상을 실행 하지를 수행 하지 않거나 도메인 컨트롤러 가상 머신의 스냅숏을 사용 합니다.
   - 도메인 컨트롤러 VHD 파일을 복사 하지 않습니다.  
   - Windows Server 2012 이상을 실행 하지, 도메인 컨트롤러를 실행 하는 가상 컴퓨터를 내보내지 마세요.  
   - Windows Server Backup 등 지원 되는 백업 솔루션에 비해 다른 방법으로 Active Directory 데이터베이스의 내용을 롤백하기 하거나 도메인 컨트롤러를 복원 하지 마십시오.  

일부 경우에서 USN 롤백이 감지 되지 않은 이동할 수 있습니다. 다른 경우에 다른 복제 오류가 발생할 수 있습니다 것입니다. 이러한 경우 문제의 범위를 식별 하 고 적시에 처리 하는 데 필요한 됩니다. USN 롤백은 인해 발생할 수 있는 느린 개체를 제거 하는 방법에 대 한 정보를 참조 하세요 [Windows Server 2003에서 이벤트 ID 1988를 생성 하는 오래 된 Active Directory 개체](https://go.microsoft.com/fwlink/?linkid=137185) Microsoft 기술 자료에서 합니다.

## <a name="usn-rollback-detection"></a>USN 롤백이 감지

대부분의 경우, 해당 하지 않고 USN 롤백의 재설정를 **invocationID** 프로시저 검색 된 잘못 된 복원으로 인해 발생 합니다. 잘못 된 도메인 컨트롤러를 복원 작업 후 Windows Server 2008 부적절 한 복제에 대 한 보호를 제공 합니다. 이러한 보호는 잘못 된 복원 작업을 결과 파트너 이미 받은 복제에는 변경 나타내는 원래 낮은 Usn에서 팩트가 트리거됩니다.

Windows Server 2008 및 Windows Server 2003 SP1에서 이전에 사용한 USN을 사용 하 여 대상 도메인 컨트롤러 요청 변경 되 면 해당 원본 복제 파트너 응답 해석 되며 대상 도메인 컨트롤러에 복제 하는 것을 의미합니다 메타 데이터가 오래 되었습니다. 이 원본 도메인 컨트롤러에서 Active Directory 데이터베이스 롤백된 이전 상태를 나타냅니다. 예를 들어, 가상 컴퓨터의 VHD 파일을 이전 버전으로 다시 롤백 되었습니다. 이 경우 대상 도메인 컨트롤러 복원 하는 경우 잘못 된 종류 것으로 확인 된 도메인 컨트롤러에서 다음과 같은 격리 조치를 시작 합니다.

   - AD DS 사용자 계정 및 컴퓨터 계정은 계정 암호를 변경 하지 못하게 하는 Net Logon 서비스가 일시 중지 합니다. 이 작업 잘못 복원 후 발생 하는 경우 이러한 변경 내용이 손실 되지 않도록 합니다.  
   - AD DS는 인바운드 및 아웃 바운드 Active Directory 복제를 해제 합니다.  
   - AD DS의 상태를 표시 하는 디렉터리 서비스 이벤트 로그에서 이벤트 ID 2095를 생성 합니다.  

다음 그림에서는 vdc2, 즉 제공 되는 가상 컴퓨터에서 실행 되는 대상 도메인 컨트롤러에서 USN 롤백이 감지 된 때 발생 하는 이벤트의 순서를 보여 줍니다. 이 그림에서 USN 롤백이 감지 미치는 VDC2 VDC2 VDC2의 데이터베이스가 롤백되어 나타내는 대상 도메인 컨트롤러에 게 이전에 표시 된 최신 USN 값을 전송한는 복제 파트너를 감지할 때 시간에 부적절 하 게 합니다.

![](media\virtualized-domain-controller-architecture\\Dd363553.373b0504-43fc-40d0-9908-13fdeb7b3f14(WS.10).gif)

디렉터리 서비스 이벤트 로그에서 이벤트 ID 2095를 보고 즉시 다음 절차를 완료 합니다.

## <a name="to-resolve-event-id2095"></a>이벤트 ID 2095를 해결 하려면

1. 네트워크에서 오류를 기록 하는 가상 컴퓨터를 격리 합니다.
2. 변경 내용을이 도메인 컨트롤러에서 발생 한 다른 도메인 컨트롤러에 전파 여부를 확인 하려고 시도 합니다. 이벤트 스냅숏의 결과 또는 시작 되 고 가상 컴퓨터의 복사본 인 경우 USN 롤백이 발생 한 시간을 확인 하려고 합니다. 그런 다음 복제 이후 발생 했는지 여부를 확인 하려면 해당 도메인 컨트롤러의 복제 파트너를 확인할 수 있습니다.

   이 확인 하기 위해 Repadmin 도구를 사용할 수 있습니다. Repadmin을 사용 하는 방법에 대 한 정보를 참조 하세요 [모니터링 및 문제 해결 Active Directory 복제를 사용 하 여 Repadmin](https://go.microsoft.com/fwlink/?linkid=122830)합니다. 이 작업을 직접 확인할 수 없는 경우에 문의 [Microsoft 지원](https://support.microsoft.com) 지원 합니다.

3. 도메인 컨트롤러를 강제로 수준을 내립니다. 도메인 컨트롤러의 메타 데이터를 정리 하 고 작업 마스터 (라고도 신축 단일 마스터 작업 또는 FSMO) 역할을 점유 해야 합니다. 자세한 내용은 "USN 롤백이에서 복구" 섹션을 참조 하세요 [검색 하 고 Windows Server 2003, Windows Server 2008 및 Windows Server 2008 R2에서 USN 롤백에서 복구 하는 방법을](https://go.microsoft.com/fwlink/?linkid=137182) Microsoft 기술 자료에서 합니다.
4. 도메인 컨트롤러에 대 한 모든 이전 VHD 파일을 삭제 합니다.

## <a name="undetected-usn-rollback"></a>USN 롤백이 감지 되지 않은

두 가지 상황 중 하나에서 USN 롤백이 발견 될 수 있습니다.

1. VHD 파일을 동시에 여러 위치에서 실행 중인 다른 가상 컴퓨터에 연결 됩니다.  
2. 복원 된 도메인 컨트롤러에서 USN 다른 도메인 컨트롤러에 받은 마지막 USN 지난 증가 했습니다.  

첫 번째 상황에서 다른 도메인 컨트롤러 가상 컴퓨터 중 하나를 사용 하 여 복제할 수 있습니다 하 고 변경 내용을 다른 복제 하지 않고 가상 컴퓨터 중 하나에서 발생할 수 있습니다. 포리스트의이 확산 감지 하기가 어렵습니다. 및 예측할 수 없는 디렉터리 응답 하면 합니다. 물리적 및 가상 컴퓨터는 동일한 네트워크에서 실행 되는 경우이 이런 P2V 마이그레이션 후 발생할 수 있습니다. 여러 가상 도메인 컨트롤러 같은 실제 도메인 컨트롤러에서 생성 되며 그런 다음 동일한 네트워크에서 실행 하는 경우에 발생할 수 있습니다이 합니다.

두 번째 상황에서 Usn 범위에는 서로 다른 두 변경 집합에 적용 됩니다. 이 검색 되지 않고 오랫동안 계속 수 있습니다. 해당 시간 중에 생성 된 개체를 수정할 때마다 느린 개체가 감지 되 고 이벤트 뷰어에서 이벤트 ID 1988으로 보고 합니다. 다음 그림에서는 USN 롤백이 이러한 상황이 발생에서 검색 되지 않을 수 있습니다 하는 방법을 보여 줍니다.

![](media\virtualized-domain-controller-architecture\Dd363553.63565fe0-d970-4b4e-b5f3-9c76bc77e2d4(WS.10).gif)

## <a name="read-only-domain-controllers"></a>읽기 전용 도메인 컨트롤러

Rodc는 Active Directory 데이터베이스의 파티션에 읽기 전용 복사본을 호스트 하는 도메인 컨트롤러입니다. Rodc는 다른 도메인 컨트롤러에 변경 내용을 복제 하지 때문에 대부분의 USN 롤백 문제를 방지 합니다. 그러나 RODC에 영향을 받은 USN 롤백에 쓰기 가능한 도메인 컨트롤러에서 복제 RODC도 받게 됩니다.

스냅숏을 사용 하 여 RODC를 복원 하는 것은 좋지 않습니다. Active Directory 호환 백업 응용 프로그램을 사용 하 여 RODC를 복원 합니다. 또한 쓰기 가능한 도메인 컨트롤러와 마찬가지로 기울여야 삭제 표시 수명 이상 오프 라인으로 RODC를 허용 하지 않도록 합니다. 이 문제는 RODC에 느린 개체에 발생할 수 있습니다.

Rodc에 대 한 자세한 내용은 참조는 [읽기 전용 도메인 컨트롤러 계획 및 배포 가이드](../../deploy/rodc/read-only-domain-controller-updates.md)합니다.