---
title: Tokens.dat 파일 다시 빌드
description: Windows 정품 인증 문제를 해결할 때 Tokens.dat 파일을 다시 빌드하는 방법
ms.topic: troubleshooting
ms.date: 09/18/2019
ms.technology: server-general
author: Teresa-Motiv
ms.author: v-tea
manager: dcscontentpm
ms.localizationpriority: medium
ms.openlocfilehash: 8a5835cd601b2eb327c8605d70bf075e6c8e8414
ms.sourcegitcommit: 9855d6b59b1f8722f39ae74ad373ce1530da0ccf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71962999"
---
# <a name="rebuild-the-tokensdat-file"></a>Tokens.dat 파일 다시 빌드

Windows 정품 인증 문제를 해결할 때 Tokens.dat 파일을 다시 빌드해야 할 수 있습니다. 이 문서에서는 이 작업을 수행하는 방법에 대해 자세히 설명합니다.

## <a name="resolution"></a>해상도

Tokens.dat 파일을 다시 빌드하려면 다음 단계를 수행합니다.

1. 관리자 권한으로 명령 프롬프트 창을 엽니다.  
   **Windows 10의 경우**

   1. **시작** 메뉴를 열고 **cmd**를 입력합니다.
   1. 검색 결과에서 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.  

   **Windows 8.1의 경우**
   1. 화면 오른쪽 가장자리에서 안쪽으로 살짝 민 다음, **검색**을 누릅니다. 또는 마우스를 사용하는 경우 화면의 오른쪽 아래 모서리를 가리킨 다음, **검색**을 선택합니다.
   1. 검색 상자에 **cmd**를 입력합니다.
   1. 표시된 **명령 프롬프트** 아이콘을 살짝 밀거나 오른쪽 단추로 클릭합니다.
   1. **관리자 권한으로 실행**을 누르거나 클릭합니다.

   **Windows 7의 경우**
   1. **시작** 메뉴를 열고 **cmd**를 입력합니다.
   1. 검색 결과에서 **cmd.exe**를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.

1. 운영 체제에 적합한 명령 목록을 입력합니다.  

   Windows 10, Windows Server 2016 이상 버전의 경우 다음 명령을 순서대로 입력합니다.
   ```cmd
   net stop sppsvc
   cd %windir%\system32\spp\store\2.0
   ren tokens.dat tokens.bar
   net start sppsvc
   cscript.exe %windir%\system32\slmgr.vbs /rilc
   ```
   Windows 8.1, Windows Server 2012 및 Windows Server 2012 R2의 경우 다음 명령을 순서대로 입력합니다.
   ```cmd
   net stop sppsvc
   cd %windir%\ServiceProfiles\LocalService\AppData\Local\Microsoft\WSLicense
   ren tokens.dat tokens.bar
   net start sppsvc
   cscript.exe %windir%\system32\slmgr.vbs /rilc
   ```
   Windows 7, Windows Server 2008 및 Windows Server 2008 R2의 경우 다음 명령을 순서대로 입력합니다.
   ```cmd
   net stop sppsvc
   cd %windir%\ServiceProfiles\NetworkService\AppData\Roaming\Microsoft\SoftwareProtectionPlatform
   ren tokens.dat tokens.bar
   net start sppsvc
   cscript.exe %windir%\system32\slmgr.vbs /rilc
   ```
1. 컴퓨터를 다시 시작합니다.

## <a name="more-information"></a>추가 정보

Tokens.dat 파일을 다시 빌드한 후에는 다음 방법 중 하나를 사용하여 제품 키를 다시 설치해야 합니다.

- 동일한 관리자 권한 프롬프트 명령에서 다음 명령을 입력한 다음, Enter를 누릅니다.

   ```cmd
   cscript.exe %windir%\system32\slmgr.vbs /ipk <Product key>
   ```

  > [!IMPORTANT]
  > **/upk** 스위치를 사용하여 제품 키를 제거하지 마세요. 기존 제품 키에 제품 키를 설치하려면 **/ipk** 스위치를 사용합니다.
- **내 컴퓨터**를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택한 다음, **제품 키 변경**을 선택합니다.

KMS 클라이언트 설정 키에 대한 자세한 내용은 [KMS 클라이언트 설정 키](kmsclientkeys.md)를 참조하세요.
