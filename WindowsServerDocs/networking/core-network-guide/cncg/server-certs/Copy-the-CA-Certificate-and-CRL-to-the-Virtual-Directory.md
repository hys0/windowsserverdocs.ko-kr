---
title: 가상 디렉터리에 CA 인증서 및 CRL 복사
description: 이 항목은 서버 배포 인증서 802.1 X 유선 및 무선 배포 가이드의 일부
manager: dougkim
ms.topic: article
ms.assetid: a1b5fa23-9cb1-4c32-916f-2d75f48b42c7
ms.prod: windows-server
ms.technology: networking
ms.author: lizross
author: eross-msft
ms.date: 07/19/2018
ms.openlocfilehash: 275bec5c950ea20c3a7d5a933648cf7e068164d1
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318351"
---
# <a name="copy-the-ca-certificate-and-crl-to-the-virtual-directory"></a>가상 디렉터리에 CA 인증서 및 CRL 복사

>적용 대상: Windows Server(반기 채널), Windows Server 2016

웹 서버의 가상 디렉터리에 인증 기관에서 인증서 해지 목록 및 엔터프라이즈 루트 CA 인증서를 복사 하 고 AD CS 올바르게 구성 되었는지 확인 하려면이 절차를 사용할 수 있습니다. 아래 명령을 실행 하기 전에 관련 된 배포에 적절 한 디렉터리 및 서버 이름을 바꾸는 확인 합니다.  
  
이 절차를 수행 하려면의 구성원 이어야 **Domain Admins**합니다.  
  
#### <a name="to-copy-the-certificate-revocation-list-from-ca1-to-web1"></a>W e b 1을 c a 1에서 인증서 해지 목록을 복사 하려면  
  
1.  C a 1에서 관리자는 Windows PowerShell을 실행 하 고 다음 명령 사용 하 여 CRL을 게시 합니다.  
  
    - `certutil -crl`를 입력하고 Enter 키를 누릅니다.  

    - C A 1 인증서를 웹 서버의 파일 공유에 복사 하려면 `copy C:\Windows\system32\certsrv\certenroll\*.crt \\WEB1\pki`를 입력 한 다음 ENTER 키를 누릅니다.  
    
    - 인증서 해지 목록 웹 서버에서 파일 공유로 복사 하려면 다음을 입력 `copy C:\Windows\system32\certsrv\certenroll\*.crl \\WEB1\pki`, 한 다음 ENTER를 누릅니다.  
  
2.  CDP 및 AIA 확장 위치 제대로 구성 되어 있는지를 확인 하려면 다음을 입력 `pkiview.msc`, 한 다음 ENTER를 누릅니다. pkiview 엔터프라이즈 PKI MMC가 열립니다.  
  
3.  왼쪽 창에서 CA 이름을 클릭 합니다.<p>예를 들어 CA 이름은 corp-c a 1-CA 인 경우 클릭 하 여 **corp-c a 1-CA**합니다. 

4. 결과 창의 상태 열에서 다음 값에 **OK**가 표시 되는지 확인 합니다.

    - **CA 인증서**
    - **AIA 위치 #1**
    - **CDP 위치 #1**   
  
  
> [!TIP]  
> 경우 **상태** 없는 모든 항목에 대 한 **확인**, 다음을 수행 합니다.  
> -   인증서 및 인증서 해지 목록 파일 공유에 복사 성공적으로 되었는지 확인 하 여 웹 서버의 공유를 엽니다. 성공적으로 공유에 복사 되지 된 경우 올바른 파일 원본과 복사 명령을 수정 및 대상 공유 하 고 명령을 다시 실행 합니다.  
> -   CA 확장 탭에서 CDP 및 AIA에 대 한 올바른 위치를 입력 했는지 확인 합니다. 입력 한 위치에 추가 공백이 나 다른 문자가 없는지 확인 하세요.  
> -   웹 서버의 올바른 위치에 CRL 및 CA 인증서를 복사 하 고 위치는 CA의 CDP 및 AIA 위치에 대해 제공 하는 위치와 일치 하는지 확인 합니다.  
> -   CA 인증서 및 CRL 저장 된 가상 폴더에 대 한 사용 권한을 올바르게 구성 했는지 확인 합니다.  
  


