---
title: WSUS 없이 매달 델타 업데이트 ISV 지원
description: WSUS(Windows Server Update Service) 항목 - ISV(독립 소프트웨어 공급업체)가 패키지 크기 감소를 위해 WSUS Express 업데이트 배달 대신 매달 델타 업데이트를 일시적으로 사용하는 방법
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: get-started article
author: sakitong
ms.author: coreyp
manager: dougkim
ms.date: 10/16/2017
ms.openlocfilehash: 4607827d73c34f50f721a2774fa498eb95f9dbb8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361734"
---
# <a name="monthly-delta-update-isv-support-without-wsus"></a>WSUS 없이 매달 델타 업데이트 ISV 지원

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows 10

모든 패키지에는 일관성과 단순성을 보장하기 위해 이전에 사용된 수정 사항이 포함되어 있으므로 Windows 10 업데이트 다운로드의 규모가 커질 수 있습니다.  

버전 7부터 Windows에는 Windows 업데이트 다운로드 크기를 줄일 수 있는 [Express](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx#Anchor_2)라는 기능이 지원됩니다. 소비자 디바이스에서 기본적으로 지원되더라도 Express 기능을 이용하기 위해서는 Windows 10 Enterprise 디바이스에 WSUS(Windows Server Update Services)가 필요합니다. WSUS를 사용할 수 있으면 [Express 업데이트 배달 ISV 지원](express-update-delivery-ISV-support.md)을 참조하세요. 이를 사용하여 Express 업데이트 배달을 활성화하는 것이 좋습니다. 

현재 WSUS가 설치되지 않았지만 중간에 더 작은 업데이트 패키지 크기가 필요하면 매달 델타 업데이트를 사용할 수 있습니다. 델타 업데이트도 패키지 크기를 상당히 줄여주지만 WSUS Express 업데이트 배달만큼은 아닙니다. 패키지 크기를 최대한 줄일 수 있도록 가능하면 언제나 WSUS Express 업데이트를 배포하는 것이 좋습니다. 다음 차트에서는 Windows 10 버전 1607을 위한 델타, 누적 및 Express 다운로드 크기를 비교해서 보여줍니다.

![다운로드 크기 비교](../../media/express-update-delivery-isv-support/delta-1.png)

## <a name="what-is-monthly-delta-update"></a>매달 델타 업데이트란?

매달 보안 업데이트에는 델타 및 누적의 두 가지 유형이 있습니다.

매달 델타 업데이트는 새로운 유형이며, 업데이트 패키지 크기를 줄이는 데 도움이 되는 WSUS가 없는 ISV를 위한 중간 솔루션입니다.

>[!IMPORTANT]
>**델타 업데이트는 Windows 10 버전 1607(Anniversary Update), 버전 1703(Creators Update) 및 버전 1709(Fall Creators Update) 서비스를 위해 제공됩니다.** 버전 1709 이후의 릴리스에서는 증분 업데이트 이점을 계속 활용하기 위해 [Express 업데이트 배달](express-update-delivery-ISV-support.md)을 지원하는 배포 인프라를 구현해야 합니다.

매달 델타 업데이트를 사용하면 패키지에 1개월 분량의 업데이트만 포함됩니다. 월별 누적에는 해당 릴리스까지의 모든 업데이트가 포함되므로, 매월 파일 크기가 커집니다. 델타 및 매달 업데이트 모두 "업데이트 화요일"이라고 부르는 매월 둘째 화요일에 릴리스됩니다. 다음 표에서는 델타 및 누적 업데이트를 비교해서 보여줍니다.

|                    | 매달 **델타** 업데이트                                                                                                                                                                                                       | 매달 **누적** 업데이트                                                                                                                                                                                             |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **범위**          | **해당 월의 신규 수정 사항만** 포함된 단일 업데이트                                                                                                                                                                           | 해당 월 및 이전 월의 모든 신규 수정 사항이 포함된 단일 업데이트                                                                                                                                                   |
| **응용 프로그램**    | 이전 달의 업데이트가 적용된 경우에만 적용 가능(누적 또는 델타)                                                                                                                                           | 언제든지 적용 가능                                                                                                                                                                                                |
| **배달**       | 다른 도구 또는 프로세스에서 사용하도록 다운로드할 수 있는 **Windows 업데이트 카탈로그에만 게시**됩니다. Windows 업데이트에 연결된 PC에는 제공되지 않음                                                         | Windows 업데이트(모든 소비자 PC가 설치하는 위치), WSUS 및 Windows 업데이트 카탈로그에 게시됨                                                                                                                |

델타 및 누적에는 동일한 KB 번호와 동일한 분류 및 릴리스가 동시에 포함됩니다. 업데이트는 카탈로그의 업데이트 제목 또는 msu 이름에 따라 구분될 수 있습니다.

- x64기반 시스템을 위한 Windows 10 버전 1607용 2017-02 *\***델타 업데이트**\**  (KB1234567)
- x86기반 시스템을 위한 Windows 10 버전 1607용 2017-02 *\***델타 업데이트**\**  (KB1234567)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      

### <a name="when-to-use-monthly-delta-update"></a>매달 델타 업데이트를 사용하는 경우

클라이언트 디바이스에 대한 업데이트 크기가 중요한 경우, 이전 달 업데이트가 포함된 디바이스에서는 델타 업데이트를 사용하고, 업데이트가 뒤쳐진 디바이스에서는 누적 업데이트를 사용하는 것이 좋습니다. 이렇게 하면 모든 디바이스에 최신 상태로 유지하기 위한 단일 업데이트만 필요합니다. 이를 위해서는 조직에서 디바이스를 최신 상태로 유지하는 방식에 따라 업데이트를 다르게 배포해야 하기 때문에 전체 업데이트 관리 프로세스에 대한 소규모 조정이 필요합니다.

![다운로드 크기 비교](../../media/express-update-delivery-isv-support/delta-2.png)

### <a name="prevent-deployment-of-delta-and-cumulative-updates-in-the-same-month"></a>같은 달 델타 및 누적 업데이트 배포 방지

델타 업데이트 및 누적 업데이트는 동시에 사용 가능하기 때문에, 두 업데이트를 같은 달에 모두 배포할 경우 어떤 결과가 발생하는지를 이해하는 것이 중요합니다.

델타 및 누적 업데이트의 동일 버전을 승인하고 배포하면, 두 버전 모두 PC에 다운로되기 때문에 추가 네트워크 트래픽이 생성될 뿐만 아니라 재시작 후 컴퓨터를 Windows로 재부팅하지 못할 수 있습니다.

델타 및 누적 업데이트가 모두 설치되고 컴퓨터가 더 이상 부팅되지 않으면 다음 단계로 문제를 복구할 수 있습니다.

1. WinRE 명령 프롬프트로 부팅
2. 보류 중인 상태의 패키지 나열:

    `x:\windows\system32\dism.exe /image:<drive letter for windows directory> /Get-Packages >> <path to text file>`
 
    > **예**: ` x:\windows\system32\dism.exe /image:c:\ /Get-Packages >> c:\temp\packages.txt`
 
3. **get-packages**로 파이프한 텍스트 파일을 엽니다. 설치 보류 중인 패치가 보이면 각 패키지 이름에 대해 **remove-package**를 실행합니다.
 
   `dism.exe /image:<drive letter for windows directory> /remove-package /packagename:<package name>`
 
    > **예**: `x:\windows\system32\dism.exe /image:c:\ /remove-package /packagename:Package_for_KB4014329~31bf3856ad364e35~amd64~~10.0.1.0`
 
    >[!NOTE]
    >제거 보류 중인 패치는 제거하지 마십시오.

>[!IMPORTANT]
>**델타 업데이트는 Windows 10 버전 1607(Anniversary Update), 버전 1703(Creators Update) 및 버전 1709(Fall Creators Update) 서비스를 위해 제공됩니다.** 버전 1709 이후의 릴리스에서는 증분 업데이트 이점을 계속 활용하기 위해 [Express 업데이트 배달](express-update-delivery-ISV-support.md)을 지원하는 배포 인프라를 구현해야 합니다.
