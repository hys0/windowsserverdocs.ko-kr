---
title: 확장에 PowerShell 사용하기
description: PowerShell을 사용 하 여 Windows Admin Center SDK (프로젝트 브라 티) 확장의
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ae5004104150c510a56c06161c9280e029968298
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867604"
---
# <a name="using-powershell-in-your-extension"></a>확장에 PowerShell 사용하기 #

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center 확장 SDK를 자세한 보겠습니다-PowerShell 명령 확장을 추가 하는 방법을 알아보겠습니다.

## <a name="powershell-in-typescript"></a>TypeScript에 대 한 PowerShell ##

Gulp 빌드 프로세스에 연결 되는 모든 ". ps1" "/ src/리소스/scripts" 폴더에 배치 되 고 "/ src/개의 생성 된" 폴더 아래에 있는 "powershell 스크립트" 클래스에는 생성 단계가 포함 되어 있습니다.

>[!NOTE] 
> "Powershell scripts.ts" 또는 "strings.ts" 파일 업데이트 수동으로 하지 마십시오. 다음 생성에서 변경은 수행 하면 덮어쓰게 됩니다.

### <a name="adding-your-own-powershell-script"></a>사용자 지정 PowerShell 스크립트를 추가합니다. ##

곧 사용자 지정 PowerShell 스크립트를 추가 하는 방법에 대 한 자세한 내용은 추가 하겠습니다.

### <a name="managing-powershell-sessions"></a>PowerShell 세션 관리 ###

Windows Admin Center PowerShell을 사용 하는 경우 세션은 스크립트 실행 프로세스의 필수 구성 요소입니다. 관리 되는 원격 서버에서 스크립트를 실행 하려면 PowerShell runspace를 사용 합니다. Windows Admin Center 수명 관리 및 순차적 스크립트 실행에 대 한 runspace 다시 사용할 수 있도록 PowerShellSession 개체에 있는 runspace 만들기 및 관리를 래핑합니다.

모든 구성 요소는 세 가지 다른 옵션을 사용 하 여 AppContextService 클래스로 만든 세션 개체에 대 한 참조 해야 합니다.
<!-- I don't 100% get this part - it looks like you're adding 3 arguments - nodeName, <session key>, and <PowerShellSessionRequestOptions>. I got that from looking at the examples, not the text. We need to rework those paras explaining. -->
``` ts
this.psSession = this.appContextService.powerShell.createSession(this.appContextService.activeConnection.nodeName);
```

노드 이름을 createSession 메서드를 제공 하 여 새 PowerShell 세션을 생성, 사용 되어 PowerShell 호출 완료 시 즉시 제거 합니다. 이 기능은 일회성 호출에 적합 하지만 반복 해 서 사용 성능에 영향을 줄 수 있습니다. 세션은 만들려면 약 1 초, 따라서 지속적으로 세션을 재생 속도 저하를 발생할 수 있습니다.

``` ts
this.psSession = this.appContextService.powerShell.createSession(this.appContextService.activeConnection.nodeName, '<session key>');
```

첫 번째 선택적 매개 변수를 \<세션 키\> 매개 변수입니다. 이 조회 하 고 구성 요소 (즉 Component1 "SME ROCKS" 키를 사용 하 여 세션을 만들 수 고 Component2 동일한 세션에 사용할 수 있습니다) 에서도 재사용할 수 있는 키가 지정 된 세션을 만듭니다.  

``` ts
this.psSession = this.appContextService.powerShell.createSession(this.appContextService.activeConnection.nodeName, '<session key>', <PowerShellSessionRequestOptions>);
```
<!-- The second optional parameter is \<PowerShellSessionRequestOptions\> that does ... ? -->
### <a name="common-patterns"></a>일반적인 패턴 ###

키가 지정 된 세션을 만들 대부분의 경우는 **ngOnInit** 메서드와의 다음 dispose는 **ngOnDestroy**합니다. 구성 요소 구성 요소 간에 공유 되지 기본 세션에 여러 PowerShell 스크립트가 있는 경우이 패턴을 따릅니다.

최상의 결과 서비스 보다는 구성 내에서 관리 되는 세션을 만든-해당 수명 동안 보장이 있는지 확인 하 고 정리를 제대로 관리할 수 있습니다.