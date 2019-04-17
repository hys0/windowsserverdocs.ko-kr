---
ms.assetid: d44d4430-41e2-483a-9685-92610cdef32a
title: "플러그 인 클러스터 인식 업데이트의 작동 방식"
ms.topic: article
ms.prod: windows-server-threshold
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 4/28/2017
ms.technology: storage-failover-clustering
description: "클러스터에 업데이트를 설치 하려면 Windows Server에서 클러스터 업데이트를 사용할 때의 업데이트를 제어 하 플러그 인을 사용 하는 방법입니다."
ms.openlocfilehash: eb606dfbe6596ecabd35e6ac36624fab2b4436b9
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="how-cluster-aware-updating-plug-ins-work"></a>플러그 인 클러스터 인식 업데이트의 작동 방식

>에 해당: (세미콜론 연간 채널) Windows Server, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

[클러스터 인식 업데이트](cluster-aware-updating.md) (CAU) 플러그 인을 사용 하 여 장애 조치 클러스터에서 노드에서 업데이트 설치를 조정할 수 있습니다. 이 항목에서 built\에서 CAU plug\ 기능 또는 CAU에 설치 하는 다른 plug\ 기능 사용에 대 한 정보를 제공 합니다.

## <a name="BKMK_INSTALL"></a>plug\ 설치  
CAU 함께 설치 하는 기본 plug\ 기능 이외에 plug\-\ (**Microsoft.WindowsUpdatePlugin** 및 **Microsoft.HotfixPlugin**\) 별도로 설치 해야 합니다. CAU 모드 self\ 업데이트에서 사용 되는 경우에 plug\ 설치 해야 일부 클러스터 노드에서 합니다. CAU 모드 remote\ 업데이트에서 사용 되는 경우에 plug\ 설치 해야 원격 업데이트 Coordinator 컴퓨터에 있습니다. plug\ 설치 하는 각 노드에서 추가 설치 요구 사항이 있을 수 있습니다.  
  
plug\를 설치 하려면 plug\에서 게시자의 지침을 따릅니다. 수동으로 CAU와에서 plug\ 등록을 실행 하 고 [등록 CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin) cmdlet에 plug\ 설치 되어 있는 각 컴퓨터에서 합니다.  
  
## <a name="specify-a-plug-in-and-plug-in-arguments"></a>Plug\ 인 및 plug\에서 인수 지정  
  
### <a name="specify-a-cau-plug-in"></a>plug\ CAU 지정

CAU UI에서 선택 plug\에서 사용 가능한 plug\ 기능 drop\ 드롭다운 목록에서 CAU를 사용 하 여 다음과 같은 작업을 수행할 때:  
  
-   클러스터에 업데이트를 적용  
  
-   클러스터에 대 한 업데이트 미리 보기  
  
-   클러스터 self\ 업데이트 옵션을 구성 합니다.  
  
기본적으로 CAU에서 plug\ 선택 **Microsoft.WindowsUpdatePlugin**합니다. 그러나 원하는 지정할 수 있습니다 plug\에는 설치 하 고 등록 CAU와 합니다.

> [!TIP]  
> CAU UI에서 plug\에서 하거나 업데이트를 적용 하는 업데이트를 실행 하는 동안 미리 보기를 사용 하 여 CAU에 대 한 번만 지정할 수 있습니다. CAU PowerShell cmdlet, 사용 하 여 하나 이상의 plug\ 기능 지정할 수 있습니다. 클러스터에 여러 종류의 업데이트를 설치 해야 할 경우 효율적 여러 plug\ 기능 지정 한 업데이트를 실행 하는 것이 아니라 각각에 대 한 업데이트를 실행 별도 사용 하 여 plug\에 있습니다. 예를 들어, 적은 노드 다시 시작 일반적으로 발생 합니다.

다음 표에서에 나열 된 CAU PowerShell cmdlet, 사용 하 여 지정할 수 있습니다 하나 이상의 plug\ 기능 업데이트를 실행 하거나 검색에 대 한 전달 하 여는 **– CauPluginName** 매개 합니다. 쉼표 사용 하 여 여러 plug\에 이름을 지정할 수 있습니다. 여러 plug\ 기능을 지정 제어할 수도 있습니다 어떻게 plug\ 기능에 영향을 다른 사용자는 업데이트를 실행 하는 동안 지정 하 여는 **\-RunPluginsSerially**, **\-StopOnPluginFailure**, 및 **– SeparateReboots** 매개 합니다. 여러 plug\ 기능을 사용 하 여에 대 한 자세한 내용은 다음 표에서 cmdlet 설명서 제공 되는 링크를 사용 합니다.  
  
|Cmdlet|설명|  
|----------|---------------|  
|[Add-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/add-cauclusterrole)|지정한 클러스터에 self\ 업데이트 기능을 제공 하는 CAU 클러스터 역할을 추가 합니다.|  
|[Invoke-CauRun](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-caurun)|해당 업데이트 클러스터 노드에서 검사를 수행 하 고 있는 지정된 클러스터 실행 업데이트를 통해 이러한 업데이트를 설치 합니다.|  
|[Invoke-CauScan](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-causcan)|해당 업데이트 클러스터 노드에서 검사를 수행 하 고 각 지정한 클러스터 노드에서에 적용 되는 업데이트의 초기 설정 목록이 반환 됩니다.|  
|[Set-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/set-cauclusterrole)|지정한 클러스터 구성 속성 CAU 클러스터 역할을 설정합니다.|  
  
