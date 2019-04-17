---
title: "설치 하는 동안 Add-Ins 설치 자동화"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e6ff6e4-8d68-4d49-9e38-8088bc8bf95e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d4c547c2fec8e2b11e5c1d9bde46e55e91c9d6fa
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="automate-installation-of-add-ins-during-setup"></a>설치 하는 동안 Add-Ins 설치 자동화

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

##  <a name="BKMK_AddIns"></a>설치 하는 동안 설치 추가 기능을 자동화  
 추가 기능을 설치 하는 동안 설치에 설명 된 PostIC.cmd 메서드를 사용는 [실행 게시물 초기 구성 작업에 대 한 PostIC.cmd 파일을 만들고](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md) 이 문서의 합니다.  
  
 다음 항목을 추가 하 여 PostIC.cmd 다음과 같습니다.  
  
```  
C:\Program Files\Windows Server\bin\Installaddin.exe <full path to wssx file> -q  
```  
  
 추가 기능을 이제 사전 설치 하 고 사용자 지정 된 제거 단계를 지원합니다.  
  
 사전 설치 단계를 모두 설치 하기 전에 실행할 **.msi** addin.xml에 지정 된 파일. 대화형 모드에서 실행 하는 경우의 진행률 대화 상자가 표시 하지만 진행 상황을 변경 하지 않고 됩니다. 취소 단추가 사전 설치 단계 사용할 수 없습니다. 사전 설치 단계를 구현 하려면 다음과 같은 내용을 (패키지)에서 직접 addin.xml에 추가 합니다.  
  
> [!NOTE]
>  Xml 스키마 정확 하 게 아래 하나를 수행 해야 합니다.  
  
```  
<Package xmlns="https://schemas.microsoft.com/WindowsServerSolutions/2010/03/Addins" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">  
  <Id>...</Id>  
  <Version>...</Version>  
  <Name>...</Name>  
  <Allow32BitOn64BitClients>...</Allow32BitOn64BitClients>  
  <ServerBinary>...</ServerBinary>  
  <ClientBinary32>...</ClientBinary32>  
  <ClientBinary64>...</ClientBinary64>  
  <SupportedSkus>...</SupportUrl>    
  <SupportUrl>...</SupportUrl>  
  <Location>...</Location>    
  <PrivacyStatement>...</PrivacyStatement>  
  <OtherBinaries>...</OtherBinaries>   
  <Preinstall>  
<Executable>exefile</Executable>  
<NormalArgs>args-for-interactive-mode</NormalArgs>  
<SilentArgs>args-for-silent-mode</SilentArgs>  
<IgnoreExitCode>true</IgnoreExitCode>  
  </Preinstall>  
  <UninstallConfirm>...</UninstallConfirm>      
</Package>  
<¦>  
<¦>  
```  
  
 Wherein **exefile** 사전 설치 단계를 수행 하는 추가 기능을 패키지에서 실행 파일 이며 지정 해야 합니다. **NormalArgs** 대화형 때 명령줄 모드로 exefile 전달 인수가 사용 되는 지정 합니다. 이 모드에서는 exefile는 사용자의 상호 작용에 대 한 일부 대화 상자를 팝업 수 있습니다. **SilentArgs** 때 소리가 명령줄 모드로 exefile 전달 인수를 사용 하도록 지정 (-q 지정 installaddin.exe 호출할 때). 이 모드에서는 모든 windows는 exefile 하지 팝업 전 해야합니다. 하는 경우 **IgnoreExitCode** 사전 설치 단계는 항상 성공 것으로 간주 됩니다, 그렇지 않은 경우 0 종료 코드가 성공을 의미, 1 취소, 의미 및 다른 값 오류를 나타냅니다 참로 지정 합니다. 태그 **NormalArgs**, **SilentArgs**, 및 **IgnoreExitCode** 는 모두 선택 사항입니다.  
  
 다음 중 하나에 대 한 사용자 지정 된 제거 단계를 사용할 수 있습니다.  
  
-   기본 제공 확인 대화 상자를 대체 합니다.  
  
-   제거 하기 전에 사용자 지정 된 대화 상자를 채웁니다.  
  
-   제거 하기 전에 특정 작업을 수행 합니다.  
  
 제거 하는 단계를 구현 하려면 다음과 같은 내용을 (패키지)에서 직접 addin.xml에 추가 합니다.  
  
```  
<Package xmlns="https://schemas.microsoft.com/WindowsServerSolutions/2010/03/Addins" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">  
  <Id>...</Id>  
  <Version>...</Version>  
  <Name>...</Name>  
  <Allow32BitOn64BitClients>...</Allow32BitOn64BitClients>  
  <ServerBinary>...</ServerBinary>  
  <ClientBinary32>...</ClientBinary32>  
  <ClientBinary64>...</ClientBinary64>  
  <SupportedSkus>...</SupportUrl>    
  <SupportUrl>...</SupportUrl>  
  <Location>...</Location>    
  <PrivacyStatement>...</PrivacyStatement>  
  <OtherBinaries>...</OtherBinaries>   
  <Preinstall>¦</Preinstall>  
<UninstallConfirm>  
<Executable>full-path-to-exefile</Executable>  
<Arguments>command-line-arguments</Arguments>  
</UninstallConfirm>  
</Package>  
```  
  
 Wherein **exefile에 전체 경로** 시스템에 이미 설치 되어 exefile 지정 합니다. **인수** 선택 가능 하며, 명령줄 인수는 exefile 지정 합니다. 기본 제공 확인 제거 하기 전에 exefile 호출 되는 대화 상자를 표시 합니다.  
  
 다음이 단계에서 작업의 exefile 수행할 수 있습니다.  
  
-   사용자의 상호 작용에 대 한 일부 대화 상자를 표시 합니다.  
  
-   일부 백그라운드 작업을 수행 합니다.  
  
 이 exe 파일의 종료 코드 제거 프로세스 앞으로 이동 하는 방법을 결정 합니다.  
  
-   0: 사용자가 이미 확인 하는 것 처럼 기본 확인 대화 채우지 않고 제거 프로세스는 계속 됩니다. (이 방법을 사용할 수 기본 확인 대화 상자를 교체 하).  
  
-   1: 제거 프로세스를 취소 하 고 사용자에 게 취소 한 메시지 마지막으로 표시 됩니다. 모든 유지 변경 되지 않습니다.  
  
-   기타: 제거 프로세스가 계속 기본 확인 대화 상자를 사용자 지정 된 제거 단계 없으면 처럼 됩니다.  
  
 exefile 반환 0 이나 1 코드는 exefile 호출 하거나, 오류 같은 동작 이어질 수 있습니다.  
  
## <a name="see-also"></a>참조 하십시오  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)