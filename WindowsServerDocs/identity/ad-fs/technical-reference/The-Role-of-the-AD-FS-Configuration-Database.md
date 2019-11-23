---
ms.assetid: 68db7f26-d6e3-4e67-859b-80f352e6ab6a
title: AD FS 구성 데이터베이스의 역할
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 22047a93ab67d3f21b3e2318fcce497feab8f996
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385577"
---
# <a name="the-role-of-the-ad-fs-configuration-database"></a>AD FS 구성 데이터베이스의 역할
AD FS 구성 데이터베이스에는 Active Directory Federation Services \(AD FS\) \(페더레이션 서비스의 단일 인스턴스를 나타내는 모든 구성 데이터가 저장 됩니다.\) AD FS 구성 데이터베이스는 페더레이션 서비스가 파트너, 인증서, 특성 저장소, 클레임 및 이러한 관련 엔터티에 대한 다양한 데이터를 식별하는 데 필요한 매개 변수 집합을 정의합니다. 이 구성 데이터는 Microsoft SQL Server® 데이터베이스에 저장 하거나 windows Server® 2008, Windows Server 2008 R2 및 Windows Server® 2012에 포함 된 Windows 내부 데이터베이스 \(WID\) 기능에 저장할 수 있습니다.  
  
> [!NOTE]  
> AD FS 구성 데이터베이스의 전체 내용을 WID 인스턴스와 SQL 데이터베이스 인스턴스 중 하나에만 저장할 수 있습니다. 즉, AD FS 구성 데이터베이스의 동일한 인스턴스에 WID를 사용하는 페더레이션 서버와 SQL Server 데이터베이스를 사용하는 페더레이션 서버를 함께 사용할 수 없습니다.  
  
