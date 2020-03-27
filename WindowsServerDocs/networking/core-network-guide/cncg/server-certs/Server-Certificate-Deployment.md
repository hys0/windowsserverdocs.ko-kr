---
title: 서버 인증서 배포
description: 이 항목은 서버 배포 인증서 802.1 X 유선 및 무선 배포 가이드의 일부
manager: brianlic
ms.topic: article
ms.assetid: 1ae4384b-f4e4-41e8-bc5f-9ac41953bca4
ms.prod: windows-server
ms.technology: networking
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 63ae9ef71b913feeeb28e9838f636b316ea2969f
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318207"
---
# <a name="server-certificate-deployment"></a>서버 인증서 배포

>적용 대상: Windows Server(반기 채널), Windows Server 2016

엔터프라이즈 루트 인증 기관 (CA)를 설치 하 고 PEAP 및 EAP에 사용할 서버 인증서를 배포 하려면 다음이 단계를 수행 합니다.  
  
> [!IMPORTANT]  
> Active Directory 인증서 서비스를 설치 하기 전에 컴퓨터의 이름, 정적 IP 주소를 가진 컴퓨터를 구성 하며 컴퓨터를 도메인에 가입 있습니다. AD CS를 설치한 후 필요한 경우에 IP 주소를 변경할 수 있지만 컴퓨터 이름 또는 도메인 구성원 컴퓨터의 변경할 수 없습니다. 이러한 작업을 수행 하는 방법에 대 한 자세한 내용은 Windows Server 참조&reg; 2016 [핵심 네트워크 가이드](../../Core-Network-Guide.md)합니다.  

  
-   [웹 서버 WEB1 설치](../../../core-network-guide/cncg/server-certs/Install-the-Web-Server-WEB1.md)  
  
-   [DNS에 WEB1에 대한 별칭(CNAME) 레코드 만들기](../../../core-network-guide/cncg/server-certs/Create-an-Alias-CNAME-Record-in-DNS-for-WEB1.md)  
  
-   [Crl (인증서 해지 목록)을 배포 하도록 WEB1 구성](../../../core-network-guide/cncg/server-certs/Configure-WEB1-to-Distribute-Certificate-Revocation-Lists.md)  
  
-   [Capolicy.inf inf 파일 준비](../../../core-network-guide/cncg/server-certs/Prepare-the-CAPolicy-inf-File.md)  
  
-   [인증 기관 설치](../../../core-network-guide/cncg/server-certs/Install-the-Certification-Authority.md)  
  
-   [C A 1에서 CDP 및 AIA 확장 구성](../../../core-network-guide/cncg/server-certs/Configure-the-CDP-and-AIA-Extensions-on-CA1.md)  
  
-   [가상 디렉터리에 CA 인증서 및 CRL 복사](../../../core-network-guide/cncg/server-certs/Copy-the-CA-Certificate-and-CRL-to-the-Virtual-Directory.md)  
  
-   [서버 인증서 템플릿 구성](../../../core-network-guide/cncg/server-certs/Configure-the-Server-Certificate-Template.md)  
  
-   [서버 인증서 자동 등록 구성](../../../core-network-guide/cncg/server-certs/Configure-Server-Certificate-Autoenrollment.md)  
  
-   [새로 고침 그룹 정책](../../../core-network-guide/cncg/server-certs/Refresh-Group-Policy.md)  
  
-   [서버 인증서의 서버 등록 확인](../../../core-network-guide/cncg/server-certs/Verify-Server-Enrollment-of-a-Server-Certificate.md)  
  
> [!NOTE]  
> 이 가이드의 절차에는 사례에 대 한 지침을 포함 하지 마십시오는 **사용자 계정 컨트롤** 를 계속 하려면 권한이 요청 대화 상자가 열립니다. 이 가이드의 절차를 수행하는 동안 이 대화 상자가 열리는 경우와 작업에 대한 응답으로 이 대화 상자가 이미 열린 경우에는 **계속**을 클릭하십시오.  
  


