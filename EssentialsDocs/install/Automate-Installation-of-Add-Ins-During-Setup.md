---
title: 설치 중 추가 기능 설치 자동화
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884624"
---
# <a name="automate-installation-of-add-ins-during-setup"></a>설치 중 추가 기능 설치 자동화

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_AddIns"></a> 설치 중 추가 기능 설치 자동화  
 설치 중 추가 기능을 설치하려면 이 문서의 [Create the PostIC.cmd File for Running Post Initial Configuration Tasks](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md) 섹션에 설명되어 있는 PostIC.cmd 메서드를 사용합니다.  
  
 PostIC.cmd에 다음 항목을 추가합니다.  
  
```  
C:\Program Files\Windows Server\bin\Installaddin.exe <full path to wssx file> -q  
```  
  
 이 추가 기능은 설치 전 단계와 사용자 지정 제거 단계를 지원합니다.  
  
 설치 전 단계는 addin.xml에 지정된 모든 **.msi** 파일을 설치하기 전에 실행됩니다. 대화형 모드에서 실행되는 경우 진행률 대화 상자가 표시되지만 진행률이 변화하지 않습니다. 설치 전 단계에서는 취소 단추가 비활성화되어 있습니다. 설치 전 단계를 구현하려면 addin.xml에 다음 내용을 추가합니다(패키지 바로 아래).  
  
> [!NOTE]
>  xml 스키마는 아래 스키마를 그대로 따라야 합니다.  
  
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
  
 **exefile**은 설치 전 단계 수행을 위한 추가 기능 패키지의 실행 가능 파일이며 반드시 지정되어야 합니다. **NormalArgs**는 대화형 모드를 사용하는 경우 명령줄의 exefile로 전달될 인수를 지정합니다. 이 모드에서 exefile은 사용자 조작을 위한 팝업 창을 표시할 수 있습니다. **SilentArgs** 는 자동 모드를 사용하는 경우 명령줄의 exefile로 전달될 인수를 지정합니다(installaddin.exe 호출 시 -q 지정). 이 모드에서 exefile은 어떤 팝업 창도 표시하지 않을 것입니다. **IgnoreExitCode**를 참으로 지정한 경우 설치 전 단계는 항상 성공적인 것으로 간주되며 그렇지 않은 경우 종료 코드 0은 성공을, 1은 취소를, 그 외의 값은 실패를 나타냅니다. **NormalArgs**, **SilentArgs**및 **IgnoreExitCode** 태그는 모두 선택 사항입니다.  
  
 다음에 대해 사용자 지정된 제거 단계를 사용할 수 있습니다.  
  
-   기본 제공 확인 대화 상자를 교체합니다.  
  
-   제거 전에 사용자 지정된 대화 상자를 채웁니다.  
  
-   제거 전 특정 작업을 수행합니다.  
  
 제거 단계를 구현하려면 addin.xml에 다음 내용을 추가합니다(패키지 바로 아래).  
  
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
  
 여기서 **full-path-to-exefile**은 시스템에 이미 설치된 exefile을 지정합니다. **인수**는 선택 사항이며 exefile에 대한 명령줄 인수를 지정합니다. exefile은 내장된 제거 확인 대화 상자가 표시되기 전에 호출됩니다.  
  
 exefile은 이 단계에서 다음 작업을 수행할 수 있습니다.  
  
-   사용자 조작을 위한 대화 상자를 표시합니다.  
  
-   백그라운드 작업을 수행합니다.  
  
 이러한 exe 파일의 종료 코드는 제거 프로세스의 진행 방식을 결정합니다.  
  
-   0: 기본 제공 확인 대화 상자를 채우지 않고 사용자가 이미 확인한 대로 제거 프로세스를 계속합니다. (이 방식은 기본 제공 확인 대화 상자 대체에 사용할 수 있습니다);  
  
-   1: 제거 프로세스가 취소되고 취소된 메시지가 사용자에게 표시됩니다. 모든 항목이 변하지 않습니다.  
  
-   기타: 사용자 지정된 제거 단계가 없는 것처럼 기본 제공 확인 대화 상자로 제거 프로세스가 계속됩니다.  
  
 exefile 호출 실패는 exefile이 0이나 1이 아닌 코드를 반환함에 따라 같은 동작의 반복으로 이어집니다.  
  
## <a name="see-also"></a>관련 항목  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포용 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)