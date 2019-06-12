---
title: Homenet 서브넷에서 단계 6 테스트 DirectAccess 연결
description: 이 항목은 일부 테스트 랩 가이드-OTP 인증 및 Windows Server 2016 RSA SecurID를 사용한 DirectAccess 시연
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9b77cfd-8dd4-476b-a118-f3d6bf59e7b1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fe3014b8b37fab35532f3ecf833188fda9e8b744
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446644"
---
# <a name="step-6-test-directaccess-connectivity-from-the-homenet-subnet"></a>Homenet 서브넷에서 단계 6 테스트 DirectAccess 연결

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이제 DirectAccess OTP (일회용 암호) 배포가 완료 되었으므로 및 Homenet 서브넷에서 연결을 테스트 하기 시작할 수 있습니다.  
  
### <a name="to-test-otp-functionality-from-the-homenet-subnet-on-client1"></a>CLIENT1에서 Homenet 서브넷에서 OTP 기능을 테스트 하려면  
  
1. CLIENT1에서로 로그온 되어 있는지 확인 **User1**합니다.  
  
2. 에 **시작** 화면에서 입력**powershell.exe**를 마우스 오른쪽 단추로 클릭 **powershell**, 클릭 **고급**를 클릭 하 고 **실행 관리자 권한으로**입니다. **사용자 계정 컨트롤** 대화 상자가 나타나면 원하는 작업이 표시되었는지 확인한 다음 **예**를 클릭합니다.  
  
3. Windows PowerShell 창에서 입력 **gpupdate /force**, ENTER 키를 누릅니다.  
  
4. Corpnet 서브넷의 CLIENT1을 뽑은 Homenet 서브넷에 연결 합니다.  
  
5. CLIENT1에서 Internet Explorer를 열고 주소 표시줄에 입력 **https://app1.corp.contoso.com/** ENTER 키를 누릅니다. F5 키를 누릅니다.  
  
   사이트 열리지 않아야 합니다.  
  
6. 에 **시작** 화면에서 입력**RSA**를 클릭 하 고 **RSA SecurID 토큰**합니다.  
  
7. RSA SecurID 토큰 일회용 암호를 변경 될 때까지 기다린 다음 클릭 **복사**합니다.  
  
8. 알림 영역에서 **네트워크 연결** 아이콘을 클릭하여 DA 미디어 관리자에 액세스합니다.  
  
9. 클릭 **Contoso DirectAccess 연결**, 클릭 **계속**합니다.  
  
10. 컨트롤 + Alt + Delete를 누르고 클릭 합니다 **OTP (일회용 암호)** 바둑판식으로 배열 합니다.  
  
11. 이전에 복사한 8 자리 토큰 코드를 붙여넣고 클릭 **확인**합니다. 인증 완료 될 때까지 기다립니다. DirectAccess 작업 공간 연결 상태를 이제 됩니다 **Connected**합니다.  
  
12. Internet Explorer 주소 표시줄에 입력 **https://app1.corp.contoso.com/** ENTER 키를 누릅니다. F5 키를 누릅니다. APP1의 기본 IIS 웹 사이트가 표시됩니다.  
  
13. Internet Explorer 주소 표시줄에 입력 **https://app2.corp.contoso.com/** ENTER 키를 누릅니다. F5 키를 누릅니다. APP2의 기본 IIS 웹 사이트가 표시 됩니다.  
  
14. 에 **시작** 화면에서 입력<strong>\\\app1\files</strong>, ENTER 키를 누릅니다.  
  
15. 에 **파일** 공유 폴더 창을 두 번 클릭 합니다 **Example.txt** 파일. Example.txt 파일의 내용을 표시 됩니다.  
  
16. 에 **시작** 화면에서 입력<strong>\\\app2\files</strong>, ENTER 키를 누릅니다.  
  
17. 에 **파일** 공유 폴더 창을 두 번 클릭 합니다 **새 텍스트 Document.txt** 파일. 새 텍스트 Document.txt 파일의 내용을 표시 됩니다.  
  


