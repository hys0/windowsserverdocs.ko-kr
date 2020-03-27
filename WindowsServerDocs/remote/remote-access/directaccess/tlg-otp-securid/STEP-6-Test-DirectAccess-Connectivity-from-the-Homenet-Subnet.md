---
title: 6 단계 Ho, 서브넷에서 DirectAccess 연결 테스트
description: 이 항목은 테스트 랩 가이드-OTP 인증을 사용 하는 DirectAccess 시연 및 Windows Server 2016에 대 한 RSA SecurID의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9b77cfd-8dd4-476b-a118-f3d6bf59e7b1
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c9bc2b54927905346c980ef2b14d65310ca930b8
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80308582"
---
# <a name="step-6-test-directaccess-connectivity-from-the-homenet-subnet"></a>6 단계 Ho, 서브넷에서 DirectAccess 연결 테스트

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이제 DirectAccess OTP (일회성 암호) 배포가 완료 되었으며 Ho의 연결 테스트를 시작할 수 있습니다.  
  
### <a name="to-test-otp-functionality-from-the-homenet-subnet-on-client1"></a>C l i e n t 1의 Ho Et 서브넷에서 OTP 기능을 테스트 하려면  
  
1. C l i e n t 1에서 **User1**으로 로그온 했는지 확인 합니다.  
  
2. **시작** 화면에서**powershell**을 입력 하 고 **powershell**을 마우스 오른쪽 단추로 클릭 한 다음 **고급**을 클릭 하 고 **관리자 권한으로 실행**을 클릭 합니다. **사용자 계정 컨트롤** 대화 상자가 표시되면 원하는 작업이 표시되어 있는지 확인하고 **예**를 클릭합니다.  
  
3. Windows PowerShell 창에서 **gpupdate/force**를 입력 하 고 enter 키를 누릅니다.  
  
4. Corpnet 서브넷에서 CLIENT1을 분리 하 고이를 Ho Et 서브넷에 연결 합니다.  
  
5. C l i e n t 1에서 Internet Explorer를 열고 주소 표시줄에 **https://app1.corp.contoso.com/** 를 입력 한 다음 enter 키를 누릅니다. F5 키를 누릅니다.  
  
   사이트가 열리지 않습니다.  
  
6. **시작** 화면에서**rsa**를 입력 하 고 **rsa SecurID 토큰**을 클릭 합니다.  
  
7. RSA SecurID 토큰이 일회성 암호를 변경할 때까지 기다렸다가 **복사**를 클릭 합니다.  
  
8. 알림 영역에서 **네트워크 연결** 아이콘을 클릭하여 DA 미디어 관리자에 액세스합니다.  
  
9. **Contoso DirectAccess 연결**을 클릭 하 고 **계속**을 클릭 합니다.  
  
10. Ctrl + Alt + Delete를 누르고 **OTP (일회용 암호)** 타일을 클릭 합니다.  
  
11. 이전에 복사한 8 자리 토큰을 붙여넣은 다음 **확인**을 클릭 합니다. 인증이 완료 될 때까지 기다립니다. 이제 DirectAccess 작업 공간 연결 상태가 **연결**됨으로 나타납니다.  
  
12. Internet Explorer의 주소 표시줄에 **https://app1.corp.contoso.com/** 를 입력 하 고 enter 키를 누릅니다. F5 키를 누릅니다. APP1의 기본 IIS 웹 사이트가 표시됩니다.  
  
13. Internet Explorer 주소 표시줄에 **https://app2.corp.contoso.com/** 를 입력 하 고 enter 키를 누릅니다. F5 키를 누릅니다. APP2의 기본 IIS 웹 사이트가 표시 됩니다.  
  
14. **시작** 화면에서<strong>\\\app1\files</strong>를 입력 하 고 enter 키를 누릅니다.  
  
15. **파일** 공유 폴더 창에서 **Example .txt** 파일을 두 번 클릭 합니다. 예 .txt 파일의 내용이 표시 됩니다.  
  
16. **시작** 화면에서<strong>\\\app2\files</strong>를 입력 하 고 enter 키를 누릅니다.  
  
17. **파일** 공유 폴더 창에서 **새 텍스트 문서 .txt** 파일을 두 번 클릭 합니다. 새 텍스트 문서 .txt 파일의 내용이 표시 됩니다.  
  


