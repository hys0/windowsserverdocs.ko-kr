---
ms.assetid: 68db7f26-d6e3-4e67-859b-80f352e6ab6a
title: "AD FS 구성 데이터베이스의 역할"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3372e1f051ba7f900753a4961d948ddabdef6f4d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="the-role-of-the-ad-fs-configuration-database"></a>AD FS 구성 데이터베이스의 역할
ADFS 구성 데이터베이스 Active Directory Federation Services \(AD FS\) \(that is, the Federation Service\)의 단일 인스턴스 나타내는 모든 구성 데이터를 저장 합니다. ADFS 구성 데이터베이스 정의 Federation 서비스 파트너, 인증서, 특성 스토어, 청구, 및 관련된 이러한 항목에 대 한 다양 한 데이터를 식별 하는 데 필요한 매개 설정 합니다. 이 구성 데이터는 Microsoft SQL Server에에서 저장할 수® 데이터베이스 또는® Windows Server 2008, Windows Server 2008 R2 및 Windows Server® 2012에 포함 되어 있는 Windows 내부 데이터베이스 \(WID\) 기능입니다.  
  
> [!NOTE]  
> ADFS 구성 데이터베이스의 전체 내용을 하나만 WID 인스턴스 또는 인스턴스 SQL 데이터베이스에 저장 될 수 있습니다. 즉, WID 등과 같은 인스턴스 ADFS 구성 데이터베이스의 SQL Server 데이터베이스를 사용 하 여 사용 하는 몇 가지 federation 서버 수는 없습니다.  
  
