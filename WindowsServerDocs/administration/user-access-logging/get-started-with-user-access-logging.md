---
title: 시작 사용자 액세스 로깅
desctription: Describes the User Access Logging feature and how to start using it.
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: manage-user-access-logging
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c395b8b-3b35-4042-b9cc-07e438f86d50
author: brentfor
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8656bf278519b48f8d26008fd98e46428106e511
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861504"
---
# <a name="get-started-with-user-access-logging"></a>시작 사용자 액세스 로깅

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

로깅 UAL (사용자 액세스)에 로컬 서버에서 역할 및 클라이언트 사용 현황 데이터를 집계 하는 Windows Server의 기능입니다. Windows 서버 관리자가 로컬 서버에서 역할 및 서비스에 대 한 클라이언트 컴퓨터의 요청을 수치화 수 있습니다.  
  
UAL 설치 되며 기본적으로 및에서 데이터를 수집 하도록 설정한 거의 실시간. UAL을 사용하거나 사용하지 않도록 설정할 수는 있지만 그 외의 관리자 구성은 수행하지 않아도 됩니다. 자세한 내용은 [Manage User Access Logging](Manage-User-Access-Logging.md)를 참조하세요. 사용자 액세스 로깅 서비스는 로컬 데이터베이스 파일에 역할 및 클라이언트 사용 현황 데이터를 집계합니다.  IT 관리자는 나중에 WMI(Windows Management Instrumentation) 또는 Windows PowerShell cmdlet을 사용하여 서버 역할(또는 소프트에어 제품), 사용자, 장치, 로컬 서버, 날짜를 기준으로 수량과 인스턴스를 검색할 수 있습니다.  
  