기본값은에서 plug\ 이러한 cmdlet 사용 하 여 CAU plug\에 매개를 지정 하지 않으면 **Microsoft.WindowsUpdatePlugin**합니다.  
  
### <a name="specify-cau-plug-in-arguments"></a>CAU plug\에서 인수 지정  
하나 이상의 업데이트 실행 옵션을 구성 지정할 수 있습니다 *name\ = 값* plug\에서 사용 하 여 선택한 \(arguments\) 쌍 합니다. 예를 들어, CAU UI에서 다음과 같은 여러 인수를 지정할 수 있습니다.  
  
**Name1\ Value1; = Name2\ Value2; = Name3\ Value3 =**  
  
이러한 *name\ = 값* 쌍 plug\ 인에 게 의미 있어야 지정 하는 합니다. 일부 plug\ 기능에 대 한 인수가 선택 합니다.  
  
인수 CAU plug\에서 구문을 일반이 규칙 다음과 같습니다.  
  
-   여러 *name\ = 값* 쌍 세미콜론으로 구분 됩니다.  
  
-   공간을 포함 하는 값 둘러싸여, 큰따옴표 예: **Name1\ = "값 공백 사용 하 여"**합니다.  
  
-   정확한 구문을 *값* 으로 plug\ 기능에 따라 달라 집니다.  
  
Plug\에서 인수 지원 CAU PowerShell cmdlet 사용 하 여 지정 하려면는 **– CauPluginParameters** 매개 양식의 매개 전달 합니다.  
  
**\-CauPluginArguments @{Name1\ = Value1; Name2\ Value2; = Name3\ Value3 =}**  
  
미리 정의 된 PowerShell 해시 표를 사용할 수 있습니다. 하나 이상의 대 한 plug\에서 인수 지정 하려면 plug\에서 쉼표로 구분 인수 여러 해시 테이블을 전달 합니다. Plug\-순서에 지정 된 plug\에서 인수 전달 **CauPluginName**합니다.  
  
