---
title: 확장에 PowerShell 사용하기
description: 확장에서 PowerShell 사용 Windows 관리 센터 SDK (Project Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 05/09/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 6e99fc43d4acb7a70dfd3a8ba19dae6492c41b2b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357046"
---
# <a name="using-powershell-in-your-extension"></a>확장에 PowerShell 사용하기 #

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows 관리 센터 확장 SDK에 대해 자세히 알아보겠습니다. 확장에 PowerShell 명령을 추가 하는 방법에 대해 알아보겠습니다.

## <a name="powershell-in-typescript"></a>TypeScript의 PowerShell ##

Gulp ```{!ScriptName}.ps1``` 빌드 프로세스에는 ```\src\resources\scripts``` 폴더에 배치 된 항목 ```powershell-scripts``` 을 가져와서 ```\src\generated``` 폴더 아래의 클래스로 빌드하는 생성 단계가 있습니다.

>[!NOTE] 
> ```powershell-scripts.ts``` 또는 파일을수동으로업데이트하지마십시오.```strings.ts``` 모든 변경 내용은 다음에 생성 될 때 덮어쓰여집니다.

## <a name="running-a-powershell-script"></a>PowerShell 스크립트 실행 ##
노드에서 실행 하려는 모든 스크립트를에 ```\src\resources\scripts\{!ScriptName}.ps1```배치할 수 있습니다. 
>[!IMPORTANT] 
> ```{!ScriptName}.ps1``` 파일의 변경 내용은가 실행 될 때까지 ```gulp generate``` 프로젝트에 반영 되지 않습니다.

이 API는 먼저 대상으로 하는 노드에서 PowerShell 세션을 만들고, 전달 해야 하는 매개 변수를 사용 하 여 PowerShell 스크립트를 만든 다음, 만들어진 세션에서 스크립트를 실행 하는 방식으로 작동 합니다.

예를 들어 다음 스크립트가 ```\src\resources\scripts\Get-NodeName.ps1```있습니다.
``` ps1
Param
 (
    [String] $stringFormat
 )
 $nodeName = [string]::Format($stringFormat,$env:COMPUTERNAME)
 Write-Output $nodeName
```

대상 노드에 대 한 PowerShell 세션을 만듭니다.
``` ts
const session = this.appContextService.powerShell.createSession('{!TargetNode}'); 
```
그런 다음 입력 매개 변수를 사용 하 여 PowerShell 스크립트를 만듭니다.
```ts
const script = PowerShell.createScript(PowerShellScripts.Get_NodeName, {stringFormat: 'The name of the node is {0}!'});
```
마지막으로, 만든 세션에서 해당 스크립트를 실행 해야 합니다.
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
이제 방금 만든 관찰 가능 함수를 구독 해야 합니다. PowerShell 스크립트를 실행 하려면 함수를 호출 해야 하는 위치에이 위치를 추가 합니다.
```ts
this.getNodeName().subscribe(
     response => {
    console.log(response)
     }
);
```
CreateSession 메서드에 노드 이름을 제공 하면 새 PowerShell 세션이 생성 되어 사용 된 후 PowerShell 호출이 완료 되 면 즉시 제거 됩니다. 

### <a name="key-options"></a>키 옵션 ###
PowerShell API를 호출할 때 몇 가지 옵션을 사용할 수 있습니다. 세션을 만들 때마다 키를 사용 하거나 사용 하지 않고 만들 수 있습니다. 

**키:** 이렇게 하면 구성 요소 간에 조회 하 여 다시 사용할 수 있는 키가 지정 된 세션이 생성 됩니다. 즉, Component1에서 키가 "SME-암석 지 어" 인 세션을 만들고 Component2는 동일한 세션을 사용할 수 있습니다. 키를 제공 하는 경우 위의 예제에서와 같이 dispose ()를 호출 하 여 생성 된 세션을 삭제 해야 합니다. 5 분 넘게 세션을 삭제 하지 않고 세션을 유지 하면 안 됩니다. 
```ts
  const session = this.appContextService.powerShell.createSession('{!TargetNode}', '{!Key}');
```

**키가 없는** 세션에 대 한 키가 자동으로 만들어집니다. 이 세션은 3 분 후에 자동으로 삭제 됩니다. 키가 없는를 사용 하면 확장에서 세션을 만들 때 이미 사용할 수 있는 Runspace 사용을 재활용할 수 있습니다. 새 Runspace를 사용할 수 없는 경우 새 Runspace가 생성 됩니다. 이 기능은 일회용 호출에 유용 하지만 반복적인 사용이 성능에 영향을 줄 수 있습니다. 세션을 만드는 데 약 1 초가 걸립니다. 따라서 연속 재활용 세션으로 인해 속도가 저하 될 수 있습니다.

```ts
  const session = this.appContextService.powerShell.createSession('{!TargetNodeName}');
```
로 구분하거나 여러 
``` ts 
const session = this.appContextService.powerShell.createAutomaticSession('{!TargetNodeName}');
```
대부분의 경우 ```ngOnInit()``` 메서드에서 키가 지정 된 세션을 만든 다음에서 ```ngOnDestroy()```해당 세션을 삭제 합니다. 구성 요소에 여러 PowerShell 스크립트가 있지만 구성 요소 간에 기본 세션이 공유 되지 않는 경우이 패턴을 따릅니다.
최상의 결과를 위해 서비스 대신 구성 요소 내에서 세션 만들기가 관리 되는지 확인 합니다 .이를 통해 수명 및 정리를 적절 하 게 관리할 수 있습니다.

최상의 결과를 위해 서비스 대신 구성 요소 내에서 세션 만들기가 관리 되는지 확인 합니다 .이를 통해 수명 및 정리를 적절 하 게 관리할 수 있습니다.

### <a name="powershell-stream"></a>PowerShell 스트림 ###
장기 실행 스크립트가 있고 데이터가 점차적으로 출력 되는 경우 PowerShell 스트림은 스크립트가 완료 될 때까지 기다리지 않고도 데이터를 처리할 수 있도록 합니다. 관찰 가능한 다음 ()은 데이터가 수신 되는 즉시 호출 됩니다.
```ts
this.appContextService.powerShellStream.run(session, script);
```

### <a name="long-running-scripts"></a>장기 실행 스크립트 ###
백그라운드에서 실행 하려는 장기 실행 스크립트가 있으면 작업 항목을 제출할 수 있습니다. 스크립트 상태는 게이트웨이에서 추적 되 고 상태에 대 한 업데이트를 알림으로 보낼 수 있습니다. 
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
> 진행률을 표시 하려면 작성 한 스크립트에 쓰기 진행률을 포함 해야 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.
> ``` ps1
>  Write-Progress -Activity ‘The script is almost done!' -percentComplete 95
>```

#### <a name="workitem-options"></a>작업 항목 옵션 ####

| function | 설명 |
| ----- | ----------- |
| submit () | 작업 항목을 제출 합니다. 
| submitAndWait () | 작업 항목을 제출 하 고 실행이 완료 될 때까지 기다립니다.
| wait () | 기존 작업 항목이 완료 될 때까지 대기
| query () | Id 별로 기존 작업 항목 쿼리
| find () | TargetNodeName, ModuleName 또는 typeId를 기준으로 기존 작업 항목을 찾습니다.

### <a name="powershell-batch-apis"></a>PowerShell Batch Api ###
여러 노드에서 동일한 스크립트를 실행 해야 하는 경우 batch PowerShell 세션을 사용할 수 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.
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
| runSingleCommand | 배열의 모든 노드에 대해 단일 명령을 실행 합니다. 
| 실행할지 | 쌍을 이루는 노드에서 해당 명령을 실행 합니다.
| 취소 | 배열의 모든 노드에 대해 명령을 취소 합니다.
