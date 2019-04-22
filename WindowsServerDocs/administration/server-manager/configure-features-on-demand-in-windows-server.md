---
title: Configure Features on Demand in Windows Server
description: 서버 관리자
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-server-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e663bbea-d025-41fa-b16c-c2bff00a88e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c77bd088a02d405b17a4f7decd6093785296d5e8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818934"
---
# <a name="configure-features-on-demand-in-windows-server"></a>Configure Features on Demand in Windows Server

>적용 대상: Windows Server 2016

이 항목에서는 Uninstall-WindowsFeature cmdlet을 사용하여 주문형 기능 구성에서 기능 파일을 제거하는 방법에 대해 설명합니다.

주문형 기능에는 Windows 8 및 Windows Server 2012 역할 및 기능 파일을 제거할 수 있도록 하는에 도입 된 기능입니다 (기능 라고도 *페이로드*) 디스크 공간을 절약 하 고 원격 위치 또는 로컬 컴퓨터에서 대신 설치 미디어에서 역할 및 기능을 설치 하는 운영 체제에서. 실행되는 물리적 컴퓨터나 가상 컴퓨터에서 기능 파일을 제거할 수 있습니다. WIM(Windows 이미지) 파일이나 오프라인 VHD(가상 하드 디스크)의 기능 파일을 추가하거나 제거하여 주문형 기능 구성의 재현할 수 있는 복사본을 만들 수도 있습니다.

요청 시 구성 기능에서 기능 파일에 설치 된 기능 파일에 필요한 경우 컴퓨터에서 사용할 수 없는 경우 Windows Server 2012 R2 또는 Windows Server 2012을 보낼 수 Windows Update에서-병렬 기능 저장소 (공유 폴더 기능 파일을 포함 하 고 네트워크에서 컴퓨터를 사용할 수 있는)에서 파일 가져오기 또는 설치 미디어에서. 기본적으로 대상 서버에서 기능 파일을 사용할 수 없는 경우 주문형 기능은 다음 작업을 순서대로 수행하여 누락된 기능 파일을 검색합니다.

1.  추가 역할 및 기능 마법사 또는 DISM 설치 명령이 사용자가 지정 된 위치에서 검색

2.  그룹 정책 설정의 구성 평가 **컴퓨터 구성 \ 관리 템플릿 \ 선택적 구성 요소 설치 및 구성 요소 복구를 위한 설정 지정**

3.  Windows 업데이트 검색

다음 작업 중 하나를 수행하여 기본 주문형 기능 동작을 재정의할 수 있습니다.

-   `Install-WindowsFeature` 매개 변수를 추가하여 `Source` cmdlet의 일부로 대체 원본 경로 지정

-   대체 원본 경로 지정 합니다 **설치 옵션 확인** 추가 역할 및 기능 마법사를 사용 하 여 기능을 설치 하는 동안 페이지

-   그룹 정책 설정, **선택적 구성 요소 설치 및 구성 요소 복구를 위한 설정**구성

이 항목에는 다음 섹션이 수록되어 있습니다.

