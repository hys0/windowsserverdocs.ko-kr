---
ms.assetid: 206b8072-1d0c-4a0b-ba8a-35a868d67b4c
title: "사이트 링크 디자인 만들기"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9eb54781035424c9a5210e11fbdeafc55496c6c3
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="creating-a-site-link-design"></a>사이트 링크 디자인 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사이트 사이트 링크를 사용 하 여 연결 하는 사이트 링크 디자인을 만듭니다. 사이트 링크 반영 간 연결 및 복제 교통 전송 하는 데 사용 하는 방법입니다. 각 사이트 도메인 컨트롤러 Active Directory 변경 복제 수 있도록 사이트 사이트 링크를 연결 해야 합니다.  
  
## <a name="connecting-sites-with-site-links"></a>사이트 사이트 링크를 사용 하 여 연결  
사이트 사이트 연결에 연결 하려면 사이트 링크를 사용 하 여 연결 사이트 링크 개체에서 해당 사이트 간 전송 컨테이너 만들고 사이트 링크 다음 이름을 하려는 멤버 사이트를 확인 합니다. 사이트 링크를 만든 후 속성을 설정 하는 사이트 링크 진행할 수 있습니다.  
  
사이트 링크를 만들 때 모든 사이트 사이트 링크를에 포함 되어 있는지 확인 합니다. 또한, 모든 사이트 연결 되어 있는지 확인 서로 다른 사이트 링크를 통해 다른 모든 사이트에 변경 내용을 모든 사이트에 있는 도메인 컨트롤러에서 복제 될 수 있도록 합니다. 이 실패 하는 경우 오류 메시지 디렉터리 서비스 로그 사이트 토폴로지 연결 되어 있지 이벤트 뷰어 되었다는에서 생성 됩니다.  
  
새로 만든된 사이트 연결에 사이트를 추가할 때마다 추가 되는 사이트의 다른 사이트 링크, 인지 확인 하 고 필요한 경우 해당 사이트의 사이트 링크 구성원을 변경 합니다. 예를 들어,를 설정 하면 사이트 Default-First-Site-Link의 회원 처음 사이트 만들 때 사용할 사이트 새로운 사이트 링크를 추가한 후 Default-First-Site-Link에서에서 해당 사이트를 제거 해야 합니다. Default-First-Site-Link에서에서 해당 사이트를 제거 하지 않는 경우 정보 일관성 검사 (KCC) 결정을 내릴 라우팅 경로 잘못 될 수 있는 사이트 링크 모두 구성원에 따라 합니다.  
  
사이트 링크를 사용 하 여 연결 하려면 구성원 사이트를 확인 하려면 "지리적 위치와 통신 연결이" (DSSTOPO_1.doc) 워크시트에 기록 하는 연결 된 위치 및 위치 목록을 사용 합니다. 여러 사이트를 사용 하는 동일한 연결 및 다른 사용자에 게 공급 하는 경우 동일한 사이트 링크와 함께 연결할 수 있습니다.  
  
간 사이트 전송 컨테이너 사이트 링크 매핑하 전송 링크를 사용 하는 방법을 제공 합니다. 사이트 링크 개체를 만들 때 IP 전송 통해 사이트 링크 원격 프로시저 호출 (RPC) 연결을 IP 컨테이너 또는 SMTP 전송 사이트 링크를 연결 하는 SMTP(Simple Mail Transfer Protocol) SMTP () 컨테이너 만듭니다.  
  
> [!NOTE]  
> SMTP 복제 (AD DS), Active Directory Domain Services의 향후 버전에서 지원 될 것 따라서 사이트 링크 개체 SMTP 컨테이너에서 만드는 권장 되지 않습니다.  
  
해당 사이트 간 전송 컨테이너 사이트 링크 개체를 만들 때 AD DS RPC over IP 사용 하는 도메인 컨트롤러 간의 사이트 간 및 내 복제 전송 합니다. 전송 중에 데이터를 보호 하기, RPC IP over Kerberos 인증 프로토콜 및 데이터가 암호화를 사용 합니다.  
  
직접 IP 연결을 사용할 수 없을 때 사이트 SMTP 사용 하 여 간 복제를 구성할 수 있습니다. 그러나 SMTP 복제 기능이 제한 이며 (캐나다)는 엔터프라이즈 인증 기관 필요 합니다. SMTP 구성, 스키마 및 응용 프로그램 파티션 복제만 수행 하 고 도메인 파티션 복제 지원 하지 않습니다.  
  
이름을 지정 사이트 링크, name_of_site1 name_of_site2 등 일관 되 게 명명 구성표를 사용 합니다. 기록 워크시트에서 이러한 사이트 연결 사이트 링크의 이름과 사이트, 연결 된 사이트 목록입니다. 워크시트 사이트 이름과 함께 연결된 사이트 링크를 녹화/녹음을 지원 하기 위해 작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit 참조 ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558))를 다운로드 Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip 하 고 "사이트와 관련 된 사이트 링크" (DSSTOPO_5.doc) 엽니다.  
  
## <a name="in-this-guide"></a>이 가이드  
[사이트 링크 속성을 설정](Setting-Site-Link-Properties.md)  
  


