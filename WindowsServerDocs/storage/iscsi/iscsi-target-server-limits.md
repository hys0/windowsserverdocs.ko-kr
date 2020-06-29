---
title: iSCSI 대상 서버 확장성 제한
TOCTitle: iSCSI Target Server Scalability Limits
ms.prod: windows-server
ms.technology: storage-iscsi
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 09/11/2018
ms.openlocfilehash: 6799e0e3b47d6cc98cbb42407ffbed1a9578675a
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473440"
---
# <a name="iscsi-target-server-scalability-limits"></a>iSCSI 대상 서버 확장성 제한

적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 Windows Server에서 지원 되 고 테스트 된 Microsoft iSCSI 대상 서버 제한을 제공 합니다. 다음 표에서는 테스트 된 지원 제한과 해당 하는 경우 제한이 적용 되는지 여부를 표시 합니다.

## <a name="general-limits"></a>일반 제한

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>항목</p></th>
<th><p>지원 제한</p></th>
<th><p>강제적?</p></th>
<th><p>주석</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>iSCSI 대상 서버당 iSCSI 대상 인스턴스</p></td>
<td><p>256</p></td>
<td><p>No</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>iscsi 대상 서버당 Lu (iSCSI 논리 단위) 또는 가상 디스크</p></td>
<td><p>512</p></td>
<td><p>No</p></td>
<td><p>포함 된 테스트 구성: 평균 64의 평균을 가진 대상 인스턴스당 8 Lu, 대상 당 LU가 하나씩 있는 256 대상 인스턴스</p></td>
</tr>
<tr class="odd">
<td><p>iscsi 대상 인스턴스당 iSCSI Lu 또는 가상 디스크</p></td>
<td><p>256 (Windows Server 2012의 경우 128)</p></td>
<td><p>Yes</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>ISCSI 대상 인스턴스에 동시에 연결할 수 있는 세션</p></td>
<td><p>544 (Windows Server 2012의 경우 512)</p></td>
<td><p>Yes</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>LU 당 스냅숏</p></td>
<td><p>512</p></td>
<td><p>Yes</p></td>
<td><p>독립 iSCSI 응용 프로그램 볼륨당 512 스냅숏의 제한이 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>저장소 어플라이언스 당 로컬로 탑재 된 가상 디스크 또는 스냅숏</p></td>
<td><p>32</p></td>
<td><p>Yes</p></td>
<td><p>로컬로 탑재 된 가상 디스크는 모든 iSCSI 관련 기능을 제공&#39;않으며 사용 되지 않습니다. 자세한 내용은 <a href="https://technet.microsoft.com/library/dn303411.aspx">Windows Server 2012 r 2에서 제거 되었거나 더 이상 사용 되지 않는 기능</a>을 참조 하세요.</p></td>
</tr>
</tbody>
</table>

## <a name="fault-tolerance-limits"></a>내결함성 제한

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>항목</p></th>
<th><p>지원 제한</p></th>
<th><p>강제적?</p></th>
<th><p>주석</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>장애 조치 (Failover) 클러스터 노드</p></td>
<td><p>8 (Windows Server 2012에서 5)</p></td>
<td><p>No</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>여러 활성 클러스터 노드</p></td>
<td><p>지원됨</p></td>
<td>
<p>해당 없음</p></td>
<td><p>장애 조치 (failover) 클러스터의 각 활성 노드는 가능한 소유자 노드 역할을 하는 다른 노드와 다른 iSCSI 대상 서버 클러스터형 인스턴스를 소유 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>오류 복구 수준 (ERL)</p></td>
<td><p>0</p></td>
<td><p>Yes</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>세션당 연결 수</p></td>
<td><p>1</p></td>
<td><p>예</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>ISCSI 대상 인스턴스에 동시에 연결할 수 있는 세션</p></td>
<td><p>544 (Windows Server 2012의 경우 512)</p></td>
<td><p>No</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>MPIO (다중 경로 입/출력)</p></td>
<td><p>지원됨</p></td>
<td><p>해당 없음</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>MPIO 경로</p></td>
<td><p>4</p></td>
<td><p>예</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>독립 실행형 iSCSI 대상 서버를 클러스터링 된 iSCSI 대상 서버로 변환 하거나 그 반대로 변환</p></td>
<td><p>지원되지 않음</p></td>
<td><p>No</p></td>
<td><p>스냅숏 메타 데이터를 포함 한 iSCSI 대상 인스턴스 및 가상 디스크 구성 데이터는 변환 중에 손실 됩니다.</p></td>
</tr>
</tbody>
</table>

