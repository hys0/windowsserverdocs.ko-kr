---
title: 모범 사례 분석기 검사 실행 및 검사 Results_1 관리
description: 서버 관리자
ms.prod: windows-server
ms.technology: manage-server-manager
ms.topic: article
ms.assetid: 232f1c80-88ef-4a39-8014-14be788c2766
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ff854bcb25e4f5891e56f1e094fd4f387cf023f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851486"
---
# <a name="run-best-practices-analyzer-scans-and-manage-scan-results"></a>모범 사례 분석기 검사 실행 및 검사 결과 관리

>적용 대상: Windows Server 2016

Windows 관리에서 *모범 사례*는 일반적인 환경에서 전문가가 정의한 대로 서버를 구성할 수 있는 이상적인 방법으로 간주됩니다. 예를 들어 다른 네트워크 컴퓨터와 통신하는 데 필요한 포트만 열어 두고 사용하지 않는 포트는 차단하는 것이 대부분의 서버 애플리케이션에서 모범 사례로 간주됩니다. 모범 사례 위반은 중대한 경우라도 반드시 문제가 되지는 않으며 성능이나 안정성 저하, 예기치 않은 충돌, 보안 위험 증가 또는 다른 잠재적 문제가 발생할 수 있는 서버 구성을 나타냅니다.

분석기 BPA (모범 사례)는 Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2008 r 2에서 사용할 수 있는 서버 관리 도구. BPA는 Windows Server 2012를 실행 하는 관리 되는 서버 또는 Windows Server 2008 r 2에 설치 된 역할 검사 및 관리자에 게 모범 사례 위반을 보고 하 여 모범 사례 위반을 줄일 수 있습니다.

또는 실행할 수 있습니다 분석기 BPA (모범 사례) 검색 하거나 서버 관리자에서 BPA GUI를 사용 하 여 Windows PowerShell에서 cmdlet을 사용 하 여 합니다. Windows Server 2012부터 서버 관리자 콘솔의 모범 사례 분석기 타일을 사용 하는지 아니면 Windows PowerShell cmdlet을 사용 하 여 검색을 실행 하는지 여부에 관계 없이 여러 서버에서 한 번에 하나의 역할 또는 여러 역할을 검사할 수 있습니다. 확인하지 않을 검사 결과는 제외하거나 무시하도록 BPA에 지정할 수도 있습니다.

이 항목에는 다음과 같은 섹션이 포함되어 있습니다.