### <a name="specify-optional-plug-in-arguments"></a>(옵션) plug\ 인수 지정  
CAU 설치 plug\ 기능 \ (**Microsoft.WindowsUpdatePlugin** 및 **Microsoft.HotfixPlugin**\) 선택할 수 있는 추가 옵션을 제공 합니다. 여기에 표시 CAU UI에서는 **추가 옵션** plug\ 기능에 대 한 업데이트를 실행 옵션을 구성 하 고 나면 페이지 합니다. CAU PowerShell cmdlet, 사용 하는 경우이 옵션은 선택적 plug\ 인수도 구성 됩니다. 자세한 내용은 참조 [사용 하 여 Microsoft.WindowsUpdatePlugin](#BKMK_WUP) 및 [사용 하 여 Microsoft.HotfixPlugin](#BKMK_HFP) 이 항목 뒷부분에 있습니다.  
  
## <a name="manage-plug-ins-using-windows-powershell-cmdlets"></a>Plug\ 기능 관리 Windows PowerShell cmdlet 사용  
  
|Cmdlet|설명|  
|----------|---------------|  
|[Get-CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/get-cauplugin)|하나 이상의 소프트웨어 로컬 컴퓨터에서 등록 plug\ 기능 업데이트에 대 한 정보를 검색 합니다.|  
|[Register-CauPlugin]((https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin))|CAU 소프트웨어 plug\에서 로컬 컴퓨터에 업데이트에 등록 합니다.|  
|[Unregister-CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/unregister-cauplugin)|소프트웨어 CAU 사용할 수 있는 plug\ 기능 목록에서 plug\ 기능 업데이트를 제거 합니다. **참고:** CAU 함께 설치 된 plug\ 기능 \ (**Microsoft.WindowsUpdatePlugin** 및 **Microsoft.HotfixPlugin**\) 등록을 취소할 수 없습니다.|  
  
## <a name="BKMK_WUP"></a>사용 하 여 Microsoft.WindowsUpdatePlugin  

Plug\에서 CAU에 대 한 기본 **Microsoft.WindowsUpdatePlugin**, 다음과 같은 작업을 수행 합니다.
- 각 노드에서 실행 되는 Microsoft 제품에 대 한 필요한 업데이트를 적용 하려면 각 장애 클러스터 노드에서 Windows 업데이트 에이전트 통신할 수 있습니다.
- Microsoft 업데이트 또는 Windows 업데이트에서 직접 또는 on\ 온-프레미스 Windows Server Update Services \(WSUS\) 서버에서 클러스터 업데이트를 설치합니다.
- 선택한만 설치 일반 배포 \(GDR\) 업데이트를 릴리스 합니다. 기본적으로에서 plug\ 중요 한 소프트웨어 업데이트에만 적용 됩니다. 구성이 필요 하지 않습니다. 기본 구성 다운로드 하 고 각 노드에서 GDR 중요 업데이트를 설치 합니다. 

> [!NOTE]
> 기본적으로 선택 하는 중요 한 소프트웨어 업데이트 이외의 업데이트를 적용 하려면 \ (예: 드라이버 updates\) 선택적 plug\에 매개 구성할 수 있습니다. 자세한 내용은 참조 [Windows 업데이트 에이전트 쿼리 문자열 구성](#BKMK_QUERY)합니다.

### <a name="requirements"></a>요구 사항

- 클러스터 장애 조치 및 원격 업데이트 Coordinator 컴퓨터 \(if used\) CAU 요구 사항을 충족 해야 및 원격 관리 필요한 구성에 나열 된 [요구 사항 및 모범 사례 CAU에 대 한](cluster-aware-updating-requirements.md)합니다.
- 리뷰 [Microsoft 업데이트 적용을 위한 권장](cluster-aware-updating-requirements.md#BKMK_BP_WUA), 다음 장애 클러스터 노드에서 대 한 Microsoft 업데이트 구성에 필요한 변경 하 고 있습니다.
- 최상의 결과 얻으려면 CAU를 사용 하 여 업데이트를 적용 하는 클러스터 및 업데이트 환경 제대로 구성 되어 있는지 확인 하려면 CAU 모범 사례 분석기 \(BPA\) 실행 하는 것이 좋습니다. 자세한 내용은 참조 [테스트 CAU 업데이트 준비](cluster-aware-updating-requirements.md#BKMK_BPA)합니다.

> [!NOTE]
> 사용자의 상호 작용 필요 또는 Microsoft 사용 약관에 동의 하는 업데이트를 제외 하 고 수동으로 설치 해야 합니다.

### <a name="additional-options"></a>추가 옵션

필요에 따라 추가 하거나 업데이트 plug\ 기능에서 적용 되는 설정 제한 다음 plug\에서 인수 지정할 수 있습니다.
- CAU UI에서 각 노드에서 중요 업데이트 외에도 권장된 업데이트를 적용 하려면 plug\-에서 구성 하 고 **추가 옵션** 페이지를 선택 하 고는 **중요 업데이트를 받을 때와 같은 방식으로 권장 업데이트 제공** 확인란을 선택 합니다.
<br>또는 구성는 **'IncludeRecommendedUpdates' \' 않게 '** plug\에서 인수 합니다.
- 각 클러스터 노드에서에 적용 되는 GDR 업데이트의 종류를 필터링 할 plug\-에서 구성 하려면 사용 하 여 Windows 업데이트 에이전트 쿼리 문자열을 지정는 **쿼리** plug\에서 인수 합니다. 자세한 내용은 참조 [Windows 업데이트 에이전트 쿼리 문자열 구성](#BKMK_QUERY)합니다.

### <a name="BKMK_QUERY"></a>Windows 업데이트 에이전트 쿼리 문자열을 구성 합니다.  
Plug\에서 기본 설정에 대 한 plug\에서 인수 구성할 수 있습니다 **Microsoft.WindowsUpdatePlugin**, Windows 업데이트 에이전트 \(WUA\) 쿼리 문자열을으로 구성 되어 있습니다. 이 명령을 WUA API를 사용 하 여 선택 특정 조건에 따라 각 노드에 적용 하려면 Microsoft 업데이트 그룹 하나 또는 여러 개의 식별 합니다. 여러 조건, 사용 하 여 논리 및 논리 OR 결합할 수 있습니다. 다음과 같이 plug\에서 인수에 WUA 쿼리 문자열 지정 됩니다.  
  
**QueryString\ = "Criterion1\ Value1 and\ = / 또는 Criterion2\ Value2 and\ = / 또는..."**  
  
예를 들어, **Microsoft.WindowsUpdatePlugin** 중요 업데이트에 기본 사용 하 여 자동으로 선택 **쿼리** 인수 사용 하 여 생성 되는 **IsInstalled**, **종류**, **IsHidden**, 및 **IsAssigned** 조건:  
  
**QueryString\ = "IsInstalled\ = 0, Type\ '소프트웨어' 및 IsHidden\ = 0과 IsAssigned\ = 1 대당"**  
  
지정 하는 경우는 **쿼리** 인수 기본 대신 사용 되는 **쿼리** plug\ 기능에 대 한 구성 된 합니다.  
  
#### <a name="example-1"></a>예제 1
  
구성 하는 **쿼리** ID로 식별 특정 업데이트를 설치 하는 인수 *f6ce46c1\-971c\-43f9\-a2aa\-783df125f003*:  
  
**QueryString\ = "UpdateID\'f6ce46c1\-971c\-43f9\-a2aa\-783df125f003' 및 IsInstalled\ = 0"**  
  
> [!NOTE]  
> 위 예제 Cluster\ 인식 업데이트 마법사를 사용 하 여 업데이트 적용에 대해 유효 합니다. CAU ui가 self\ 업데이트 옵션을 구성 하거나 사용 하 여 특정 업데이트를 설치 하려는 경우는 **Add\ CauClusterRole** 또는 **Set\ CauClusterRole**PowerShell cmdlet 두 single\ 인용 문자를 사용 하 여 되는지 값 포맷 해야 합니다.  
>   
> **QueryString\ = "UpdateID\ ' f6ce46c1\-971c\-43f9\-a2aa\-783df125f003 ' 및 IsInstalled\ = 0"**  
  
#### <a name="example-2"></a>예제 2
  
구성 하는 **쿼리** 인수만 드라이버를 설치 하는 다음과 같습니다.  
  
**QueryString\ = "IsInstalled\ = 0, Type\ '드라이버' 및 IsHidden\ = 0"**  
  
Plug\에서 기본 설정에 대 한 문자열 쿼리에 대 한 자세한 내용은 **Microsoft.WindowsUpdatePlugin**, 검색 조건을 \ (와 같은 **IsInstalled**\), 쿼리 문자열로 포함 될 수 있는 구문을 검색 조건에 대 한 섹션을 참조 하 고 있는 [Windows 업데이트 에이전트 (WUA) API 참조](http://go.microsoft.com/fwlink/p/?LinkId=223304)합니다.  
  
## <a name="BKMK_HFP"></a>사용 하 여 Microsoft.HotfixPlugin  
plug\ **Microsoft.HotfixPlugin** 제한 Microsoft 배포 릴리스 \(LDR\) 업데이트를 적용 하는 데 사용 될 \ (핫픽스 라고도 및 QFEs\ 이전의)를 다운로드 하는 하지 개별적으로 특정 Microsoft 소프트웨어 문제를 해결 하기 위해 합니다. 플러그 인 SMB 파일 공유에서 루트 폴더에서 업데이트를 설치 하 고 Microsoft non\ 드라이버, 펌웨어 및 BIOS 업데이트 적용을 사용자 지정할 수 있습니다.

> [!NOTE]
> 때때로 핫픽스 Microsoft 기술 자료 문서에서 다운로드할 수 있지만 as\ 필요할 고객에 게 제공 됩니다.

### <a name="requirements"></a>요구 사항

- 클러스터 장애 조치 및 원격 업데이트 Coordinator 컴퓨터 \(if used\) CAU 요구 사항을 충족 해야 및 원격 관리 필요한 구성에 나열 된 [요구 사항 및 모범 사례 CAU에 대 한](cluster-aware-updating-requirements.md)합니다.
- 리뷰 [사용 되는 Microsoft.HotfixPlugin 추천](cluster-aware-updating-requirements.md#BKMK_BP_HF)합니다.
- 최상의 결과 얻으려면 CAU 모범 사례 분석기 \(BPA\) 모델을 CAU를 사용 하 여 업데이트를 적용 하는 클러스터 및 업데이트 환경 제대로 구성 되어 있는지 확인를 실행 하는 것이 좋습니다. 자세한 내용은 참조 [테스트 CAU 업데이트 준비](cluster-aware-updating-requirements.md#BKMK_BPA)합니다.
- 게시자가 업데이트를 가져올 하 고 복사 하거나 서버 메시지 블록 \(SMB\) 파일 공유 추출 \ (핫픽스 루트 folder\)를 지 원하는 이상 SMB 2.0가 클러스터 노드 및 원격 업데이트 Coordinator 컴퓨터의 모든 하 여 액세스할 수 있는 \ (경우 CAU mode\ remote\ 업데이트에서 사용). 자세한 내용은 참조 [핫픽스 루트 폴더 구조 구성](#BKMK_HF_ROOT) 이 항목 뒷부분. 

    > [!NOTE]
    > 기본적으로이 plug\ 인만 설치 핫픽스 다음 파일 이름 확장명을 가진:.msu,.msi, 및.msp 합니다.

- DefaultHotfixConfig.xml 파일을 복사 \ (에서 제공 되는 **%systemroot%\\System32\\WindowsPowerShell\\v1.0\\Modules\\ClusterAwareUpdating** CAU 도구 installed\ 사용 되는 컴퓨터에서 폴더)는 하 고 사용자가 만든 핫픽스 루트 폴더로 압축을 푼 핫픽스 합니다. 예를 들어 구성 파일을 복사 *\\\MyFileServer\\Hotfixes\\Root\\*합니다. 

    > [!NOTE]
    > Microsoft와 다른 업데이트에서 제공 하는 대부분 핫픽스 설치를 기본 핫픽스 구성 파일을 수정 하지 않고 사용할 수 있습니다. 시나리오에 필요한 경우 고급 작업으로 구성 파일을 사용자 지정할 수 있습니다. 특정 확장명을 가진 파일 핫픽스 처리 하기 위한 작업이 또는 특정 종료 조건에 대 한 동작을 정의 하 구성 파일 예를 들어, 사용자 지정 규칙 포함 될 수 있습니다. 자세한 내용은 참조 [핫픽스 구성 파일을 사용자 지정](#BKMK_CONFIG_FILE) 이 항목 뒷부분.

### <a name="configuration"></a>구성

다음 설정을 구성 됩니다. 자세한 내용은이 항목 뒷부분에서 섹션으로 링크를 클릭 하십시오.
- 경로 포함 하 고 업데이트를 적용 하는 공유 핫픽스 루트 폴더를 핫픽스 구성 파일을 포함 합니다. 이 경로 CAU UI에 입력 하거나 구성할 수는 **HotfixRootFolderPath\ = \ < 경로 >** PowerShell plug\에서 인수 합니다. 

   > [!NOTE]
   > 로컬 폴더 경로로 또는 양식 UNC 경로로 핫픽스 루트 폴더를 지정할 수 *\\\ServerName\\Share\\RootFolderName*합니다. 독립 실행형 또는 domain\ 기반 DFS Namespace 경로 사용할 수 있습니다. 그러나 하나를 구성 사용 하지 않아야 확인 하므로 핫픽스 구성 파일에 대 한 액세스 권한을 DFS Namespace 경로와 호환 되지 않는 확인 plug\에 기능 액세스 권한을 구성 하거나 CAU UI를 사용 하 여는 **DisableAclChecks\' 않게 '** plug\에서 인수 합니다.
- 설정에서 폴더에 액세스 하는 SMB에서 액세스 하는 데이터의 무결성 적절 한 권한이 있는지 확인 하려면 핫픽스 루트 폴더 호스트 하는 서버 공유 폴더 \ (SMB 로그인 또는 SMB Encryption\). 자세한 내용은 참조 [핫픽스 루트 폴더에 대 한 액세스를 제한](#BKMK_ACL)합니다.

### <a name="additional-options"></a>추가 옵션

- 필요에 따라 SMB 암호화가 핫픽스 파일 공유에서 데이터에 액세스할 때 적용 되도록에서 plug\ 구성 합니다. CAU UI에서에 **추가 옵션** 페이지를 선택 하 고 있는 **SMB 암호화 핫픽스 루트 폴더에 액세스 하** 옵션 하거나 구성는 **RequireSMBEncryption\' 않게 '** PowerShell plug\에서 인수 합니다. 
  > [!IMPORTANT]
  > SMB 데이터 무결성 SMB 로그인 또는 SMB 암호화를 사용 하도록 설정 하려면 SMB server에서 추가 구성 단계를 수행 해야 합니다. 자세한 내용은 참조 4 단계에서 [핫픽스 루트 폴더에 대 한 액세스를 제한](#BKMK_ACL)합니다. 옵션 선택 SMB 암호화를 사용 하 고 핫픽스 루트 폴더를 적용 하는 대해 구성 되지 액세스 SMB 암호화를 사용 하 여, 업데이트 실행 하지 못합니다.
- 필요에 따라 비활성화 핫픽스 루트 폴더 및 핫픽스 구성 파일에 대 한 충분 한 사용 권한에 대 한 기본 검사 합니다. CAU UI에서 **핫픽스 루트 폴더 및 구성 파일에 대 한 관리자에 대 한 확인란을 사용 하지 않도록 설정**를 구성 하거나는 **DisableAclChecks\' 않게 '** plug\에서 인수 합니다.
- 필요에 따라 구성는 **HotfixInstallerTimeoutMinutes\ =<Integer>** 인수 돌아가려면 핫픽스 설치 프로세스에 대 한 plug\에 핫픽스 대기 기간 지정할 수 있습니다. \ (은 30 분 정도 \) 등 2 시간 제한 기간을 지정 하려면 설정 **HotfixInstallerTimeoutMinutes\ 120 =**합니다.
- 필요에 따라 구성는 **HotfixConfigFileName \ = <name>**plug\에서 인수 핫픽스 루트 폴더에 있는 핫픽스 구성 파일 이름을 지정할 수 있습니다. 지정 하지 기본 이름 DefaultHotfixConfig.xml 사용 됩니다.
  
### <a name="BKMK_HF_ROOT"></a>구성 핫픽스 루트 폴더 구조

Plug\에 핫픽스에 대 한 작업을 하 핫픽스에에서 저장 해야 SMB 파일 공유에서 well\ 정의 구조 \ (핫픽스 루트 folder\) CAU UI 또는 CAU PowerShell cmdlet 사용 하 여 plug\에 핫픽스 핫픽스 루트 폴더는 경로로 구성 해야 합니다. 이 경로 plug\ 기능에으로 전달 되 고 **HotfixRootFolderPath** 인수 합니다. 다음과 같이 업데이트 필요에 따라 핫픽스 루트 폴더에 대 한 몇 가지 구조 중 하나를 선택할 수 있습니다. 파일 또는 폴더를 구조 준수 하지 않는 무시 됩니다.  
  
#### <a name="example-1---folder-structure-used-to-apply-hotfixes-to-all-cluster-nodes"></a>예제 1-폴더 구조 핫픽스 모든 클러스터 노드에서 적용 하는 데 사용
  
라는 폴더에 복사 핫픽스 모든 클러스터 노드에서에 적용 되도록를 지정 하려면 **CAUHotfix\_All** 핫픽스 루트 폴더 합니다. 여기서에서는 **HotfixRootFolderPath** plug\에서 인수로 설정 되어 *\\\MyFileServer\\Hotfixes\\Root\\*합니다. **CAUHotfix\_All** 폴더 확장.msu,.msi, 및.msp 일부 클러스터 노드에서에 적용 되는 세 개의 업데이트가 포함 되어 있습니다. 업데이트 파일 이름은 돕기 위해만 됩니다.  
  
> [!NOTE]  
> 이 및 다음 예제 DefaultHotfixConfig.xml 기본 이름으로 핫픽스 구성 파일의 필요한 위치에 핫픽스 루트 폴더에 표시 됩니다.  
  
```
\\MyFileServer\Hotfixes\Root\   
   DefaultHotfixConfig.xml  
   CAUHotfix_All\   
      Update1.msu   
      Update2.msi   
      Update3.msp  
      ...  
```  
  
#### <a name="example-2---folder-structure-used-to-apply-certain-updates-only-to-a-specific-node"></a>예제 2-폴더 구조 특정 노드만에 특정 업데이트를 적용 하는 데 사용
  
특정 노드에만 적용 핫픽스를 지정 하려면 노드의 이름으로 핫픽스 루트 폴더 하위 폴더를 사용 합니다. 예를 들어, 클러스터 노드에서 NetBIOS 이름을 사용 하 여 *ContosoNode1*합니다. 그런 다음이 노드가 하위이 폴더를에 적용 되는 업데이트를 이동 합니다. 다음 예제에서는 **HotfixRootFolderPath** plug\에서 인수로 설정 되어 *\\\MyFileServer\\Hotfixes\\Root\\*합니다. 업데이트에 **CAUHotfix\_All** 폴더 모든 클러스터 노드가에 적용 됩니다 및 *Node1\_Specific\_Update.msu* 에 적용 됩니다 *ContosoNode1*합니다.  
  
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
  
#### <a name="example-3---folder-structure-used-to-apply-updates-other-than-msu-msi-and-msp-files"></a>예제 3-폴더 구조.msu,.msi,.msp 파일 이외의 업데이트를 적용 하는 데 사용
  
기본적으로 **Microsoft.HotfixPlugin** .msu,.msi, 또는.msp 확장을 사용 하 여 업데이트에만 적용 됩니다. 그러나 특정 업데이트 확장명이 다른 나 다른 설치 명령이 필요 합니다. 예를 들어, 노드에서 클러스터에서에 확장.exe로 펌웨어 업데이트 적용 해야 할 수 있습니다. 특정 나타내는 하위 폴더와 핫픽스 루트 폴더를 구성할 수, non\ 기본 업데이트 종류를 설치 해야 합니다. 설치 명령 지정 하는 해당 폴더 설치 규칙 구성 해야는 `<FolderRules>`핫픽스 구성 XML 파일의 요소입니다.  
  
다음 예제에서는 **HotfixRootFolderPath** plug\에서 인수로 설정 되어 *\\\MyFileServer\\Hotfixes\\Root\\*합니다. 몇 가지 사항을 업데이트 모든 클러스터 노드가 및 펌웨어 업데이트 적용 됩니다 *SpecialHotfix1.exe* 에 적용할 수 *ContosoNode1* 사용 하 여 *FolderRule1*합니다. 구성에 대 한 내용은 *FolderRule1* 핫픽스 구성 파일을 볼 [핫픽스 구성 파일을 사용자 지정](#BKMK_CONFIG_FILE) 이 항목 뒷부분에 있습니다.  
  
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

### <a name="BKMK_CONFIG_FILE"></a>핫픽스 구성 파일을 사용자 지정  
핫픽스 구성 컨트롤 어떻게 파일 **Microsoft.HotfixPlugin** 핫픽스 특정 파일 형식을 클러스터 장애 조치를 설치 합니다. 구성 파일에 대 한 데도 HotfixConfigSchema.xsd, CAU 도구가 설치 되어 있는 컴퓨터에서 다음과 같은 폴더에 있는에 정의 됩니다.  
  
**%systemroot%\\System32\\WindowsPowerShell\\v1.0\\Modules\\ClusterAwareUpdating 폴더**  
  
핫픽스 구성 파일을 사용자 지정 하려면 핫픽스 루트 폴더로 구성 파일 DefaultHotfixConfig.xml 샘플이이 위치에서 복사 하 고 시나리오에 대 한 적절 한 수정 사항을 확인 합니다.  
  
> [!IMPORTANT]  
> Microsoft와 다른 업데이트에서 제공 하는 대부분 핫픽스를 적용 하려면 기본 핫픽스 구성 파일을 수정 하지 않고 사용할 수 있습니다. 사용자 지정 핫픽스 구성 파일은 고급 사용 경우에만 작업입니다.  
  
기본적으로 핫픽스 구성 XML 파일 정의 설치 규칙과 핫픽스 다음과 같은 두 가지 범주에 대 한 종료 조건을:  
  
-   plug\ 기본적으로 설치할 수 있는 확장명을 가진 파일 핫픽스 \ (.msu,.msi, 및.msp 폴더).  
  
    이러한으로 정의 됩니다 `<ExtensionRules>`요소는 `<DefaultRules>`요소입니다. 하나는 `<Extension>`각 기본 지원 되는 파일 형식에 대 한 요소 합니다. 일반 XML 구조는 다음과 같습니다.  
  
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
  
    사용자 환경에서 일부 클러스터 노드에서에 특정 업데이트 유형에 적용 하려는 경우 추가 정의 수 `<Extension>`요소입니다.  
  
-   핫픽스 또는.msi,.msu, 또는.msp 파일 하지 않은 다른 업데이트 파일을 예를 들어, BIOS non\ Microsoft 드라이버 및 펌웨어를 업데이트 합니다.  
  
    각 기본 non\ 파일 형식으로 구성 된는 `<Folder>`요소에는 `<FolderRules>`요소입니다. 이름 특성은 `<Folder>`요소는 해당 종류의 업데이트를 포함 하는 핫픽스 루트 폴더에 폴더의 이름으로 동일 해야 합니다. 폴더에 있을 수 있습니다의 **CAUHotfix\_All** 폴더 또는 특정 node\ 폴더에 있습니다. 예를 들어, 경우 *FolderRule1* 는 XML 파일 설치 템플릿을 정의 하 종료 해당 폴더에 업데이트에 대 한 조건에에서 다음과 같은 요소를 구성 핫픽스 루트 폴더를 구성 합니다.  
  
    ```xml  
    <FolderRules>  
          <Folder name="FolderRule1">  
            <!-- Template and ExitConditions elements for installation of updates in FolderRule1 follow -->  
             ...  
          </Folder>  
          ...  
    </FolderRules>  
    ```  
  
다음 표에서 `<Template>`특성과 가능한 `<ExitConditions>`하위 합니다.  
  
|`<Template>` 특성|설명|  
|--------------------------|---------------|  
|`path`|설치 프로그램에 정의 된 파일 형식에 대 한 전체 경로 `<Extension name>`특성 합니다.<br /><br />업데이트 파일을 경로 핫픽스 루트 폴더 구조에서를 지정 하려면 `$update$`합니다.|  
|`parameters`|필요한 및 선택 사항 매개 변수에 지정 된 프로그램에 대 한 문자열 `path`합니다.<br /><br />사용 하 여 경로를 핫픽스 루트 폴더 구조에서 업데이트 파일이 있는 매개 변수를 지정 하려면 `$update$`합니다.|  
  
|`<ExitConditions>` 하위|설명|  
|---------------------------------|---------------|  
|`<Success>`|지정 된 업데이트의 성공 여부를 나타내는 하나 또는 여러 개의 종료 코드 정의 합니다. 이 필요한 하위입니다.|  
|`<Success_RebootRequired>`|필요에 따라 정의 지정된 업데이트에 성공 하 고 노드를 다시 시작 해야 나타내는 하나 또는 여러 개의 종료 코드 합니다. <br>**참고:** 필요에 따라는 `<Folder>`요소 포함 될 수는 `alwaysReboot`특성 합니다. 이 특성을 설정 하는 경우 니다 종료 코드에 정의 된 중 하나를 반환 핫픽스가이 규칙에 의해 설치 된 경우 `<Success>`,으로 해석 하는 `<Success_RebootRequired>`상태를 종료 합니다.|  
|`<Fail_RebootRequired>`|필요에 따라 정의 지정된 된 업데이트 실패 하 고 노드 다시 시작 해야 나타내는 하나 또는 여러 개의 종료 코드 합니다.|  
|`<AlreadyInstalled>`|이미 설치 되어 있으므로 지정된 업데이트 적용 되지 않은 나타내는 하나 또는 여러 개의 종료 코드 필요에 따라 정의 합니다.|  
|`<NotApplicable>`|필요에 따라 정의 클러스터 노드에서에 적용 되지 않습니다 때문에 지정된 된 업데이트 적용 되지 않은 나타내는 하나 또는 여러 개의 종료 코드 합니다.|  
  
> [!IMPORTANT]  
> 명시적으로 정의 하지 않은 코드가 종료 된 `<ExitConditions>`업데이트가 실패 하 고 노드 다시 시작 되지 않으면 해석 됩니다.  
  
### <a name="BKMK_ACL"></a>핫픽스 루트 폴더에 대 한 액세스를 제한  
핫픽스 루트 폴더 파일과 핫픽스 구성 파일의 경우에만 액세스할에 대 한 보안을 유지 하려면 SMB 파일 서버 및 파일 공유 구성 하려면 몇 가지 단계를 수행 해야 **Microsoft.HotfixPlugin**합니다. 이러한 단계 클러스터 장애 조치를 손상 시킬 수 있는 방법으로 핫픽스 파일 사용 가능한 무단 변경을 방지 하는 데 도움이 되는 몇 가지 기능이 사용 하도록 설정 합니다.  
  
일반적인 단계는 다음과 같습니다.  
  
1.  사용자 계정 plug\ 기능을 사용 하 여 실행 업데이트에 대 한 사용 되는 사용자의 신원을 확인합니다  
  
2.  SMB 파일 서버에 필요한 그룹에서이 사용자의 계정 구성을  
  
3.  핫픽스 루트 폴더에 액세스 권한을 구성합니다  
  
4.  SMB 데이터 무결성 설정을 구성합니다  
  
5.  Windows 방화벽 규칙 SMB server에서 활성화  
  
#### <a name="step-1-identify-the-user-account-that-is-used-for-updating-runs-by-using-the-hotfix-plug-in"></a>1 단계입니다. 사용자 계정에서 plug\ 핫픽스를 사용 하 여 실행 업데이트에 대 한 사용 되는 사용자의 신원을 확인합니다
  
CAU에는 실행 업데이트를 사용 하 여 수행 하는 동안 보안 설정을 확인 하는 데 사용 되는 계정을 **Microsoft.HotfixPlugin** CAU 사용 되는지 여부 remote\ 업데이트 모드나 self\ 업데이트 모드에서는 다음과 같은에 따라 달라 집니다.  
  
-   **모드 Remote\ 업데이트** 미리 보기 및 업데이트를 적용 하 클러스터에서 관리자 권한이 있는 계정 합니다.  
  
-   **모드 Self\ 업데이트** 클러스터 역할은 CAU에 대 한 Active directory에서 구성 된 가상 컴퓨터 개체의 이름입니다. 미리 준비 가상 컴퓨터 CAU 클러스터 역할에 대 한 Active directory에서 개체의 이름이 나 클러스터 역할 CAU에서 생성 되는 이름입니다. 이름을 CAU에서 생성 되는 경우를 얻으려면 실행는 **Get\ CauClusterRole** CAU PowerShell cmdlet 합니다. 출력에서 **ResourceGroupName** 생성 된 가상 컴퓨터 개체 계정 이름입니다.  
  
#### <a name="step-2-configure-this-user-account-in-the-necessary-groups-on-an-smb-file-server"></a>2 단계입니다. SMB 파일 서버에 필요한 그룹에서이 사용자의 계정 구성을
  
> [!IMPORTANT]  
> 실행 업데이트에 대 한 SMB server에서 로컬 관리자 계정으로 사용 되는 계정을 추가 해야 합니다. 이 조직의 보안 정책을 때문 허용 되지 않습니다 경우 다음 절차를 사용 하 여이 계정을 필요한 SMB server에 대 한 권한을으로 구성 됩니다.  
  
##### <a name="to-configure-a-user-account-on-the-smb-server"></a>SMB 서버에서 사용자 계정을 구성 하려면  
  
1.  분산 COM 사용자 그룹 하 고 그룹에서 다음 중 하나를 실행 업데이트에 대 한 사용 되는 계정을 추가: 전원 사용자나 서버 작업 인쇄 통신사 합니다.  
  
2.  계정에 대 한 권한이 WMI을 사용 하려면 WMI Management Console SMB server에 시작 됩니다. PowerShell을 시작한 다음 명령을 입력 합니다.  
  
    ```  
    wmimgmt.msc  
    ```  
  
3.  콘솔 트리에서 right\ 클릭 **WMI 컨트롤 \(Local\)**을 차례로 클릭 하 고 **속성**합니다.  
  
4.  클릭 **보안**를 확장 한 다음 **루트**합니다.  
  
5.  클릭 **CIMV2**을 차례로 클릭 하 고 **보안**합니다.  
  
6.  실행 업데이트에 대 한 사용 되는 계정을 추가 **그룹 또는 사용자 이름** 목록입니다.  
  
7.  부여는 **메서드 실행** 및 **원격 설정** 실행 업데이트에 대 한 사용 되는 계정에 대 한 권한을 합니다.  
  
#### <a name="step-3-configure-permissions-to-access-the-hotfix-root-folder"></a>3 단계입니다. 핫픽스 루트 폴더에 액세스 권한을 구성합니다
  
기본적으로 업데이트를 적용 하려고 할 때 plug\에 핫픽스 핫픽스 루트 폴더에 대 한 액세스 NTFS 파일 시스템 권한 구성을 확인 합니다. 폴더 액세스 권한을 제대로 구성 되어 있지 않으면는 업데이트 사용 하 여 실행 plug\에 핫픽스 실패할 수 있습니다.  
  
Plug\에 핫픽스의 기본 설정 사용 하는 경우 폴더 액세스 권한을 다음 요구 사항을 충족 하는지 확인 합니다.  
  
-   사용자 그룹 읽기을 있습니다.  
  
-   plug\.exe 확장을 사용 하 여 업데이트를 적용 됩니다의 사용자 그룹에 실행 권한을 것입니다.  
  
-   특정 보안 사용자가 허용 되는지 \ (하지만 required\ 없는) 쓰기 또는 사용 권한 수정 합니다. 허용된 사용자는 로컬 관리자가 그룹, 시스템, 만든 소유자 TrustedInstaller 있습니다. 다른 계정 또는 그룹 쓰기 또는 수정 핫픽스 루트 폴더에 권한이에 허용 되지 않습니다.  
  
필요에 따라 plug\ 기능에 기본적으로 수행 하는 이전 검사 비활성화할 수 있습니다. 이 두 가지 방법 중 하나를 수행할 수 있습니다.  
  
-   구성 CAU PowerShell cmdlet, 사용 하는 경우는 **DisableAclChecks\' 않게 '** 에서 인수는 **CauPluginArguments** 매개 plug\에 핫픽스 합니다.  
  
-   CAU UI를 사용 하는 경우는 **핫픽스 루트 폴더 및 구성 파일에 대 한 관리자에 대 한 확인란을 사용 하지 않도록 설정** 옵션에 **업데이트 옵션을 추가** 실행 업데이트 옵션을 구성 하는 데 사용 되는 마법사의 페이지 합니다.  
  
하지만 많은 환경에서 최상의 기본 설정 사용 하 여 이러한 검사를 실행 하는 것이 좋습니다.  
  
#### <a name="step-4-configure-settings-for-smb-data-integrity"></a>4 단계입니다. SMB 데이터 무결성 설정을 구성합니다
  
클러스터 노드에서 사이의 SMB 파일 공유 연결에 대 한 데이터 무결성을 확인 하려면 plug\에 핫픽스 SMB 로그인 또는 SMB 암호화 SMB 파일 공유에서 설정을 사용 하도록 설정 해야 합니다. Windows Server 2012에서 시작 강화 된 보안 및 다양 한 환경에서 성능 향상을 제공 하는 SMB 암호화를 지원 됩니다. 이러한 설정 중 하나 또는 모두 다음과 같은 설정할 수 있습니다.  
  
-   절차 참조 SMB 로그인 하는 것을 사용 하도록 설정 하 고 [887429 문서](http://support.microsoft.com/kb/887429) Microsoft 기술 자료 합니다.  
  
-   SMB 암호화 SMB 공유 폴더를 사용 하려면 다음 PowerShell cmdlet SMB server에서 실행 합니다.  
  
    ```PowerShell  
    Set-SmbShare <ShareName> -EncryptData $true  
    ```  
  
    여기서 <*공유*> SMB 공유 폴더의 이름입니다.  
  
필요에 따라 SMB 암호화 SMB server에 대 한 연결에 사용을 적용 하려면 선택는 **SMB 암호화 핫픽스 루트 폴더에 액세스 하** CAU UI에서 옵션을 구성 하거나는 **RequireSMBEncryption\' 않게 '** plug\에서 인수 CAU PowerShell cmdlet 사용 하 여 합니다.  
  
> [!IMPORTANT]  
> 옵션 선택 SMB 암호화를 사용 하 고 핫픽스 루트 폴더를 적용 하는 대해 구성 되지 SMB 암호화를 사용 하는 연결, 업데이트 실행 하지 못합니다.  
  
#### <a name="step-5-enable-a-windows-firewall-rule-on-the-smb-server"></a>5 단계입니다. Windows 방화벽 규칙 SMB server에서 활성화
  
사용 하도록 설정 해야는 **원격 파일 서버 관리 \(SMB\-in\)** SMB 파일 서버에서 Windows 방화벽에서 규칙 합니다. 이 Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012에서 기본적으로 설정 됩니다.  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [클러스터 업데이트 개요](cluster-aware-updating.md)
  
-   [업데이트 Windows PowerShell Cmdlet 클러스터 인식](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating)  
  
-   [클러스터 인식 플러그 인 참조 업데이트](http://msdn.microsoft.com/library/hh418084.aspx)  
  