## <a name="network-limits"></a>네트워크 제한

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>항목</p></th>
<th><p>지원 제한</p></th>
<th><p>강제적?</p></th>
<th><p>주석</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>최대 활성 네트워크 어댑터 수</p></td>
<td><p>8</p></td>
<td><p>No</p></td>
<td><p>어플라이언스의 총 네트워크 어댑터 수가 아니라 iSCSI 트래픽에 전용으로 적용 되는 네트워크 어댑터에 적용 됩니다.</p></td>
</tr>
<tr class="even">
<td><p>지원 되는 포털 (IP 주소)</p></td>
<td><p>64</p></td>
<td><p>Yes</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>네트워크 포트 속도</p></td>
<td><p>1Gbps, 10gbps, 40Gbps, 56 Gbps (Windows Server 2012 R2 이상에만 해당)</p></td>
<td><p>No</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>IPv4</p></td>
<td><p>지원됨</p></td>
<td><p>해당 없음</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>IPv6</p></td>
<td><p>지원됨</p></td>
<td><p>해당 없음</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>TCP 오프 로드</p></td>
<td><p>지원됨</p></td>
<td><p>해당 없음</p></td>
<td><p>대량 전송 (조각화), 체크섬, 인터럽트 중재 및 RSS 오프 로드 활용</p></td>
</tr>
<tr class="odd">
<td><p>iSCSI 오프 로드</p></td>
<td><p>지원되지 않음</p></td>
<td><br/><p>해당 없음</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Jumbo 프레임</p></td>
<td><p>지원됨</p></td>
<td><p>해당 없음</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>IPSec</p></td>
<td><p>지원됨</p></td>
<td><p>해당 없음</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>CRC 오프 로드</p></td>
<td><p>지원됨</p></td>
<td><p>해당 없음</p></td>
<td></td>
</tr>
</tbody>
</table>

