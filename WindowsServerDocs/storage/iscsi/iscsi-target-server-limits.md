---
title: iSCSI 대상 서버 확장성 제한
TOCTitle: iSCSI Target Server Scalability Limits
ms.prod: windows-server-threshold
ms.technology: storage-iscsi
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 09/11/2018
ms.openlocfilehash: d912047ab0e3136c6dc05064f3a28aaaafd36c79
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447719"
---
# <a name="iscsi-target-server-scalability-limits"></a>iSCSI 대상 서버 확장성 제한

적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 Windows Server에서 지원 되는 테스트를 거친 Microsoft iSCSI 대상 서버 제한 제공합니다. 다음 표에서 테스트 지원 제한 및 제한 사항 적용 되는지 여부를 해당 하는 경우.

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
<th><p>적용 되나요?</p></th>
<th><p>설명</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>iSCSI 대상 서버 당 iSCSI 대상 인스턴스</p></td>
<td><p>256</p></td>
<td><p>아니요</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>iSCSI 대상 서버 당 가상 디스크 또는 iSCSI Lu (논리 단위)</p></td>
<td><p>512</p></td>
<td><p>아니오</p></td>
<td><p>포함 된 테스트 구성: 평균 64 개 대상으로 사용 하 여 대상 인스턴스와 대상 마다 한 LU 사용 하 여 256 대상 인스턴스 당 8 Lu 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>iSCSI Lu 또는 당 iSCSI 가상 디스크 인스턴스 대상</p></td>
<td><p>256 (Windows Server 2012에서 128)</p></td>
<td><p>예</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>ISCSI 대상 인스턴스에 동시에 연결할 수 있는 세션</p></td>
<td><p>544 (Windows Server 2012에서 512)</p></td>
<td><p>예</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>LU 당 스냅숏</p></td>
<td><p>512</p></td>
<td><p>예</p></td>
<td><p>독립적 iSCSI 응용 프로그램에 대 한 볼륨당 512 스냅숏 제한이 됩니다.</p></td>
</tr>
<tr class="even">
<td><p>로컬 탑재 된 가상 디스크 또는 저장소 어플라이언스 당 스냅숏</p></td>
<td><p>32</p></td>
<td><p>예</p></td>
<td><p>로컬 가상 디스크 don 탑재 된&#39;t 제품 모든 iSCSI 관련 기능과 사용 되지 않음-자세한 내용은 참조 <a href="https://technet.microsoft.com/library/dn303411.aspx">Features Removed or Deprecated in Windows Server 2012 R2</a>합니다.</p></td>
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
<th><p>적용 되나요?</p></th>
<th><p>설명</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>장애 조치 클러스터 노드</p></td>
<td><p>8 (Windows Server 2012에서 5)</p></td>
<td><p>아니요</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>여러 활성 클러스터 노드</p></td>
<td><p>지원됨</p></td>
<td> 
<p>해당 사항 없음</p></td>
<td><p>장애 조치 클러스터의 각 활성 노드 역할을 가능한 소유자 노드에서 다른 노드와 다른 iSCSI 대상 서버 클러스터 된 인스턴스를 소유 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>오류 복구 수준 (ERL)</p></td>
<td><p>0</p></td>
<td><p>예</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>세션당 연결</p></td>
<td><p>1</p></td>
<td><p>예</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>ISCSI 대상 인스턴스에 동시에 연결할 수 있는 세션</p></td>
<td><p>544 (Windows Server 2012에서 512)</p></td>
<td><p>아니오</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>다중 경로 입/출력 (MPIO)</p></td>
<td><p>지원됨</p></td>
<td><p>해당 사항 없음</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>MPIO 경로</p></td>
<td><p>4</p></td>
<td><p>아니오</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>ISCSI 대상 서버를 독립 실행형 클러스터 된 iSCSI 대상 서버 하거나 그 반대 방향으로 변환</p></td>
<td><p>지원되지 않음</p></td>
<td><p>아니요</p></td>
<td><p>ISCSI 대상 인스턴스 및 가상 디스크 스냅숏 메타 데이터를 포함 하 여 구성 데이터를 변환 하는 동안 손실 됩니다.</p></td>
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
<th><p>적용 되나요?</p></th>
<th><p>설명</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>활성 네트워크 어댑터의 최대 수</p></td>
<td><p>8</p></td>
<td><p>아니오</p></td>
<td><p>어플라이언스의 네트워크 어댑터의 총 것이 아니라 iSCSI 트래픽 전용 네트워크 어댑터에 적용 됩니다.</p></td>
</tr>
<tr class="even">
<td><p>포털 (IP 주소) 지원</p></td>
<td><p>64</p></td>
<td><p>예</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>네트워크 포트 속도</p></td>
<td><p>1Gbps, 10gbps 40Gbps, 56 Gbps (Windows Server 2012 R2 이상만)</p></td>
<td><p>아니오</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>IPv4</p></td>
<td><p>지원됨</p></td>
<td><p>해당 사항 없음</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>IPv6</p></td>
<td><p>지원됨</p></td>
<td><p>해당 사항 없음</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>TCP 오프 로드</p></td>
<td><p>지원됨</p></td>
<td><p>해당 사항 없음</p></td>
<td><p>큰 (구분), 체크섬, 인터럽트 조절을 보내고 RSS 오프 로드를 활용 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>iSCSI 오프 로드</p></td>
<td><p>지원되지 않음</p></td>
<td><br/><p>해당 사항 없음</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Jumbo 프레임</p></td>
<td><p>지원됨</p></td>
<td><p>해당 사항 없음</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>IPSec</p></td>
<td><p>지원됨</p></td>
<td><p>해당 사항 없음</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>CRC 오프 로드</p></td>
<td><p>지원됨</p></td>
<td><p>해당 사항 없음</p></td>
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
<th><p>적용 되나요?</p></th>
<th><p>설명</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>기본 디스크에서 가상 디스크를 동적 디스크로 변환 하는 iSCSI 초기자에서 </p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>가상 하드 디스크 형식</p></td>
<td><p>.vhdx (Windows Server 2012 R2 이상만)</p>
<p>.vhd</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>VHD 형식으로 최소 크기</p></td>
<td><p>.vhdx: 3MB</p>
<p>.vhd: 8MB</p></td>
<td><p>예</p></td>
<td><p>모든 지원 되는 VHD 형식에 적용: 부모 차이점 보관용 및 고정 합니다.</p></td>
</tr>
<tr class="even">
<td><p>부모 VHD의 최대 크기</p></td>
<td><p>.vhdx: 64TB</p>
<p>.vhd: 2TB</p></td>
<td><p>예</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>고정된 VHD의 최대 크기</p></td>
<td><p>.vhdx: 64TB</p>
<p>.vhd: 16TB</p></td>
<td><p>예</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>차이점 보관용 VHD의 최대 크기</p></td>
<td><p>.vhdx: 64TB</p>
<p>.vhd: 2TB</p></td>
<td><p>예</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>고정 형식 VHD</p></td>
<td><p>지원됨</p></td>
<td><p>아니요</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>차이점 보관용 VHD 형식</p></td>
<td><p>지원됨</p></td>
<td><p>아니오</p></td>
<td><p>차이점 보관용 VHD 기반 iSCSI 가상 디스크의 스냅숏은 만들 수 없습니다.</p></td>
</tr>
<tr class="odd">
<td><p>부모 VHD 당 차이점 보관용 Vhd 수</p></td>
<td><p>256</p></td>
<td><p>(예: Windows Server 2012)에 아니요</p></td>
<td><p>두 가지 수준의 깊이 (손자.vhdx 파일)는.vhdx 파일에 대 한 최대값 한 수준의 깊이 (자식.vhd 파일)에.vhd 파일에 대 한 최대입니다.</p></td>
</tr>
<tr class="even">
<td><p>동적 VHD 형식</p></td>
<td><p>.vhdx: 예</p>
<p>.vhd: 예 (Windows Server 2012에는 아니요)</p></td>
<td><p>예</p></td>
<td><p>로그인의 매핑을 해제&#39;t 지원 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>exFAT/FAT32/FAT (호스팅 VHD의 볼륨)</p></td>
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
<td><p>해당 사항 없음</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>NTFS</p></td>
<td><p>지원됨</p></td>
<td><p>해당 사항 없음</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Non-Microsoft CFS</p></td>
<td><p>지원되지 않음</p></td>
<td><p>예</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>씬 프로비저닝</p></td>
<td><p>아니오</p></td>
<td><p>해당 사항 없음</p></td>
<td><p>동적 Vhd는 지원 되지만 로그인의 매핑을 해제&#39;t 지원 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>논리 단위 축소</p></td>
<td><p>예 (Windows Server 2012 R2 이상만)</p></td>
<td><p>해당 사항 없음</p></td>
<td><p>사용 하 여 <a href="https://docs.microsoft.com/powershell/module/iscsitarget/resize-iscsivirtualdisk">크기 조정 iSCSIVirtualDisk</a> LUN을 축소 합니다.</p></td>
</tr>
<tr class="even">
<td><p>복제 논리 단위</p></td>
<td><p>지원되지 않음</p></td>
<td><p>해당 사항 없음</p></td>
<td><p>차이점 보관용 Vhd를 사용 하 여 디스크 데이터를 신속 하 게 복제할 수 있습니다.</p></td>
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
<th><p>설명</p></th>
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
<td><p>스냅숏 – full로 변환</p></td>
<td><p>지원되지 않음</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>스냅숏 – online 롤백</p></td>
<td><p>지원되지 않음</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>쓰기 가능한 변환 – 스냅숏</p></td>
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
<td><p>로컬로 탑재 된 iSCSI 가상 디스크는 사용 되지 않음-자세한 내용은 <a href="https://technet.microsoft.com/library/dn303411.aspx">Features Removed or Deprecated in Windows Server 2012 R2</a>합니다. 동적 디스크 스냅숏을 로컬로 탑재 될 수 없습니다.</p></td>
</tr>
</tbody>
</table>

