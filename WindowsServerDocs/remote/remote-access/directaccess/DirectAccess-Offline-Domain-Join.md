---
title: DirectAccess 오프라인 도메인 가입
description: 이 가이드에서는 Windows Server 2016에서 DirectAccess를 사용 하 여 오프 라인 도메인 가입을 수행 하는 단계를 설명 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 55528736-6c19-40bd-99e8-5668169ef3c7
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 229e2955c7f382ff630829990a9dd6485d62652e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388880"
---
# <a name="directaccess-offline-domain-join"></a>DirectAccess 오프라인 도메인 가입

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 가이드에서는 DirectAccess를 사용 하 여 오프 라인 도메인 가입을 수행 하는 단계를 설명 합니다. 오프 라인 도메인 가입 중에 컴퓨터는 물리적 또는 VPN 연결 없이 도메인에 가입 하도록 구성 됩니다.  
  
이 가이드에는 다음 섹션이 수록되어 있습니다.  
  
- 오프 라인 도메인 가입 개요  
  
- 오프 라인 도메인 가입을 위한 요구 사항
  
- 오프 라인 도메인 가입 프로세스
  
- 오프 라인 도메인 가입을 수행 하는 단계  
  
## <a name="offline-domain-join-overview"></a>오프 라인 도메인 가입 개요  
Windows Server 2008 r 2에 도입 된 도메인 컨트롤러에는 오프 라인 도메인 가입 이라는 기능이 포함 되어 있습니다. 이름이 ecluster.exe 인 명령줄 유틸리티를 사용 하면 도메인 가입 작업을 완료 하는 동안 도메인 컨트롤러에 실제로 연결 하지 않고도 도메인에 컴퓨터를 연결할 수 있습니다. 다음은 일반적으로 다음과 같은 작업을 수행 하는 단계입니다.  
  
1.  **Vjoin/프로 비전** 을 실행 하 여 컴퓨터 계정 메타 데이터를 만듭니다. 이 명령의 출력은 base-64로 인코딩된 blob을 포함 하는 .txt 파일입니다.  
  
2.  **/RequestODJ** 를 실행 하 여 .txt 파일의 컴퓨터 계정 메타 데이터를 대상 컴퓨터의 Windows 디렉터리에 삽입 합니다.  
  
3.  대상 컴퓨터를 다시 부팅 하면 컴퓨터가 도메인에 가입 됩니다.  
  
### <a name="BKMK_ODJOverview"></a>DirectAccess 정책을 사용한 오프 라인 도메인 가입 시나리오 개요  
DirectAccess 오프 라인 도메인 가입은 Windows Server 2016, Windows Server 2012, Windows 10 및 Windows 8을 실행 하는 컴퓨터에서를 사용 하 여 회사 네트워크에 실제로 가입 하거나 VPN을 통해 연결 하지 않고도 도메인에 가입할 수 있는 프로세스입니다. 따라서 회사 네트워크에 연결 되지 않은 위치에서 도메인에 컴퓨터를 가입 시킬 수 있습니다. DirectAccess에 대 한 오프 라인 도메인 조인은 원격 프로 비전을 허용 하는 DirectAccess 정책을 클라이언트에 제공 합니다.  
  
도메인 조인은 컴퓨터 계정을 만들고 Windows 운영 체제와 Active Directory 도메인을 실행 하는 컴퓨터 간의 트러스트 관계를 설정 합니다.  
  
## <a name="BKMK_ODJRequirements"></a>오프 라인 도메인 가입 준비  
  
1.  컴퓨터 계정을 만듭니다.  
  
2.  컴퓨터 계정이 속한 모든 보안 그룹의 멤버 자격을 인벤토리에 넣습니다.  
  
3.  새 클라이언트에 적용할 필수 컴퓨터 인증서, 그룹 정책 및 그룹 정책 개체를 수집 합니다.  
  
을 선택합니다. 다음 섹션에서는 node.js를 사용 하 여 DirectAccess 오프 라인 도메인 가입을 수행 하기 위한 운영 체제 요구 사항 및 자격 증명 요구 사항에 대해 설명 합니다.  
  
### <a name="operating-system-requirements"></a>운영 체제 요구 사항  
Windows Server 2016, Windows Server 2012 또는 Windows 8을 실행 하는 컴퓨터 에서만 DirectAccess에 대해 node.js를 실행할 수 있습니다. Node.js를 실행 하 여 컴퓨터 계정 데이터를 AD DS에 프로 비전 하는 컴퓨터는 Windows Server 2016, Windows 10, Windows Server 2012 또는 Windows 8을 실행 해야 합니다. 도메인에 가입 시킬 컴퓨터도 Windows Server 2016, Windows 10, Windows Server 2012 또는 Windows 8을 실행 해야 합니다.  
  