## <a name="iscsi-virtual-disk-limits"></a>iSCSI 가상 디스크 제한

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>항목</p></th>
<th><p>지원 제한</p></th>
<th><p>강제적?</p></th>
<th><p>주석</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ISCSI 초기자에서 기본 디스크의 가상 디스크를 동적 디스크로 변환 </p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>가상 하드 디스크 형식</p></td>
<td><p>.vhdx (Windows Server 2012 R2 이상에만 해당)</p>
<p>.vhd</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>VHD 최소 형식 크기</p></td>
<td><p>.vhdx: 3MB</p>
<p>.vhd: 8mb</p></td>
<td><p>Yes</p></td>
<td><p>모든 지원 되는 VHD 형식 (부모, 차이점 보관용 및 고정)에 적용 됩니다.</p></td>
</tr>
<tr class="even">
<td><p>부모 VHD 최대 크기</p></td>
<td><p>.vhdx: 64 TB</p>
<p>.vhd: 2tb</p></td>
<td><p>Yes</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>고정 VHD 최대 크기</p></td>
<td><p>.vhdx: 64 TB</p>
<p>.vhd: 16TB</p></td>
<td><p>Yes</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>차이점 보관용 VHD 최대 크기</p></td>
<td><p>.vhdx: 64 TB</p>
<p>.vhd: 2tb</p></td>
<td><p>Yes</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>VHD 고정 형식</p></td>
<td><p>지원됨</p></td>
<td><p>No</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>VHD 차이점 보관용 형식</p></td>
<td><p>지원됨</p></td>
<td><p>No</p></td>
<td><p>스냅숏은 차이점 보관용 VHD 기반 iSCSI 가상 디스크를 만들 수 없습니다.</p></td>
</tr>
<tr class="odd">
<td><p>부모 VHD 당 차이점 보관용 Vhd 수</p></td>
<td><p>256</p></td>
<td><p>아니요 (Windows Server 2012에 대 한 예)</p></td>
<td><p>.Vhdx 파일의 경우 두 수준의 깊이 (손자 파일)가 최대입니다. 하나는 .vhd 파일의 최대 수준 (즉, 하위 .vhd 파일)입니다.</p></td>
</tr>
<tr class="even">
<td><p>VHD 동적 형식</p></td>
<td><p>.vhdx: 예</p>
<p>.vhd: 예 (Windows Server 2012의 경우 아니요)</p></td>
<td><p>Yes</p></td>
<td><p>매핑 해제&#39;t가 지원 됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>exFAT/FAT32/FAT (VHD의 호스팅 볼륨)</p></td>
<td><p>지원되지 않음</p></td>
<td><p>예</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>CSV v2</p></td>
<td><p>지원되지 않음</p></td>
<td><p>예</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>ReFS</p></td>
<td><p>지원됨</p></td>
<td><p>해당 없음</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>NTFS</p></td>
<td><p>지원됨</p></td>
<td><p>해당 없음</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>타사 CFS</p></td>
<td><p>지원되지 않음</p></td>
<td><p>예</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>씬 프로비저닝</p></td>
<td><p>예</p></td>
<td><p>해당 없음</p></td>
<td><p>동적 Vhd는 지원 되지만 매핑 해제는 지원 되지&#39;.</p></td>
</tr>
<tr class="odd">
<td><p>논리 단위 축소</p></td>
<td><p>예 (Windows Server 2012 R2 이상에만 해당)</p></td>
<td><p>해당 없음</p></td>
<td><p><a href="https://docs.microsoft.com/powershell/module/iscsitarget/resize-iscsivirtualdisk">Convert-iscsivirtualdisk</a> 를 사용 하 여 LUN을 축소 합니다.</p></td>
</tr>
<tr class="even">
<td><p>논리 단위 복제</p></td>
<td><p>지원되지 않음</p></td>
<td><p>해당 없음</p></td>
<td><p>차이점 보관용 Vhd를 사용 하 여 디스크 데이터를 빠르게 복제할 수 있습니다.</p></td>
</tr>
</tbody>
</table>

## <a name="snapshot-limits"></a>스냅샷 제한 사항

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>항목</p></th>
<th><p>지원 제한</p></th>
<th><p>주석</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>스냅숏 만들기</p></td>
<td><p>지원됨</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>스냅샷 복원</p></td>
<td><p>지원됨</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>쓰기 가능한 스냅숏</p></td>
<td><p>지원되지 않음</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>스냅숏 – 전체로 변환</p></td>
<td><p>지원되지 않음</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>스냅숏 – 온라인 롤백</p></td>
<td><p>지원되지 않음</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Snapshot – 쓰기 가능으로 변환</p></td>
<td><p>지원되지 않음</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>스냅숏-리디렉션</p></td>
<td><p>지원되지 않음</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>스냅숏-고정</p></td>
<td><p>지원되지 않음</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>로컬 탑재</p></td>
<td><p>지원됨</p></td>
<td><p>로컬로 탑재 된 iSCSI 가상 디스크는 더 이상 사용 되지 않습니다. 자세한 내용은 <a href="https://technet.microsoft.com/library/dn303411.aspx">Windows Server 2012 r 2에서 제거 되었거나 더 이상 사용 되지 않는 기능</a>을 참조 하십시오. 동적 디스크 스냅숏은 로컬로 탑재할 수 없습니다.</p></td>
</tr>
</tbody>
</table>

## <a name="iscsi-target-server-manageability-and-backup"></a>iSCSI 대상 서버 관리 효율성 및 백업

