---
title: 복제 된 폴더에 대 한 최소 준비 영역 DFSR 요구 사항을 확인 하는 방법
description: 이 문서는 DFSR이 제대로 작동 하는 데 필요한 최소 준비 영역을 계산 하는 방법에 대 한 빠른 참조 가이드입니다.
ms.prod: windows-server
ms.technology: server-general
ms.date: 06/10/2020
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: 5e5bfdbb90d2b3e631aaa020a173eca779f0d6b3
ms.sourcegitcommit: fa9a8badf4eb366aeeca7d2905e2cad711ee8dae
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715007"
---
# <a name="how-to-determine-the-minimum-staging-area-dfsr-needs-for-a-replicated-folder"></a>복제 된 폴더에 대 한 최소 준비 영역 DFSR 요구 사항을 확인 하는 방법

이 문서는 DFSR이 제대로 작동 하는 데 필요한 최소 준비 영역을 계산 하는 방법에 대 한 빠른 참조 가이드입니다. 이러한 값 보다 낮으면 복제가 느리거나 완전히 중지 될 수 있습니다. 

이는 *최소값만*을 염두에 두어야 합니다. 준비 영역 크기를 고려 하는 경우 복제 된 폴더의 크기까지 준비 영역이 더 커집니다. 적절 한 크기의 준비 영역을 설정 하는 것이 중요 한 이유에 대 한 자세한 내용은이 문서의 끝 부분에 있는 "준비 영역 문제가 있는지 확인 하는 방법" 섹션을 참조 하세요.