-   [기능 파일 또는 side-by-side-저장소 만들기](#BKMK_store)

-   [기능 파일을 제거 하는 방법](#BKMK_methods)

-   [Uninstall-windowsfeature를 사용 하 여 기능 파일 제거](#BKMK_remove)

## <a name="BKMK_store"></a>기능 파일 또는 side-by-side-저장소 만들기
이 섹션에는 폴더를 설정 하는 원격 기능 파일 공유 (-병렬 저장소 라고도 함) Windows Server 2012 r 2를 실행 하는 서버 또는 Windows Server 2012에 역할, 역할 서비스 및 기능을 설치 하는 데 필요한 파일을 저장 하는 방법을 설명 합니다. 기능 저장소를 설정한 후에 이러한 운영 체제를 실행 하는 서버에 역할, 역할 서비스 및 기능을 설치할 수 있으며 설치 원본 파일의 위치와 기능 저장소를 지정할 수 있습니다.

#### <a name="to-create-a-feature-file-store"></a>기능 파일 저장소를 만들려면

1.  네트워크의 서버에서 공유 폴더를 만듭니다(예: 예를 들어 *\\\network\share\sxs*합니다.

2.  기능 저장소에 올바른 권한이 할당되었는지 확인합니다. 원본 경로 또는 파일 공유 권한을 부여 해야 합니다 **읽기** 권한 하는 **Everyone** (권장 하지 않음 보안상의 이유로), 그룹 또는 컴퓨터 계정에 (*도메인* \\ *SERverNAME*$) 서버는이 기능 저장소를 사용 하 여 기능을 설치 하려는; 사용자 계정 액세스 권한 부여로 부족 합니다.

    Windows 바탕 화면에서 다음 작업 중 하나를 수행하여 파일 공유 및 사용 권한 설정에 액세스할 수 있습니다.

    -   공유 폴더를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭한 후 **보안** 탭에서 해당 폴더에 대해 허용된 사용자 및 해당 액세스 권한을 변경합니다.

    -   공유 폴더를 마우스 오른쪽 단추로 클릭하고 **공유 대상**을 가리킨 다음 **특정 사용자**를 클릭합니다.

    > [!NOTE]
    > 작업 그룹에 속한 서버에서는 외부 공유에 대한 **읽기** 권한이 작업 그룹 서버의 컴퓨터 계정에 있더라도 외부 파일 공유에 액세스할 수 없습니다. 작업 그룹 서버에 사용되는 대체 원본 위치에는 로컬 작업 그룹 서버에 저장된 설치 미디어, Windows 업데이트 및 VHD 또는 WIM 파일이 포함됩니다.

3.  Windows Server 설치 미디어에서 **Sources\SxS** 폴더를 1단계에서 만든 공유 폴더에 복사합니다.

## <a name="BKMK_methods"></a>기능 파일을 제거 하는 방법
두 가지 방법 중 하나를 사용하여 Windows Server의 주문형 기능 구성에서 기능 파일을 제거할 수 있습니다.

-   `remove` 의 매개 변수는 `Uninstall-WindowsFeature` cmdlet를 사용 하면 서버 또는 오프 라인 가상 하드 디스크 (VHD) Windows Server 2012 R2 또는 Windows Server 2012를 실행 하에서 기능 파일을 삭제 합니다. 에 대 한 유효한 값은 `remove` 매개 변수는 이름, 역할, 역할 서비스 및 기능입니다.

-   DISM(배포 이미지 서비스 및 관리) 명령을 통해 필요하지 않거나 다른 원격 원본에서 가져올 수 있는 기능 파일을 생략하여 디스크 공간을 확보하는 사용자 지정 WIM 파일을 만들 수 있습니다. DISM을 사용하여 사용자 지정 이미지를 준비하는 방법에 대한 자세한 내용은 [Windows 기능을 사용하거나 사용하지 않도록 설정하는 방법](https://technet.microsoft.com/library/hh824822.aspx)를 참조하세요.

## <a name="BKMK_remove"></a>Uninstall-windowsfeature를 사용 하 여 기능 파일 제거
서버 및 Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 오프 라인 Vhd에서 역할, 역할 서비스 및 기능을 제거 하 고 기능 파일을 삭제 하려면 Uninstall-windowsfeature cmdlet을 사용할 수 있습니다. 제거 및 수 원하는 경우 동일한 역할, 역할 서비스 및 동일한 명령에는 기능을 삭제 합니다.

> [!IMPORTANT]
> 역할에 대 한 기능 파일을 삭제 하면 역할 서비스 또는 기능, 역할, 역할 서비스 및 기능 제거 하는 파일에 종속 된도 삭제 됩니다. 역할 서비스나 하위 기능에 대한 기능 파일을 삭제하는 경우 부모 역할이나 기능에 대한 다른 역할 서비스나 하위 기능이 설치되어 있지 않으면 전체 부모 역할이나 기능에 대한 파일이 삭제됩니다. `Uninstall-WindowsFeature -remove` 명령으로 삭제되는 모든 기능 파일을 보려면 명령에 `whatif` 매개 변수를 추가하여 이 명령을 실행함으로써 기능 파일을 실제로 삭제하지 않고도 결과를 볼 수 있습니다.

#### <a name="to-remove-role-and-feature-files-by-using-uninstall-windowsfeature"></a>Uninstall-WindowsFeature를 사용하여 역할 및 기능 파일을 제거하려면

1.  다음 중 하나를 수행하여 관리자 권한으로 Windows PowerShell 세션을 엽니다.

    > [!NOTE]
    > 원격 서버에서 역할 및 기능을 제거 하려는, 관리자 권한으로 Windows PowerShell을 실행할 필요가 없습니다.

    -   Windows 바탕 화면의 작업 표시줄에서 **Windows PowerShell**을 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 클릭합니다.

    -   Windows 온 **시작** 화면, Windows PowerShell 타일을 마우스 오른쪽 단추로 클릭 한 다음 앱 바에서를 클릭 **관리자 권한으로 실행**합니다.

    -   Server Core 설치 옵션을 실행 하는 서버에서 입력 **PowerShell** 명령 프롬프트에 다음 키를 눌러 **Enter**합니다.

2.  다음을 입력하고 **Enter** 키를 누릅니다.

    ```
    Uninstall-WindowsFeature -Name <feature_name> -computerName <computer_name> -remove
    ```

    **예:** 원격 데스크톱 라이선싱은 설치 된 원격 데스크톱 서비스의 마지막으로 남은 역할 서비스입니다. 이 명령은 원격 데스크톱 라이선싱을 제거한 후 지정된 서버인 *contoso_1*에서 전체 원격 데스크톱 서비스 역할에 대한 기능 파일을 삭제합니다.

    ```
    Uninstall-WindowsFeature -Name rdS-Licensing -computerName contoso_1 -remove
    ```

    **예:** 다음 예제에서는 명령을 오프 라인 VHD에서 active directory Domain Services 및 그룹 정책 관리를 제거합니다. 오프라인 VHD, *Contoso.vhd*에서 먼저 역할 및 기능이 제거된 다음 기능 파일이 전부 제거됩니다.

    > [!NOTE]
    > 추가 해야는 `computerName` Windows 8.1 또는 Windows 8 실행 하는 경우 cmdlet은 컴퓨터에서 하는 매개 변수를 실행 합니다.
    > 
    > 경우 네트워크 공유에서 VHD 파일의 이름을 입력을 공유 하는 권한을 부여 해야 합니다 **읽기** 하 고 **작성** VHD를 탑재 하도록 선택한 서버의 컴퓨터 계정에 사용 합니다. 사용자 전용 계정 액세스 권한으로는 충분하지 않습니다. 공유는 **읽기** 및 **쓰기** 권한을 **Everyone** 그룹에 부여하여 VHD에 액세스하도록 할 수 있지만 보안상의 이유로 권장되지 않습니다.

    ```
    Uninstall-WindowsFeature -Name AD-Domain-Services,GPMC -VHD C:\WS2012VHDs\Contoso.vhd -computerName ContosoDC1
    ```

## <a name="see-also"></a>관련 항목
[역할, 역할 서비스 또는 기능 설치 또는 제거](install-or-uninstall-roles-role-services-or-features.md)
[Windows Server 설치 옵션](https://technet.microsoft.com/library/hh831786.aspx)
[하거나 Windows 기능을 사용 하지 않도록 설정 하는 방법을](https://technet.microsoft.com/library/hh824822.aspx)
[배포 이미지 서비스 및 관리 (DISM) 개요](https://technet.microsoft.com/library/hh825236.aspx)


