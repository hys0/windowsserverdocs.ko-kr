---
ms.assetid: d44d4430-41e2-483a-9685-92610cdef32a
title: 클러스터 인식 업데이트 플러그 인 작동 방식
ms.topic: article
ms.prod: windows-server-threshold
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 04/28/2017
ms.technology: storage-failover-clustering
description: 사용 하 여 클러스터 인식 업데이트 Windows Server의 클러스터에 업데이트를 설치할 때 업데이트를 조정 하기 위해 플러그 인을 사용 하는 방법입니다.
ms.openlocfilehash: d09addb5e6787a8386d50570c0d27640646aa587
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854564"
---
# <a name="how-cluster-aware-updating-plug-ins-work"></a>클러스터 인식 업데이트 플러그 인 작동 방식

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

[클러스터 인식 업데이트](cluster-aware-updating.md) (CAU) 플러그 인을 사용 하 여 장애 조치 클러스터의 노드에서 업데이트 설치를 조정 합니다. 이 항목에서는 기본 제공 사용에 대 한 정보를 제공\-CAU 플러그에서\-기능 또는 다른 플러그\-CAU 용으로 설치 하는 기능입니다.

## <a name="BKMK_INSTALL"></a>설치 된 플러그 앤\-에서  
플러그\-에서 연결에 기본값 이외의\-CAU와 함께 설치 된 기능을 \( **Microsoft.WindowsUpdatePlugin** 하 고 **Microsoft.HotfixPlugin** \)별도로 설치 해야 합니다. CAU 사용 되는 경우 자체\-업데이트 모드를 플러그\-에서 모든 클러스터 노드에 설치 수 있어야 합니다. 원격에 CAU를 사용 하면\-업데이트 모드를 플러그\-에서 원격 업데이트 코디네이터 컴퓨터의 설치 수 있어야 합니다. 플러그 인을\-설치 각 노드의 추가 설치 요구 사항이 있습니다.  
  
플러그 인을 설치 하려면\-에서는 플러그에서 지침에 따라\-게시자에서 합니다. 플러그 인을 수동으로 등록 하\-CAU를 사용 하 여 실행 합니다 [Register-cauplugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin) 각 컴퓨터에 cmdlet 여기서 플러그\-설치 됩니다.  
  
## <a name="specify-a-plug-in-and-plug-in-arguments"></a>플러그 인을 지정\-에 연결 하 고\-인수  
  
### <a name="specify-a-cau-plug-in"></a>지정 된 CAU 플러그 인\-에서

플러그 인을 CAU ui에서 선택한\-의 드롭다운에서\-사용 가능한 플러그인 목록을 아래로\-CAU를 사용 하 여 다음 작업을 수행 하는 기능:  
  
-   클러스터에 업데이트 적용  
  
-   클러스터의 업데이트 미리 보기  
  
-   구성 클러스터 자체\-업데이트 옵션  
  
기본적으로 CAU는 플러그 인을 선택\-에 **Microsoft.WindowsUpdatePlugin**합니다. 그러나 모든 플러그 인을 지정할 수 있습니다\-에 설치 하 고 CAU를 사용 하 여 등록 합니다.

> [!TIP]  
> CAU UI에서 단일 플러그 인을 지정할 수 있습니다\-에서 미리 보거나 업데이트 실행 중 업데이트를 적용 하는 데는 CAU에 대 한 합니다. CAU PowerShell cmdlet을 사용 하 여 하나 이상의 플러그 인을 지정할 수 있습니다\-기능입니다. 클러스터에 여러 종류의 업데이트를 설치 해야 할 경우 것이 여러 플러그 인을 지정 하려면 일반적으로 더 효율적\-각 플러그 인에 대 한 별도 업데이트 실행을 사용 하는 것이 아니라 하나의 업데이트 실행 기능\-에서 합니다. 예를 들어 대개 노드가 다시 시작되는 횟수가 줄어듭니다.

다음 표에 나와 있는 CAU PowerShell cmdlet을 사용 하 여 하나 이상의 플러그 인을 지정할 수 있습니다\-업데이트 실행 또는 전달 하 여 검색 기능을 **– CauPluginName** 매개 변수입니다. 여러 플러그 인을 지정할 수 있습니다\-쉼표로 구분 하 여 이름에 있습니다. 여러 플러그 인을 지정 하는 경우\-기능을 제어할 수 있습니다 어떻게 플러그\-기능에 영향을 기타 각 업데이트 실행 중 지정 하 여 합니다  **\-RunPluginsSerially**,  **\- StopOnPluginFailure**, 및 **– SeparateReboots** 매개 변수입니다. 여러 플러그 인을 사용 하는 방법에 대 한 자세한 내용은\-cmdlet 설명서의 다음 표에 링크를 제공 하는 기능을 사용 합니다.  
  
|Cmdlet|설명|  
|----------|---------------|  
|[Add-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/add-cauclusterrole)|CAU 클러스터 된 역할 자체를 제공 하는 추가\-지정된 된 클러스터에 기능을 업데이트 합니다.|  
|[Invoke-CauRun](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-caurun)|적용 가능한 업데이트에 대해 클러스터 노드 검사를 수행하고, 지정된 클러스터에서 업데이트 실행을 통해 해당 업데이트를 설치합니다.|  
|[Invoke-CauScan](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-causcan)|적용 가능한 업데이트에 대해 클러스터 노드 검사를 수행하고, 지정된 클러스터의 각 노드에 적용되는 초기 업데이트 집합의 목록을 반환합니다.|  
|[Set-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/set-cauclusterrole)|지정된 클러스터에서 CAU 클러스터된 역할의 구성 속성을 설정합니다.|  
  
