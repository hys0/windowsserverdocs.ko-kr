---
ms.assetid: d44d4430-41e2-483a-9685-92610cdef32a
title: 클러스터 인식 업데이트 플러그 인 작동 방식
ms.topic: article
ms.prod: windows-server
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 04/28/2017
ms.technology: storage-failover-clustering
description: Windows Server에서 클러스터 인식 업데이트를 사용 하 여 클러스터에 업데이트를 설치 하는 경우 플러그 인을 사용 하 여 업데이트를 조정 하는 방법입니다.
ms.openlocfilehash: f6c572a397530704dd91d9c67c5c1758ccc085c4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361293"
---
# <a name="how-cluster-aware-updating-plug-ins-work"></a>클러스터 인식 업데이트 플러그 인 작동 방식

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

CAU ( [클러스터 인식 업데이트](cluster-aware-updating.md) )는 플러그 인을 사용 하 여 장애 조치 (failover) 클러스터의 노드 간에 업데이트 설치를 조정 합니다. 이 항목에서는 cau 플러그\-의 빌드된\-또는 CAU 용으로 설치 하는 다른 플러그\-의 사용에 대 한 정보를 제공 합니다.

## <a name="BKMK_INSTALL"></a>플러그\-설치  
**Microsoft.windowsupdateplugin** 및 **microsoft.hotfixplugin**\) \(를 사용 하 여 설치 된 기본 플러그\-기능 외의 플러그\-는 별도로 설치 해야 합니다. CAU를 자체\-업데이트 모드에서 사용 하는 경우의 플러그\-모든 클러스터 노드에 설치 해야 합니다. CAU를 원격\-업데이트 모드에서 사용 하는 경우의 플러그\-원격 업데이트 코디네이터 컴퓨터에 설치 해야 합니다. 설치 하는 플러그\-에는 각 노드에 대 한 추가 설치 요구 사항이 있을 수 있습니다.  
  
에서 플러그\-를 설치 하려면 게시자의 플러그\-에 있는 지침을 따르세요. CAU를 사용 하 여에서 플러그\-를 수동으로 등록 하려면\-플러그 인이 설치 된 각 컴퓨터에서 [register-cauplugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin) cmdlet을 실행 합니다.  
  
## <a name="specify-a-plug-in-and-plug-in-arguments"></a>에서 플러그\-지정 및 인수에\-플러그 인  
  
### <a name="specify-a-cau-plug-in"></a>에서 CAU 플러그\-지정

Cau UI에서는 CAU를 사용 하 여 다음 작업을 수행할 때 사용 가능한 플러그\-의 드롭\-다운 목록에서 플러그\-를 선택 합니다.  
  
-   클러스터에 업데이트 적용  
  
-   클러스터의 업데이트 미리 보기  
  
-   클러스터 자체\-업데이트 옵션 구성  
  
기본적으로 CAU는 **microsoft.windowsupdateplugin**에서 플러그\-를 선택 합니다. 그러나 설치 되 고 CAU에 등록 된의 모든 플러그\-를 지정할 수 있습니다.

> [!TIP]  
> CAU UI에서는 업데이트 실행 중에 업데이트를 미리 보거나 적용 하기 위해 CAU에 사용할 단일 플러그\-지정할 수 있습니다. CAU PowerShell cmdlet을 사용 하 여 하나 이상의 플러그\-기능을 지정할 수 있습니다. 클러스터에 여러 유형의 업데이트를 설치 해야 하는 경우 일반적으로의 각 플러그\-에 대해 별도의 업데이트 실행을 사용 하는 대신 하나의 업데이트 실행에서 여러 플러그\-를 지정 하는 것이 더 효율적입니다. 예를 들어 대개 노드가 다시 시작되는 횟수가 줄어듭니다.

다음 표에 나열 된 CAU PowerShell cmdlet을 사용 하 여 **– CauPluginName** 매개 변수를 전달 하 여 업데이트 실행 또는 검사에 대 한 플러그\-기능을 하나 이상 지정할 수 있습니다. 쉼표로 구분 하 여 여러 플러그\-를 이름에 지정할 수 있습니다. 플러그\-여러 개를 지정 하는 경우 **\-RunPluginsSerially**, **\-StopOnPluginFailure**및 **– SeparateReboots** 매개 변수를 지정 하 여 업데이트 실행 중에 플러그\-가 서로 어떻게 영향을 미치는지 제어할 수도 있습니다. 여러 플러그\-기능을 사용 하는 방법에 대 한 자세한 내용은 다음 표에 나와 있는 cmdlet 설명서에 제공 된 링크를 사용 하십시오.  
  
|Cmdlet|설명|  
|----------|---------------|  
|[Add-cauclusterrole](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/add-cauclusterrole)|지정 된 클러스터에 자체\-업데이트 기능을 제공 하는 CAU 클러스터 된 역할을 추가 합니다.|  
|[Invoke-caurun](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/invoke-caurun)|적용 가능한 업데이트에 대해 클러스터 노드 검사를 수행하고, 지정된 클러스터에서 업데이트 실행을 통해 해당 업데이트를 설치합니다.|  
|[Invoke-causcan](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/invoke-causcan)|적용 가능한 업데이트에 대해 클러스터 노드 검사를 수행하고, 지정된 클러스터의 각 노드에 적용되는 초기 업데이트 집합의 목록을 반환합니다.|  
|[Add-cauclusterrole](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/set-cauclusterrole)|지정된 클러스터에서 CAU 클러스터된 역할의 구성 속성을 설정합니다.|  
  
이러한 cmdlet을 사용 하 여 매개 변수에서 CAU 플러그\-를 지정 하지 않는 경우 기본값은 **microsoft.windowsupdateplugin**의 플러그\-입니다.  
  
### <a name="specify-cau-plug-in-arguments"></a>인수에 CAU 플러그\-지정  
업데이트 실행 옵션을 구성 하는 경우에서 사용할 선택 된 플러그\-에 대해 하나 이상의 *이름\=값* 쌍 \(\) 인수를 지정할 수 있습니다. 예를 들어 CAU UI에서 다음과 같은 여러 인수를 지정할 수 있습니다.  
  
**Name1\=Value1; Name2\=Value2 Name3\=Value3**  
  
이러한 *이름\=값* 쌍은 지정 하는의 플러그\-에 의미가 있어야 합니다. 일부 플러그\-의 경우 인수는 선택 사항입니다.  
  
인수의 CAU 플러그\-구문은 다음과 같은 일반 규칙을 따릅니다.  
  
-   여러 *이름\=값* 쌍은 세미콜론으로 구분 됩니다.  
  
-   공백이 포함 된 값은 따옴표로 묶습니다 (예: **Name1\="value With spaces")** .  
  
-   *값* 의 정확한 구문은의 플러그\-에 따라 달라 집니다.  
  
**– CauPluginParameters** 매개 변수를 지 원하는 CAU PowerShell cmdlet을 사용 하 여 인수에 플러그\-를 지정 하려면 다음 형식의 매개 변수를 전달 합니다.  
  
**\-CauPluginArguments @ {Name1\=Value1; Name2\=Value2 Name3\=Value3}**  
  
미리 정의 된 PowerShell 해시 테이블을 사용할 수도 있습니다. 에서 둘 이상의 플러그\-에 대 한 인수에 플러그\-를 지정 하려면 인수의 여러 해시 테이블을 쉼표로 구분 하 여 전달 합니다. **CauPluginName**에 지정 된 순서 대로 플러그\-의 인수에 플러그\-를 전달 합니다.  
  
### <a name="specify-optional-plug-in-arguments"></a>인수에 선택적 플러그\-지정  
CAU가 설치 하는 플러그\-\(**microsoft.windowsupdateplugin** 및 **microsoft.hotfixplugin**\) 선택할 수 있는 추가 옵션을 제공 합니다. CAU UI에서이 옵션은의 플러그\-에 대 한 업데이트 실행 옵션을 구성한 후 **추가 옵션** 페이지에 표시 됩니다. CAU PowerShell cmdlet을 사용 하는 경우 이러한 옵션은 인수에 선택적 플러그\-구성 됩니다. 자세한 내용은 이 항목의 뒷부분에 있는 [Microsoft.WindowsUpdatePlugin 사용](#BKMK_WUP) 및 [Microsoft.HotfixPlugin 사용](#BKMK_HFP) 을 참조하세요.  
  
## <a name="manage-plug-ins-using-windows-powershell-cmdlets"></a>Windows PowerShell cmdlet을 사용 하 여 플러그\-기능 관리  
  
|Cmdlet|설명|  
|----------|---------------|  
|[Register-cauplugin](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/get-cauplugin)|로컬 컴퓨터에 등록 된 하나 이상의 소프트웨어 업데이트 플러그\-기능에 대 한 정보를 검색 합니다.|  
|[Register-cauplugin]((https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/register-cauplugin))|CAU 소프트웨어 업데이트 플러그\-를 로컬 컴퓨터에 등록 합니다.|  
|[Register-cauplugin](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/unregister-cauplugin)|CAU에서 사용할 수 있는 플러그\-의 목록에서의 소프트웨어 업데이트 플러그\-를 제거 합니다. **참고:** CAU \(**microsoft.windowsupdateplugin** 및 **microsoft.hotfixplugin**\)를 사용 하 여 설치 된 플러그\-기능을 등록 취소할 수 없습니다.|  
  
## <a name="BKMK_WUP"></a>Microsoft.windowsupdateplugin 사용  

CAU **microsoft.windowsupdateplugin**의 기본 플러그\-는 다음 작업을 수행 합니다.
- 각 장애 조치 클러스터 노드에서 실행 중인 Microsoft 제품에 필요한 업데이트를 적용하기 위해 각 노드에서 Windows 업데이트 에이전트와 통신합니다.
- Windows 업데이트 또는 Microsoft 업데이트에서 또는 WSUS \(Server\) 온\-프레미스 Windows Server Update Services에서 직접 클러스터 업데이트를 설치 합니다.
- 선택한, 일반 배포 릴리스 \(GDR\) 업데이트만 설치 합니다. 기본적으로의 플러그\-는 중요 한 소프트웨어 업데이트만 적용 합니다. 구성이 필요하지 않습니다. 기본 구성에서 중요한 GDR 업데이트를 다운로드하여 각 노드에 설치합니다. 

> [!NOTE]
> \(기본적으로 선택 된 중요 소프트웨어 업데이트 이외의 업데이트를 적용 하려면 (예: 드라이버 업데이트\)) 매개 변수에서 선택적 플러그\-를 구성할 수 있습니다. 자세한 내용은 [Windows 업데이트 에이전트 쿼리 문자열 구성](#BKMK_QUERY)을 참조하세요.

### <a name="requirements"></a>요구 사항

- 장애 조치 (failover) 클러스터와 원격 업데이트 코디네이터 컴퓨터 \(\) 사용 하는 경우 cau에 대 한 요구 사항 [및 cau에 대 한 요구 사항 및 모범 사례](cluster-aware-updating-requirements.md)에 나열 된 원격 관리에 필요한 구성을 충족 해야 합니다.
- [Microsoft 업데이트 적용에 대한 권장 사항](cluster-aware-updating-requirements.md#BKMK_BP_WUA)을 검토한 다음 필요에 따라 장애 조치(failover) 클러스터 노드에 대한 Microsoft 업데이트 구성을 변경합니다.
- 최상의 결과를 위해서는 CAU를 사용 하 여 클러스터 및 업데이트 환경이 업데이트를 적용 하도록 제대로 구성 되었는지 확인 하기 위해 CAU 모범 사례 분석기 \(\)를 실행 하는 것이 좋습니다. 자세한 내용은 [CAU 업데이트 준비 테스트](cluster-aware-updating-requirements.md#BKMK_BPA)를 참조하세요.

> [!NOTE]
> Microsoft 사용 조건에 대한 동의가 필요하거나 사용자의 개입이 필요한 업데이트는 제외되며, 이는 수동으로 설치해야 합니다.

### <a name="additional-options"></a>추가 옵션

필요에 따라 다음 플러그\-를 인수로 지정 하 여의 플러그\-적용 되는 업데이트 집합을 확장 하거나 제한할 수 있습니다.
- 각 노드의 중요 업데이트 뿐 아니라 권장 업데이트를 적용 하도록에서 플러그\-를 구성 하려면 CAU UI의 **추가 옵션** 페이지에서 **중요 업데이트를 받을 때와 동일한 방식으로 권장 업데이트 지정** 확인란을 선택 합니다.
<br>또는 인수에서 **' IncludeRecommendedUpdates '\=' True '** 플러그\-를 구성 합니다.
- 에서 플러그\-를 구성 하려면 각 클러스터 노드에 적용 되는 GDR 업데이트 유형을 필터링 하려면 **QueryString** 플러그\-in 인수를 사용 하 여 Windows 업데이트 에이전트 쿼리 문자열을 지정 합니다. 자세한 내용은 [Windows 업데이트 에이전트 쿼리 문자열 구성](#BKMK_QUERY)을 참조하세요.

### <a name="BKMK_QUERY"></a>Windows 업데이트 에이전트 쿼리 문자열 구성  
Windows 업데이트 에이전트 \(WUA\) 쿼리 문자열을 구성 하는 **microsoft.windowsupdateplugin**의 기본 플러그\-인수에 플러그\-를 구성할 수 있습니다. 이 명령은 WUA API를 사용하여 특정 선택 조건에 따라 각 노드에 적용할 하나 이상의 Microsoft 업데이트 그룹을 식별합니다. 논리 AND 또는 논리 OR을 사용하여 여러 조건을 조합할 수 있습니다. WUA 쿼리 문자열은 다음과 같이 플러그\-in 인수에 지정 됩니다.  
  
**QueryString\="Criterion1\=Value1 and\/또는 Criterion2\=Value2 and\/or ..."**  
  
예를 들어 **Microsoft.WindowsUpdatePlugin**은 **IsInstalled**, **Type**, **IsHidden**, 및 **IsAssigned** 조건을 통해 생성된 기본 **QueryString** 인수를 사용하여 중요 업데이트를 자동으로 선택합니다.  
  
**QueryString\="IsInstalled\=0 및 Type\=' Software ' 및 IsHidden\=0 및 Isinstalled\=1"**  
  
**QueryString** 인수를 지정 하는 경우의 플러그\-에 대해 구성 된 기본 **querystring** 대신이 인수가 사용 됩니다.  
  
#### <a name="example-1"></a>예제 1
  
ID *f6ce46c1\-971c\-43f9\-a2aa\-783df125f003*에 의해 식별 되는 특정 업데이트를 설치 하는 **QueryString** 인수를 구성 하려면 다음을 수행 합니다.  
  
**QueryString\="UpdateID\=' f6ce46c1\-971c\-43f9\-a2aa\-783df125f003 ' 및 IsInstalled\=0"**  
  
> [!NOTE]  
> 위의 예제는 클러스터\-인식 업데이트 마법사를 사용 하 여 업데이트를 적용 하는 데 유효 합니다. CAU UI를 사용 하 여 자체\-업데이트 옵션을 구성 하거나 **Add\-add-cauclusterrole** 또는 **Set\-** PowerShell cmdlet을 사용 하 여 특정 업데이트를 설치 하려는 경우 두 개의 단일\-따옴표 문자를 사용 하 여 updateid 값의 형식을 지정 해야 합니다.  
>   
> **QueryString\="UpdateID\=' ' f6ce46c1\-971c\-43f9\-a2aa\-783df125f003 ' ' 및 IsInstalled\=0"**  
  
#### <a name="example-2"></a>예제 2
  
드라이버만 설치하는 **QueryString** 인수를 구성하려면  
  
**QueryString\="IsInstalled\=0 및 Type\=' Driver ' 및 IsHidden\=0"**  
  
, **Microsoft.windowsupdateplugin**에서 기본 플러그\-의 쿼리 문자열에 대 한 자세한 내용은 **isinstalled**\)와 같은 검색 조건 \(, 쿼리 문자열에 포함할 수 있는 구문에 대 한 자세한 내용은 [WUA (Windows 업데이트 에이전트) API 참조](https://go.microsoft.com/fwlink/p/?LinkId=223304)에서 검색 기준에 대 한 섹션을 참조 하세요.  
  
## <a name="BKMK_HFP"></a>Microsoft.hotfixplugin 사용  
**Microsoft.hotfixplugin** 의 플러그\-를 사용 하 여 특정 microsoft 소프트웨어 문제를 해결 하기 위해 독립적으로 다운로드 하는 microsoft 제한 된 배포 릴리스 \(LDR\) 업데이트 \(, 이전에는 qfe\)를 적용할 수 있습니다. 플러그 인은 SMB 파일 공유의 루트 폴더에서 업데이트를 설치 하 고 비\-Microsoft 드라이버, 펌웨어 및 BIOS 업데이트를 적용 하도록 사용자 지정할 수도 있습니다.

> [!NOTE]
> 핫픽스는 기술 자료 문서의 Microsoft에서 다운로드할 수 있는 경우도 있지만 고객에 게 필요한\-기준으로 제공 됩니다.

### <a name="requirements"></a>요구 사항

- 장애 조치 (failover) 클러스터와 원격 업데이트 코디네이터 컴퓨터 \(\) 사용 하는 경우 cau에 대 한 요구 사항 [및 cau에 대 한 요구 사항 및 모범 사례](cluster-aware-updating-requirements.md)에 나열 된 원격 관리에 필요한 구성을 충족 해야 합니다.
- [Microsoft.HotfixPlugin 사용에 대한 권장 사항](cluster-aware-updating-requirements.md#BKMK_BP_HF)을 검토하세요.
- 최상의 결과를 위해서는 CAU를 사용 하 여 클러스터 및 업데이트 환경이 업데이트를 적용 하도록 올바르게 구성 되어 있는지 확인 하기 위해 CAU 모범 사례 분석기 \(BPA\) 모델을 실행 하는 것이 좋습니다. 자세한 내용은 [CAU 업데이트 준비 테스트](cluster-aware-updating-requirements.md#BKMK_BPA)를 참조하세요.
- 게시자에서 업데이트를 가져온 후이를 복사 하거나 서버 메시지 블록 \(SMB\) 파일 공유 \(핫픽스 루트 폴더에 추출 합니다 .이\) 폴더는 SMB 2.0 이상을 지원 하 고, CAU가 원격 \(업데이트 모드\-에서 사용 되는 경우 모든 클러스터 노드 및 원격 업데이트 코디네이터 컴퓨터\)에서 액세스할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 있는 [핫픽스 루트 폴더 구조 구성](#BKMK_HF_ROOT)을 참조하세요. 

    > [!NOTE]
    > 기본적으로의이 플러그\-는 파일 이름 확장명이 .msu, .msi 및 .msp 인 핫픽스를 설치 합니다.

- CAU 도구가 설치 되어 있는 컴퓨터의 **% systemroot%\\System32\\WindowsPowerShell\\v 1.0\\모듈\\clusterawareupdating.dll** 폴더에 지정 된 DefaultHotfixConfig .xml 파일 \(를 복사 하 여, 사용자가 만든 핫픽스 루트 폴더에\) 핫픽스를 추출 합니다. 예를 들어 구성 파일을 *\\\\MyFileServer\\핫픽스\\루트\\* 에 복사 합니다. 

    > [!NOTE]
    > Microsoft 및 기타 업데이트에서 제공하는 대부분의 핫픽스를 설치하려면 기본 핫픽스 구성 파일을 수정하지 않고 사용하면 됩니다. 시나리오에 필요한 경우 고급 작업으로 구성 파일을 사용자 지정할 수 있습니다. 예를 들어 특정 확장명이 있는 핫픽스 파일을 처리하거나 특정 종료 조건에 대한 동작을 정의하려면 이 구성 파일을 사용자 지정 규칙에 포함할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 있는 [핫픽스 구성 파일 사용자 지정](#BKMK_CONFIG_FILE)을 참조하세요.

### <a name="configuration"></a>Configuration

다음 설정을 구성합니다. 자세한 내용은 이 항목의 뒷부분에 있는 섹션의 링크를 참조하세요.
- 적용할 업데이트 및 핫픽스 구성 파일이 포함된 공유 핫픽스 루트 폴더의 경로. CAU UI에서이 경로를 입력 하거나 인수에서 PowerShell 플러그\- **> HotfixRootFolderPath\=\<경로** 를 구성할 수 있습니다. 

   > [!NOTE]
   > 핫픽스 루트 폴더를 로컬 폴더 경로 또는\\형식의 UNC 경로 ( *\\ServerName\\공유\\RootFolderName*)로 지정할 수 있습니다. 도메인\-기반 또는 독립 실행형 DFS 네임 스페이스 경로를 사용할 수 있습니다. 그러나 핫픽스 구성 파일에서 액세스 권한을 확인 하는 기능에 포함 된 플러그\-는 DFS 네임 스페이스 경로와 호환 되지 않으므로이를 구성 하는 경우 CAU UI를 사용 하 여 액세스 권한 확인을 사용 하지 않도록 설정 하거나 인수에서 **' True ' 플러그\-\=Disableaclchecks** 를 구성 해야 합니다.
- 핫픽스 루트 폴더를 호스트 하는 서버의 설정으로, 폴더에 액세스할 수 있는 적절 한 권한이 있는지 확인 하 고 smb 공유 폴더 \(SMB 서명 또는 SMB 암호화\)에서 액세스 되는 데이터의 무결성을 확인 합니다. 자세한 내용은 [핫픽스 루트 폴더에 대한 액세스 제한](#BKMK_ACL)를 참조하세요.

### <a name="additional-options"></a>추가 옵션

- 필요한 경우 핫픽스 파일 공유에서 데이터에 액세스할 때 SMB 암호화가 적용 되도록 플러그\-를 구성 합니다. CAU UI의 **추가 옵션** 페이지에서 **핫픽스 루트 폴더에 액세스할 때 SMB 암호화 필요** 옵션을 선택 하거나, 인수에 **RequireSMBEncryption\=' True '** PowerShell 플러그\-를 구성 합니다. 
  > [!IMPORTANT]
  > SMB 서명 또는 SMB 암호화를 통해 SMB 데이터 무결성을 보장하려면 SMB 서버에서 추가 구성 단계를 수행해야 합니다. 자세한 내용은 [핫픽스 루트 폴더에 대한 액세스 제한](#BKMK_ACL)의 4단계를 참조하세요. SMB 암호화 사용을 적용하는 옵션을 선택했는데 핫픽스 루트 폴더가 SMB 암호화를 사용해 액세스하도록 구성되어 있지 않으면 업데이트 실행이 실패하게 됩니다.
- 필요한 경우 핫픽스 루트 폴더 및 핫픽스 구성 파일에 대한 기본 권한 확인을 사용하지 않도록 설정합니다. CAU UI에서 **핫픽스 루트 폴더 및 구성 파일에 대 한 관리자 액세스를 사용 하지 않도록 설정**을 선택 하거나 인수에서 **' True ' 플러그\-\=disableaclchecks** 를 구성 합니다.
- 필요에 따라 **필요한 경우 hotfixinstallertimeoutminutes\=<Integer>** 인수를 구성 하 여 핫픽스 플러그\-인이 핫픽스 설치 관리자 프로세스가 반환 될 때까지 대기 하는 기간을 지정 합니다. \(기본값은 30 분입니다. 예\) 들어 2 시간의 제한 시간을 지정 하려면 **필요한 경우 hotfixinstallertimeoutminutes\=120**를 설정 합니다.
- 필요에 따라 **필요한 경우 hotfixconfigfilename \= <name>** 플러그\-에 구성 하 여 핫픽스 루트 폴더에 있는 핫픽스 구성 파일의 이름을 지정 합니다. 이름을 지정하지 않으면 기본 이름인 DefaultHotfixConfig.xml이 사용됩니다.
  
### <a name="BKMK_HF_ROOT"></a>핫픽스 루트 폴더 구조 구성

에서 핫픽스 플러그\-을 작동 하려면 핫픽스 루트 폴더\)\(SMB 파일 공유에 정의 된 잘\-구조에 핫픽스를 저장 해야 하며, CAU UI 또는 CAU PowerShell cmdlet을 사용 하 여 핫픽스 루트 폴더에 대 한 경로를 사용 하 여에서 핫픽스 플러그\-을 구성 해야 합니다. 이 경로는 **HotfixRootFolderPath** 인수로의 플러그\-전달 됩니다. 다음 예제에 표시된 대로 업데이트 필요에 따라 핫픽스 루트 폴더에 대한 몇 가지 구조 중 하나를 선택할 수 있습니다. 구조를 준수하지 않는 파일이나 폴더는 무시됩니다.  
  
#### <a name="example-1---folder-structure-used-to-apply-hotfixes-to-all-cluster-nodes"></a>예 1-모든 클러스터 노드에 핫픽스를 적용 하는 데 사용 되는 폴더 구조
  
모든 클러스터 노드에 핫픽스를 적용 하도록 지정 하려면 핫픽스 루트 폴더 아래에 있는 **\_CAUHotfix** 라는 폴더에 핫픽스를 복사 합니다. 이 예제에서 **HotfixRootFolderPath** 플러그\-in 인수는 *\\\\MyFileServer\\핫픽스\\루트\\* 로 설정 됩니다. **CAUHotfix\_all** 폴더에는 모든 클러스터 노드에 적용 되는 확장명이 .msu, .msi 및 .msp 인 3 개의 업데이트가 포함 되어 있습니다. 업데이트 파일 이름은 설명을 위한 용도로만 제공됩니다.  
  
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
  
#### <a name="example-2---folder-structure-used-to-apply-certain-updates-only-to-a-specific-node"></a>예제 2-특정 업데이트를 특정 노드에만 적용 하는 데 사용 되는 폴더 구조
  
특정 노드에만 적용되는 핫픽스를 지정하려면 노드 이름에 핫픽스 루트 폴더 아래의 하위 폴더를 사용합니다. 예를 들어 클러스터 노드의 NetBIOS 이름인 *ContosoNode1*을 사용합니다. 그런 다음 이 노드에만 적용되는 업데이트를 이 하위 폴더로 이동합니다. 다음 예제에서는 **HotfixRootFolderPath** 플러그\-in 인수를 *\\\\MyFileServer\\핫픽스\\Root\\* 로 설정 합니다. **CAUHotfix\_all** 폴더의 업데이트는 모든 클러스터 노드에 적용 되 고 *노드 1\_특정\_업데이트* 에 적용 됩니다. msu는 *ContosoNode1*에만 적용 됩니다.  
  
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
  
#### <a name="example-3---folder-structure-used-to-apply-updates-other-than-msu-msi-and-msp-files"></a>예제 3-.msu, .msi 및 .msp 파일 이외의 업데이트를 적용 하는 데 사용 되는 폴더 구조
  
기본적으로 **Microsoft.HotfixPlugin**은 확장명이 .msu, .msi 또는 .msp인 업데이트만 적용합니다. 그러나 특정 업데이트는 확장명이 다르며, 다른 설치 명령이 필요할 수 있습니다. 예를 들어 확장명이 .exe인 펌웨어 업데이트를 클러스터의 노드에 적용해야 할 수 있습니다. 핫픽스 루트 폴더를 구성 하 여\-기본이 아닌 특정 업데이트 유형을 설치 해야 함을 나타내는 하위 폴더로 구성할 수 있습니다. 또한 핫픽스 구성 XML 파일의 `<FolderRules>` 요소에 설치 명령을 지정하는 해당 폴더 설치 규칙을 구성해야 합니다.  
  
다음 예제에서는 **HotfixRootFolderPath** 플러그\-in 인수를 *\\\\MyFileServer\\핫픽스\\Root\\* 로 설정 합니다. 여러 업데이트가 모든 클러스터 노드에 적용되며, 펌웨어 업데이트 *SpecialHotfix1.exe*는 *FolderRule1*을 사용하여 *ContosoNode1*에 적용됩니다. 핫픽스 구성 파일에서 *ContosoNode1* 을 구성하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [핫픽스 구성 파일 사용자 지정](#BKMK_CONFIG_FILE) 을 참조하세요.  
  
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
  
**% systemroot%\\System32\\WindowsPowerShell\\v 1.0\\모듈\\Clusterawareupdating.dll 폴더**  
  
핫픽스 구성 파일을 사용자 지정하려면 이 위치에서 핫픽스 루트 폴더로 예제 구성 파일 DefaultHotfixConfig.xml을 복사한 다음 시나리오에 맞게 적절히 수정합니다.  
  
> [!IMPORTANT]  
> Microsoft 및 기타 업데이트에서 제공하는 대부분의 핫픽스를 적용하려면 기본 핫픽스 구성 파일을 수정하지 않고 사용하면 됩니다. 핫픽스 구성 파일의 사용자 지정은 고급 사용 시나리오에서만 사용되는 작업입니다.  
  
기본적으로 핫픽스 구성 XML 파일은 다음 두 가지 범주의 핫픽스에 대한 설치 규칙 및 종료 조건을 정의합니다.  
  
-   플러그\-확장을 포함 하는 핫픽스 파일은 기본적으로 \(.msu, .msi 및 .msp 파일\)으로 설치할 수 있습니다.  
  
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
  
-   .Msi, .msu 또는 .msp 파일이 아닌 핫픽스 또는 기타 업데이트 파일 (예: 비\-Microsoft 드라이버, 펌웨어 및 BIOS 업데이트).  
  
    \-기본이 아닌 각 기본 파일 형식은 `<FolderRules>` 요소의 `<Folder>` 요소로 구성 됩니다. `<Folder>` 요소의 이름 특성은 핫픽스 루트 폴더에서 해당 유형의 업데이트가 포함되는 폴더의 이름과 동일해야 합니다. 폴더는 **CAUHotfix\_All** 폴더 또는 노드\-특정 폴더에 있을 수 있습니다. 예를 들어 *FolderRule1* 이 핫픽스 루트 폴더에 구성된 경우 XML 파일에서 해당 폴더의 업데이트에 대한 설치 템플릿 및 종료 조건을 정의하는 다음 요소를 구성합니다.  
  
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
|`<Success_RebootRequired>`|지정된 업데이트가 성공했으며 노드를 다시 시작해야 함을 나타내는 하나 이상의 종료 코드를 선택적으로 정의합니다. <br>**참고:** 선택적으로 `<Folder>` 요소는 `alwaysReboot` 특성을 포함할 수 있습니다. 이 특성을 설정하면 이 규칙에 의해 설치된 핫픽스가 `<Success>`에 정의된 종료 코드 중 하나를 반환하는 경우 `<Success_RebootRequired>` 종료 조건으로 해석됩니다.|  
|`<Fail_RebootRequired>`|지정된 업데이트가 실패했으며 노드를 다시 시작해야 함을 나타내는 하나 이상의 종료 코드를 선택적으로 정의합니다.|  
|`<AlreadyInstalled>`|지정된 업데이트가 이미 설치되어 있어 적용되지 않았음을 나타내는 하나 이상의 종료 코드를 선택적으로 정의합니다.|  
|`<NotApplicable>`|지정된 업데이트가 클러스터 노드에 적용되지 않아 적용하지 못했음을 나타내는 하나 이상의 종료 코드를 선택적으로 정의합니다.|  
  
> [!IMPORTANT]  
> `<ExitConditions>` 에 명시적으로 정의되지 않은 모든 종료 코드는 업데이트 실패로 해석되며, 노드는 다시 시작되지 않습니다.  
  
### <a name="BKMK_ACL"></a>핫픽스 루트 폴더에 대 한 액세스 제한  
**Microsoft.HotfixPlugin**의 컨텍스트에서만 액세스할 수 있도록 하여 핫픽스 루트 폴더 파일과 핫픽스 구성 파일의 보안을 유지하도록 SMB 파일 서버 및 파일 공유를 구성하려면 몇 가지 단계를 수행해야 합니다. 이러한 단계를 수행하면 장애 조치(failover) 클러스터를 손상시킬 수 있는 방식의 핫픽스 파일 변조를 방지하는 데 도움이 되는 몇 가지 기능이 설정됩니다.  
  
일반적인 단계는 다음과 같습니다.  
  
1.  의 플러그\-를 사용 하 여 업데이트 실행에 사용 되는 사용자 계정을 식별 합니다.  
  
2.  SMB 파일 서버의 필요한 그룹에서 이 사용자 계정 구성  
  
3.  핫픽스 루트 폴더 액세스 권한 구성  
  
4.  SMB 데이터 무결성에 대한 설정 구성  
  
5.  SMB 서버에서 Windows 방화벽 규칙 사용  
  
#### <a name="step-1-identify-the-user-account-that-is-used-for-updating-runs-by-using-the-hotfix-plug-in"></a>1단계. 에서 핫픽스 플러그\-를 사용 하 여 업데이트 실행에 사용 되는 사용자 계정을 식별 합니다.
  
**Microsoft.hotfixplugin** 를 사용 하 여 업데이트 실행을 수행 하는 동안 cau에서 보안 설정을 확인 하는 데 사용 되는 계정은 다음과 같이 cau가 원격\-업데이트 모드에서 사용 되는지 아니면 자체\-업데이트 모드에서 사용 되는지에 따라 달라 집니다.  
  
-   **원격\-업데이트 모드** 업데이트를 미리 보고 적용 하기 위해 클러스터에 대 한 관리 권한이 있는 계정입니다.  
  
-   **자체\-업데이트 모드** CAU 클러스터 된 역할에 대 한 Active Directory에서 구성 된 가상 컴퓨터 개체의 이름입니다. CAU 클러스터된 역할에 대해 Active Directory에서 사전 준비된 가상 컴퓨터 개체 이름이거나, 클러스터된 역할에 대해 CAU에서 생성되는 이름입니다. CAU에서 생성 되는 경우 이름을 가져오려면 **Get\-Add-cauclusterrole** CAU PowerShell cmdlet을 실행 합니다. 출력에서 **ResourceGroupName**이 생성된 가상 컴퓨터 개체 계정의 이름입니다.  
  
#### <a name="step-2-configure-this-user-account-in-the-necessary-groups-on-an-smb-file-server"></a>2단계. SMB 파일 서버의 필요한 그룹에서 이 사용자 계정 구성
  
> [!IMPORTANT]  
> 업데이트 실행에 사용되는 계정을 SMB 서버에서 로컬 관리자 계정으로 추가해야 합니다. 조직의 보안 정책 때문에 이 작업이 허용되지 않으면 다음 절차를 사용하여 SMB 서버에서 필요한 사용 권한으로 이 계정을 구성합니다.  
  
##### <a name="to-configure-a-user-account-on-the-smb-server"></a>SMB 서버에서 사용자 계정을 구성하려면  
  
1.  업데이트 실행에 사용되는 계정을 Distributed COM Users 그룹과 Power User, Server Operation 또는 Print Operator 그룹 중 하나에 추가합니다.  
  
2.  계정에 대해 필요한 WMI 권한을 사용하도록 설정하려면 SMB 서버에서 WMI 관리 콘솔을 시작합니다. PowerShell을 시작 하 고 다음 명령을 입력 합니다.  
  
    ```  
    wmimgmt.msc  
    ```  
  
3.  콘솔 트리에서 마우스 오른쪽 단추로 **WMI 컨트롤 \(로컬\)** \-클릭 한 다음 **속성**을 클릭 합니다.  
  
4.  **보안**을 클릭하고 **루트**를 확장합니다.  
  
5.  **CIMV2**를 클릭한 다음 **보안**을 클릭합니다.  
  
6.  업데이트 실행에 사용되는 계정을 **그룹 또는 사용자 이름** 목록에 추가합니다.  
  
7.  업데이트 실행에 사용되는 계정에 **메서드 실행** 및 **원격으로부터 사용 가능** 권한을 부여합니다.  
  
#### <a name="step-3-configure-permissions-to-access-the-hotfix-root-folder"></a>3단계. 핫픽스 루트 폴더 액세스 권한 구성
  
기본적으로 업데이트를 적용 하려고 하면의 핫픽스 플러그\-에서 핫픽스 루트 폴더에 대 한 액세스에 대 한 NTFS 파일 시스템 권한의 구성을 확인 합니다. 폴더 액세스 권한이 제대로 구성 되지 않은 경우에서 핫픽스 플러그\-를 사용 하 여 업데이트 실행이 실패할 수 있습니다.  
  
에서 핫픽스 플러그\-의 기본 구성을 사용 하는 경우 폴더 액세스 권한이 다음 요구 사항을 충족 하는지 확인 합니다.  
  
-   Users 그룹에 읽기 권한이 있어야 합니다.  
  
-   플러그\-의 확장명이 .exe 인 업데이트를 적용 하는 경우 Users 그룹에 실행 권한이 있어야 합니다.  
  
-   특정 보안 주체 \(허용 되지만 쓰기 또는 수정 권한이\) 필요가 없습니다. 허용되는 주체는 로컬 Administrators 그룹, SYSTEM, CREATOR OWNER 및 TrustedInstaller입니다. 다른 계정 또는 그룹에는 핫픽스 루트 폴더에 대한 쓰기 또는 수정 권한이 허용되지 않습니다.  
  
필요에 따라 플러그\-기본적으로 수행 되는 위의 검사를 사용 하지 않도록 설정할 수 있습니다. 다음 두 가지 방법 중 하나로 이 작업을 수행할 수 있습니다.  
  
-   CAU PowerShell cmdlet을 사용 하는 경우의 핫픽스 플러그\-에 대 한 **CauPluginArguments** 매개 변수에서 **disableaclchecks\=' True '** 인수를 구성 합니다.  
  
-   CAU UI를 사용하는 경우 업데이트 실행 옵션을 구성하는 데 사용되는 마법사의 **추가 업데이트 옵션** 페이지에서 **핫픽스 루트 폴더 및 구성 파일에 대한 관리자 권한 확인 안 함** 옵션을 선택합니다.  
  
그러나 대부분의 환경에서는 기본 구성을 사용하여 이러한 확인을 적용하는 것이 좋습니다.  
  
#### <a name="step-4-configure-settings-for-smb-data-integrity"></a>4단계. SMB 데이터 무결성에 대한 설정 구성
  
클러스터 노드와 SMB 파일 공유 간의 연결에서 데이터 무결성을 확인 하려면의 핫픽스 플러그\-를 사용 하려면 smb 파일 공유에서 smb 서명 또는 SMB 암호화를 위한 설정을 사용 하도록 설정 해야 합니다. 많은 환경에서 향상 된 보안 및 더 나은 성능을 제공 하는 SMB 암호화는 Windows Server 2012부터 지원 됩니다. 이러한 설정 중 하나 또는 모두를 다음과 같이 설정할 수 있습니다.  
  
-   SMB 서명을 사용하려면 Microsoft 기술 자료 [문서 887429](https://support.microsoft.com/kb/887429) 의 절차를 참조하세요.  
  
-   Smb 공유 폴더에 SMB 암호화를 사용 하도록 설정 하려면 SMB 서버에서 다음 PowerShell cmdlet을 실행 합니다.  
  
    ```PowerShell  
    Set-SmbShare <ShareName> -EncryptData $true  
    ```  
  
    여기서 <*ShareName*>은 SMB 공유 폴더의 이름입니다.  
  
필요에 따라 SMB 서버 연결에서 smb 암호화 사용을 적용 하려면 CAU UI에서 **핫픽스 루트 폴더에 액세스할 때 Smb 암호화 필요** 옵션을 선택 하거나 cau PowerShell cmdlet을 사용 하 여 인수에 **RequireSMBEncryption\=' True '** 플러그\-를 구성 합니다.  
  
> [!IMPORTANT]  
> SMB 암호화 사용을 적용하는 옵션을 선택했는데 핫픽스 루트 폴더가 SMB 암호화를 사용해 연결하도록 구성되어 있지 않으면 업데이트 실행이 실패하게 됩니다.  
  
#### <a name="step-5-enable-a-windows-firewall-rule-on-the-smb-server"></a>5단계. SMB 서버에서 Windows 방화벽 규칙 사용
  
Smb 파일 서버의 Windows 방화벽에서 **\)규칙에 있는 smb\-\(파일 서버 원격 관리** 를 사용 하도록 설정 해야 합니다. 이는 Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012에서 기본적으로 사용 하도록 설정 되어 있습니다.  
  
## <a name="see-also"></a>참고 항목  
  
-   [클러스터 인식 업데이트 개요](cluster-aware-updating.md)
  
-   [클러스터 인식 업데이트 Windows PowerShell Cmdlet](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating)  
  
-   [클러스터 인식 업데이트 플러그 인 참조](https://msdn.microsoft.com/library/hh418084.aspx)  
  
