---
title: 확장에 PowerShell 사용하기
description: PowerShell을 사용 하 여 Windows Admin Center SDK (프로젝트 브라 티) 확장의
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 05/09/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 7375732fd464519cd1533043d271065e488fd46a
ms.sourcegitcommit: 7cb939320fa2613b7582163a19727d7b77debe4b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65621362"
---
# <a name="using-powershell-in-your-extension"></a>확장에 PowerShell 사용하기 #

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center 확장 SDK를 자세한 보겠습니다-PowerShell 명령 확장을 추가 하는 방법을 알아보겠습니다.

## <a name="powershell-in-typescript"></a>TypeScript에 대 한 PowerShell ##

Gulp 빌드 프로세스에 연결 되는 모든 생성 단계가 포함 되어 ```{!ScriptName}.ps1``` 에 배치 되는 합니다 ```\src\resources\scripts``` 폴더 및 빌드에 ```powershell-scripts``` 에서 클래스를 ```\src\generated``` 폴더.

>[!NOTE] 
> 수동으로 업데이트 하지는 ```powershell-scripts.ts``` 또는 ```strings.ts``` 파일입니다. 다음 생성에서 변경은 수행 하면 덮어쓰게 됩니다.

## <a name="running-a-powershell-script"></a>PowerShell 스크립트 실행 ##
노드에서 실행 하려는 모든 스크립트에 배치할 수 있습니다 ```\src\resources\scripts\{!ScriptName}.ps1```합니다. 
>[!IMPORTANT] 
> 변경에 ```{!ScriptName}.ps1``` 파일까지 프로젝트에 반영 되지 것입니다 ```gulp generate``` 실행 된 합니다.

API를 대상 지정을 전달 해야 하는 매개 변수를 사용 하 여 PowerShell 스크립트 만들기 및 만들어진 세션에서 스크립트를 실행 한 다음는 노드에서 PowerShell 세션을 만들어 작동 합니다.

이 스크립트를 있다고 예를 들어 ```\src\resources\scripts\Get-NodeName.ps1```:
``` ps1
Param
 (
    [String] $stringFormat
 )
 $nodeName = [string]::Format($stringFormat,$env:COMPUTERNAME)
 Write-Output $nodeName
```

여기서는 대상 노드에 대 한 PowerShell 세션을 만듭니다.
``` ts
const session = this.appContextService.powerShell.createSession('{!TargetNode}'); 
```
다음 PowerShell 스크립트를 입력된 매개 변수를 사용 하 여 만듭니다.
```ts
const script = PowerShell.createScript(PowerShellScripts.Get_NodeName, {stringFormat: 'The name of the node is {0}!'});
```
마지막으로 만든 세션에서 해당 스크립트를 실행 해야 합니다.
``` ts
  public ngOnInit(): void {
    this.session = this.appContextService.powerShell.createAutomaticSession('{!TargetNode}');
  }

  public getNodeName(): Observable<any> {
    const script = PowerShell.createScript(PowerShellScripts.Get_NodeName.script, { stringFormat: 'The name of the node is {0}!'});
    return this.appContextService.powerShell.run(this.session, script)
    .pipe(
        map(
        response => {
            if (response && response.results) {
                return response.results;
            }
            return 'no response';
        }
      ) 
    );
  }

  public ngOnDestroy(): void {
    this.session.dispose()
  }

```
이제 방금 만든 관찰 가능한 함수를 구독 해야 합니다. PowerShell 스크립트를 실행 하려면 함수를 호출 해야 하는이 배치 합니다.
```ts
this.getNodeName().subscribe(
     response => {
    console.log(response)
     }
);
```
노드 이름을 createSession 메서드를 제공 하 여 새 PowerShell 세션을 생성, 사용 되어 PowerShell 호출 완료 시 즉시 제거 합니다. 

### <a name="key-options"></a>키 옵션 ###
PowerShell API를 호출 하는 경우 몇 가지 옵션이 제공 됩니다. 세션이 만들어질 때마다 만들 수 있습니다 또는 키가 없는 합니다. 

**키:** 이 조회 하 고 구성 요소 (즉 Component1 "SME ROCKS" 키를 사용 하 여 세션을 만들 수 고 Component2 동일한 세션에 사용할 수 있습니다) 에서도 재사용할 수 있는 키가 지정 된 세션을 만듭니다. 키가 제공 하는 경우 만들어지는 세션 삭제 해야 호출 dispose ()에서 위의 예제에서 수행 했던 것 처럼 합니다. 5 분 넘게의 삭제 되지 않고 세션을 유지 되어야 합니다. 
```ts
  const session = this.appContextService.powerShell.createSession('{!TargetNode}', '{!Key}');
```