> [!NOTE]  
> UAL은 [Microsoft Assessment and Planning Toolkit](https://go.microsoft.com/fwlink/?LinkID=111000)(영문)을 지원합니다.  
  
## <a name="BKMK_APP"></a>실제 응용 프로그램  
UAL를 로컬 데이터베이스에 기록 되는 고유한 클라이언트 장치 및 사용자 요청 이벤트를 집계 합니다. 이렇게 레코드는 서버 관리자가 쿼리를 통해 서버 역할, 사용자, 장치, 로컬 서버 및 날짜를 기준으로 수량과 인스턴스를 검색하는 데 사용할 수 있습니다.  또한 UAL Microsoft 이외의 소프트웨어 개발자는 Windows 서버에서 집계 될 UAL 이벤트를 사용할 수 있도록 확장 되었습니다.  
  
UAL 다음 작업을 수행할 수 있습니다.  
  
-   로컬의 실제 서버 또는 가상 서버에 대한 클라이언트 사용자 요청 수를 수치화합니다.  
  
-   로컬의 실제 또는 가상 서버에 설치된 소프트웨어 제품에 대한 클라이언트 사용자 요청 수를 수치화합니다.  
  
-   Hyper-V를 실행하는 로컬 서버에서 데이터를 검색하여 Hyper-V 가상 컴퓨터에서 최고/최저 요구 기간을 확인합니다.  
  
-   여러 원격 서버에서 UAL 데이터를 검색합니다.  
  
또한 소프트웨어 개발자는 다음 집계 고 WMI 및 Windows PowerShell 인터페이스를 사용 하 여 검색할 수 있는 UAL 이벤트를 계측할 수 있습니다.  
  
UAL에서 지원할 수 있는 서버 역할 및 서비스는 다음과 같습니다.  
  
-   AD CS(Active Directory 인증서 서비스)  
  
-   AD RMS(Active Directory Rights Management Services)  
  
-   BranchCache  
  
-   DNS(Domain Name System)  
  
    > [!NOTE]  
    > UAL은 24시간마다 DNS 데이터를 수집하며, 이 시나리오에 사용할 수 있는 별도의 UAL cmdlet이 있습니다.  
  
-   DHCP(동적 호스트 구성 프로토콜)  
  
-   팩스 서버  
  
-   파일 서비스  
  
-   FTP(파일 전송 프로토콜) 서버  
  
-   Hyper-V  
  
    > [!NOTE]  
    > UAL은 24시간마다 Hyper-V 데이터를 수집하며, 이 시나리오에 사용할 수 있는 별도의 UAL cmdlet이 있습니다.  
  
-   웹 서버(IIS)  
  
    > [!WARNING]  
    > IIS에서 UAL을 사용하려면 iisual.exe를 사용해야 합니다. 자세한 내용은 [IIS 사용자 액세스 로깅을 사용하여 클라이언트 사용 현황 데이터 분석](http://www.iis.net/learn/manage/configuring-security/analyzing-client-usage-data-with-iis-user-access-logging)(영문)을 참조하세요.  
  
-   MSMQ(Microsoft Message Queue) 서비스  
  
-   네트워크 정책 및 액세스 서비스  
  
-   인쇄 및 문서 서비스  
  
-   RRAS(라우팅 및 원격 액세스 서비스)  
  
-   WDS(Windows 배포 서비스)  
  
-   WSUS(Windows Server Update Services)  
  
> [!IMPORTANT]  
> 인터넷에 액세스할 수 있는 주소 공간의 웹 서버와 같이 인터넷에 직접 연결된 서버나, 서버의 주요 기능이 초고성능인 시나리오(예: HPC 워크로드 환경)에서는 UAL을 사용하지 않는 것이 좋습니다. UAL은 정기적으로 인터넷 연결 트래픽 볼륨을 제공 하는 배포로 볼륨이 많지 않지만 소형, 중형 및 대기업 인트라넷 시나리오 높은 볼륨이 필요한 경우에 적합  
  
## <a name="BKMK_NEW"></a>중요 한 기능  
다음 표에서는 UAL의 주요 기능 및 사용 가능한 값에 대해 설명합니다.  
  
|기능|값|  
|-----------------|---------|  
|클라이언트 요청 이벤트 데이터를 거의 실시간으로 수집 및 집계합니다.|최대 3년 동안의 데이터를 저장할 수 있습니다. **중요:** 관리자는 조직의 개인 정보 취급 방침 및 현지 규정에 따라 수집되는 데이터 및 데이터 보존 기간 관련 규정을 준수해야 합니다.|  
|WMI 또는 Windows PowerShell 인터페이스를 사용하여 UAL을 쿼리하여 로컬 또는 원격 서버에서 클라이언트 요청 데이터를 검색합니다.|UAL에서는 시간의 경과에 따른 사용 현황 데이터를 하나의 보기에서 확인할 수 있습니다. 서버 및 엔터프라이즈 관리자는 이 데이터를 검색한 다음 비즈니스 관리자와 협력하여 볼륨 소프트웨어 라이선스 사용을 최적화할 수 있습니다.|  
|기본적으로 사용하도록 설정되어 있습니다.|서버 관리자가 이 기능을 구성하거나 별도로 설정하지 않아도 모든 핵심 기능이 사용 가능하고 작동합니다.|  
  
## <a name="data-logged-with-ual"></a>UAL을 통해 기록되는 데이터  
다음과 같은 사용자 관련 데이터가 UAL에서 기록됩니다.  
  
|data|설명|  
|--------|---------------|  
|**UserName**|설치된 역할과 제품에서 UAL 항목을 포함하는 클라이언트의 사용자 이름(해당하는 경우)입니다.|  
|**ActivityCount**|특정 사용자가 역할이나 서비스에 액세스한 횟수입니다.|  
|**FirstSeen**|사용자가 역할 또는 서비스에 처음으로 액세스한 날짜와 시간입니다.|  
|**LastSeen**|사용자가 역할 또는 서비스에 마지막으로 액세스한 날짜와 시간입니다.|  
|**ProductName**|UAL 데이터를 제공하는 상위 소프트웨어 제품의 이름(예: Windows)입니다.|  
|**RoleGUID**|UAL에서 할당하거나 등록하는 GUID(서버 역할이나 설치된 제품을 나타냄)입니다.|  
|**RoleName**|UAL 데이터를 제공하는 역할, 구성 요소 또는 하위 제품의 이름입니다. ProductName 및 RoleGUID와도 관련되어 있습니다.|  
|**TenantIdentifier**|설치된 역할의 테넌트 클라이언트 또는 UAL 데이터를 포함하는 제품의 고유한 GUID(해당하는 경우)입니다.|  
  
다음과 같은 장치 관련 데이터가 UAL에서 기록됩니다.  
  
|data|설명|  
|--------|---------------|  
|**IPAddress**|역할 또는 서비스에 액세스하는 데 사용되는 클라이언트 장치의 IP 주소입니다.|  
|**ActivityCount**|특정 장치가 역할이나 서비스에 액세스한 횟수입니다.|  
|**FirstSeen**|IP 주소가 처음으로 역할 또는 서비스에 액세스하는 데 사용된 날짜와 시간입니다.|  
|**LastSeen**|IP 주소가 마지막으로 역할 또는 서비스에 액세스하는 데 사용된 날짜와 시간입니다.|  
|**ProductName**|UAL 데이터를 제공하는 상위 소프트웨어 제품의 이름(예: Windows)입니다.|  
|**RoleGUID**|UAL에서 할당하거나 등록하는 GUID(서버 역할이나 설치된 제품을 나타냄)입니다.|  
|**RoleName**|UAL 데이터를 제공하는 역할, 구성 요소 또는 하위 제품의 이름입니다. ProductName 및 RoleGUID와도 관련되어 있습니다.|  
|**TenantIdentifier**|설치된 역할의 테넌트 클라이언트 또는 UAL 데이터를 포함하는 제품의 고유한 GUID(해당하는 경우)입니다.|  
  
## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항  
UAL은 Windows Server 2012 이후 버전의 Windows Server를 실행 하는 컴퓨터에서 사용할 수 있습니다.  
  
## <a name="see-also"></a>참조  
MSDN의[사용자 액세스 로깅](https://msdn.microsoft.com/library/windows/desktop/hh437528(v=vs.85).aspx)  
[관리 사용자 액세스 로깅](Manage-User-Access-Logging.md)  
  