### <a name="credential-requirements"></a>자격 증명 요구 사항  
오프 라인 도메인 가입을 수행 하려면 워크스테이션을 도메인에 가입 시키는 데 필요한 권한이 있어야 합니다. Domain Admins 그룹의 구성원에 게는 기본적으로 이러한 권한이 있습니다. Domain Admins 그룹의 구성원이 아닌 경우 domain Admins 그룹의 구성원은 다음 작업 중 하나를 완료 하 여 워크스테이션을 도메인에 가입 시킬 수 있도록 해야 합니다.  
  
-   그룹 정책를 사용 하 여 필요한 사용자 권한을 부여 합니다. 이 방법을 사용 하면 기본 컴퓨터 컨테이너와 나중에 생성 된 OU (조직 구성 단위)에 컴퓨터를 만들 수 있습니다 (거부 된 Ace (액세스 제어 항목)이 추가 되지 않은 경우).  
  
-   도메인에 대 한 기본 컴퓨터 컨테이너의 ACL (액세스 제어 목록)을 편집 하 여 올바른 사용 권한을 사용자에 게 위임 합니다.  
  
-   OU를 만들고 해당 OU에 대 한 ACL을 편집 하 여 **자식 허용 만들기** 권한을 부여 합니다. **/Wvou** 매개 변수를 **vjoin/프로 비전** 명령에 전달 합니다.  
  
다음 절차에서는 그룹 정책에 대 한 사용자 권한을 부여 하는 방법과 적절 한 권한을 위임 하는 방법을 보여 줍니다.  
  
#### <a name="granting-user-rights-to-join-workstations-to-the-domain"></a>도메인에 워크스테이션을 가입 시킬 수 있는 사용자 권한 부여  
GPMC (그룹 정책 관리 콘솔)를 사용 하 여 도메인 정책을 수정 하거나 도메인에 워크스테이션을 추가할 수 있는 권한을 사용자에 게 부여 하는 설정이 있는 새 정책을 만들 수 있습니다.  
  