[AD FS 배포 토폴로지 고려 사항](https://technet.microsoft.com/library/gg982489.aspx)에 제공된 내용과 함께 이 항목의 다음 정보를 사용하여 WID 또는 SQL Server를 통해 AD FS 구성 데이터베이스를 저장할 경우의 장단점을 파악할 수 있습니다.  
  
WID는 관계형 데이터 저장소를 사용 하 여 및 자체 관리 사용자 인터페이스가 없는 \(UI\)합니다. 대신 관리자는, Fsconfig .exe 또는 Windows PowerShell™ cmdlet의 AD FS 관리 스냅인\-를 사용 하 여 AD FS 구성 데이터베이스의 콘텐츠를 수정할 수 있습니다.  
  
## <a name="using-wid-to-store-the-ad-fs-configuration-database"></a>WID를 사용하여 AD FS 구성 데이터베이스 저장  
Fsconfig .exe 명령\-줄 도구 또는 AD FS 페더레이션 서버 구성 마법사를 사용 하 여 WID를 저장소로 사용 하 여 AD FS 구성 데이터베이스를 만들 수 있습니다. 이러한 도구 중 하나를 사용할 때 다음 옵션 중 하나를 선택하여 페더레이션 서버 토폴로지를 만들 수 있습니다. 이러한 각 옵션에서는 WID를 사용하여 AD FS 구성 데이터베이스를 저장합니다.  
  
-   스탠드 만들기\-만 페더레이션 서버  
  
-   페더레이션 서버 팜의 첫 번째 페더레이션 서버 만들기  
  
-   페더레이션 서버 팜에 페더레이션 서버 추가  
  
독립\-단독 옵션을 선택 하는 경우 WID는 AD FS 구성 데이터베이스의 단일 인스턴스를 저장 하는 데 사용 됩니다. 이 인스턴스는 여러 페더레이션 서버 간에 공유할 수 없습니다. 이 옵션은 테스트 랩 환경만을 위한 것입니다. 대기 모드에 대 한 자세한 내용은\-단독으로 페더레이션 서버 옵션 또는 하나를 설정 하는 방법을 참조 [독립 실행형 페더레이션 서버를 사용 하 여 WID](https://technet.microsoft.com/library/gg982486.aspx) 또는 [독립 실행형 페더레이션 서버를 만들](https://technet.microsoft.com/library/ee913579.aspx)합니다.  
  
페더레이션 서버 팜의 첫 번째 페더레이션 서버 옵션을 선택하면 나중에 추가 페더레이션 서버를 팜에 추가할 수 있도록 확장성을 지원하도록 WID가 구성됩니다. WID 팜 배포 또는 이를 설정하는 방법에 대한 자세한 내용은 [WID를 사용하는 페더레이션 서버 팜](https://technet.microsoft.com/library/gg982492.aspx) 또는 [페더레이션 서버 팜의 첫 번째 페더레이션 서버 만들기](https://technet.microsoft.com/library/dd807070.aspx)를 참조하세요.  
  
페더레이션 서버 추가 옵션을 선택하면 설정된 간격으로 구성 데이터베이스의 변경 내용을 새 페더레이션 서버에 복제하도록 WID가 구성됩니다. WID 팜에 페더레이션 서버를 추가 하는 방법에 대 한 자세한 내용은 참조 [WID 페더레이션 서버 팜을 사용 하 여](https://technet.microsoft.com/library/gg982492.aspx) 또는 [페더레이션 서버 팜에 페더레이션 서버 추가](https://technet.microsoft.com/library/ee913575.aspx)합니다.  
  
> [!NOTE]  
> WID를 사용 하 여 페더레이션 서버 팜을 배포 하는 경우 AD FS의 일부 기능 없을 수도 있습니다. 전체 기능 집합에 액세스하려면 서버 팜을 구성할 때 Microsoft SQL Server를 사용하여 AD FS 구성 데이터베이스를 저장하는 것이 좋습니다. 자세한 내용은 [AD FS 배포 토폴로지 고려 사항](https://technet.microsoft.com/library/gg982489(v=ws.11).aspx)을 참조하세요.  
  
### <a name="how-a-wid-federation-server-farm-works"></a>WID 페더레이션 서버 팜 작동 방식  
이 섹션에서는 WID 페더레이션 서버 팜에서 기본 페더레이션 서버와 보조 페더레이션 서버 간에 데이터를 복제하는 방법을 설명하는 중요한 개념에 대해 알아봅니다. .  
  
#### <a name="primary-federation-server"></a>기본 페더레이션 서버  
기본 페더레이션 서버는 AD FS 페더레이션 서버 구성 마법사를 사용 하 여 페더레이션 서버 역할에 구성 되어 있고 AD FS 구성 데이터베이스의 읽기/쓰기 복사본이 있는 windows Server 2008, Windows Server 2008 R2 또는 Windows Server® 2012를 실행 하는 컴퓨터입니다. 기본 페더레이션 서버 AD FS 페더레이션 서버 구성 마법사를 사용 하 고 새 페더레이션 서비스를 팜의 첫 번째 페더레이션 서버 컴퓨터를 만들어 옵션을 선택 하는 경우에 항상 만들어집니다. 이 팜의 다른 모든 페더레이션 서버(보조 페더레이션 서버라고도 함)는 기본 페더레이션 서버에 적용된 모든 변경 내용을 로컬로 저장된 AD FS 구성 데이터베이스의 복사본에 동기화해야 합니다.  
  
#### <a name="secondary-federation-servers"></a>보조 페더레이션 서버  
보조 페더레이션 서버는 기본 페더레이션 서버에서 AD FS 구성 데이터베이스의 복사본을 저장 하지만 이러한 복사본은 읽기\-에만 해당 됩니다. 보조 페더레이션 서버는 데이터가 변경되었는지 확인하기 위해 정기적으로 폴링하여 팜의 기본 페더레이션 서버에 연결하고 데이터를 동기화합니다. 보조 페더레이션 서버를 찾을 수 로드 동작 하는 동안 기본 페더레이션 서버에 대 한 내결함성을 제공\-전체 네트워크 환경에서 서로 다른 사이트에 적용 된 액세스 요청을 분산 합니다.  
  
> [!NOTE]  
> 기본 페더레이션 서버가 작동이 중단되거나 오프라인 상태인 경우 모든 보조 페더레이션 서버는 계속 정상적으로 요청을 처리합니다. 그러나 기본 페더레이션 서버가 다시 온라인 상태가 될 때까지 새 변경 내용을 페더레이션 서비스에 적용할 수 없습니다. Windows PowerShell을 사용하여 보조 페더레이션 서버를 기본 페더레이션 서버로 지정할 수도 있습니다. 자세한 내용은 [Windows PowerShell을 사용한 AD FS 관리](https://go.microsoft.com/fwlink/?LinkID=179634)를 참조하세요.  
  
#### <a name="how-the-adfs-configuration-database-is-synchronized"></a>AD FS 구성 데이터베이스를 동기화하는 방법  
AD FS 구성 데이터베이스는 중요 한 역할을 하기 때문에 네트워크의 모든 페더레이션 서버에서 네트워크 로드\-균형 조정기를\)사용 하는 경우 \(요청을 처리할 때 내결함성 및 부하\-분산 기능을 제공 하기 위해 네트워크의 모든 페더레이션 서버에서 사용할 수 있습니다. 그러나 보조 페더레이션 서버가 이 용량에서 작동하려면 기본 페더레이션 서버에 저장된 AD FS 구성 데이터베이스를 동기화합니다.  
  
팜에 페더레이션 서버를 추가하면 보조 페더레이션 서버로 사용되는 새 컴퓨터가 기본 페더레이션 서버에 연결하여 AD FS 구성 데이터베이스의 복사본을 복제합니다. 이 시점부터 새 페더레이션 서버는 다음 그림에 표시된 대로 기본 페더레이션 서버에서 정기적으로 업데이트를 가져옵니다.  
  
![AD FS 역할](media/adfs2_WID.png)  
  
각 보조 페더레이션 서버는 5분마다 변경 내용에 대해 기본 페더레이션 서버를 폴링합니다. Windows PowerShell cmdlet을 사용 하 여 언제 든 지이 기본 5\-분 값을 조정 하거나 즉시 동기화를 강제로 적용할 수 있습니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 [Windows PowerShell을 사용한 AD FS 관리](https://go.microsoft.com/fwlink/?LinkID=179634)합니다.  
  
WID 동기화 프로세스는 중간 변경 내용에 대한 보다 효율적인 전송을 위해 증분 전송도 지원합니다. 증분 전송 프로세스는 상당히 적은 네트워크 트래픽을 사용하며 전송이 훨씬 빨리 완료됩니다.  
  
> [!NOTE]  
> WID에서 SQL Server 인스턴스로 AD FS 구성 데이터베이스를 마이그레이션할 수 있습니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 [AD FS: AD FS 구성 데이터베이스를 SQL Server로 마이그레이션할](https://go.microsoft.com/fwlink/?LinkId=192232) TechNet Wiki 사이트에 있습니다.  
  
## <a name="using-sql-server-to-store-the-ad-fs-configuration-database"></a>SQL Server를 사용하여 AD FS 구성 데이터베이스 저장  
Fsconfig .exe 명령\-줄 도구를 사용 하 여 저장소로 단일 SQL Server 데이터베이스 인스턴스를 사용 하 여 AD FS 구성 데이터베이스를 만들 수 있습니다. SQL Server 데이터베이스를 AD FS 구성 데이터베이스로 사용하면 WID에 비해 다음과 같은 이점을 얻을 수 있습니다.  
  
-   관리자가 SQL Server의 고가용성 기능을 활용할 수 있습니다.  
  
-   높은 트래픽에 대한 추가 성능 향상을 제공합니다.  
  
-   아래\)설명 된 \(SAML 아티팩트 확인 및 SAML/WS\-페더레이션 토큰 재생 검색 기능을 지원 합니다.  
  
"기본 페더레이션 서버"라는 용어는 AD FS 구성 데이터베이스가 SQL 데이터베이스 인스턴스에 저장된 경우에는 적용되지 않습니다. 이 경우에는 다음 그림에 표시된 대로 모든 페더레이션 서버에서 클러스터된 동일한 SQL Server 인스턴스를 사용하는 AD FS 구성 데이터베이스를 동일하게 읽고 쓸 수 있기 때문입니다.  
  
![AD FS 역할](media/adfs2_SQL.png)  
  
SQL Server를 사용 하 여 서버 클러스터로 함께 작동 하도록 두 대 이상의 서버를 구성 하 여 들어오는 클라이언트 요청을 서비스 하는 데 항상 사용 가능한 AD FS 되도록 할 수 있습니다. 고가용성 제공 소수\-아키텍처는 추가 서버를 추가 하 여 서버 용량을 늘릴 수 있습니다. 자동 클러스터 장애 조치(failover)를 통해 단일 실패 지점이 완화됩니다.  
  
네트워크 부하를 사용 하 여 고가용성을 얻을 수 있습니다\-SQL 클러스터링 기술에서 제공 하는 분산 및 장애 조치 서비스입니다. 고가용성을 위해 SQL Server를 구성 하는 방법에 대 한 자세한 내용은 [고가용성 솔루션 개요](https://go.microsoft.com/fwlink/?LinkId=179853)를 참조 하세요.  
  
### <a name="saml-artifact-resolution"></a>SAML 아티팩트 확인  
Security Assertion Markup Language \(SAML\) 아티팩트 확인은 신뢰 당사자가 클레임 공급자에서 직접 토큰을 검색 하는 방법을 설명 하는 SAML 2.0 프로토콜 기반의 끝점입니다. 확인 프로세스의 첫 번째 단계에서는 브라우저 클라이언트가 리소스 페더레이션 서버에 연결하여 이 서버에 아티팩트를 제공합니다. 두 번째 단계에서는 리소스 페더레이션 서버가 아티팩트 메시지를 확인하기 위해 계정 파트너 조직에서 호스트되는 SAML 아티팩트 끝점 URL로 아티팩트를 보냅니다. 마지막 단계에서는 계정 페더레이션 서버가 브라우저 클라이언트를 대신해 페더레이션 서버에 토큰을 발급합니다.  
  
> [!NOTE]  
> 계정 파트너 조직의 관리자 인 경우 Windows 루트 인증서 프로그램 구성원의 루트 인증서에 연결 된 SSL 인증서를 IIS의 페더레이션 수동 웹 사이트에 할당 하거나 바인딩해야 합니다 .이 인증서는 팜의 모든 계정 페더레이션 서버\\\\기본 웹 사이트\\\\사이트 기본 웹 사이트\) <ComputerName>\(합니다. 이는 리소스 페더레이션 서버에서 Local Computers Trusted People 인증서 저장소에 SSL 인증서를 수동으로 추가하거나 조직에 게시된 아티팩트를 확인하는 것을 방지하는 데 중요합니다.  
  
### <a name="samlws---federation-token-replay-detection"></a>SAML/WS-FEDERATION 토큰 재생 검색  
*토큰 재생*이라는 용어는 계정 파트너 조직의 브라우저 클라이언트가 계정 페더레이션 서버에서 받은 토큰을 여러 번 보내 리소스 페더레이션 서버에 인증하려고 시도하는 작업을 의미합니다.  이 동작은 인증 페이지를 다시 전송 하기 위해 사용자가 브라우저의 **뒤로** 단추를 클릭할 때 발생 합니다.  
  
AD FS에서는 동일한 토큰을 사용한 여러 번의 토큰 요청을 검색한 다음 삭제하는 *토큰 재생 검색* 기능을 제공합니다. 이 기능을 사용 하는 경우 토큰 재생 검색 모두 WS에서 인증 요청의 무결성을 보호\-페더레이션 passive 프로필과 SAML WebSSO 프로필에서 같은 토큰이 두 번 이상 사용 되지 않았는지 확인 하 여 합니다. 키오스크를 사용하는 경우 등 보안이 매우 중요한 상황에서 이 기능을 사용해야 합니다.  
  
예를 들어 키오스크에서는 사용자가 모든 웹 사이트에서 로그오프할 수 있는데, 이 경우 나중에 악의적인 사용자가 브라우저 기록을 사용해 이전 사용자가 로드한 페더레이션된 인증 페이지를 다시 제출하려고 시도할 수 있습니다. 이 기능은 토큰의 후속 재생을 감지 하 고 여러 인증 시도가 성공 하지 않도록 방지 하기 위해 계정 파트너 조직에서 수행 하는 각 인증에 대 한 추가 정보를 저장 하 여 이러한 문제를 완화 합니다.  
  

