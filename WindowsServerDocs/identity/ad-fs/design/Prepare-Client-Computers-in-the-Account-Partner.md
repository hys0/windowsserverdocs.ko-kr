---
ms.assetid: cea6011d-3753-4b95-aaa5-38d4e97d6e42
title: "클라이언트 컴퓨터에 계정 파트너 준비"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0c5bdcb0a80b15a1905109229ddd20ee642a8dd7
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="prepare-client-computers-in-the-account-partner"></a>클라이언트 컴퓨터에 계정 파트너 준비

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

관리자 계정 파트너 조직에서에 대 한 클라이언트 컴퓨터 Active Directory Federation Services 연방 \(AD FS\) 응용 프로그램에 대 한 액세스를 준비 하는 가장 쉬운 방법은 그룹 정책을 사용 하는 합니다. 그룹 정책을 특정 인증서 및 설정에 액세스 연결 된 응용 프로그램을 사용할 수 있는 모든 클라이언트 컴퓨터 federation 필요한 배포할 수 간편 합니다.  
  
클라이언트 컴퓨터 인증서 프롬프트 또는 신뢰할 수 있는 사이트과 관련 된 프롬프트를 않고도 연결 된 응용 프로그램에 원활 하 게 액세스할 수, 있는 조직에서 광범위 하 게 Adfs를 배포 하기 전에 각 클라이언트 컴퓨터 먼저 준비 하는 것이 좋습니다. 자동으로 그룹 정책을 사용 하는 것이 좋습니다.  
  
-   계정 federation 서버 신뢰할 수 각 클라이언트 컴퓨터에서 Internet Explorer를 구성 합니다.  
  
    자세한 내용은 참조 [계정 Federation 서버 신뢰 하는 클라이언트 컴퓨터 구성](../../ad-fs/deployment/Configure-Client-Computers-to-Trust-the-Account-Federation-Server.md)합니다.  
  
-   계정 해당 federation 서버, 리소스 federation 서버 및 웹 서버 주소 \(SSL\) 인증서를 설치 \ (해당 하는 인증서 나 해당 신뢰할 수 있는 root\ 체인) 클라이언트 각 컴퓨터에서 합니다.  
  
    자세한 내용은 참조 [인증서 그룹 정책을 사용 하 여 컴퓨터에 배포](../../ad-fs/deployment/Distribute-Certificates-to-Client-Computers-by-Using-Group-Policy.md)합니다.  
  

## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