## <a name="iscsi-target-server-manageability-and-backup"></a>iSCSI 대상 서버 관리 효율성 및 백업

응용 프로그램 서버에서 iSCSI 가상 디스크에 볼륨 데이터의 섀도 복사본 (VSS 열린 파일 스냅숏)을 생성 하려는 경우 이전 (예: Diskraid 명령) 필요한 앱에 가상 디스크 서비스 (VDS) 하드웨어를 사용 하 여 iSCSI 가상 디스크를 관리. 공급자 스냅숏을 또는 VDS 관리 앱을 사용 하려는 서버에서 iSCSI 대상 저장소 공급자를 설치 합니다.

ISCSI 대상 저장소 공급자는 Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012;의 역할 서비스 또한 다운로드 하 고 설치할 수 있습니다 [하위 수준 응용 프로그램 서버에 대 한 iSCSI 대상 저장소 공급자 (VDS/VSS)](http://www.microsoft.com/download/details.aspx?id=34759) iSCSI 대상 서버는 Windows Server 2012에서 실행 되는 동안 다음 운영 체제:

  - Windows Storage Server 2008 R2

  - Windows Server 2008 R2

  - Windows HPC 서버 2008 R2

  - Windows HPC Server 2008

Note는 iSCSI 대상 서버는 Windows Server 2012 R2를 실행 하는 서버에서 호스트 또는 최신 원격 서버에서 VDS 또는 VSS를 사용 하려는 경우 원격 서버에도 동일한 버전의 Windows Server를 실행 하 고 iSCSI 대상 저장소 공급자 역할 서비스 e를 설치 합니다. 또한 Windows의 모든 버전에서 iSCSI 대상 저장소 공급자 역할 서비스의 버전을 하나만 설치 해야 note 합니다.

ISCSI 대상 저장소 공급자에 대 한 자세한 내용은 참조 하세요. [iSCSI 대상 저장소 (VDS/VSS) 공급자](http://blogs.technet.com/b/filecab/archive/2012/10/08/iscsi-target-storage-vds-vss-provider.aspx)합니다.

## <a name="tested-compatibility-with-iscsi-initiators"></a>ISCSI 초기자를 사용 하 여 테스트 거친된 호환성

ISCSI 대상 서버 소프트웨어는 다음 iSCSI 초기자를 사용 하 여 테스트 했습니다.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>초기자</p></td>
<td><p>Windows Server 2012 R2</p></td>
<td><p>Windows Server 2012</p></td>
<td><p>주석</p></td>
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
<td><p>로그 세션 아웃 하 고 크기가 조정 된 가상 디스크를 검색 하려면 다시 로그인 해야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>Red Hat Enterprise Linux 6</p></td>
<td><p>유효성 검사</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>RedHat Enterprise Linux 5 and 5</p></td>
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

또한 다음 iSCSI 초기자가 iSCSI 대상 서버에서 호스팅되는 가상 디스크에서 디스크 없는 부팅을 수행 테스트 했습니다.

  - Windows Server 2012 R2

  - Windows Server 2012

  - : IPXE 사용 하 여 PCIe NIC

  - : IPXE 사용 하 여 CD 또는 USB 디스크

## <a name="see-also"></a>참조

다음 목록에서는 iSCSI 대상 서버 및 관련 기술에 대한 추가 리소스를 제공합니다.

- [iSCSI 대상 블록 저장소 개요](iscsi-target-server.md)

- [iSCSI 대상 부팅 개요](iscsi-boot-overview.md)

- [Windows Server에서 저장소](../storage.md)

