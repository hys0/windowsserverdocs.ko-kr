---
title: 확장에 PowerShell 사용하기
description: Windows Admin Center SDK (Project Honolulu) 확장에 PowerShell을 사용 하 여
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: b1be4fe7639d913243cc28371dff9e98e0f5827e
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296725"
---
# 확장에 PowerShell 사용하기 #

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center 확장 SDK에 더 자세히 살펴보겠습니다-확장에 PowerShell 명령을 추가 하는 방법에 대 한 살펴보겠습니다.

## PowerShell typescript로 작성 ##

Gulp 빌드 프로세스에는 모든 작업은 생성 단계 ```{!ScriptName}.ps1``` 에 배치 되는 합니다 ```\src\resources\scripts``` 폴더에 빌드합니다 합니다 ```powershell-scripts``` 아래에서 클래스는 ```\src\generated``` 폴더.

>[!NOTE] 
> 수동으로 업데이트 하지는 ```powershell-scripts.ts``` 및 ```strings.ts``` 파일. 변경한 다음 생성에 덮어씁니다.

## Powerhell 스크립트를 실행 ##
노드에서 실행 하려는 모든 스크립트에 배치할 수 있습니다 ```\src\resources\scripts\{!ScriptName}.ps1```. 
>[!IMPORTANT] 
> 변경에 ```{!ScriptName}.ps1``` 파일 하지 않는 한 프로젝트에 반영 되지 것입니다는 생성 

API를 대상으로, PowerShell 스크립트를 전달 해야 하는 매개 변수를 사용 하 여 만들고 생성 된 세션에서 스크립트를 실행 한 다음 노드에서 PowerShell 세션을 만들면 작동 합니다.

이 스크립트는 예를 들어 ```\src\resources\scripts\Get-NodeName.ps1```:
``` ps1
Param
 (
    [String] $stringFormat
 )
 $nodeName = [string]::Format($stringFormat,$env:COMPUTERNAME)
 Write-Output $nodeName
```

우리의 대상 노드에 대 한 PowerShell 세션을 만듭니다.
``` ts
const session = this.appContextService.powerShell.createSession('{!TargetNode}'); 
```
그런 다음 입력된 매개 변수를 사용 하 여 PowerShell 스크립트를 만듭니다.
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
이제 방금 만든 관찰 가능한 함수에 가입 해야 합니다. PowerShell 스크립트를 실행 하는 함수를 호출 해야이 배치 합니다.
```ts
this.getNodeName().subscribe(
     response => {
    console.log(response)
     }
);
```
노드 이름을 createSession 메서드를 제공 하 여 새 PowerShell 세션은 생성 하 고 사용한 PowerShell 호출이 완료 되 면 즉시 삭제 합니다. 

### 키 옵션 ###
몇 가지 옵션은 PowerShell API를 호출할 때 사용할 수 있습니다. 세션이 만들어질 때마다 만들어질 수 있습니다에 관계 없이 키. 

**키:** 조회 하 고 (즉 Component1 "SME 바위" 키를 사용 하 여 세션을 만들 수 고 Component2 동일한 해당 세션을 사용할 수 있습니다) 구성 요소에서 재사용할 수 있는 키가 지정 된 세션을 만듭니다. 키를 제공 하는 경우 만들어진 세션 삭제 해야의 호출 dispose () 하 여 위의 예제 에서처럼. 세션을 5 분 이상의 삭제 되지 않고 유지 되어야 합니다. 
```ts
  const session = this.appContextService.powerShell.createSession('{!TargetNode}', '{!Key}');
```

**키가 없는:** 키를 세션에 대 한 자동으로 생성 됩니다. 3 분 후에 자동으로이 세션을 삭제 합니다. 키가 없는 사용 하면 재생 세션의 생성 시 이미 사용할 수 있는 모든 Runspace 사용 하도록 확장 합니다. 없는 Runspace 새로 만들 수는 보다 사용할 수 있는 경우. 이 기능은 일회용 호출에 대 한 좋은 하지만 반복 해 서 사용 성능에 영향을 줄 수 있습니다. 세션은 만들려는 약 1 초, 따라서 지속적으로 세션을 재활용 성능 저하 될 수 있습니다.

```ts
  const session = this.appContextService.powerShell.createSession('{!TargetNodeName}');
```
또는 
``` ts 
const session = this.appContextService.powerShell.createAutomaticSession('{!TargetNodeName}');
```
대부분의 경우에 키 입력된 세션 만들기는 ```ngOnInit()``` 메서드와의 다음 dispose ```ngOnDestroy()```. 여러 PowerShell 스크립트는 구성 요소 구성 요소 간에 공유 되지 않고는 기본 세션의 경우이 패턴을 따릅니다.
최상의 결과 서비스 보다는 구성 요소 내에서 관리 되는 세션 만들기-해당 수명 보장이 있는지 확인 한 정리를 제대로 관리할 수 있습니다.

최상의 결과 서비스 보다는 구성 요소 내에서 관리 되는 세션 만들기-해당 수명 보장이 있는지 확인 한 정리를 제대로 관리할 수 있습니다.

### PowerShell 스트림 ###
장기 실행 스크립트 및 데이터가 있는 경우는 출력 점진적으로 하면 PowerShell 스트림을 스크립트를 완료 될 때까지 기다릴 필요 없이 데이터를 처리할 수 있습니다. 데이터를 수신할 때 관찰 가능한 next () 호출 됩니다.
```ts
this.appContextService.powerShellStream.run(session, script);
```

### 장기 실행 스크립트 ###
장기 실행 스크립트를 백그라운드에서 실행 하려는 경우에 작업 항목을 제출할 수 있습니다. 게이트웨이 스크립트의 상태 추적 및 상태에 대 한 업데이트 알림을 보낼 수 있습니다. 
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
> 표시할 진행 중에 대 한 쓰기 진행 중인 작성 하는 스크립트에 포함 되어야 합니다. 예를 들면 다음과 같습니다.
> ``` ps1
>  Write-Progress -Activity ‘The script is almost done!’ -percentComplete 95
>```

#### 작업 항목 옵션 ####

| function | 설명 |
| ----- | ----------- |
| submit() | 작업 항목 제출 
| submitAndWait() | 작업 항목을 제출 하 고 실행의 완료 될 때까지
| wait() | 기존 작업에 대 한 대기 완료 하는 항목
| query() | Id로 기존 작업 항목에 대 한 쿼리
| find) | 검색 및 TargetNodeName, ModuleName, 또는 typeId 작업 항목을 기존.

### PowerShell 일괄 처리 Api # # #
여러 노드에서 동일한 스크립트를 실행 해야 할 경우 일괄 처리 PowerShell 세션을 사용할 수 있습니다. 예를 들면 다음과 같습니다.
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


#### PowerShellBatch 옵션 ####
| 옵션 | 설명 |
| ----- | ----------- |
| runSingleCommand | 배열에 있는 모든 노드에 대해 하나의 명령 실행 
| 실행 | 해당 명령을 쌍을 이루는 노드에서 실행
| 취소 | 배열에 있는 모든 노드에서 명령을 취소합니다