응용 프로그램 서버에서 iSCSI 가상 디스크에 대 한 데이터의 볼륨 섀도 복사본 (VSS open file 스냅숏)을 만들려는 경우 또는 VDS (가상 디스크 서비스) 하드웨어 공급자가 필요한 이전 앱 (예: Diskraid 명령)을 사용 하 여 iSCSI 가상 디스크를 관리 하려면 스냅숏을 만들거나 VDS 관리 앱을 사용 하려는 서버에 iSCSI 대상 저장소 공급자를 설치 합니다.

ISCSI 대상 저장소 공급자는 Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012의 역할 서비스입니다. iSCSI 대상 서버가 Windows Server 2012에서 실행 되는 경우 다음 운영 체제에서 [하위 수준 응용 프로그램 서버에 대 한 Iscsi 대상 저장소 공급자 (VDS/VSS)](https://www.microsoft.com/download/details.aspx?id=34759) 를 다운로드 하 여 설치할 수도 있습니다.

  - Windows Storage Server 2008 R2

  - Windows Server 2008 R2

  - Windows HPC 서버 2008 R2

  - Windows HPC Server 2008

ISCSI 대상 서버가 Windows Server 2012 R2 이상을 실행 하는 서버에서 호스트 되 고 원격 서버에서 VSS 또는 VDS를 사용 하려는 경우 원격 서버 에서도 동일한 버전의 Windows Server를 실행 하 고 iSCSI 대상 저장소 공급자 역할 서비스를 설치 해야 합니다. 또한 모든 버전의 Windows에서 특정 버전의 iSCSI 대상 저장소 공급자 역할 서비스를 설치 해야 합니다.

ISCSI 대상 저장소 공급자에 대 한 자세한 내용은 [Iscsi 대상 저장소 (VDS/VSS) 공급자](https://blogs.technet.com/b/filecab/archive/2012/10/08/iscsi-target-storage-vds-vss-provider.aspx)를 참조 하십시오.

## <a name="tested-compatibility-with-iscsi-initiators"></a>ISCSI 초기자와의 테스트 된 호환성

다음 iSCSI 초기자를 사용 하 여 iSCSI 대상 서버 소프트웨어를 테스트 했습니다.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>시작자</p></td>
<td><p>Windows Server 2012 R2</p></td>
<td><p>Windows Server 2012</p></td>
<td><p>의견</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012 R2</p></td>
<td><p>유효성 검사</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows Server 2003</p></td>
<td><p>유효성 검사</p></td>
<td><p>유효성 검사</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>VMWare vSphere 5</p></td>
<td></td>
<td><p>유효성 검사</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>VMWare ESXi 5.0</p></td>
<td><p>유효성 검사</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>VMWare ESX 4.1</p></td>
<td><p>유효성 검사</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>CentOS 6.x</p></td>
<td><p>유효성 검사</p></td>
<td></td>
<td><p>에서 세션을 로그 아웃 했다가 다시 로그인 하 여 크기 조정 된 가상 디스크를 검색 해야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>Red Hat Enterprise Linux 6</p></td>
<td><p>유효성 검사</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>RedHat Enterprise Linux 5 및 5</p></td>
<td><p>유효성 검사</p></td>
<td><p>유효성 검사</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>SUSE Linux Enterprise Server 10</p></td>
<td></td>
<td><p>유효성 검사</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Oracle Solaris 11.x</p></td>
<td><p>유효성 검사</p></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

ISCSI 대상 서버에서 호스트 되는 가상 디스크에서 디스크 없는 부팅을 수행 하는 다음 iSCSI 초기자도 테스트 했습니다.

  - Windows Server 2012 R2

  - Windows Server 2012

  - IPXE를 사용한 PCIe NIC

  - IPXE를 사용 하는 CD 또는 USB 디스크

## <a name="additional-references"></a>추가 참조

다음 목록에서는 iSCSI 대상 서버 및 관련 기술에 대한 추가 리소스를 제공합니다.

- [iSCSI 대상 블록 저장소 개요](iscsi-target-server.md)

- [iSCSI Target Boot Overview](iscsi-boot-overview.md)

- [Windows Server의 스토리지](../storage.yml)