사용자 권한을 부여 하려면 최소한 **Domain Admins**의 구성원 이거나 이와 동등한 자격이 필요 합니다.  [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) 에서 적절 한 계정 및 그룹 구성원 자격 사용에 대 한 세부 정보를 검토 합니다 (https://go.microsoft.com/fwlink/?LinkId=83477) ).   
  
###### <a name="to-grant-rights-to-join-workstations-to-a-domain"></a>워크스테이션을 도메인에 가입 시킬 수 있는 권한을 부여 하려면  
  
1.  **시작**, **관리 도구**를 차례로 클릭 한 다음 **그룹 정책 관리**를 클릭 합니다.  
  
2.  포리스트의 이름을 두 번 클릭 하 고 **도메인**을 두 번 클릭 한 다음 컴퓨터에 가입 시킬 도메인의 이름을 두 번 클릭 하 고 **기본 도메인 정책**을 마우스 오른쪽 단추로 클릭 한 다음 **편집**을 클릭 합니다.  
  
3.  콘솔 트리에서 **컴퓨터 구성**을 두 번 클릭 하 고 **정책**을 두 번 클릭 한 다음 **Windows 설정**을 두 번 클릭 하 고 **보안 설정**, **로컬 정책**을 차례로 두 번 클릭 한 후 다음을 두 번 클릭 **합니다. 사용자 권한 할당**.  
  
4.  세부 정보 창에서 **도메인에 워크스테이션 추가**를 두 번 클릭 합니다.  
  
5.  **이 정책 설정 정의** 확인란을 선택 하 고 **사용자 또는 그룹 추가**를 클릭 합니다.  
  
6.  사용자에 게 권한을 부여 하려는 계정 이름을 입력 하 고 **확인** 을 두 번 클릭 합니다.  
  
## <a name="BKMK_ODKSxS"></a>오프 라인 도메인 가입 프로세스  
관리자 권한 명령 프롬프트에서 node.js를 실행 하 여 컴퓨터 계정 메타 데이터를 프로 비전 합니다. 프로 비전 명령을 실행 하면 컴퓨터 계정 메타 데이터가 명령의 일부로 지정 된 이진 파일에 생성 됩니다.  
  
오프 라인 도메인 가입 중에 컴퓨터 계정을 프로 비전 하는 데 사용 되는 NetProvisionComputerAccount 함수에 대 한 자세한 내용은 [NetProvisionComputerAccount 함수](https://go.microsoft.com/fwlink/?LinkId=162426) (https://go.microsoft.com/fwlink/?LinkId=162426) 을 참조 하세요. 대상 컴퓨터에서 로컬로 실행 되는 Netrequest외부 Domainjoin 함수에 대 한 자세한 내용은 [Netrequestststdomainjoin 함수](https://go.microsoft.com/fwlink/?LinkId=162427) (https://go.microsoft.com/fwlink/?LinkId=162427) 을 참조 하세요.  
  
## <a name="BKMK_ODJSteps"></a>DirectAccess 오프 라인 도메인 가입을 수행 하는 단계  
오프 라인 도메인 가입 프로세스에는 다음 단계가 포함 됩니다.  
  
1.  각 원격 클라이언트에 대 한 새 컴퓨터 계정을 만들고 회사 네트워크에 있는 이미 도메인에 가입 된 컴퓨터의. n e x 명령을 사용 하 여 프로 비전 패키지를 생성 합니다.  
  
2.  클라이언트 컴퓨터를 DirectAccessClients 보안 그룹에 추가 합니다.  
  
3.  프로 비전 패키지를 도메인에 가입 하는 원격 컴퓨터에 안전 하 게 전송 합니다.  
  
4.  프로 비전 패키지를 적용 하 고 클라이언트를 도메인에 가입 시킵니다.  
  
5.  클라이언트를 다시 부팅 하 여 도메인 가입을 완료 하 고 연결을 설정 합니다.  
  
클라이언트에 대 한 프로 비전 패킷을 만들 때 고려해 야 할 두 가지 옵션이 있습니다. 시작 마법사를 사용 하 여 PKI 없이 DirectAccess를 설치한 경우 아래 옵션 1을 사용 해야 합니다. 고급 설치 마법사를 사용 하 여 PKI를 사용 하 여 DirectAccess를 설치한 경우 아래 옵션 2를 사용 해야 합니다.  
  
오프 라인 도메인 가입을 수행 하려면 다음 단계를 완료 합니다.  
  
##### <a name="option1-create-a-provisioning-package-for-the-client-without-pki"></a>옵션 1: PKI 없이 클라이언트에 대 한 프로 비전 패키지 만들기  
  
1.  원격 액세스 서버의 명령 프롬프트에서 다음 명령을 입력 하 여 컴퓨터 계정을 프로 비전 합니다.  
  
    ```  
    Djoin /provision /domain <your domain name> /machine <remote machine name> /policynames DA Client GPO name /rootcacerts /savefile c:\files\provision.txt /reuse  
    ```  
  
##### <a name="option2-create-a-provisioning-package-for-the-client-with-pki"></a>옵션 2 마이그레이션 PKI를 사용 하 여 클라이언트용 프로 비전 패키지 만들기  
  
1.  원격 액세스 서버의 명령 프롬프트에서 다음 명령을 입력 하 여 컴퓨터 계정을 프로 비전 합니다.  
  
    ```  
    Djoin /provision /machine <remote machine name> /domain <Your Domain name> /policynames <DA Client GPO name> /certtemplate <Name of client computer cert template> /savefile c:\files\provision.txt /reuse  
    ```  
  
##### <a name="add-the-client-computer-to-the-directaccessclients-security-group"></a>클라이언트 컴퓨터를 DirectAccessClients 보안 그룹에 추가 합니다.  
  
1.  도메인 컨트롤러의 **시작** 화면에서 **Active** 를 입력 하 고 **앱** 에서 **사용자 및 컴퓨터 Active Directory** 화면을 선택 합니다.  
  
2.  도메인 아래의 트리를 확장 하 고 **사용자** 컨테이너를 선택 합니다.  
  
3.  세부 정보 창에서 **Directaccessclients**를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 합니다.  
  
4.  **구성원** 탭에서 **추가**를 클릭합니다.  
  
5.  **개체 유형**을 클릭 하 고 **컴퓨터**를 선택한 다음 **확인**을 클릭 합니다.  
  
6.  추가할 클라이언트 이름을 입력 한 다음 **확인**을 클릭 합니다.  
  
7.  **확인** 을 클릭 하 여 **directaccessclients** 속성 대화 상자를 닫은 다음 **Active Directory 사용자 및 컴퓨터**를 닫습니다.  
  
##### <a name="copy-and-then-apply-the-provisioning-package-to-the-client-computer"></a>프로 비전 패키지를 복사 하 여 클라이언트 컴퓨터에 적용 합니다.  
  
1.  C:\files\provision.txt의 프로 비전 패키지를 저장 된 원격 액세스 서버에서 클라이언트 컴퓨터의 c:\provision\provision.txt로 복사 합니다.  
  
2.  클라이언트 컴퓨터에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 입력 하 여 도메인 가입을 요청 합니다.  
  
    ```  
    Djoin /requestodj /loadfile C:\provision\provision.txt /windowspath %windir% /localos  
    ```  
  
3.  클라이언트 컴퓨터를 다시 부팅 합니다. 컴퓨터가 도메인에 가입 됩니다. 다시 부팅 한 후 클라이언트는 도메인에 가입 되 고 DirectAccess를 사용 하 여 회사 네트워크에 연결 됩니다.  
  
## <a name="see-also"></a>관련 항목  
[NetProvisionComputerAccount 함수](https://go.microsoft.com/fwlink/?LinkId=162426)  
[Netrequest외부 Domainjoin 함수](https://go.microsoft.com/fwlink/?LinkId=162427)  
  


