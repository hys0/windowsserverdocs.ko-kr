---
ms.assetid: cea6011d-3753-4b95-aaa5-38d4e97d6e42
title: 계정 파트너에서 클라이언트 컴퓨터 준비
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e3a746ec003cf312ffe0b9804f84a55c98aa8089
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190993"
---
# <a name="prepare-client-computers-in-the-account-partner"></a>계정 파트너에서 클라이언트 컴퓨터 준비

가장 쉬운 방법은 계정 관리자가 파트너 조직에서 Active Directory Federation Services에 대 한 액세스에 대 한 클라이언트 컴퓨터를 준비 \(AD FS\) 페더레이션된 응용 프로그램 그룹 정책을 사용 하는 것입니다. 그룹 정책은 페더레이션 응용 프로그램에 액세스하는 데 사용하는 모든 클라이언트 컴퓨터에 페더레이션에 필요한 특정 인증서 및 설정을 푸시하는 편리한 방법을 제공합니다.  
  
클라이언트 컴퓨터가 인증서 프롬프트 또는 신뢰할 수 있는 사이트 관련 프롬프트 없이 페더레이션된 응용 프로그램에 원활 하 게 액세스할 수 있도록 조직에서 광범위 하 게 AD FS를 배포 하기 전에 각 클라이언트 컴퓨터 먼저 준비 하는 것이 좋습니다. 다음 작업이 자동으로 수행되도록 그룹 정책 사용을 고려해 보세요.  
  
-   계정 페더레이션 서버를 신뢰 하려면 각 클라이언트 컴퓨터에 Internet Explorer를 구성 합니다.  
  
    자세한 내용은 [계정 페더레이션 서버를 신뢰 하도록 클라이언트 컴퓨터를 구성 합니다](../../ad-fs/deployment/Configure-Client-Computers-to-Trust-the-Account-Federation-Server.md)를 참조하세요.  
  
-   적절 한 계정 페더레이션 서버, 리소스 페더레이션 서버 및 웹 서버 설치 Secure Sockets Layer \(SSL\) 인증서 \(해당 하는 연결 된 신뢰할 수 있는 루트 인증서 또는\) 각 클라이언트 컴퓨터입니다.  
  
    자세한 내용은 [그룹 정책을 사용 하 여 클라이언트 컴퓨터에 대 한 인증서 배포](../../ad-fs/deployment/Distribute-Certificates-to-Client-Computers-by-Using-Group-Policy.md)합니다.  
  

## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
