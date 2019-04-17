---
title: 가상 디렉터리에는 선택 된 인증서 CRL 복사
description: 이 항목은 802.1 X 유선 및 무선 배포에 대 한 배포 서버 인증서 가이드
manager: brianlic
ms.topic: article
ms.assetid: a1b5fa23-9cb1-4c32-916f-2d75f48b42c7
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e37bfce7f8cf33fd7fcb5e6227d783c28bd29d35
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="copy-the-ca-certificate-and-crl-to-the-virtual-directory"></a>가상 디렉터리에는 선택 된 인증서 CRL 복사

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 절차 가상 디렉터리 웹 서버의 인증서 해지 목록 및 엔터프라이즈 루트 캘리포니아 인증서 인증 기관에서 복사 하 고 AD CS 올바르게 구성 되어 있는지 확인를 사용할 수 있습니다. 아래 명령을 실행 하기 전에 디렉터리와 서버 이름 배포에 대 한 적절 한 되는 것으로 대체 하는 있는지 확인 합니다.  
  
이 절차를 수행 하려면의 회원 있어야 **도메인 관리자**합니다.  
  
#### <a name="to-copy-the-certificate-revocation-list-from-ca1-to-web1"></a>CA1 WEB1 인증서 해지 목록을 복사합니다  
  
1.  CA1에서 Windows PowerShell을 관리자 권한으로 실행 하 고 CRL 다음 명령 사용 하 여 게시 합니다.  
  
    - 입력 `certutil -crl`, ENTER 키를 누릅니다.  
  
    - 캘리포니아 인증서 웹 서버에서 파일 공유를 복사 하려면 입력 `copy C:\Windows\system32\certsrv\certenroll\*.crt \\WEB1\pki`, ENTER 키를 누릅니다.  
    - 인증서 해지 목록 웹 서버에서 파일 공유를 복사 하려면 입력 `copy C:\Windows\system32\certsrv\certenroll\*.crl \\WEB1\pki`, ENTER 키를 누릅니다.  
  
2. AD CS 다시 시작 하려면 다음을 입력 `Restart-Service certsvc`, ENTER 키를 누릅니다.  
  
2.  입력을 CDP 및 AIA 확장 위치 제대로 구성 되어 있는지 확인 하려면 `pkiview.msc`, ENTER 키를 누릅니다. Pkiview 엔터프라이즈 PKI MMC을 엽니다.  
  
3.  캘리포니아 이름을 클릭 합니다. 예를 들어, 캐나다 이름이 corp-CA1-캐나다 이면 클릭 **corp-CA1-캐나다**합니다. 세부 정보 창에서 다음을 확인는 **상태** 가치에 대 한는 **인증서**, **AIA 위치 #1**, 및 **CDP 위치 #1** 는 모두 **확인**합니다.  
  
다음 그림에서는 상태 확인 모든 항목에 대 한와 함께 pkiview 결과 창을 보여 줍니다.  
  
! [adcs_pkiviewmedia/adcs_pkiview.png)  
  
> [!IMPORTANT]  
> 하는 경우 **상태** 항목은 되지 **확인**, 다음을 수행 합니다.  
> -   열기 공유 인증서, 해지 파일 목록을 확인 하려면 웹 서버에 복사 되었습니다을 공유 합니다. 성공적으로 공유를 복사 하지 된 경우 올바른 파일 원본과 데이터의 복사본 명령을 수정 하 고 목적지를 공유 하 고 다시 명령을 실행 합니다.  
> -   캘리포니아 확장 탭 공백 없음 또는 기타 문자 제공 되는 위치에 있는지 확인 CDP 및 AIA에 대 한 정확한 위치를 입력 했는지 확인 합니다.  
> -   웹 서버의 하 여 정확한 위치 CRL과 캘리포니아 인증서를 복사 하 고 위치에는 캘리포니아 CDP 및 AIA 위치에 대 한 제공한 위치와 일치 하는지 확인 합니다.  
> -   가상 폴더 선택 된 인증서 및 CRL 저장 된 위치에 대 한 권한 올바르게 구성 되었는지 확인 합니다.  
  