CAU 플러그 인을 지정 하지 않는 경우\-이러한 cmdlet을 사용 하 여 매개 변수, 기본값은 플러그\-에 **Microsoft.WindowsUpdatePlugin**합니다.  
  
### <a name="specify-cau-plug-in-arguments"></a>CAU 플러그 인 지정\-인수  
하나 이상의 업데이트 실행 옵션을 구성할 때 지정할 수 있습니다 *이름\=값* 쌍 \(인수\) 선택한 플러그 인에 대 한\-하려면 사용 합니다. 예를 들어 CAU UI에서 다음과 같은 여러 인수를 지정할 수 있습니다.  
  
**Name1\=Value1; Name2\=Value2; Name3\=Value3**  
  
이러한 *이름을\=값* 쌍의 플러그 인에 의미가 있어야\-지정할에 합니다. 일부 플러그 인에 대 한\-기능 인수는 선택 사항입니다.  
  
CAU 플러그 인 구문을\-인수에서 이러한 일반 규칙을 따릅니다.  
  
-   여러 *이름을\=값* 쌍은 세미콜론으로 구분 합니다.  
  
-   공백이 포함된 값은 따옴표로 묶습니다(예: **Name1\="Value with Spaces"** 합니다.  
  
-   정확한 구문은 *값* 플러그 종속\-에서 합니다.  
  
플러그 인을 지정 하려면\-지 원하는 CAU PowerShell cmdlet을 사용 하 여 인수에서를 **– CauPluginParameters** 매개 변수를 폼의 매개 변수 전달 합니다.  
  
**\-CauPluginArguments @{Name1\=Value1; Name2\=Value2; Name3\=Value3}**  
  
또한 미리 정의 된 PowerShell 해시 테이블을 사용할 수 있습니다. 플러그 인을 지정 하려면\-둘 이상의 플러그 인에 대 한 인수에서\-에서는 쉼표로 구분 하 여 인수의 여러 해시 테이블을 전달 합니다. 전달 플러그\-인수에 플러그\-에 지정 된 순서에 **CauPluginName**합니다.  
  
### <a name="specify-optional-plug-in-arguments"></a>선택적 플러그 인을 지정\-인수  
플러그\-CAU를 설치 하는 기능 \( **Microsoft.WindowsUpdatePlugin** 하 고 **Microsoft.HotfixPlugin** \) 선택할 수 있는 추가 옵션을 제공 합니다. CAU UI에서 이러한 표시에 **추가 옵션** 페이지는 플러그 인에 대 한 업데이트 실행 옵션을 구성한 후\-에서 합니다. 이러한 옵션 선택적 플러그 인으로 구성 된 CAU PowerShell cmdlet을 사용 하는 경우\-인수에서입니다. 자세한 내용은 이 항목의 뒷부분에 있는 [Microsoft.WindowsUpdatePlugin 사용](#BKMK_WUP) 및 [Microsoft.HotfixPlugin 사용](#BKMK_HFP) 을 참조하세요.  
  
## <a name="manage-plug-ins-using-windows-powershell-cmdlets"></a>플러그 인 관리\-Windows PowerShell cmdlet을 사용 하는 기능  
  
|Cmdlet|설명|  
|----------|---------------|  
|[Get-CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/get-cauplugin)|하나 이상의 소프트웨어 업데이트 플러그 인에 대 한 정보를 검색\-는 로컬 컴퓨터의 등록 기능을 합니다.|  
|[Register-CauPlugin]((https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin))|CAU 소프트웨어 업데이트 플러그 인 등록\-에서 로컬 컴퓨터의 합니다.|  
|[Unregister-CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/unregister-cauplugin)|플러그 인을 업데이트 하는 소프트웨어를 제거\-에서 플러그 인 목록에서\-CAU에서 사용할 수 있는 기능입니다. **참고:** 플러그\-CAU와 함께 설치 된 기능을 \( **Microsoft.WindowsUpdatePlugin** 하며 **Microsoft.HotfixPlugin** \) 등록 취소할 수 없습니다.|  
  
## <a name="BKMK_WUP"></a>Microsoft.WindowsUpdatePlugin 사용  

기본 플러그\-에서 CAU에 대 한 **Microsoft.WindowsUpdatePlugin**, 다음 작업을 수행 합니다.
- 각 장애 조치 클러스터 노드에서 실행 중인 Microsoft 제품에 필요한 업데이트를 적용하기 위해 각 노드에서 Windows 업데이트 에이전트와 통신합니다.
- 설치 또는 Windows Update 나 Microsoft Update에서 업데이트를 직접 클러스터는 온\-프레미스 Windows Server Update Services \(WSUS\) 서버.
- 설치만 선택, 일반 배포 릴리스 \(GDR\) 업데이트 합니다. 기본적으로 플러그\-에서 중요 한 소프트웨어 업데이트에만 적용 됩니다. 구성이 필요하지 않습니다. 기본 구성에서 중요한 GDR 업데이트를 다운로드하여 각 노드에 설치합니다. 

> [!NOTE]
> 기본적으로 선택 되어 있는 중요 한 소프트웨어 업데이트 이외의 업데이트를 적용할 \(드라이버 업데이트 하는 예를 들어\)는 선택적 플러그 인을 구성할 수 있습니다\-매개 변수에서입니다. 자세한 내용은 [Windows 업데이트 에이전트 쿼리 문자열 구성](#BKMK_QUERY)을 참조하세요.

### <a name="requirements"></a>요구 사항

- 장애 조치 클러스터와 원격 업데이트 코디네이터 컴퓨터 \(사용 하는 경우\) 에 나열 된 원격 관리에 필요한 구성 및 CAU에 대 한 요구 사항에 맞아야 [요구 사항 및 CAU에 대 한 모범 사례 ](cluster-aware-updating-requirements.md).
- [Microsoft 업데이트 적용에 대한 권장 사항](cluster-aware-updating-requirements.md#BKMK_BP_WUA)을 검토한 다음 필요에 따라 장애 조치(failover) 클러스터 노드에 대한 Microsoft 업데이트 구성을 변경합니다.
- 최상의 결과 얻으려면 CAU 모범 사례 분석기를 실행 하는 권장 \(BPA\) 클러스터 및 업데이트 환경이 CAU를 사용 하 여 업데이트를 적용 하도록 올바르게 구성 되어 있는지 확인 합니다. 자세한 내용은 [CAU 업데이트 준비 테스트](cluster-aware-updating-requirements.md#BKMK_BPA)를 참조하세요.

> [!NOTE]
> Microsoft 사용 조건에 대한 동의가 필요하거나 사용자의 개입이 필요한 업데이트는 제외되며, 이는 수동으로 설치해야 합니다.

### <a name="additional-options"></a>추가 옵션

필요에 따라 다음 플러그 인을 지정할 수 있습니다\-늘리거나는 플러그 인으로 적용 되는 업데이트 집합을 제한 하기 위해 인수에서\-에서:
- 플러그를 구성 하려면\-에서 CAU UI의 각 노드에서 중요 업데이트와 함께 권장된 업데이트를 적용 하는 **추가 옵션** 페이지에서를 **제공 me 권장 업데이트 동일한 방식으로 중요 한 업데이트를 받을 때** 확인란 합니다.
<br>또는 구성 합니다 **'IncludeRecommendedUpdates'\='True'** 플러그 인\-in 인수입니다.
- 플러그를 구성 하려면\-각 클러스터 노드에 적용 되는 GDR 업데이트 종류를 필터링 하려면 지정 사용 하 여 Windows 업데이트 에이전트 쿼리 문자열을 **QueryString** 플러그 인\-인수에 합니다. 자세한 내용은 [Windows 업데이트 에이전트 쿼리 문자열 구성](#BKMK_QUERY)을 참조하세요.

### <a name="BKMK_QUERY"></a>Windows 업데이트 에이전트 쿼리 문자열 구성  
플러그 인을 구성할 수 있습니다\-기본 인수에 연결\-에서는 **Microsoft.WindowsUpdatePlugin**, Windows Update 에이전트의 구성 된 \(WUA\) 쿼리 문자열입니다. 이 명령은 WUA API를 사용하여 특정 선택 조건에 따라 각 노드에 적용할 하나 이상의 Microsoft 업데이트 그룹을 식별합니다. 논리 AND 또는 논리 OR을 사용하여 여러 조건을 조합할 수 있습니다. WUA 쿼리 문자열을 플러그 인에 지정 된\-같이 인수에:  
  
**QueryString\="Criterion1\=Value1 및\/또는 Criterion2\=Value2 및\/또는..."**  
  
예를 들어 **Microsoft.WindowsUpdatePlugin**은 **IsInstalled**, **Type**, **IsHidden**, 및 **IsAssigned** 조건을 통해 생성된 기본 **QueryString** 인수를 사용하여 중요 업데이트를 자동으로 선택합니다.  
  
**QueryString\="IsInstalled\=0 유형과\='소프트웨어' 및 IsHidden\=0과 IsAssigned\=1"**  
  
지정 하는 경우는 **QueryString** 인수를 기본값 대신 사용 됩니다 **QueryString** 플러그에 대해 구성한\-에서 합니다.  
  
#### <a name="example-1"></a>예제 1
  
구성 하는 **QueryString** ID로 식별 되는 특정 업데이트를 설치 하는 인수 *f6ce46c1\-971 c\-43f9\-a2aa\-783df125f003*:  
  
**QueryString\="UpdateID\=' f6ce46c1\-971 c\-43f9\-a2aa\-783df125f003' 및 IsInstalled\=0"**  
  
> [!NOTE]  
> 앞의 예제는 클러스터를 사용 하 여 업데이트를 적용 하는 것에 대 한 유효한\-업데이트 마법사를 인식 합니다. 자체를 구성 하 여 특정 업데이트를 설치 하려는 경우\-CAU UI 또는 사용 하 여 옵션을 업데이트 하는 **추가\-CauClusterRole** 하거나 **설정\-CauClusterRole**PowerShell cmdlet 인 두 개의 단일 UpdateID 값에 서식을 지정 해야\-따옴표 문자:  
>   
> **QueryString\="UpdateID\=' f6ce46c1\-971 c\-43f9\-a2aa\-783df125f003 ' 및 IsInstalled\=0"**  
  
#### <a name="example-2"></a>예제 2
  
드라이버만 설치하는 **QueryString** 인수를 구성하려면  
  
**QueryString\="IsInstalled\=0 유형과\='Driver' 및 IsHidden\=0"**  
  
기본값에 대 한 쿼리 문자열에 대 한 자세한 정보에 대 한 플러그\-에서는 **Microsoft.WindowsUpdatePlugin**, 검색 조건을 \(와 같은 **IsInstalled**\), 쿼리 문자열에 포함할 수 있는 구문에서 검색 조건 관련 섹션을 참조 하 고는 [Windows Update Agent (WUA) API 참조](https://go.microsoft.com/fwlink/p/?LinkId=223304)합니다.  
  
## <a name="BKMK_HFP"></a>Microsoft.HotfixPlugin 사용  
플러그\-에 **Microsoft.HotfixPlugin** 제한 된 Microsoft 배포 릴리스를 적용할 수 있습니다 \(LDR\) 업데이트 \(핫픽스 라고도 하 고 이전의 Qfe\) 하지 독립적으로 다운로드 특정 Microsoft 소프트웨어 문제를 해결 합니다. 플러그 인으로 SMB 파일 공유의 루트 폴더에서 업데이트를 설치 하 고 비 적용할 사용자 지정할 수 있습니다\-Microsoft 드라이버, 펌웨어 및 BIOS 업데이트 합니다.

> [!NOTE]
> 핫픽스는 기술 자료 문서에서는 Microsoft에서 다운로드할 수 있는 경우도 있지만 따라 고객에 게 제공 되기도\-별로 필요 합니다.

### <a name="requirements"></a>요구 사항

- 장애 조치 클러스터와 원격 업데이트 코디네이터 컴퓨터 \(사용 하는 경우\) 에 나열 된 원격 관리에 필요한 구성 및 CAU에 대 한 요구 사항에 맞아야 [요구 사항 및 CAU에 대 한 모범 사례 ](cluster-aware-updating-requirements.md).
- [Microsoft.HotfixPlugin 사용에 대한 권장 사항](cluster-aware-updating-requirements.md#BKMK_BP_HF)을 검토하세요.
- 최상의 결과 얻으려면 CAU 모범 사례 분석기를 실행 하는 권장 \(BPA\) 클러스터 및 업데이트 환경이 CAU를 사용 하 여 업데이트를 적용 하도록 올바르게 구성 되어 있는지 확인 하기 위해 모델입니다. 자세한 내용은 [CAU 업데이트 준비 테스트](cluster-aware-updating-requirements.md#BKMK_BPA)를 참조하세요.
- 게시자에서 업데이트를 가져오도록 및 복사 또는 서버 메시지 블록에 압축을 풀어 \(SMB\) 파일 공유 \(핫픽스 루트 폴더\) 이상 지 원하는 SMB 2.0 및는 클러스터의 모든 액세스할 수 노드 및 원격 업데이트 코디네이터 컴퓨터 \(원격에 CAU를 사용 하면\-업데이트 모드\)합니다. 자세한 내용은 이 항목의 뒷부분에 있는 [핫픽스 루트 폴더 구조 구성](#BKMK_HF_ROOT)을 참조하세요. 

    > [!NOTE]
    > 기본적으로이 플러그 인\-에서 인 핫픽스만 설치는 다음 파일 이름 확장명:.msu,.msi 및.msp이 고 합니다.

- DefaultHotfixConfig.xml 파일 복사 \(에서 제공 하는 합니다 **%systemroot%\\System32\\WindowsPowerShell\\v1.0\\모듈\\ ClusterAwareUpdating** CAU 도구가 설치 되어 있는 컴퓨터의 폴더\) 핫픽스를 추출 하는 사용자가 만든 핫픽스 루트 폴더에 있습니다. 예를 들어 구성 파일을 복사 합니다  *\\ \\MyFileServer\\핫픽스\\루트\\*합니다. 

    > [!NOTE]
    > Microsoft 및 기타 업데이트에서 제공하는 대부분의 핫픽스를 설치하려면 기본 핫픽스 구성 파일을 수정하지 않고 사용하면 됩니다. 시나리오에 필요한 경우 고급 작업으로 구성 파일을 사용자 지정할 수 있습니다. 예를 들어 특정 확장명이 있는 핫픽스 파일을 처리하거나 특정 종료 조건에 대한 동작을 정의하려면 이 구성 파일을 사용자 지정 규칙에 포함할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 있는 [핫픽스 구성 파일 사용자 지정](#BKMK_CONFIG_FILE)을 참조하세요.

### <a name="configuration"></a>Configuration

다음 설정을 구성합니다. 자세한 내용은 이 항목의 뒷부분에 있는 섹션의 링크를 참조하세요.
- 적용할 업데이트 및 핫픽스 구성 파일이 포함된 공유 핫픽스 루트 폴더의 경로. CAU UI에서이 경로 입력 하거나 구성할 수 있습니다 합니다 **HotfixRootFolderPath\=\<경로 >** PowerShell 플러그\-in 인수입니다. 

   > [!NOTE]
   > 폼의 UNC 경로 또는 로컬 폴더 경로로 핫픽스 루트 폴더를 지정할 수 있습니다  *\\ \\ServerName\\공유\\RootFolderName*합니다. 도메인\-기반 또는 독립 실행형 DFS Namespace 경로 사용할 수 있습니다. 그러나 플러그\-액세스를 확인 하는 기능은에서 핫픽스 구성 파일에서 권한을 하지 않으므로 DFS Namespace 경로 호환 구성 하거나 CAU UI를 사용 하 여 액세스 권한 확인을 해제 해야 하나를 구성 하는 경우는 **DisableAclChecks\='True'** 플러그 인\-in 인수입니다.
- 폴더에 액세스 하 고 SMB에서 액세스 하는 데이터의 무결성을 보장 하는 데 필요한 권한을 확인 하려면 핫픽스 루트 폴더를 호스팅하는 서버에서 설정을 공유 폴더 \(SMB 서명 또는 SMB 암호화\)합니다. 자세한 내용은 [핫픽스 루트 폴더에 대한 액세스 제한](#BKMK_ACL)를 참조하세요.

### <a name="additional-options"></a>추가 옵션

- 필요에 따라 플러그 구성\-에 있으므로 해당 SMB 암호화가 적용 핫픽스 파일 공유에서 데이터에 액세스 하는 경우. CAU ui에서에 **추가 옵션** 페이지에서 선택 합니다 **핫픽스 루트 폴더에 액세스할 때 SMB 암호화 필요** 옵션을 사용 하거나 구성를 **RequireSMBEncryption\= 'True'** PowerShell 플러그\-in 인수입니다. 
  > [!IMPORTANT]
  > SMB 서명 또는 SMB 암호화를 통해 SMB 데이터 무결성을 보장하려면 SMB 서버에서 추가 구성 단계를 수행해야 합니다. 자세한 내용은 [핫픽스 루트 폴더에 대한 액세스 제한](#BKMK_ACL)의 4단계를 참조하세요. SMB 암호화 사용을 적용하는 옵션을 선택했는데 핫픽스 루트 폴더가 SMB 암호화를 사용해 액세스하도록 구성되어 있지 않으면 업데이트 실행이 실패하게 됩니다.
- 필요한 경우 핫픽스 루트 폴더 및 핫픽스 구성 파일에 대한 기본 권한 확인을 사용하지 않도록 설정합니다. CAU ui에서 선택 **핫픽스 루트 폴더 및 구성 파일에 대 한 관리자 액세스 검사 사용 안 함**, 구성 또는 합니다 **DisableAclChecks\='True'** 플러그\-에서 인수입니다.
- 필요에 따라 구성 합니다 **HotfixInstallerTimeoutMinutes\= <Integer>**  핫픽스 기간을 지정 하는 인수 연결\-핫픽스 설치 관리자 프로세스 복귀를 기다리는에서. \(기본값은 30 분입니다.\) 예를 들어 2 시간 제한 기간을 지정 하려면 설정 **HotfixInstallerTimeoutMinutes\=120**합니다.
- 필요에 따라 구성 합니다 **HotfixConfigFileName \= <name>**  플러그\-핫픽스 루트 폴더에 있는 핫픽스 구성 파일의 이름을 지정 하는 인수에 있습니다. 이름을 지정하지 않으면 기본 이름인 DefaultHotfixConfig.xml이 사용됩니다.
  
### <a name="BKMK_HF_ROOT"></a>핫픽스 루트 폴더 구조 구성

핫픽스 플러그\-에서 작동 하려면 핫픽스가에 저장 되어야 합니다는 제대로\-SMB 파일 공유에서 정의 된 구조인 \(핫픽스 루트 폴더\), 핫픽스 플러그 인을 구성 해야 합니다\-경로를 사용 하 여 로그인 합니다 CAU UI 또는 CAU PowerShell cmdlet을 사용 하 여 핫픽스 루트 폴더입니다. 이 경로 플러그 인에 전달 됩니다\-에서의 **HotfixRootFolderPath** 인수입니다. 다음 예제에 표시된 대로 업데이트 필요에 따라 핫픽스 루트 폴더에 대한 몇 가지 구조 중 하나를 선택할 수 있습니다. 구조를 준수하지 않는 파일이나 폴더는 무시됩니다.  
  
#### <a name="example-1---folder-structure-used-to-apply-hotfixes-to-all-cluster-nodes"></a>모든 클러스터 노드에 핫픽스를 적용 하는 데 사용 되는 예제 1-폴더 구조
  
핫픽스가 모든 클러스터 노드에 적용 되도록를 지정 하려면 폴더에 복사 **CAUHotfix\_모든** 핫픽스 루트 폴더입니다. 이 예제는 **HotfixRootFolderPath** 플러그\-인수로 설정 되어 *\\ \\MyFileServer\\핫픽스\\루트\\*. 합니다 **CAUHotfix\_모든** 폴더에는 확장명이.msu,.msi 및.msp 모든 클러스터 노드에 적용 될 업데이트 세 개가 포함 되어 있습니다. 업데이트 파일 이름은 설명을 위한 용도로만 제공됩니다.  
  
> [!NOTE]  
> 이 예제와 다음 예제에서 기본 이름이 DefaultHotfixConfig.xml인 핫픽스 구성 파일은 핫픽스 루트 폴더의 필요한 위치에 표시됩니다.  
  
```
\\MyFileServer\Hotfixes\Root\   
   DefaultHotfixConfig.xml  
   CAUHotfix_All\   
      Update1.msu   
      Update2.msi   
      Update3.msp  
      ...  
```  
  
#### <a name="example-2---folder-structure-used-to-apply-certain-updates-only-to-a-specific-node"></a>특정 업데이트를 특정 노드에만 적용 하는 데 사용 되는 예제 2-폴더 구조
  
특정 노드에만 적용되는 핫픽스를 지정하려면 노드 이름에 핫픽스 루트 폴더 아래의 하위 폴더를 사용합니다. 예를 들어 클러스터 노드의 NetBIOS 이름인 *ContosoNode1*을 사용합니다. 그런 다음 이 노드에만 적용되는 업데이트를 이 하위 폴더로 이동합니다. 다음 예제에서는 **HotfixRootFolderPath** 플러그\-인수로 설정 되어  *\\ \\MyFileServer\\핫픽스\\루트\\*. 업데이트를 **CAUHotfix\_모든** 폴더를 모든 클러스터 노드에 적용할 및 *Node1\_특정\_Update.msu* 에게만적용할*ContosoNode1*합니다.  
  
```
\\MyFileServer\Hotfixes\Root\   
   DefaultHotfixConfig.xml  
   CAUHotfix_All\   
      Update1.msu   
      Update2.msi   
      Update3.msp  
      ...  
   ContosoNode1\   
      Node1_Specific_Update.msu   
      ...  
```  
  
#### <a name="example-3---folder-structure-used-to-apply-updates-other-than-msu-msi-and-msp-files"></a>예제 3-폴더 구조.msu,.msi 및.msp 파일 이외의 업데이트를 적용 하는 데 사용
  
기본적으로 **Microsoft.HotfixPlugin**은 확장명이 .msu, .msi 또는 .msp인 업데이트만 적용합니다. 그러나 특정 업데이트는 확장명이 다르며, 다른 설치 명령이 필요할 수 있습니다. 예를 들어 확장명이 .exe인 펌웨어 업데이트를 클러스터의 노드에 적용해야 할 수 있습니다. 비 특정 나타내는 하위 폴더를 사용 하 여 핫픽스 루트 폴더를 구성할 수 있습니다\-기본 업데이트 유형을 설치 해야 합니다. 또한 핫픽스 구성 XML 파일의 `<FolderRules>` 요소에 설치 명령을 지정하는 해당 폴더 설치 규칙을 구성해야 합니다.  
  
다음 예제에서는 **HotfixRootFolderPath** 플러그\-인수로 설정 되어  *\\ \\MyFileServer\\핫픽스\\루트\\*. 여러 업데이트가 모든 클러스터 노드에 적용되며, 펌웨어 업데이트 *SpecialHotfix1.exe*는 *FolderRule1*을 사용하여 *ContosoNode1*에 적용됩니다. 핫픽스 구성 파일에서 *ContosoNode1* 을 구성하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [핫픽스 구성 파일 사용자 지정](#BKMK_CONFIG_FILE) 을 참조하세요.  
  
```
\\MyFileServer\Hotfixes\Root\   
   DefaultHotfixConfig.xml  
   CAUHotfix_All\   
      Update1.msu   
      Update2.msi   
      Update3.msp  
      ...  
  
   ContosoNode1\   
      FolderRule1\  
          SpecialHotfix1.exe  
      ...  
```

### <a name="BKMK_CONFIG_FILE"></a>핫픽스 구성 파일 사용자 지정  
핫픽스 구성 파일은 **Microsoft.HotfixPlugin** 이 장애 조치(failover) 클러스터에 특정 핫픽스 파일 형식을 설치하는 방식을 제어합니다. 구성 파일의 XML 스키마는 HotfixConfigSchema.xsd에 정의되며, 이 파일은 CAU 도구가 설치되어 있는 컴퓨터의 다음 폴더에 있습니다.  
  
**%systemroot%\\System32\\WindowsPowerShell\\v1.0\\모듈\\ClusterAwareUpdating 폴더**  
  
핫픽스 구성 파일을 사용자 지정하려면 이 위치에서 핫픽스 루트 폴더로 예제 구성 파일 DefaultHotfixConfig.xml을 복사한 다음 시나리오에 맞게 적절히 수정합니다.  
  
> [!IMPORTANT]  
> Microsoft 및 기타 업데이트에서 제공하는 대부분의 핫픽스를 적용하려면 기본 핫픽스 구성 파일을 수정하지 않고 사용하면 됩니다. 핫픽스 구성 파일의 사용자 지정은 고급 사용 시나리오에서만 사용되는 작업입니다.  
  
기본적으로 핫픽스 구성 XML 파일은 다음 두 가지 범주의 핫픽스에 대한 설치 규칙 및 종료 조건을 정의합니다.  
  
-   확장명이 있는 핫픽스 파일을 플러그\-기본적으로 설치할 수 있습니다 \(.msu,.msi 및.msp 파일\)합니다.  
  
    `<ExtensionRules>` 요소의 `<DefaultRules>` 요소로 정의되며, 지원되는 기본 파일 형식마다 하나의 `<Extension>` 요소가 있습니다. 일반적인 XML 구조는 다음과 같습니다.  
  
    ```xml  
    <DefaultRules>  
        <ExtensionRules>  
          <Extension name="MSI">  
            <!-- Template and ExitConditions elements for installation of .msi files follow -->  
             ...  
          </Extension>  
          <Extension name="MSU">  
            <!-- Template and ExitConditions elements for installation of .msu files follow -->  
             ...  
          </Extension>  
          <Extension name="MSP">  
            <!-- Template and ExitConditions elements for installation of .msp files follow -->  
             ...  
          </Extension>  
             ...  
       </ExtensionRules>  
    </DefaultRules>  
    ```  
  
    사용자 환경의 모든 클러스터 노드에 특정 업데이트 유형을 적용해야 하는 경우 추가 `<Extension>` 요소를 정의할 수 있습니다.  
  
-   핫픽스나 다른 업데이트.msi,.msu 또는.msp 파일이 아닌 되지 않은 파일\-Microsoft 드라이버, 펌웨어 및 BIOS 업데이트 합니다.  
  
    각 비\-기본 파일 형식으로 구성 된를 `<Folder>` 요소에는 `<FolderRules>` 요소입니다. `<Folder>` 요소의 이름 특성은 핫픽스 루트 폴더에서 해당 유형의 업데이트가 포함되는 폴더의 이름과 동일해야 합니다. 폴더에 있을 수 있습니다 합니다 **CAUHotfix\_모든** 폴더 또는 노드\-특정 폴더입니다. 예를 들어 *FolderRule1* 이 핫픽스 루트 폴더에 구성된 경우 XML 파일에서 해당 폴더의 업데이트에 대한 설치 템플릿 및 종료 조건을 정의하는 다음 요소를 구성합니다.  
  
    ```xml  
    <FolderRules>  
          <Folder name="FolderRule1">  
            <!-- Template and ExitConditions elements for installation of updates in FolderRule1 follow -->  
             ...  
          </Folder>  
          ...  
    </FolderRules>  
    ```  
  
다음 표에서는 `<Template>` 특성 및 가능한 `<ExitConditions>` 하위 요소에 대해 설명합니다.  
  
|`<Template>` 특성|설명|  
|--------------------------|---------------|  
|`path`|`<Extension name>` 특성에 정의된 파일 형식에 대한 설치 프로그램의 전체 경로입니다.<br /><br />핫픽스 루트 폴더 구조 내 업데이트 파일의 경로를 지정하려면 `$update$`를 사용합니다.|  
|`parameters`|`path`에 지정된 프로그램에 대한 필수 및 선택적 매개 변수 문자열입니다.<br /><br />핫픽스 루트 폴더 구조 내 업데이트 파일의 경로인 매개 변수를 지정하려면 `$update$`를 사용합니다.|  
  
|`<ExitConditions>` 하위 요소|설명|  
|---------------------------------|---------------|  
|`<Success>`|지정된 업데이트가 성공했음을 나타내는 하나 이상의 종료 코드를 정의합니다. 이는 필수 하위 요소입니다.|  
|`<Success_RebootRequired>`|지정된 업데이트가 성공했으며 노드를 다시 시작해야 함을 나타내는 하나 이상의 종료 코드를 선택적으로 정의합니다. <br>**참고:** 필요한 경우 `<Folder>` 요소에 `alwaysReboot` 특성을 포함할 수 있습니다. 이 특성을 설정하면 이 규칙에 의해 설치된 핫픽스가 `<Success>`에 정의된 종료 코드 중 하나를 반환하는 경우 `<Success_RebootRequired>` 종료 조건으로 해석됩니다.|  
|`<Fail_RebootRequired>`|지정된 업데이트가 실패했으며 노드를 다시 시작해야 함을 나타내는 하나 이상의 종료 코드를 선택적으로 정의합니다.|  
|`<AlreadyInstalled>`|지정된 업데이트가 이미 설치되어 있어 적용되지 않았음을 나타내는 하나 이상의 종료 코드를 선택적으로 정의합니다.|  
|`<NotApplicable>`|지정된 업데이트가 클러스터 노드에 적용되지 않아 적용하지 못했음을 나타내는 하나 이상의 종료 코드를 선택적으로 정의합니다.|  
  
> [!IMPORTANT]  
> `<ExitConditions>` 에 명시적으로 정의되지 않은 모든 종료 코드는 업데이트 실패로 해석되며, 노드는 다시 시작되지 않습니다.  
  
### <a name="BKMK_ACL"></a>핫픽스 루트 폴더에 대 한 액세스 제한  
**Microsoft.HotfixPlugin**의 컨텍스트에서만 액세스할 수 있도록 하여 핫픽스 루트 폴더 파일과 핫픽스 구성 파일의 보안을 유지하도록 SMB 파일 서버 및 파일 공유를 구성하려면 몇 가지 단계를 수행해야 합니다. 이러한 단계를 수행하면 장애 조치(failover) 클러스터를 손상시킬 수 있는 방식의 핫픽스 파일 변조를 방지하는 데 도움이 되는 몇 가지 기능이 설정됩니다.  
  
일반적인 단계는 다음과 같습니다.  
  
1.  플러그를 사용 하 여 업데이트 실행에 사용 되는 사용자 계정을 식별할\-에서  
  
2.  SMB 파일 서버의 필요한 그룹에서 이 사용자 계정 구성  
  
3.  핫픽스 루트 폴더 액세스 권한 구성  
  
4.  SMB 데이터 무결성에 대한 설정 구성  
  
5.  SMB 서버에서 Windows 방화벽 규칙 사용  
  
#### <a name="step-1-identify-the-user-account-that-is-used-for-updating-runs-by-using-the-hotfix-plug-in"></a>1단계. 핫픽스 플러그 인을 사용 하 여 업데이트 실행에 사용 되는 사용자 계정을 식별할\-에서
  
하 여 업데이트 실행을 수행 하는 동안 보안 설정을 확인 하려면 CAU에 사용 되는 계정이 **Microsoft.HotfixPlugin** CAU를 원격에서 사용 되는지 여부에 따라 달라 집니다\-모드 또는 자체 업데이트\-로 업데이트 모드 다음과 같습니다.  
  
-   **원격\-업데이트 모드** 미리 보기 업데이트를 적용 하는 클러스터에 대 한 관리 권한이 있는 계정입니다.  
  
-   **Self\-업데이트 모드** 클러스터 된 역할을 CAU에 대 한 Active Directory에 구성 된 가상 컴퓨터 개체의 이름입니다. CAU 클러스터된 역할에 대해 Active Directory에서 사전 준비된 가상 컴퓨터 개체 이름이거나, 클러스터된 역할에 대해 CAU에서 생성되는 이름입니다. CAU에서 생성 되는 경우 이름을 가져오려면를 실행 합니다 **가져옵니다\-CauClusterRole** CAU PowerShell cmdlet. 출력에서 **ResourceGroupName**이 생성된 가상 컴퓨터 개체 계정의 이름입니다.  
  
#### <a name="step-2-configure-this-user-account-in-the-necessary-groups-on-an-smb-file-server"></a>2단계. SMB 파일 서버의 필요한 그룹에서 이 사용자 계정 구성
  
> [!IMPORTANT]  
> 업데이트 실행에 사용되는 계정을 SMB 서버에서 로컬 관리자 계정으로 추가해야 합니다. 조직의 보안 정책 때문에 이 작업이 허용되지 않으면 다음 절차를 사용하여 SMB 서버에서 필요한 사용 권한으로 이 계정을 구성합니다.  
  
##### <a name="to-configure-a-user-account-on-the-smb-server"></a>SMB 서버에서 사용자 계정을 구성하려면  
  
1.  업데이트 실행에 사용되는 계정을 Distributed COM Users 그룹과 Power User, Server Operation 또는 Print Operator 그룹에 추가합니다.  
  
2.  계정에 대해 필요한 WMI 권한을 사용하도록 설정하려면 SMB 서버에서 WMI 관리 콘솔을 시작합니다. PowerShell을 시작 하 고 다음 명령을 입력 합니다.  
  
    ```  
    wmimgmt.msc  
    ```  
  
3.  콘솔 트리에서 마우스 오른쪽\-클릭 **WMI 컨트롤 \(로컬\)** 를 클릭 하 고 **속성**합니다.  
  
4.  **보안**을 클릭하고 **루트**를 확장합니다.  
  
5.  **CIMV2**를 클릭한 다음 **보안**을 클릭합니다.  
  
6.  업데이트 실행에 사용되는 계정을 **그룹 또는 사용자 이름** 목록에 추가합니다.  
  
7.  업데이트 실행에 사용되는 계정에 **메서드 실행** 및 **원격으로부터 사용 가능** 권한을 부여합니다.  
  
#### <a name="step-3-configure-permissions-to-access-the-hotfix-root-folder"></a>3단계. 핫픽스 루트 폴더 액세스 권한 구성
  
기본적으로 업데이트를 적용 하려는 경우 핫픽스 플러그\-에서 핫픽스 루트 폴더에 대 한 액세스에 대 한 NTFS 파일 시스템 권한의 구성을 확인 합니다. 폴더 액세스 권한이 구성 되어 있지 않으면 제대로 업데이트 실행 핫픽스 플러그 인을 사용 하 여\-에 실패할 수 있습니다.  
  
핫픽스 플러그의 기본 구성을 사용 하는 경우\-에서는 폴더 액세스 권한이 다음 요구 사항을 충족 하는지 확인 합니다.  
  
-   Users 그룹에 읽기 권한이 있어야 합니다.  
  
-   하는 경우 플러그\-에서는 확장명이.exe updates 적용, 사용자 그룹에 Execute 권한을 가집니다.  
  
-   특정 보안 주체에만 허용 됩니다 \(필요 하지는 않지만\) 쓰기 또는 수정 권한이 있습니다. 허용되는 주체는 로컬 Administrators 그룹, SYSTEM, CREATOR OWNER 및 TrustedInstaller입니다. 다른 계정 또는 그룹에는 핫픽스 루트 폴더에 대한 쓰기 또는 수정 권한이 허용되지 않습니다.  
  
필요에 따라 위 확인을 해제할 수 있습니다 하는 플러그\-기본적으로 수행 합니다. 다음 두 가지 방법 중 하나로 이 작업을 수행할 수 있습니다.  
  
-   CAU PowerShell cmdlet을 사용 하는 경우 구성 된 **DisableAclChecks\='True'** 인수에는 **CauPluginArguments** 핫픽스 플러그 인에 대 한 매개 변수\-에서.  
  
-   CAU UI를 사용하는 경우 업데이트 실행 옵션을 구성하는 데 사용되는 마법사의 **추가 업데이트 옵션** 페이지에서 **핫픽스 루트 폴더 및 구성 파일에 대한 관리자 권한 확인 안 함** 옵션을 선택합니다.  
  
그러나 대부분의 환경에서는 기본 구성을 사용하여 이러한 확인을 적용하는 것이 좋습니다.  
  
#### <a name="step-4-configure-settings-for-smb-data-integrity"></a>4단계. SMB 데이터 무결성에 대한 설정 구성
  
핫픽스 플러그 인 클러스터 노드와 SMB 파일 공유 간의 연결에서 데이터 무결성을 확인 하려면\-에 SMB 서명 또는 SMB 암호화를 위해 SMB 파일 공유에 대 한 설정을 사용 해야 합니다. 다양 한 환경에서 더 나은 성능과 향상 된 보안을 제공 하는 SMB 암호화는 Windows Server 2012부터 지원 됩니다. 이러한 설정 중 하나 또는 모두를 다음과 같이 설정할 수 있습니다.  
  
-   SMB 서명을 사용하려면 Microsoft 기술 자료 [문서 887429](https://support.microsoft.com/kb/887429) 의 절차를 참조하세요.  
  
-   SMB 공유 폴더에 SMB 암호화를 사용 하려면 SMB 서버에서 다음 PowerShell cmdlet을 실행 합니다.  
  
    ```PowerShell  
    Set-SmbShare <ShareName> -EncryptData $true  
    ```  
  
    여기서 <*ShareName*>은 SMB 공유 폴더의 이름입니다.  
  
필요에 따라 SMB 서버 연결에서 SMB 암호화 사용을 적용 하려면 선택 합니다 **핫픽스 루트 폴더에 액세스할 때 SMB 암호화 필요** CAU UI에서는 옵션 또는 구성 된 **RequireSMBEncryption \='True'** 플러그 인\-CAU PowerShell cmdlet을 사용 하 여 인수에 있습니다.  
  
> [!IMPORTANT]  
> SMB 암호화 사용을 적용하는 옵션을 선택했는데 핫픽스 루트 폴더가 SMB 암호화를 사용해 연결하도록 구성되어 있지 않으면 업데이트 실행이 실패하게 됩니다.  
  
#### <a name="step-5-enable-a-windows-firewall-rule-on-the-smb-server"></a>5단계. SMB 서버에서 Windows 방화벽 규칙 사용
  
사용 하도록 설정 해야 합니다 **파일 서버 원격 관리 \(SMB\-에서\)**  SMB 파일 서버의 Windows 방화벽에서 규칙입니다. Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012에서 기본적으로 사용 됩니다.  
  
## <a name="see-also"></a>참조  
  
-   [클러스터 인식 업데이트 개요](cluster-aware-updating.md)
  
-   [클러스터 인식 업데이트 Windows PowerShell Cmdlet](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating)  
  
-   [클러스터 인식 업데이트 플러그 인 참조](https://msdn.microsoft.com/library/hh418084.aspx)  
  