> [!Note]
> 또한 준비 크기를 계산 하는 데 도움이 되는 핫픽스도 제공 합니다. [DFSR (DFS 복제) 관리 인터페이스에 대 한 업데이트를 사용할 수 있습니다.](https://support.microsoft.com/kb/2607047)

## <a name="rules-of-thumb"></a>Thumb의 규칙

**Windows Server 2003 R2** – 준비 영역 할당량은 복제 된 폴더의 최대 9 개 파일 크기 보다 커야 합니다.

**Windows Server 2008 및 2008 R2** – 준비 영역 할당량은 복제 된 폴더에 있는 32 가장 큰 파일 만큼 커야 합니다.

초기 복제는 일상적인 복제 보다 준비 영역을 훨씬 더 많이 사용 합니다. 초기 복제 중 준비 영역을 최소 이상으로 설정 하는 것은 드라이브 공간을 사용할 수 있는 경우에 권장 됩니다.

## <a name="where-do-i-get-powershell"></a>PowerShell은 어디에서 얻을 까 요?

PowerShell은 Windows 2008 이상에 포함 되어 있습니다. Windows Server 2003에 PowerShell을 설치 해야 합니다. [여기](https://support.microsoft.com/kb/968930)에서 Windows 2003에 대 한 PowerShell을 다운로드할 수 있습니다.

## <a name="how-do-you-find-these-x-largest-files"></a>이러한 X 가장 큰 파일은 어떻게 찾을 수 있나요?

PowerShell 스크립트를 사용 하 여 32 또는 9 개의 가장 큰 파일을 찾고 얼마나 많은 기가바이트 (PowerShell 명령에 대 한 Pyle)를 확인 합니다. 실제로는 세 개의 PowerShell 스크립트를 제공 합니다. 각각은 자체적으로 유용 합니다. 그러나 숫자 3이 가장 유용 합니다.

1. 다음 명령을 실행합니다.  
   ```Powershell
   Get-ChildItem c:\\temp -recurse | Sort-Object length -descending | select-object -first 32 | ft name,length -wrap –auto
   ```
   
   이 명령은 파일 이름과 파일 크기 (바이트)를 반환 합니다. 복제 된 폴더에서 가장 큰 32 파일이 무엇 인지 파악 하 여 소유자를 "방문" 할 수 있는 경우에 유용 합니다.

2. 다음 명령을 실행합니다.  
   ```Poswershell
   Get-ChildItem c:\\temp -recurse | Sort-Object length -descending | select-object -first 32 | measure-object -property length –sum
   ```
   이 명령은 파일 이름을 나열 하지 않고 폴더에 있는 32 가장 큰 파일의 총 바이트 수를 반환 합니다.

3. 다음 명령을 실행합니다.  
   ```Poswershell
   $big32 = Get-ChildItem c:\\temp -recurse | Sort-Object length -descending | select-object -first 32 | measure-object -property length –sum
   
   $big32.sum /1gb
   ```
   이 명령은 폴더에 있는 최대 32 바이트의 총 바이트 수를 가져오고 계산을 수행 하 여 바이트를 기가바이트로 변환 합니다. 이 명령은 두 줄로 구분 됩니다. 두 항목을 모두 PowerShell 명령 셸에 한 번에 붙여넣거나 다시 실행할 수 있습니다.

## <a name="manual-walkthrough"></a>수동 연습

프로세스를 시연 하 고 수행 하는 작업을 더 잘 이해 하기 위해 각 파트를 수동으로 단계별로 진행 합니다.

명령 1을 실행 하면 아래 출력과 비슷한 결과가 반환 됩니다. 이 예제에서는 간결 하 게 16 파일만 사용 합니다. Windows 2008 이상 운영 체제의 경우 항상 32을 사용 하 고 Windows 2003 r 2에는 9를 사용 합니다.

### <a name="example-data-returned-by-powershell"></a>PowerShell에서 반환 된 데이터 예제

<table>
<tbody>
<tr class="odd">
<td>속성</td>
<td>길이</td>
</tr>
<tr class="even">
<td><strong>File5.zip</strong></td>
<td>10286089216</td>
</tr>
<tr class="odd">
<td><strong>archive.zip</strong></td>
<td>6029853696</td>
</tr>
<tr class="even">
<td><strong>BACKUP.zip</strong></td>
<td>5751522304</td>
</tr>
<tr class="odd">
<td> <strong>file9.zip</strong></td>
<td>5472683008</td>
</tr>
<tr class="even">
<td><strong>MENTOS.zip</strong></td>
<td>5241586688</td>
</tr>
<tr class="odd">
<td><strong>File7.zip</strong></td>
<td>4321264640</td>
</tr>
<tr class="even">
<td><strong>file2.zip</strong></td>
<td>4176765952</td>
</tr>
<tr class="odd">
<td><strong>frd2.zip</strong></td>
<td>4176765952</td>
</tr>
<tr class="even">
<td><strong>BACKUP.zip</strong></td>
<td>4078994432</td>
</tr>
<tr class="odd">
<td><strong>File44.zip</strong></td>
<td>4058424320</td>
</tr>
<tr class="even">
<td><strong>file11.zip</strong></td>
<td>3858056192</td>
</tr>
<tr class="odd">
<td><strong>Backup2.zip</strong></td>
<td>3815138304</td>
</tr>
<tr class="even">
<td><strong>BACKUP3.zip</strong></td>
<td>3815138304</td>
</tr>
<tr class="odd">
<td><strong>Current.zip</strong></td>
<td>3576931328</td>
</tr>
<tr class="even">
<td><strong>Backup8.zip</strong></td>
<td>3307488256</td>
</tr>
<tr class="odd">
<td><strong>File999.zip</strong></td>
<td>3274982400</td>
</tr>
</tbody>
</table>

### <a name="how-to-use-this-data-to-determine-the-minimum-staging-area-size"></a>이 데이터를 사용 하 여 최소 준비 영역 크기를 확인 하는 방법:

  - Name = 파일의 이름입니다.
  - 길이 = 바이트
  - 1 기가바이트 = 1073741824 바이트

먼저 총 바이트 수의 합계를 계산 해야 합니다. 그런 다음 합계를 1073741824으로 나눕니다. Excel 또는 원하는 스프레드시트를 사용 하 여 계산을 수행 하는 것이 좋습니다.

### <a name="example"></a>예제

위의 예제에서 총 바이트 수 = 75241684992입니다. 필요한 최소 준비 영역 할당량을 얻으려면 75241684992을 1073741824로 나누려고 합니다.

> 75241684992/1073741824 = 70.07 GB

이 데이터를 기반으로 하 여 가장 근사한 정수로 반올림 하는 경우 준비 영역을 71 GB로 설정 합니다.

### <a name="real-world-scenario"></a>실제 시나리오:

수동 연습이 흥미로운 것은 아니지만 사용자가 직접 수치를 계산 하는 데 시간이 많이 소요 되는 것은 아닙니다. 프로세스를 자동화 하려면 위의 예제에서 명령 3을 사용 합니다. 결과는 다음과 같습니다.

> [![이미지로](https://msdnshared.blob.core.windows.net/media/TNBlogsFS/prod.evol.blogs.technet.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/58/02/metablogapi/8204.image_thumb_02CB3914.png "이미지")](https://msdnshared.blob.core.windows.net/media/TNBlogsFS/prod.evol.blogs.technet.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/58/02/metablogapi/0876.image_03A39EFE.png)

가장 근사한 정수로 반올림 하는 경우를 제외 하 고 예제 명령 3을 사용 하면 d: docs에 대해 6gb의 준비 영역 할당량이 필요 하다는 것을 알 수 있습니다 \\ .

## <a name="do-i-need-to-reboot-or-restart-the-service-for-the-changes-to-be-picked-up"></a>변경 내용을 적용 하려면 서비스를 다시 부팅 하거나 다시 시작 해야 하나요?

준비 영역 할당량을 변경 하는 경우 다시 부팅 하거나 서비스를 다시 시작 해야 적용 됩니다. 변경 내용을 적용 하려면 AD 복제 및 DFSR의 AD 폴링 주기에서 대기 해야 합니다.

## <a name="how-to-determine-if-you-have-a-staging-area-problem"></a>준비 영역 문제가 있는지 확인 하는 방법

DFSR 서버에서 특정 이벤트 Id를 모니터링 하 여 준비 영역 문제를 검색 합니다. 이벤트 목록은 4202, 4204, 4206, 4208 및 4212입니다. 이러한 이벤트의 텍스트는 다음과 같습니다. 4202과 4204 및 기타 이벤트를 구분 하는 것이 중요 합니다. 정상적인 운영 상태에서 많은 수의 4202 및 4204 이벤트를 기록할 수 있습니다. 4202 및 4204 이벤트는 펄스를 수행 하는 것과 유사 하지만 4206, 4208 및 4212은 pains와 비슷합니다. 아래에서 4202 및 4204 이벤트를 해석 하는 방법을 설명 합니다.

### <a name="staging-area-events"></a>준비 영역 이벤트

> 이벤트 ID: **4202**  
> 심각도: **경고**
> 
> DFS 복제 서비스에서 로컬 경로 (경로)에 있는 복제 된 폴더에 사용 중인 준비 공간이 상위 워터 마크 위에 있음을 검색 했습니다. 서비스에서 가장 오래 된 준비 파일을 삭제 하려고 합니다. 성능에 영향을 줄 수 있습니다.
> 
> 이벤트 ID: **4204**  
> 심각도: **정보**
> 
> DFS 복제 서비스가 로컬 경로 (경로)에서 복제 된 폴더에 대 한 오래 된 준비 파일을 삭제 했습니다. 이제 준비 공간이 상위 워터 마크 아래에 있습니다.
> 
> 이벤트 ID: **4206**  
> 심각도: **경고**
> 
> DFS 복제 서비스가 로컬 경로 (경로)에서 복제 된 폴더에 대 한 오래 된 준비 파일을 정리 하지 못했습니다. 서비스가 일부 크기의 파일을 복제 하지 못할 수 있으며 복제 된 폴더가 동기화 되지 않을 수 있습니다. 서비스는 (x) 분 내에 준비 공간 정리를 자동으로 다시 시도 합니다. 잠금 해제 된 일부 준비 파일이 검색 되 면 서비스는 이전에 정리를 시작할 수 있습니다.
> 
> 이벤트 ID: **4208**  
> 심각도: **경고**
> 
> DFS 복제 서비스에서 준비 공간 사용량이 로컬 경로 (경로)에 있는 복제 된 폴더의 준비 할당량을 초과 하는 것을 감지 했습니다. 서비스가 일부 크기의 파일을 복제 하지 못할 수 있으며 복제 된 폴더가 동기화 되지 않을 수 있습니다. 서비스는 자동으로 준비 공간 정리를 시도 합니다.
> 
> 이벤트 ID: **4212**  
> 심각도: **오류**
> 
> 준비 경로가 잘못 되었거나 액세스할 수 없기 때문에 DFS 복제 서비스에서 로컬 경로 (경로)에 복제 된 폴더를 복제할 수 없습니다.

## <a name="what-is-the-difference-between-4202-and-4208"></a>4202와 4208의 차이는 무엇 인가요?

이벤트 4202 및 4208에 비슷한 텍스트가 있습니다. 즉, DFSR에서 준비 영역 사용량이 상위 워터 마크를 초과 하는 것을 감지 했습니다. 차이점은 준비 영역 정리가 실행 되 고 준비 할당량은 여전히 초과 된 후 4208이 기록 된다는 것입니다. 4202는 정상 및 예상 이벤트 이지만, 4208은 비정상 이며 작업이 필요 합니다.

## <a name="how-many-4202-4204-events-are-too-many"></a>4202, 4204 이벤트는 몇 개 인가요?

이 질문에 대 한 대답은 하나입니다. 항상 유효 하지 않은 4206, 4208 또는 4212 이벤트와 달리 정상적인 운영 조건에서 4202 및 4204 이벤트가 발생 합니다. 많은 4202 및 4204 이벤트를 보면 문제가 있음을 나타낼 *수 있습니다* . 고려 사항은 다음과 같습니다.

1.  복제 된 폴더 (RF) 로깅 4202에서 초기 복제를 수행 하나요? 이 경우 4202 및 4204 이벤트를 기록 하는 것이 정상입니다. 가능한 한 많은 준비 영역을 제공 하 여 초기 복제 중에 최대한 적은 수로 유지 하는 것이 좋습니다.
2.  4202 이벤트의 총 수를 확인 하는 것 만으로는 충분 하지 않습니다. RF 당 로깅되는 수를 알고 있어야 합니다. 24 시간 동안 한 RF에 대해 20 4202 이벤트를 기록 하는 경우 (높음). 그러나 복제 된 폴더가 20 개 있고 폴더당 하나의 이벤트가 있는 경우에는이 작업을 수행 하는 것이 좋습니다.
3.  몇 일 동안의 데이터를 검사 하 여 추세를 설정 해야 합니다.

일반적으로 일반 운영 상태에서 매일 복제 된 폴더에 1 4202 개 이하의 이벤트를 허용 하는 고객을 자문 위원 합니다. "Normal"은 초기 복제가 발생 하지 않음을 의미 합니다. 이를 기반으로 하는 이유는 다음과 같습니다.

1.  준비 영역을 정리 하는 데 걸린 시간은 파일을 복제 하는 데 소요 된 시간입니다. 준비 영역이 지워지는 동안 복제가 일시 중지 되었습니다.
2.  DFSR은 RDC 및 파일 간 RDC를 사용 하 여 전체 준비 영역을 활용 하거나 동일한 파일을 다른 구성원에 게 복제 합니다.
3.  더 많은 4202 및 4204 이벤트를 기록 하는 경우 DFSR이 준비 영역을 정리할 수 없거나 준비 영역에서 파일을 중간에 제거 해야 하는 조건에 따라 실행 됩니다.
4.  4206, 4208 및 4212 이벤트는 항상 앞과 뒤에 많은 4202 및 4204 이벤트의 앞과 뒤에 있습니다.

초당 RF 당 1 4202 이벤트를 허용 하는 것은 매우 간단 하지만, 준비 영역 문제로 인해 발생 하는 것이 저하 되는 것은 매우 저하 되며 파일 복제를 위한 목적으로 DFSR 서버 리소스를 활용 하는 것이 더 효율적입니다.