**키:** 키를 세션에 대해 자동으로 만들어집니다. 3 분 후 자동으로이 세션을 삭제 합니다. 키를 사용 하 여 사용자 지정 확장을 세션을 만들 때 이미 사용할 수 있는 모든 Runspace 사용 재활용을 수 있습니다. 없으면 없습니다 Runspace 보다 새로 만들어집니다. 이 기능은 일회성 호출에 적합 하지만 반복 해 서 사용 성능에 영향을 줄 수 있습니다. 세션은 만들려면 약 1 초, 따라서 지속적으로 세션을 재생 속도 저하를 발생할 수 있습니다.

```ts
  const session = this.appContextService.powerShell.createSession('{!TargetNodeName}');
```
로 구분하거나 여러 
``` ts 
const session = this.appContextService.powerShell.createAutomaticSession('{!TargetNodeName}');
```
대부분의 경우에 키가 지정 된 세션을 만들 합니다 ```ngOnInit()``` 메서드를 다음 dispose를 ```ngOnDestroy()```입니다. 구성 요소 구성 요소 간에 공유 되지 기본 세션에 여러 PowerShell 스크립트가 있는 경우이 패턴을 따릅니다.
최상의 결과 서비스 보다는 구성 내에서 관리 되는 세션을 만든-해당 수명 동안 보장이 있는지 확인 하 고 정리를 제대로 관리할 수 있습니다.

최상의 결과 서비스 보다는 구성 내에서 관리 되는 세션을 만든-해당 수명 동안 보장이 있는지 확인 하 고 정리를 제대로 관리할 수 있습니다.

### <a name="powershell-stream"></a>PowerShell Stream ###
장기 실행 스크립트 및 데이터를 있는 경우 출력 됩니다 점진적으로 PowerShell 스트림을 스크립트가 완료 될 때까지 기다릴 필요 없이 데이터를 처리할 수 있습니다. Observable next ()는 데이터를 수신할 때 호출 됩니다.
```ts
this.appContextService.powerShellStream.run(session, script);
```

### <a name="long-running-scripts"></a>장기 실행 스크립트 ###
장기 실행 스크립트를 백그라운드에서 실행 하려는 경우에 작업 항목을 제출할 수 있습니다. 게이트웨이에서 추적할 스크립트의 상태 및 상태에 대 한 업데이트 알림을 보낼 수 있습니다. 
```ts
const workItem: WorkItemSubmitRequest = {
    typeId: 'Long Running Script',
    objectName: 'My long running service',
    powerShellScript: script,
    
    //in progress notifications
    inProgressTitle: 'Executing long running request',
    startedMessage: 'The long running request has been started',
    progressMessage: 'Working on long running script – {{ percent }} %',

    //success notification
    successTitle: 'Successfully executed a long running script!',
    successMessage: '{{objectName}} was successful',
    successLinkText: 'Bing',
    successLink: 'http://www.bing.com',
    successLinkType: NotificationLinkType.Absolute,

    //error notification
    errorTitle: 'Failed to execute long running script',
    errorMessage: 'Error: {{ message }}'

    nodeRequestOptions: {
       logAudit: true,
       logTelemetry: true
    }
};

return this.appContextService.workItem.submit('{!TargetNode}', workItem);
```

>[!NOTE] 
> 표시할 진행률에 대 한 Write-progress는 작성 한 스크립트에 포함 되어야 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.
> ``` ps1
>  Write-Progress -Activity ‘The script is almost done!’ -percentComplete 95
>```

#### <a name="workitem-options"></a>작업 항목 옵션 ####

| function | 설명 |
| ----- | ----------- |
| submit() | 작업 항목 전송 
| submitAndWait() | 작업 항목을 제출 하 고 해당 실행 완료 될 때까지
| wait() | 기존 작업에 대 한 대기를 완료 하는 항목
| query() | Id 별로 기존 작업 항목에 대 한 쿼리
| find() | 찾기 및 기존 TargetNodeName, ModuleName, 또는 typeId 작업 항목.

### <a name="powershell-batch-apis"></a>Batch PowerShell Api ###
여러 노드에서 동일한 스크립트를 실행 해야 할 경우에 batch PowerShell 세션을 사용할 수 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.
```ts
const batchSession = this.appContextService.powerShell.createBatchSession(
    ['{!TargetNode1}', '{!TargetNode2}', sessionKey);
  this.appContextService.powerShell.runBatchSingleCommand(batchSession, command).subscribe((responses: PowerShellBatchResponseItem[]) => {
    for (const response of responses) { 
      if (response.error || response.errors) {
        //handle error
      } else {
        const results = response.properties && response.properties.results;
        //response.nodeName
        //results[0]
      }
    }
     },
     Error => { /* handle error */ });  

```


#### <a name="powershellbatch-options"></a>PowerShellBatch 옵션 ####
| 옵션 | 설명 |
| ----- | ----------- |
| runSingleCommand | 배열에 있는 모든 노드가 단일 명령 실행 
| 실행 | 쌍으로 연결 된 노드에서 해당 명령 실행
| 취소 | 배열에 있는 모든 노드에서 명령을 취소합니다