다음 정보를 사용 하 여이 항목에서 제공 하는 내용 함께 [광고 FS 배포 토폴로지 고려](https://technet.microsoft.com/library/gg982489.aspx) WID 또는 SQL Server ADFS 구성 데이터베이스를 저장 하도록 선택 하면의 장단점에 대 한 자세한 내용은 다음과 같습니다.  
  
관계 데이터 저장 하 고 관리 사용자 하지 않은 WID 사용 하 여 인터페이스 \(UI\) 합니다. 관리자 snap\에서 광고 FS 관리, Fsconfig.exe 또는 Windows PowerShell를 사용 하 여 ADFS 구성 데이터베이스의 콘텐츠를 수정할 수 대신™ cmdlet 합니다.  
  
## <a name="using-wid-to-store-the-ad-fs-configuration-database"></a>ADFS 구성 데이터베이스를 저장 하기 위해 WID 사용  
ADFS 구성 데이터베이스 WID Fsconfig.exe command\ 선 도구 또는 광고 FS Federation 서버 구성 마법사를 사용 하 여 스토어도 사용 하 여 만들 수 있습니다. 이러한 도구를 사용 하면 federation 서버 토폴로지를 작성 하 고 다음 옵션 중 하나를 선택할 수 있습니다. 이러한 옵션에 WID ADFS 구성 데이터베이스에 저장 하는 데 사용 합니다.  
  
-   Stand\만 federation 서버 만들기  
  
-   첫 번째 federation 서버 federation 서버 팜에서 만들기  
  
-   Federation 서버 federation 서버 팜을 추가  
  
Stand\ 만으로 옵션을 선택 하면 WID ADFS 구성 데이터베이스의 단일 인스턴스 저장할 사용 됩니다. 이 경우 여러 federation 서버 공유할 수 없습니다. 테스트 랩 환경을 의미 합니다. Stand\만 federation 서버 옵션이 나 하나 설정 하는 방법에 대 한 자세한 내용은 참조 [독립 실행형 Federation 서버를 사용 하 여 WID](https://technet.microsoft.com/library/gg982486.aspx) 또는 [독립 실행형 Federation 서버를 만들](https://technet.microsoft.com/library/ee913579.aspx)합니다.  
  
첫 번째 federation 서버 federation 서버 팜 옵션을 선택 하면 WID 확장성 추가 federation 서버를 나중에 있는 그룹에 추가할 수 있도록 구성 되어 있습니다. 배포 WID 팜 또는 하나 설정 하는 방법에 대 한 자세한 내용은 참조 [Federation 서버 농장을 사용 하 여 WID](https://technet.microsoft.com/library/gg982492.aspx) 또는 [Federation 서버 농장의 첫 번째 Federation 서버 만들기](https://technet.microsoft.com/library/dd807070.aspx)  
  
추가 federation 서버 옵션을 선택 하면 WID 설정 간격으로 새로운 federation 서버에 구성 데이터베이스 변경 복제으로 구성 됩니다. Federation 서버 WID 그룹에 추가 대 한 자세한 내용은 참조 [Federation 서버 농장을 사용 하 여 WID](https://technet.microsoft.com/library/gg982492.aspx) 또는 [Federation 서버 Federation 서버 팜을 추가](https://technet.microsoft.com/library/ee913575.aspx)합니다.  
  
> [!NOTE]  
> WID를 사용 하 여 federation 서버 팜 배포할 때 Adfs의 일부 기능을 사용할 수 있는 수 없습니다. 서버 농장 구성 하는 경우 모든 기능에 대 한 액세스를 대신 ADFS 구성 데이터베이스를 저장 하기 위해 Microsoft SQL Server를 사용 하는 것이 좋습니다. 자세한 내용은 참조 [광고 FS 배포 토폴로지 고려](https://technet.microsoft.com/library/gg982489(v=ws.11).aspx)합니다.  
  
### <a name="how-a-wid-federation-server-farm-works"></a>WID federation 서버 농장의 작동 방식  
여기서는 WID federation 서버 팜 기본 federation 서버와 보조 federation 서버 데이터를 복제 하는 방법을 설명 하는 중요 한 개념 설명 합니다. .  
  
#### <a name="primary-federation-server"></a>기본 federation 서버  
기본 federation 서버는 Windows Server 2008, Windows Server 2008 R2 또는 Windows Server® 2012 federation 서버 역할 AD FS Federation 서버 구성 마법사도 구성 된를 ADFS 구성 데이터베이스의 읽기/쓰기 복사본을 실행 하는 컴퓨터 합니다. AD FS Federation 서버 구성 마법사를 사용 하 고 새 Federation 서비스를 만들고 그룹에서 해당 컴퓨터 첫 번째 federation 서버를 확인 하는 옵션을 선택 하는 경우 기본 federation 서버 항상 만들어집니다. 이 농장 라고도 보조 federation 서버의에서 다른 모든 federation 서버 변경한 로컬에 저장 된 ADFS 구성 데이터베이스의 복사본을 기본 federation 서버에 동기화 해야 합니다.  
  
#### <a name="secondary-federation-servers"></a>보조 federation 서버  
보조 federation 서버 기본 federation 서버에서 ADFS 구성 데이터베이스의 복사본을 저장할 하지만 이러한 복사본은 read\ 전용 합니다. 보조 federation 서버에 연결 하 고 데이터가 변경 있는지 여부를 확인 하려면 정기적으로 투표 하 여 데이터 팜에서 기본 federation 서버와 동기화 합니다. 보조 federation 서버 네트워크 환경에서 다른 사이트에 대 한 액세스 요청 load\ 잔액에 역할 기본 federation 서버에 대 한 결함 허용 제공할 수 있습니다.  
  
> [!NOTE]  
> 기본 federation 서버 충돌 오프 라인 상태인 경우 모든 보조 federation 서버 정상적으로 요청을 처리 하기 위해 계속 합니다. 그러나 새로운 없이 변경 가능 Federation 서비스에 기본 federation 서버 다시 온라인 상태가 될 때까지 합니다. 보조 federation 서버 Windows PowerShell를 사용 하 여 기본 federation 서버를 지정할 수 있습니다. 자세한 내용은 참조는 [광고 FS 관리를 Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=179634)합니다.  
  
#### <a name="how-the-ad-fs-configuration-database-is-synchronized"></a>ADFS 구성 데이터베이스 동기화 방법  
ADFS 구성 데이터베이스 재생 되는 중요 한 역할을 때문 사용할 수 네트워크의 모든 federation 서버에서 오류 허용 및 load\ 균형 제공 하기 위해 기능 요청을 처리할 때 \ (경우 네트워크 load\ 분산은 used\). 하지만 이러한 기능에 보조 federation 서버에 대 한 기본 federation 서버에 저장 된 ADFS 구성 데이터베이스를 동기화 합니다.  
  
Federation 서버 그룹에 추가 하면 보조 federation 서버를가 하는 새 컴퓨터 ADFS 구성 데이터베이스의 복사본 복제 하는 기본 federation 서버에 연결 합니다. 이 시점에서 새 federation 서버 다음과 같이 기본 federation 서버를 정기적으로 업데이트를 계속 합니다.  
  
![광고 FS 역할](media/adfs2_WID.png)  
  
각 보조 federation 서버 업데이트 이벤트를 지원 기본 federation 서버 변경에 대 일 분 마다 합니다. 기본값 five\ 분이 조정 하거나 Windows PowerShell cmdlet 사용 하 여 언제 든 지 바로 동기화 할 수 있습니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 [광고 FS 관리를 Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=179634)합니다.  
  
또한 WID 동기화 프로세스 중간 변경 내용을 더 효율적으로 전송 증분 전송 지원합니다. 증분 전송 네트워크에서 떨어집니다 교통 차지 하며 전송 훨씬 빨리 완료 됩니다.  
  
> [!NOTE]  
> 마이그레이션 SQL Server 인스턴스 ADFS 구성 데이터베이스 WID에서 지원 됩니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 [ADFS: AD FS 구성 데이터베이스 SQL Server를 마이그레이션해야](https://go.microsoft.com/fwlink/?LinkId=192232) TechNet Wiki 사이트에 있습니다.  
  
## <a name="using-sql-server-to-store-the-ad-fs-configuration-database"></a>SQL Server ADFS 구성 데이터베이스를 저장 하기 위해 사용  
ADFS 구성 데이터베이스 Fsconfig.exe command\ 선 도구를 사용 하 여 스토어로 단일 데이터베이스 SQL Server 인스턴스를 사용 하 여 만들 수 있습니다. ADFS 구성 데이터베이스와 SQL Server 데이터베이스를 사용 하 여 WID을 통해 다음과 같은 이점을 제공 합니다.  
  
-   관리자는 SQL Server의 높은 기능을 활용  
  
-   높은 교통 추가 성능 향상을 제공합니다.  
  
-   SAML 아티팩트 해상도 및 SAML/WS\-Federation 토큰 재생 감지 \(described below\) 기능 지원을 제공합니다.  
  
ADFS 구성 데이터베이스 동일 하 게 모든 federation 서버 읽고 다음 그림과 같이 동일한 클러스터 SQL Server 인스턴스를 사용 하는 ADFS 구성 데이터베이스에 쓸 수 있으므로 SQL 데이터베이스 인스턴스에 저장 될 때 "주 federation 서버" 라는 용어 적용 되지 않습니다.  
  
![광고 FS 역할](media/adfs2_SQL.png)  
  
두 개 이상의 서버 ADFS 매우 서비스 수신 클라이언트 요청을 사용할 수 있는지 확인 하는 서버 클러스터로 함께 작동 하도록 구성할 수 SQL Server 사용할 수 있습니다. 높은 가용성 scale\ 아웃 아키텍처 서버 추가 하 여 서버 용량을 높일 수 있는 제공 합니다. 자동 클러스터 장애 조치 단일 지점 실패 줄어듭니다 됩니다.  
  
네트워크 load\ 분산 및 SQL 클러스터링 기술을 제공 하는 장애 서비스를 사용 하 여 가용성 우선 얻을 수 있습니다. 항상 사용 가능 SQL Server 구성 하는 방법에 대 한 자세한 내용은 참조 [높은 가용성 솔루션 개요](https://go.microsoft.com/fwlink/?LinkId=179853)합니다.  
  
### <a name="saml-artifact-resolution"></a>SAML 아티팩트 해상도  
보안 설정 Markup Language \(SAML\) 아티팩트 해상도 당사자가 클레임 공급자 로부터 직접 토큰을 검색 하는 방법을 설명 하는 SAML 2.0 프로토콜에서 기반 끝점입니다. 해상도 프로세스의 첫 번째 단계에서 브라우저 클라이언트 리소스 federation 서버에 연결 하 고 보물을 제공 합니다. 2 단계에서 리소스 federation 서버 유물 아티팩트 메시지를 해결 하기 위해 계정 파트너 조직에 어떤 곳 호스트 SAML 아티팩트 끝점 URL를 보냅니다. 마지막 단계에서 계정 federation 서버 브라우저 클라이언트를 대표 하 여 토큰 연합 서버에 발급합니다.  
  
> [!NOTE]  
> 계정 파트너 조직에서 관리자 인 경우 지정 하거나 IIS federation 수동 사이트로 SSL 인증서 Windows 루트 인증서 프로그램의 구성원 루트 인증서에 연결 하는 연결 되어 있는지 확인 \ (<ComputerName>\\Sites\\Default WebSite\\adfs\\ls\) 그룹의 모든 계정 federation 서버에 있습니다. 이 조직에 게시 유물 해결할 수 없는 나에서 수동으로 SSL 인증서 로컬 컴퓨터 신뢰할 수 있는 사람 인증서 저장소를 추가 하는 데 리소스 federation 서버를 방지 하는 것이 중요 합니다.  
  
### <a name="samlws---federation-token-replay-detection"></a>SAML/WS 토큰 연합 재생 검색  
라는 용어 *토큰 재생* 는 인증을 여러 번 계정 federation 서버에서 받은 것과 동일한 토큰 리소스 federation 서버에 전송 하 여 계정 파트너 조직에서 브라우저 클라이언트 시도 것을 의미 합니다.  사용자가이 법 발생는 **다시** 인증 페이지 다시 전송 하기 위해에서 해당 브라우저의 단추.  
  
ADFS 라고도 하는 기능을 제공 *재생 검색 토큰* 여러 토큰 요청 하 여 동일한 토큰을 사용 하 여 검색 하 후 삭제 됩니다. 이 기능을 활성화 토큰 재생 검색 동일한 토큰 두 번 이상 사용 하지 않도록 하 여 WS\ Federation 수동 프로필 및 SAML WebSSO 프로필 인증 요청의 무결성을 보호 합니다. 이 기능은에서 없는 경우 보안 매우 높은 관심사와 같은 사용 하도록 설정 해야 단말기를 사용할 때입니다.  
  
키오스크 예제에서 모든 웹 사이트에서 사용자 기록할 수를 브라우저 기록 이전 사용자가 로드 된 연합된 인증 페이지 다시 전송 하기 위해 사용 하 여 악의적인 사용자 수 시도 하는 나중에 합니다. 이 기능은 토큰의 후속 재생을 감지 하 고 후속 여러 인증 시도 방지 하기 위해 계정 파트너 조직에서 각 성공적으로 인증에 대 한 추가 정보를 저장 하 여이 문제를 줄입니다.  
  

