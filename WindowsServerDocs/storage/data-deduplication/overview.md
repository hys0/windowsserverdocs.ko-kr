---
ms.assetid: 4b844404-36ba-4154-aa5d-237a3dd644be
title: 데이터 중복 제거 개요
ms.technology: storage-deduplication
ms.prod: windows-server-threshold
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 05/09/2017
ms.openlocfilehash: bf346844337740f7585070ff78de4e7f61f25624
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447263"
---
# <a name="data-deduplication-overview"></a>데이터 중복 제거 개요

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널) 

## <a name="what-is-dedup"></a>데이터 중복 제거란 무엇입니까?

데이터 중복 제거를 줄여서 중복 제거 라고도 기능은 중복 데이터 저장소 비용의 영향을 줄일 수 있습니다. 사용하도록 설정된 경우 데이터 중복 제거는 볼륨에서 중복된 부분을 찾기 위해 볼륨의 데이터를 검사하여 볼륨의 여유 공간을 최적화합니다. 볼륨의 데이터 집합에서 중복된 부분이 한 번 저장되며 필요한 경우 추가적인 절약을 위해 압축됩니다. 데이터 중복 제거는 데이터 충실도 또는 무결성을 손상시키지 않고 중복성을 최적화합니다. 데이터 중복 제거 작동 방식에 대한 자세한 내용은 '[데이터 중복 제거 작동 방식](understand.md#how-does-dedup-work)' 섹션([데이터 중복 제거 이해](understand.md) 페이지)에서 확인할 수 있습니다.

