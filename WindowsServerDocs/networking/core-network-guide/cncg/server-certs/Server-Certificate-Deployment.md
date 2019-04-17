---
title: 서버 인증서 배포
description: 이 항목은 802.1 X 유선 및 무선 배포에 대 한 배포 서버 인증서 가이드
manager: brianlic
ms.topic: article
ms.assetid: 1ae4384b-f4e4-41e8-bc5f-9ac41953bca4
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4a10a9bafa6a8c9fddecac799ec8e837bf339d0e
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="server-certificate-deployment"></a>서버 인증서 배포

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

엔터프라이즈 루트 인증 기관 (캐나다)를 설치 하 고 서버 인증서 PEAP EAP와 사용에 대 한 배포 다음이 단계를 수행 합니다.  
  
> [!IMPORTANT]  
> Active Directory 인증서 서비스를 설치 하기 전에 컴퓨터 이름 지정 해야, 고정 IP 주소를 사용 하는 컴퓨터 구성 및 컴퓨터에서 도메인에 가입입니다. 그러나 AD CS를 설치한 후 필요한 경우에 IP 주소를 변경할 수는 컴퓨터의 컴퓨터 이름을 또는 도메인 변경할 수 없습니다. 이러한 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 Windows Server&reg; 2016 [Core 네트워크 가이드](../../Core-Network-Guide.md)합니다.  

  
-   [웹 서버 WEB1 설치](../../../core-network-guide/cncg/server-certs/Install-the-Web-Server-WEB1.md)  
  
-   [Dns에서 (CNAME) 별칭 기록 WEB1 만들려면](../../../core-network-guide/cncg/server-certs/Create-an-Alias-CNAME-Record-in-DNS-for-WEB1.md)  
  
-   [인증서 Crl (해지 목록)을 배포 하는 WEB1 구성](../../../core-network-guide/cncg/server-certs/Configure-WEB1-to-Distribute-Certificate-Revocation-Lists.md)  
  
-   [CAPolicy inf 파일을 준비](../../../core-network-guide/cncg/server-certs/Prepare-the-CAPolicy-inf-File.md)  
  
-   [인증 기관 설치](../../../core-network-guide/cncg/server-certs/Install-the-Certification-Authority.md)  
  
-   [확장 CDP 및 AIA CA1에서 구성](../../../core-network-guide/cncg/server-certs/Configure-the-CDP-and-AIA-Extensions-on-CA1.md)  
  
-   [가상 디렉터리에는 선택 된 인증서 CRL 복사](../../../core-network-guide/cncg/server-certs/Copy-the-CA-Certificate-and-CRL-to-the-Virtual-Directory.md)  
  
-   [서버 인증서 템플릿을 구성합니다](../../../core-network-guide/cncg/server-certs/Configure-the-Server-Certificate-Template.md)  
  
-   [자동 서버 인증서 등록이 구성](../../../core-network-guide/cncg/server-certs/Configure-Server-Certificate-Autoenrollment.md)  
  
-   [새로 고침 그룹 정책](../../../core-network-guide/cncg/server-certs/Refresh-Group-Policy.md)  
  
-   [서버 인증서 등록이 서버를 확인 합니다.](../../../core-network-guide/cncg/server-certs/Verify-Server-Enrollment-of-a-Server-Certificate.md)  
  
> [!NOTE]  
> 이 가이드는 절차 있는 경우에 대 한 지침 포함 되지 않는다는 **사용자 계정 컨트롤** 대화 상자에서 열리는 계속에서 사용 권한을 요청 합니다. 이 가이드에서는 절차를 수행 하는 및 프로그램 작업에 대 한 응답에서 대화 상자를 연 경우 클릭 동안이 대화 상자에서 열리는 경우 **계속**합니다.  
  


