---
ms.assetid: 206b8072-1d0c-4a0b-ba8a-35a868d67b4c
title: 사이트 링크 디자인 만들기
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4e0607cf66d41e1747b108a3ecc10562120d9174
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861934"
---
# <a name="creating-a-site-link-design"></a>사이트 링크 디자인 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사이트 링크를 사용 하 여 사이트에 연결 하려면 사이트 링크 디자인 만들기 사이트 링크는 사이트 간 연결 및 복제 트래픽을 전송 하는 데 사용 되는 메서드를 반영 합니다. 각 사이트에서 도메인 컨트롤러에 Active Directory 변경 내용을 복제할 수 있도록 사이트 링크를 사용 하 여 사이트를 연결 해야 합니다.  
  
## <a name="connecting-sites-with-site-links"></a>사이트 링크를 사용하여 사이트 연결

사이트 링크를 사용 하 여 사이트에 연결 하려면 사이트 링크를 사용 하 여 연결 하 고 해당 사이트 간 전송 컨테이너에 사이트 링크 개체를 만드는 다음 사이트 링크의 이름을 하려는 멤버 사이트를 식별 합니다. 사이트 링크를 만든 후에 사이트 링크 속성을 설정 하려면 진행할 수 있습니다.  
  
사이트 링크를 만들 때 모든 사이트는 사이트 링크에 포함 되어 있는지 확인 합니다. 또한 모든 사이트에 연결 되어 있는지 서로 다른 사이트 링크를 통해 다른 모든 사이트에 모든 사이트에 도메인 컨트롤러에서 변경 내용을 복제할 수 있도록 확인 합니다. 이 작업을 수행 하지 않으면 디렉터리 서비스 로그에서 이벤트 뷰어 사이트 토폴로지 연결 되어 있지 않다고 알리는 오류 메시지가 생성 됩니다.  
  
새로 만든된 사이트 링크에 사이트를 추가할 때마다 추가 되 고 사이트가 다른 사이트 링크의 구성원 인지 확인 하 고 필요한 경우 사이트의 사이트 링크 멤버 자격을 변경 합니다. 예를 들어을 하는 경우 사이트 기본 첫 번째 사이트 링크의 멤버는 사이트를 처음 만들 때 해야 새 사이트 링크에 사이트를 추가한 후 기본 첫 번째 사이트 링크에서 사이트를 제거 합니다. 기본 첫 번째 사이트 링크에서 사이트를 제거 하지 않으면 잘못 된 라우팅에 따를 수 있는 두 사이트 링크의 멤버 자격을 기반으로 하는 라우팅 결정 지식 일관성 검사기 (KCC) 생성 됩니다.  
  
사이트 링크를 사용 하 여 연결 하려는 멤버 사이트를 식별 하려면 위치 목록과 "지리적 위치 및 통신 링크" (DSSTOPO_1.doc) 워크시트에 기록 된 연결 된 위치를 사용 합니다. 여러 사이트 연결 및 가용성을 서로 동일한 경우에 동일한 사이트 링크를 사용 하 여 연결할 수 있습니다.  
  
사이트 간 전송 컨테이너는 링크를 사용 하는 전송에 사이트 링크를 매핑하기 위한 수단을 제공 합니다. 사이트 링크 개체를 만들 때 만든 IP 전송 프로토콜을 통해 원격 프로시저 호출 (RPC)을 사용 하 여 사이트 링크를 연결 하는 IP 컨테이너 또는 SMTP를 사용 하 여 사이트 링크를 연결 하는 SMTP Simple Mail Transfer Protocol () 컨테이너 전송 합니다.  
  
> [!NOTE]  
> SMTP 복제 Active Directory Domain Services (AD DS);의 이후 버전에서 지원 되지 않습니다. 따라서 SMTP 컨테이너에 사이트 링크 개체를 만들기도 권장 되지 않습니다.  
  
각 사이트 간 전송 컨테이너에 사이트 링크 개체를 만들 때 AD DS를 사용 하 여 RPC IP를 통해 도메인 컨트롤러 간의 사이트 간 및 사이트 간 복제를 전송 합니다. RPC over IP는 전송 중에 데이터를 보호 하기, Kerberos 인증 프로토콜 및 데이터 암호화를 사용 합니다.  
  
직접 IP 연결을 사용할 수 없을 때 SMTP를 사용 하는 사이트 간 복제를 구성할 수 있습니다. 하지만 SMTP 복제 기능은 제한 되며는 엔터프라이즈 CA (인증 기관) 필요 합니다. SMTP 구성, 스키마 및 응용 프로그램 디렉터리 파티션을 복제할 수 있습니다 및 도메인 디렉터리 파티션의 복제를 지원 하지 않습니다.  
  
사이트 링크의 이름을, name_of_site1 name_of_site2 등 일관성 있는 명명 체계를 사용 합니다. 사이트, 연결 된 사이트 및 사이트 링크 워크시트에서 이러한 사이트 연결의 이름 목록을 기록 합니다. 사이트 이름 및 연결 된 사이트 링크 이름을 기록 하는 데 도움이 되는 워크시트를 참조 하세요 [작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558), Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip를 다운로드 하 고 "사이트 및 연결 된 사이트 링크"를 엽니다 (DSSTOPO_5.doc).  
  
## <a name="in-this-guide"></a>이 가이드의 내용

[사이트 링크 속성 설정](Setting-Site-Link-Properties.md)  