-   [BPA 찾기](#BKMK_find)

-   [BPA 작동 방법](#BKMK_how)

-   [역할에 대 한 모범 사례 분석기 검색 수행](#BKMK_BPAscan)

-   [검사 결과 관리](#BKMK_manage)

## <a name="find-bpa"></a><a name=BKMK_find></a>BPA 찾기
서버 그룹 페이지에서 Windows Server 2012 R2 및 Windows Server 2012 서버 관리자의 모범 사례 분석기 cmdlet을 실행 하려면 관리자 권한으로 Windows PowerShell 세션을 열 수 및 역할에 모범 사례 분석기 타일을 찾을 수 있습니다.

## <a name="how-bpa-works"></a><a name=BKMK_how></a>BPA 작동 방법
BPA는 효율성, 신뢰성 및 안정성의 모범 사례 규칙 8 가지 다른 범주에 있는 역할의 호환성을 측정 하 여 작동 합니다. 측정 결과는 다음 표에 설명된 세 개의 심각도 수준 중 하나일 수 있습니다.

|심각도|설명|
|---------|--------|
|오류|오류 결과는 역할이 모범 사례 규칙 조건을 충족하지 않을 때 반환되며 기능상의 문제가 예상될 수 있습니다.|
|정보|역할이 모범 사례 규칙 조건을 충족할 경우 정보 결과가 반환됩니다.|
|경고|경고 결과는 변경 작업을 수행하지 않을 경우 규칙 위반으로 인해 문제가 발생될 수 있을 때 반환됩니다. 애플리케이션이 현재 작동하면서 정책을 준수하고 있지만 해당 구성이나 정책 설정을 변경하지 않으면 규칙 조건을 충족하지 않을 수도 있습니다. 예를 들어 라이선스 서버를 역할에 사용할 수 없는 경우 원격 데스크톱 서비스 검사에서 경고 결과를 표시할 수 있는데, 이는 검사 시에 활성 상태인 원격 연결이 없더라도 라이선스가 서버가 없으면 유효한 클라이언트 라이선스를 새 원격 연결에서 획득할 수 없기 때문입니다.|

### <a name="rule-categories"></a>규칙 범주
다음 표에서 모범 사례 규칙 범주 역할이 측정 되는 동안 모범 사례 분석기에 대 한 검색 합니다.

|범주 이름|설명|
|---------|--------|
|보안|보안 규칙은 역할의 기밀 또는 소유 데이터의 무단 또는 악의적인 사용자, 또는 손실이 나 도난 등의 위협에 노출 될 상대적인 위험 측정에 적용 됩니다.|
|성능|성능 규칙은 요청을 처리 하는 역할의 작업이 제공 된 예상된 기간 내에서 엔터프라이즈의 지정 된 임무를 수행 하는 역할의 능력을 측정에 적용 됩니다.|
|구성|역할이 최적으로 수행되도록 수정이 필요할 수 있는 역할 설정을 식별하기 위한 구성 규칙이 적용됩니다. 구성 규칙을 통해 오류 메시지가 발생하는 설정 충돌을 방지하거나 엔터프라이즈에서 규정된 임무를 역할이 수행하지 못하게 할 수 있습니다.|
|정책|역할이 최적으로 안전 하 게 작동 하도록 수정이 필요할 수 있는 그룹 정책 또는 Windows 레지스트리 설정을 식별 하기 위한 정책 규칙이 적용 됩니다.|
|연산|엔터프라이즈에서 규정된 작업을 역할이 수행하지 못할 가능성을 식별하기 위한 작업 규칙이 적용됩니다.|
|사전 배포|사전 배포 규칙은 설치된 역할이 엔터프라이즈에 배포되기 전에 적용됩니다. 이 규칙을 통해 관리자는 역할이 프로덕션 환경에서 사용되기 전에 모범 사례가 충족되었는지 평가할 수 있습니다.|
|사후 배포|사후 배포 규칙은 역할에 필요한 모든 서비스가 시작된 후와 역할이 엔터프라이즈에서 실행된 후에 적용됩니다.|
|필수 조건|필수 구성 요소 규칙은 BPA가 다른 범주의 특정 규칙을 적용할 수 있도록 사전에 역할이 갖춰야 할 구성 설정, 정책 설정 및 기능에 대해 설명합니다. 검사 결과의 필수 구성 요소는 잘못된 설정, 누락된 프로그램, 잘못된 활성화 정책이나 비활성화 정책, 레지스트리 키 설정 또는 기타 구성으로 인해 BPA가 검사 중에 하나 이상의 규칙을 적용하지 못했다는 것을 나타냅니다. 필수 구성 요소의 결과가 정책 준수 또는 정책 위반을 의미하지는 않습니다. 규칙을 적용할 수 없다는 뜻이므로, 검사 결과에 속하지 않습니다.|

## <a name="performing-best-practices-analyzer-scans-on-roles"></a><a name=BKMK_BPAscan></a>역할에 대 한 모범 사례 분석기 검색 수행
수행할 수 있습니다 BPA 검사 역할 중 하나를 사용 하 여 BPA GUI를 사용 하는 서버 관리자에서 또는 Windows PowerShell cmdlet을 사용 하 여.

Windows Server 2012 R2 및 Windows Server 2012에서 일부 역할 묻는 메시지를 특정 서버 또는 BPA 검사를 시작 하기 전에 역할의 일부 또는 서브 모델의 Id를 실행 하는 공유의 이름과 같은 추가 매개 변수를 지정할 수 있습니다. 추가 매개 변수를 지정해야 하는 모델에 대한 BPA 검사 시 BPA cmdlet을 사용합니다. BPA GUI에서는 서브모델 ID와 같은 추가 매개 변수를 사용할 수 없습니다. 예를 들어 하위 모델 ID **FSRM** 은 파일 및 저장소 서비스의 역할 서비스인 파일 서버 리소스 관리자의 파일 서비스 BPA 하위 모델을 나타냅니다. 파일 서버 리소스 관리자 역할 서비스에 Windows PowerShell cmdlet을 사용 하 여 BPA 검사를 실행 하 고 매개 변수를 추가 검색을 실행 하려면 `SubmodelId` cmdlet입니다.

BPA GUI에서 시작 하는 스캔에 추가 매개 변수를 전달할 수 있지만 BPA 타일에서 서버 관리자는 검사를 시작한 방법과 상관 없이 최신 BPA 검사에 대 한 결과 표시 합니다.

-   [BPA GUI를 사용 하 여 역할 검사](#BKMK_GUIscan)

-   [Windows PowerShell cmdlet을 사용 하 여 역할 검사](#BKMK_PSscan)

### <a name="scanning-roles-by-using-the-bpa-gui"></a><a name=BKMK_GUIscan></a>BPA GUI를 사용 하 여 역할 검사
BPA GUI에서 하나 이상의 역할을 검사하려면 다음 단계를 따릅니다.

##### <a name="to-scan-roles-by-using-the-bpa-gui"></a>BPA GUI를 사용하여 역할을 검사하려면

1.  아직 열려 있지 않은 경우 서버 관리자를 열려면 다음 중 하나를 수행 합니다.

    -   Windows 작업 표시줄에서 서버 관리자 단추를 클릭 합니다.

    -   **시작** 화면에서 서버 관리자 타일을 클릭 합니다.

2.  탐색 창에서 역할이나 그룹 페이지를 엽니다.

    역할이나 그룹 페이지에서 BPA 검사를 실행하면 해당 그룹의 서버에 설치되어 있는 모든 역할이 검사됩니다.

3.  **모범 사례 분석기** 타일의 **작업** 메뉴에서 **BPA 검사 시작**을 클릭 합니다.

4.  선택한 역할이나 그룹에 대해 평가된 규칙의 개수에 따라 BPA 검사를 완료하는 데 몇 분이 소요될 수 있습니다.

### <a name="scanning-roles-by-using-windows-powershell-cmdlets"></a><a name=BKMK_PSscan></a>Windows PowerShell cmdlet을 사용 하 여 역할 검사
Windows PowerShell cmdlet을 사용 하 여 하나 이상의 역할을 검사 하려면 다음 절차를 따르십시오.

> [!NOTE]
> 이 섹션의 절차에는 모든 BPA cmdlet 및 매개 변수가 나와 있지 않습니다. Windows powershell의 BPA 작업에 대 한 자세한 내용을 보려면 Windows PowerShell 세션에서 **Get-help***BPACmdlet***-full**을 입력 합니다. 여기서 *BPACmdlet* 은 다음 값 중 하나일 수 있습니다. [Windows Server TechCenter](https://go.microsoft.com/fwlink/p/?LinkId=240177)에서 BPA cmdlet 도움말 항목을 찾을 수도 있습니다.

-   **Invoke-bpamodel**

-   **Invoke-bpamodel**

-   **Get-BPAResult**

-   **설정-BPAResult**

#### <a name="to-scan-a-single-role-by-using-windows-powershell-cmdlets"></a><a name=BKMK_singlerole></a>Windows PowerShell cmdlet을 사용 하 여 단일 역할을 검사 하려면

1.  관리자 권한으로 Windows PowerShell을 실행 하려면 다음 중 하나를 수행 합니다.

    -   **시작** 화면에서 관리자 권한으로 windows powershell을 실행 하려면 **앱** 결과에서 **windows powershell** 타일을 마우스 오른쪽 단추로 클릭 한 다음 앱 바에서 **관리자 권한으로 실행**을 클릭 합니다.

    -   Windows PowerShell 관리자 권한으로 바탕 화면에서를 실행 하려면 마우스 오른쪽 단추로 클릭는 **Windows PowerShell** 바로 가기를 클릭 한 다음 확인 하 고 작업 표시줄에서 **관리자 권한으로 실행**합니다.

2.  Windows PowerShell 3.0부터 모듈의 cmdlet이 처음 사용 될 때 cmdlet 모듈을 Windows PowerShell 세션으로 자동으로 가져옵니다. 따라서 BPA cmdlet 모듈을 가져오거나 로드할 필요가 없습니다.

3.  다음 예제와 같이 **invoke-bpamodel** cmdlet을 입력 하 여 BPA 검사를 수행할 수 있는 모든 역할의 모델 id를 찾습니다.

    `Get-Bpamodel`

4.  3단계의 결과에서 BPA 검사를 실행할 역할의 모델 ID를 찾습니다.

5.  다음 명령 중 하나를 입력하여 특정 역할에 대한 BPA 검사를 시작합니다. 역할이 여러 개인 경우에는 쉼표로 모델 ID를 구분합니다.

    `Invoke-BPAmodel -modelId <modelID_from_Step3>`

    `Invoke-BPAmodel <modelID_from_Step3>`

    **예제:** `Invoke-BPAmodel -modelId Microsoft/Windows/DNSServer,Microsoft/Windows/FileServices`

    > [!NOTE]
    > 모형 ID에는 **Id** 열에 표시되어 있는 전체 경로가 포함됩니다(예: **Microsoft/Windows/Hyper-V**).

    또한 다음 예제와 같이 `Get-BPAmodel` cmdlet의 결과를 `Invoke-BPAmodel` cmdlet에 파이프하여 3단계 결과로부터 특정 역할에 대한 검사를 시작할 수도 있습니다.

    `Get-BPAmodel <model_ID> | Invoke-BPAmodel`

    모델 ID를 지정 하지 않고이 cmdlet을 실행 하 여 반환 되는 모든 모델을 파이프는 `Get-BPAmodel` cmdlet에는 `Invoke-BPAmodel` cmdlet, 서버 관리자 서버 풀에 추가 된 서버에서 사용할 수 있는 모든 모델에 대 한 검사가 시작 됩니다.

#### <a name="to-scan-all-roles-by-using-windows-powershell-cmdlets"></a><a name=BKMK_allroles></a>Windows PowerShell cmdlet을 사용 하 여 모든 역할을 검색 하려면

1.  하나 아직 열려 있지 않은 경우, 관리자 권한으로 Windows PowerShell 세션을 엽니다. 지침의 이전 절차를 참조하십시오.

2.  BPA 검사를 수행할 수 있는 모든 역할을 `Invoke-BPAmodel` cmdlet에 파이프하여 검사를 시작합니다.

    `Get-BPAmodel | Invoke-BPAmodel`

3.  검색이 완료 되 면 Windows PowerShell 반환 결과 검색 한 각 역할에 대해 다음과 유사 하 게 합니다.

    ```
    modelId                 :  Microsoft/Windows/FileServices
    SubmodelId              :
    Success                 :  True
    Scantime                :  1/01/2012  12:18:40 PM
    ScantimeUtcOffset       :  -08:00:00
    detail                  :  {server_name1, server_name2}

    ```

## <a name="manage-scan-results"></a><a name=BKMK_manage></a>검사 결과 관리
GUI에서 BPA 검사를 완료하고 나면 BPA 타일에서 검사 결과를 볼 수 있습니다. 타일에 표시된 결과를 선택하면 역할이 관련 모범 사례를 준수하는지를 나타내는 등 결과 속성이 타일 내 미리 보기 창에 표시됩니다. 결과가 호환 되지 않는 경우 결과 속성에 설명 된 문제를 해결 하는 방법을 알고 싶으면, 오류 및 경고 결과 속성의 하이퍼링크는 Windows Server TechCenter에 대 한 자세한 해결 도움말 항목을 엽니다.

> [!NOTE]
> BPA 검사 결과는 자동으로 저장되거나 보관되지 않습니다. 모델이나 서브모델에 대해 새로운 검사를 실행하면 이전 검사 결과를 덮어씁니다. BPA 검사 결과를 보관, 인쇄하거나 다른 사용자에게 보내기 위해 저장하려면 이 섹션의 [Windows PowerShell 세션에 표시되는 BPA 결과를 다른 형식으로 보거나 저장하려면](#BKMK_formats)을 참조하십시오.

### <a name="exclude-and-include-bpa-results"></a>BPA 결과 포함 및 제외
BPA 검사에서 자주 발생 하지만 해결 하지 않아도 되는 결과와 같은 일부 BPA 결과를 확인할 필요가 없는 경우에는 Windows PowerShell에서 BPA GUI 또는 bpa cmdlet을 사용 하 여 결과를 제외할 수 있습니다. 결과는 언제든 다시 포함할 수 있습니다.

> [!NOTE]
> 제외된 결과는 관리 서버의 뷰에서도 제외됩니다. 다른 관리자는 관리 서버의 제외된 결과를 볼 수 없습니다. 로컬 서버 관리자 콘솔만의 보기에서 결과 제외 하려면 사용 하는 대신 사용자 지정 쿼리를 만들기는 **결과 제외** 명령입니다.

#### <a name="exclude-scan-results"></a><a name=BKMK_exclude></a>검사 결과 제외
**제외** 설정은 영구적이므로, 다시 포함하지 않는 한 제외된 결과는 동일한 컴퓨터의 동일한 모델에 대한 후속 검사에서 계속 제외됩니다.

`Set-BPAResult` 매개 변수와 함께 `Exclude` cmdlet을 사용하여 검사 결과를 제외할 수 있습니다. 서버 관리자의 모범 사례 분석기 타일에서와 같이 개별 결과 개체를 제외할 수 또는 해당 필드 (범주, 제목 및 예를 들어 심각도)와 동일 하거나 지정 된 값을 포함 하는 결과 집합을 제외할 수 있습니다. 예를 들어 모델에 대한 검사 결과 집합에서 모든 **성능** 결과를 제외할 수 있습니다.

> [!NOTE]
> 이 섹션의 절차를 수행하려면 먼저 모델에 대해 하나 이상의 BPA 검사를 실행해야 합니다.

###### <a name="to-exclude-scan-results-by-using-the-gui"></a>GUI를 사용하여 검사 결과를 제외하려면

1.  서버 관리자에서 역할 또는 서버 그룹 페이지를 엽니다.

2.  역할 또는 서버 그룹에 대 한 모범 사례 분석기 타일에서 목록에서 결과 마우스 오른쪽 단추로 누른 **결과 제외**합니다.

    이 결과는 더 이상 결과 목록에 표시되지 않습니다.

3.  제외된 결과를 GUI에서 보려면 내장된 **제외된 결과** 쿼리를 실행합니다. **저장된 검색 쿼리**를 클릭한 다음 **제외된 결과**를 클릭합니다.

    **제외된 결과** 쿼리를 실행하고 나면 목록에 표시되는 결과에 대한 설명에 해당하는 타일 부제가 **제외된 결과**로 바뀝니다. 제외된 결과만 목록에 표시됩니다.

###### <a name="to-exclude-scan-results-by-using-windows-powershell-cmdlets"></a>Windows PowerShell cmdlet을 사용하여 검사 결과를 제외하려면

1.  높은 사용자 권한으로 Windows PowerShell 세션을 엽니다.

2.  다음 명령을 실행하여 모델 검사에서 특정 결과를 제외합니다.

    `Get-BPAResult -modelId <model ID> | Where { $_.<Field Name> -eq Value} | Set-BPAResult -Exclude $true`

    위의 명령은 *모델 id*가 나타내는 모델 id에 대 한 BPA 검사 결과 항목을 검색 합니다.

    명령의 두 번째 섹션은 `Get-BPAResult` cmdlet의 결과를 필터링하여 *필드 이름*이 나타내는 결과 필드의 값이 따옴표 안의 텍스트와 일치하는 검사 결과만 검색합니다.

    두 번째 파이프 문자 뒤에 오는 명령의 마지막 섹션은 cmdlet의 이전 섹션에서 필터링된 결과를 제외합니다.

    **예제:** `Get-BPAResult -Microsoft/Windows/FileServices | Where { $_.Severity -eq Information} | Set-BPAResult -Exclude $true`

#### <a name="include-scan-results"></a>검사 결과 포함
제외된 검사 결과를 보려면 해당 검사 결과를 포함하면 됩니다. **포함** 설정은 영구적이므로 포함된 결과는 동일한 컴퓨터의 동일한 모델에 대한 후속 검사에 계속 포함됩니다.

##### <a name="to-include-scan-results-by-using-the-gui"></a><a name=BKMK_gui></a>GUI를 사용 하 여 검사 결과를 포함 하려면

1.  서버 관리자에서 역할 또는 서버 그룹 페이지를 엽니다.

2.  역할 또는 서버 그룹에 대 한 모범 사례 분석기 타일에 있는 결과 중 하나를 마우스 오른쪽 단추로 **결과 제외** 목록, 쿼리 및 클릭 **결과 포함**합니다.

    이 결과는 더 이상 제외된 결과 목록에 표시되지 않습니다. **모두 지우기**를 클릭하여 이 쿼리를 지우면 포함된 결과로만 구성된 목록으로 포함된 결과를 볼 수 있습니다.

##### <a name="to-include-scan-results-by-using-windows-powershell-cmdlets"></a><a name=BKMK_cmdlets></a>Windows PowerShell cmdlet을 사용 하 여 검사 결과를 포함 하려면

1.  높은 사용자 권한으로 Windows PowerShell 세션을 엽니다.

2.  다음 명령을 입력한 다음 **Enter** 키를 눌러 모델 검사에서 특정 결과를 포함합니다.

    `Get-BPAResult -modelId <model Id> | Where { $_.<Field Name> -eq Value } | Set-BPAResult -Exclude $false`

    위의 명령은 *모델 Id*가 나타내는 모델에 대 한 BPA 검사 결과 항목을 검색 합니다.

    첫 번째 파이프 문자 뒤에 있는 명령의 두 번째 부분 ( **|** )의 결과 필터링 하는 **Get-bparesult** 검사 결과만 여 표시 되는 결과 필드의 값을 검색 하는 cmdlet *필드 이름*, 따옴표 안의 텍스트와 일치 합니다.

    두 번째 파이프 문자 뒤에 있는 명령의 마지막 부분은 **-Exclude** 매개 변수 값을 **false**로 설정하여 cmdlet의 두 번째 부분에서 필터링된 결과를 포함합니다.

    **예제:** `Get-BPAResult -Microsoft/Windows/FileServices | Where { $_.Severity -eq Information} | Set-BPAResult -Exclude $false`

### <a name="view-and-export-bpa-scan-results-in-windows-powershell"></a>Windows PowerShell에서 BPA 검사 결과 보기 및 내보내기
다음 절차를 참조를 확인 하 고 Windows PowerShell cmdlet을 사용 하 여 검사 결과 관리 합니다. 다음 절차를 수행하려면 먼저 하나 이상의 모델이나 서브모델에 대해 BPA 검사를 한 번 이상 실행해야 합니다.

#### <a name="to-view-results-of-the-most-recent-scan-of-a-role-by-using-windows-powershell"></a><a name=BKMK_recentPS></a>Windows PowerShell을 사용 하 여 역할의 가장 최근 검색 결과를 보려면

1.  높은 사용자 권한으로 Windows PowerShell 세션을 엽니다.

2.  지정된 모델 ID에 대한 최신 검사 결과를 가져옵니다. 모델 *ID*로 표시 되는 다음을 입력 하 고 **enter**키를 누릅니다. 쉼표로 모델 ID를 구분하여 여러 모델 ID에 대한 결과를 얻을 수 있습니다.

    `Get-BPAResult <model ID>`

    **예:** `Get-BPAResult Microsoft/Windows/DNSServer,Microsoft/Windows/FileServices`

    역할 서비스와 같이 모델의 서브 모델을 검사 한 경우 cmdlet에 서브 모델 ID를 포함 하 여 해당 서브 모델에 대 한 결과만 가져옵니다.

    **예:** `Get-BPAResult Microsoft/Windows/FileServices -SubmodelID FSRM`

#### <a name="to-view-or-save-bpa-results-from-windows-powershell-sessions-in-different-formats"></a><a name=BKMK_formats></a>Windows PowerShell 세션에서 BPA 결과를 다른 형식으로 보거나 저장 하려면

-   Windows PowerShell에서 각 BPA 결과 다음과 같습니다.

    ```
    ResultNumber     :  14
    ResultId         :  1557706192
    modelId          :  Microsoft/Windows/FileServices
    SubmodelId       :  FSRM
    RuleId           :  16
    computerName     :  server_name1, server_name2
    Context          :  FileServices
    Source           :  server_name1
    Severity         :  Information
    Category         :  Configuration
    Title            :  Access Denied remediation requires remote management be enabled on this server
    Problem          :
    Impact           :
    Resolution       :
    compliance       :  The File Server Best Practices Analyzer scan has determined that you are in compliance with this best practice.
    help             :
    Excluded         :  False

    ```

    다음 중 하나를 수행합니다.

    -   BPA 결과를 표 형식으로 나타내려면 다음의 cmdlet과 같이 이전 예에서 보려는 결과 속성을 추가하여 실행합니다.

        `Get-BPAResult model ID | format-Table -Property <property1,property2,property3...>`

        **예제:** `Get-BPAResult Microsoft/Windows/FileServices | format-Table -Property modelId,SubmodelId,computerName,Source,Severity,Category,Title,Problem,Impact,Resolution,compliance,help`

    -   BPA 결과를 텍스트 문자열 필터와 열 제목(열 제목을 클릭하여 결과를 정렬할 수 있음)이 포함된 GUI 기반 그리드 뷰어 형식으로 나타내려면 다음 cmdlet을 실행합니다.

        `Get-BPAResult <model ID> | OGV`

    -   BPA 결과를 보관 하거나 전자 메일 수신자에 게 보낼 수 있는 HTML 파일로 내보내려면 다음 cmdlet을 실행 합니다. 여기서 *path* 는 html 결과를 저장할 경로와 파일 이름을 나타냅니다.

        `Get-BPAResult <model ID> | convertTo-Html | Set-Content <path>`

        **예제:** `Get-BPAResult Microsoft/Windows/FileServices | convertTo-Html | Set-Content C:\BPAResults\FileServices.htm`

    -   BPA 결과를 쉼표로 구분 된 값 (CSV) 텍스트 파일로 내보내려면 다음 cmdlet을 실행 합니다. 여기서 *path* 는 csv 결과를 저장할 경로와 텍스트 파일 이름을 나타냅니다. CSV 결과 Microsoft Excel 또는 데이터가 스프레드시트나 그리드 표시 하는 다른 프로그램으로 가져올 수 있습니다.

        `Get-BPAResult <model ID> | Export-CSV <path>`

        **예제:** `Get-BPAResult Microsoft/Windows/FileServices | Export-CSV C:\BPAResults\FileServices.txt`

## <a name="see-also"></a>관련 항목
[Windows Server TechCenter의 모범 사례 분석기 해결 내용](https://go.microsoft.com/fwlink/p/?LinkId=241597)
[서버 관리자 타일의 데이터를 필터링, 정렬 및 쿼리](filter-sort-and-query-data-in-server-manager-tiles.md)
[서버 관리자를 사용 하 여 여러 원격 서버 관리](manage-multiple-remote-servers-with-server-manager.md)