> [!Important]  
> [KB4025334](https://support.microsoft.com/kb/4025334) 롤포워드를 포함 합니다. 중요 한 안정성을 포함 하 여 데이터 중복 제거에 대 한 수정 프로그램의 최대 수정 사항, 및 Windows Server 2016 및 Windows Server 2019를 사용 하 여 데이터 중복 제거를 사용 하는 경우 설치는 것이 좋습니다.

## <a name="why-is-dedup-useful"></a>데이터 중복 제거 유용한 이유는 무엇입니까?

데이터 중복 제거를 사용하면 저장소 관리자가 중복된 데이터와 관련된 비용을 줄일 수 있습니다. 대규모 데이터 집합에는 종종 데이터 저장 비용을 증가시키는 **<u>많은</u>** 중복 데이터가 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

- 사용자 파일 공유에 같거나 유사한 파일의 여러 복사본이 있을 수 있습니다.
- 가상화 게스트가 VM 간에 거의 동일할 수 있습니다.
- 매일 생성되는 백업 스냅샷이 약간의 차이만 있을 수 있습니다.

데이터 중복 제거에서 얻을 수 있는 공간 절약은 볼륨의 데이터 집합 또는 워크로드에 따라 달라집니다. 중복성이 높은 데이터 집합은 최적화 비율이 최대 95%에 이르거나 저장소 사용률이 20배 감소할 수 있습니다. 다음 표에는 다양한 콘텐츠 유형에 대한 일반적인 중복 제거 절감률이 나와 있습니다.

| 시나리오       | 콘텐츠                                        | 일반적인 공간 절약 비율 |
|----------------|------------------------------------------------|-----------------------|
| 사용자 문서 | Office 문서, 사진, 음악, 비디오 등  | 30~50%                |
| 배포 공유 | 소프트웨어 이진 파일, cab 파일, 기호 등 | 70~80%                |
| 가상화 라이브러리 | ISO, 가상 하드 디스크 파일 등  | 80~95%                |
| 일반 파일 공유 | 위의 모든 항목                           | 50~60%                |

## <a id="when-can-dedup-be-used"></a>데이터 중복 제거 사용 시기  
<table>
    <tbody>
        <tr>
            <td style="text-align:center;min-width:150px;vertical-align:center;"><img src="media/overview-clustered-gpfs.png" alt="Illustration of file servers" /></td>
            <td style="vertical-align:top">
                <b>일반용 파일 서버</b><br />
일반용 파일 서버는 일반적으로 다음과 같은 유형의 공유를 포함할 수 있는 범용 파일 서버입니다. <ul>
                    <li>팀 공유</li>
                    <li>사용자 홈 폴더</li>
                    <li><a href="https://technet.microsoft.com/library/dn265974.aspx">클라우드 폴더</a></li>
                    <li>소프트웨어 개발 공유</li>
                </ul>
일반용 파일 서버는 여러 사용자가 같은 파일의 여러 복사본 또는 버전을 가지고 있는 경향이 많기 때문에 데이터 중복 제거에 적합한 대상입니다. 소프트웨어 개발 공유는 많은 이진 파일이 빌드 간에 기본적으로 변경되지 않은 상태로 유지되기 때문에 데이터 중복 제거의 이점을 활용할 수 있습니다. 
            </td>
        </tr>
        <tr>
            <td style="text-align:center;min-width:150px;vertical-align:center;"><img src="media/overview-vdi.png" alt="Illustration of VDI servers" /></td>
            <td style="vertical-align:top">
                <b>가상화 된 데스크톱 인프라 (VDI) 배포</b><br />
<a href="https://technet.microsoft.com/library/cc725560.aspx">원격 데스크톱 서비스</a>와 같은 VDI 서버는 조직에서 사용자에게 데스크톱을 프로비전할 수 있는 간단한 옵션을 제공합니다. 조직에서 이러한 기술에 의존하는 여러 가지 이유가 있습니다. <ul>
                    <li><b>응용 프로그램 배포</b>: 기업 전체에서 응용 프로그램을 신속 하 게 배포할 수 있습니다. 이는 자주 업데이트되거나, 자주 사용되지 않거나, 관리하기 어려운 응용 프로그램이 있는 경우에 특히 유용합니다.</li>
                    <li><b>응용 프로그램 통합</b>: 설치 하 고 중앙에서 관리 되는 가상 컴퓨터 집합에서 응용 프로그램을 실행 하면 클라이언트 컴퓨터에서 응용 프로그램을 업데이트할 필요가 없습니다. 이 옵션은 응용 프로그램에 액세스하는 데 필요한 네트워크 대역폭 양도 줄여 줍니다.</li>
                    <li><b>원격 액세스</b>: 사용자가 가정용 컴퓨터, 키오스크, 저전력 하드웨어 및 Windows 이외의 운영 체제와 같은 장치에서 엔터프라이즈 응용 프로그램을 액세스할 수 있습니다.</li>
                    <li><b>지점 액세스</b>: VDI 배포는 사무실 작업자 중앙된 데이터 저장소에 액세스 해야 하는 분기에 대 한 더 나은 응용 프로그램 성능을 제공할 수 있습니다. 데이터 사용량이 많은 응용 프로그램에는 저속 연결에 최적화된 클라이언트/서버 프로토콜이 없는 경우가 있습니다.</li>
                </ul>
사용자를 위해 원격 데스크톱을 구동하는 가상 하드 디스크는 기본적으로 동일하기 때문에 VDI 배포는 데이터 중복 제거에 적합한 대상입니다. 또한 데이터 중복 제거는 많은 사용자가 데스크톱에 동시에 로그인하여 일과를 시작할 때 저장소 성능이 저하되는 <em>VDI 부팅 스톰</em>에도 도움이 될 수 있습니다.
            </td>
        </tr>
        <tr>
            <td style="text-align:center;min-width:150px;vertical-align:center;"><img src="media/overview-backup.png" alt="Illustration of backup applications" /></td>
            <td style="vertical-align:top">
                <b>가상화 된 백업 응용 프로그램과 같은 백업 대상</b><br />
<a href="https://technet.microsoft.com/library/hh758173.aspx">Microsoft DPM(Data Protection Manager)</a>과 같은 백업 응용 프로그램은 백업 스냅숏 간의 상당한 중복으로 인해 데이터 중복 제거에 매우 적합한 대상입니다.
            </td>
        </tr>
        <tr>
            <td style="text-align:center;min-width:150px;vertical-align:center;"><img src="media/overview-other.png" alt="Illustration of other workloads" /></td>
            <td style="vertical-align:top">
                <b>다른 워크 로드</b><br />
                <a href="install-enable.md#enable-dedup-candidate-workloads" data-raw-source="[Other workloads may also be excellent candidates for Data Deduplication](install-enable.md#enable-dedup-candidate-workloads)">다른 워크로드도 데이터 중복 제거에 매우 적합한 대상일 수 있습니다</a>.
            </td>
        </tr>
    </tbody>
</table>
