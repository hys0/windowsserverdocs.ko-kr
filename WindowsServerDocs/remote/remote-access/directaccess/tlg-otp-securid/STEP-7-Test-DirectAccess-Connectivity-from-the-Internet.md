---
title: 7 단계 인터넷에서 DirectAccess 연결 테스트
description: 이 항목은 테스트 랩 가이드-OTP 인증을 사용 하는 DirectAccess 시연 및 Windows Server 2016에 대 한 RSA SecurID의 일부입니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: ed2a1616-30c6-482a-9a02-4a5023621f58
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 9aa43301614f75112ce83d51486e6076e6d55391
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814446"
---
# <a name="step-7-test-directaccess-connectivity-from-the-internet"></a>7 단계 인터넷에서 DirectAccess 연결 테스트

>적용 대상: Windows Server(반기 채널), Windows Server 2016

DirectAccess OTP (일회성 암호) 배포가 Ho기능에서 테스트 되었으며 이제 인터넷에서 테스트할 수 있습니다.  
  
### <a name="to-test-otp-functionality-from-the-internet-on-client1"></a>CLIENT1에서 인터넷을 통해 OTP 기능을 테스트 하려면  
  
1. C l i e n t 1에서 **User1**으로 로그온 했는지 확인 합니다. CLIENT1을 Corpnet 서브넷에 연결 합니다.  
  
2. **시작** 화면에서**powershell**을 입력 하 고 **powershell**을 마우스 오른쪽 단추로 클릭 한 다음 **고급**을 클릭 하 고 **관리자 권한으로 실행**을 클릭 합니다. **사용자 계정 컨트롤** 대화 상자가 표시되면 원하는 작업이 표시되어 있는지 확인하고 **예**를 클릭합니다.  
  
3. Windows PowerShell 창에서 **gpupdate/force** 를 입력 하 고 enter 키를 누릅니다.  
  
4. Ho Et 서브넷에서 CLIENT1을 분리 하 고, 인터넷에 연결 하 고, 컴퓨터를 다시 시작 합니다.  
  
5. C l i e n t 1에서 Internet Explorer를 열고 주소 표시줄에 **https://app1.corp.contoso.com/** 를 입력 한 다음 enter 키를 누릅니다. F5 키를 누릅니다.  
  
   사이트가 열리지 않습니다.  
  
6. **시작** 화면에서**rsa**를 입력 하 고 **rsa SecurID 토큰**을 클릭 합니다.  
  
7. RSA SecurID 토큰이 일회성 암호를 변경할 때까지 기다렸다가 **복사**를 클릭 합니다.  
  
8. 알림 영역에서 **네트워크 연결** 아이콘을 클릭하여 DA 미디어 관리자에 액세스합니다.  
  
9. **작업 공간 연결**을 클릭 하 고 **계속**을 클릭 합니다.  
  
10. Ctrl + Alt + Delete를 누르고 **OTP (일회용 암호)** 타일을 클릭 합니다.  
  
11. 이전에 복사한 8 자리 토큰을 붙여넣은 다음 **확인**을 클릭 합니다. 인증이 완료 될 때까지 기다립니다. 이제 DirectAccess 작업 공간 연결 상태가 **연결**됨으로 나타납니다.  
  
12. Internet Explorer의 주소 표시줄에 **https://app1.corp.contoso.com/** 를 입력 하 고 enter 키를 누릅니다. F5 키를 누릅니다. APP1의 기본 IIS 웹 사이트가 표시됩니다.  
  
13. Internet Explorer 주소 표시줄에 **https://app2.corp.contoso.com/** 를 입력 하 고 enter 키를 누릅니다. F5 키를 누릅니다. APP2의 기본 IIS 웹 사이트가 표시 됩니다.  
  
14. **시작** 화면에서<strong>\\\app1\files</strong>를 입력 하 고 enter 키를 누릅니다.  
  
15. **파일** 공유 폴더 창에서 **Example .txt** 파일을 두 번 클릭 합니다. 예 .txt 파일의 내용이 표시 됩니다.  
  
16. **시작** 화면에서<strong>\\\app2\files</strong>를 입력 하 고 enter 키를 누릅니다.  
  
17. **파일** 공유 폴더 창에서 **새 텍스트 문서 .txt** 파일을 두 번 클릭 합니다. 새 텍스트 문서 .txt 파일의 내용이 표시 됩니다.  
  


