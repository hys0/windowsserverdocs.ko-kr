---
ms.assetid: 206b8072-1d0c-4a0b-ba8a-35a868d67b4c
title: 사이트 링크 디자인 만들기
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: fdff477a1fb7cbe42402b2bb608eea55f2f9ec09
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402708"
---
# <a name="creating-a-site-link-design"></a>사이트 링크 디자인 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사이트 링크를 만들어 사이트 링크와 사이트를 연결 합니다. 사이트 링크에는 복제 트래픽을 전송 하는 데 사용 되는 사이트 간 연결 및 방법이 반영 됩니다. 사이트 링크를 사용 하 여 사이트를 연결 해야 각 사이트의 도메인 컨트롤러가 Active Directory 변경 내용을 복제할 수 있습니다.  
  
## <a name="connecting-sites-with-site-links"></a>사이트 링크를 사용하여 사이트 연결

사이트 링크를 사용 하 여 사이트를 연결 하려면 사이트 링크를 사용 하 여 연결 하려는 구성원 사이트를 확인 하 고, 해당 사이트 간 전송 컨테이너에 사이트 링크 개체를 만든 다음, 사이트 링크의 이름을로 지정 합니다. 사이트 링크를 만든 후 사이트 링크 속성을 설정 하 여 계속 진행할 수 있습니다.  
  
사이트 링크를 만들 때 모든 사이트가 사이트 링크에 포함 되는지 확인 합니다. 또한 모든 사이트의 도메인 컨트롤러에서 다른 모든 사이트로 변경 내용을 복제할 수 있도록 모든 사이트가 다른 사이트 링크를 통해 서로 연결 되어 있는지 확인 합니다. 이 작업을 수행 하지 못하면 디렉터리 서비스 이벤트 뷰어 로그에서 사이트 토폴로지가 연결 되지 않았음을 나타내는 오류 메시지가 생성 됩니다.  
  
새로 만든 사이트 링크에 사이트를 추가할 때마다 추가 되는 사이트가 다른 사이트 링크의 멤버 인지 확인 하 고 필요한 경우 사이트의 사이트 링크 구성원 자격을 변경 합니다. 예를 들어 사이트를 처음 만들 때 사이트를 기본 사이트 링크의 멤버로 지정 하는 경우 새 사이트 링크에 사이트를 추가한 후에 사이트를 기본 사이트 링크에서 제거 해야 합니다. 기본-사이트 링크에서 사이트를 제거 하지 않으면 지식 일관성 검사기 (KCC)가 두 사이트 링크의 멤버 자격을 기준으로 라우팅 결정을 내리는 데이로 인해 잘못 된 라우팅이 발생할 수 있습니다.  
  
사이트 링크를 사용 하 여 연결 하려는 구성원 사이트를 식별 하려면 "지리적 위치 및 통신 링크" (DSSTOPO_1) 워크시트에서 기록한 위치 및 연결 된 위치 목록을 사용 합니다. 여러 사이트의 연결 및 가용성이 동일한 경우 동일한 사이트 링크를 사용 하 여 연결할 수 있습니다.  
  
사이트 간 전송 컨테이너는 링크에 사용 되는 전송에 사이트 링크를 매핑하는 방법을 제공 합니다. 사이트 링크 개체를 만드는 경우 사이트 링크를 ip 전송에 대 한 RPC (원격 프로시저 호출)와 연결 하는 IP 컨테이너 또는 사이트 링크를 SMTP와 연결 하는 SMTP (Simple Mail Transfer Protocol) 컨테이너에 연결 하는 IP 컨테이너에서 사이트 링크 개체를 만듭니다. 트랜스포트가.  
  
> [!NOTE]  
> 이후 버전의 Active Directory Domain Services에서는 SMTP 복제가 지원 되지 않습니다 (AD DS). 따라서 SMTP 컨테이너에 사이트 링크 개체를 만드는 것은 권장 되지 않습니다.  
  
각 사이트 간 전송 컨테이너에서 사이트 링크 개체를 만들 때 RPC over IP를 사용 하 여 도메인 컨트롤러 간에 사이트 간 복제와 사이트 간 복제를 모두 전송할 AD DS. 전송 중에 데이터를 안전 하 게 유지 하기 위해 RPC over IP 복제는 Kerberos 인증 프로토콜 및 데이터 암호화를 모두 사용 합니다.  
  
직접 IP 연결을 사용할 수 없는 경우 사이트 간에 SMTP를 사용 하도록 복제를 구성할 수 있습니다. 그러나 SMTP 복제 기능은 제한적 이며 엔터프라이즈 CA (인증 기관)가 필요 합니다. SMTP는 구성, 스키마 및 응용 프로그램 디렉터리 파티션만 복제할 수 있으며 도메인 디렉터리 파티션의 복제는 지원 하지 않습니다.  
  
사이트 링크의 이름을 지정 하려면 name_of_site1-name_of_site2와 같은 일관 된 이름 지정 체계를 사용 합니다. 사이트, 연결 된 사이트 및 해당 사이트를 연결 하는 사이트 링크의 이름을 워크시트에 기록 합니다. 사이트 이름 및 연결 된 사이트 링크 이름을 기록 하는 데 도움이 되는 워크시트의 경우 [Windows Server 2003 배포 키트의 작업 지원](https://go.microsoft.com/fwlink/?LinkID=102558)을 참조 하 고, Job_Aids_Designing_and_Deploying_Directory_and_Security_Services를 다운로드 하 고, "사이트 및 연결 된 사이트 링크 "(DSSTOPO_5).  
  
## <a name="in-this-guide"></a>이 가이드의 내용

[사이트 링크 속성 설정](Setting-Site-Link-Properties.md)  
