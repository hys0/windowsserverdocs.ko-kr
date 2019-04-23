---
title: DirectAccess 오프라인 도메인 가입
description: 이 가이드에서는 Windows Server 2016에서 DirectAccess 사용 하 여 오프 라인 도메인 가입을 수행 하는 단계를 설명 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 55528736-6c19-40bd-99e8-5668169ef3c7
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a9cd811c680f15d53ecbd28d9201f28d9cb8af2f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853064"
---
# <a name="directaccess-offline-domain-join"></a>DirectAccess 오프라인 도메인 가입

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 가이드는 DirectAccess 사용 하 여 오프 라인 도메인 가입을 수행 하는 단계를 설명 합니다. 오프 라인 도메인 가입을 하는 동안 컴퓨터는 물리적 컴퓨터 또는 VPN 연결 없이 도메인에 가입 하도록 구성 됩니다.  
  
이 가이드에는 다음 섹션이 수록되어 있습니다.  
  
- 오프 라인 도메인 가입 개요  
  
- 오프 라인 도메인 가입에 대 한 요구 사항
  
- 오프 라인 도메인 가입 프로세스
  
- 오프 라인 도메인 가입을 수행 하기 위한 단계  
  
## <a name="offline-domain-join-overview"></a>오프 라인 도메인 가입 개요  
도메인 컨트롤러가 Windows Server 2008 R2에 도입 된, 오프 라인 도메인 가입 기능을 포함 합니다. Djoin.exe 라는 명령줄 유틸리티를 사용 하면 도메인 가입 작업을 완료 하는 동안 도메인 컨트롤러를 물리적으로 연결 하지 않고 컴퓨터를 도메인에 가입 수 있습니다. Djoin.exe를 사용 하 여 일반적인 단계는 다음과 같습니다.  
  
1.  실행할 **djoin /provision** 컴퓨터 계정 메타 데이터를 만들려고 합니다. 이 명령의 출력은 base-64로 인코딩된 blob을 포함 하는.txt 파일.  
  
2.  실행할 **djoin /requestODJ** .txt 파일의 대상 컴퓨터의 Windows 디렉터리에 컴퓨터 계정 메타 데이터를 삽입 합니다.  
  
3.  대상 컴퓨터를 다시 부팅 하 고 컴퓨터는 도메인에 가입 합니다.  
  
### <a name="BKMK_ODJOverview"></a>DirectAccess 정책 시나리오 개요를 사용 하 여 오프 라인 도메인 가입  
DirectAccess 오프 라인 도메인 가입에는 Windows Server 2016, Windows Server 2012, Windows 10 및 Windows 8을 실행 하는 컴퓨터 사용 하 여 회사 네트워크에 물리적으로 참가 하지 않은 도메인에 가입 하거나 VPN을 통해 연결 하는 프로세스입니다. 따라서 위치에서 컴퓨터를 도메인에 가입 시킬 수 있는 회사 네트워크에 대 한 연결이 없습니다. DirectAccess에 대 한 오프 라인 도메인 가입 원격 프로 비전 할 수 있도록 클라이언트에 DirectAccess 정책을 제공 합니다.  
  
도메인 가입 컴퓨터 계정을 만들고 Active Directory 도메인과 Windows 운영 체제를 실행 하는 컴퓨터 간의 트러스트 관계를 설정 합니다.  
  
## <a name="BKMK_ODJRequirements"></a>오프 라인 도메인 가입에 대 한 준비  
  
1.  컴퓨터 계정을 만듭니다.  
  
2.  인벤토리 할 모든 보안 그룹의 컴퓨터 계정이 속한 멤버 자격.  
  
3.  인증서 필요한 컴퓨터, 그룹 정책 및 새 클라이언트에 적용 될 그룹 정책 개체를 수집 합니다.  
  
. 다음 섹션에서는 운영 체제 요구 사항 및 Djoin.exe를 사용 하 여 DirectAccess 오프 라인 도메인 가입을 수행 하기 위한 자격 증명 요구를 설명 합니다.  
  
### <a name="operating-system-requirements"></a>운영 체제 요구 사항  
Windows Server 2016, Windows Server 2012 또는 Windows 8을 실행 하는 컴퓨터 에서만 directaccess Djoin.exe를 실행할 수 있습니다. Windows Server 2016, Windows 10, Windows Server 2012 또는 Windows 8 실행 하는 Djoin.exe 프로 비전 컴퓨터 계정 데이터를 AD DS에 컴퓨터를 실행 되어야 합니다. 컴퓨터를 도메인에 가입 하려는 Windows Server 2016, Windows 10, Windows Server 2012 또는 Windows 8 실행 되어야 합니다.  
  
### <a name="credential-requirements"></a>자격 증명 요구 사항  
오프 라인 도메인 가입을 수행 하려면 도메인에 워크스테이션을 조인 하는 데 필요한 권한이 있어야 합니다. Domain Admins 그룹의 멤버는 기본적으로 이러한 권한을 갖습니다. Domain Admins 그룹의 멤버에 없는 경우 Domain Admins 그룹의 멤버인 도메인에 워크스테이션을 조인할 수 있도록 다음 작업 중 하나를 완료 해야 합니다.  
  
-   그룹 정책을 사용 하 여 필요한 사용자 권한을 부여 합니다. 이 메서드를 사용 하면 (없습니다 Deny Ace (액세스 제어 항목)는 추가 됨) 하는 경우 나중에 만들어진 모든 조직 구성 단위 (OU)에 기본 컴퓨터 컨테이너에 컴퓨터를 만들 수 있습니다.  
  
-   올바른 권한을 위임 하려면 도메인에 대 한 기본 컴퓨터 컨테이너의 액세스 제어 목록 (ACL)을 편집 합니다.  
  
-   OU를 만들고 편집 하는 권한을 부여 하려면 해당 OU에 대 한 ACL을 **자식 만들기-허용** 권한. 전달 합니다 **/machineOU** 매개 변수를 **djoin /provision** 명령입니다.  
  
다음 절차에는 그룹 정책을 사용 하 여 사용자 권한을 부여 하는 방법 및 올바른 권한을 위임 하는 방법을 보여 줍니다.  
  
#### <a name="granting-user-rights-to-join-workstations-to-the-domain"></a>도메인에 워크스테이션을 조인할 사용자 권한 부여  
그룹 정책 관리 콘솔 (GPMC)를 사용 하 여 도메인 정책을 수정 하거나 사용자에 게 도메인에 워크스테이션 추가 권한을 부여 하는 설정이 포함 된 새 정책 만들기를 수 있습니다.  
  
멤버 자격이 **Domain Admins**, 또는 이와 동등한 사용자 권한을 부여 하는 데 필요한 최소값입니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) (https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
###### <a name="to-grant-rights-to-join-workstations-to-a-domain"></a>도메인에 워크스테이션을 조인 하는 권한을 부여 하려면  
  
1.  클릭 **시작**, 클릭 **관리 도구**를 클릭 하 고 **그룹 정책 관리**합니다.  
  
2.  포리스트의 이름을 두 번 클릭, 두 번 클릭 **도메인**를 마우스 오른쪽 단추로 클릭 하는 컴퓨터를 가입 하려는 도메인 이름을 두 번 **기본 도메인 정책**를 클릭 하 고  **편집**합니다.  
  
3.  콘솔 트리에서 **컴퓨터 구성**를 두 번 클릭 **정책을**를 두 번 클릭 **Windows 설정**를 두 번 클릭 **보안 설정**를 두 번 클릭 **로컬 정책**를 차례로 클릭 한 다음 **사용자 권한 할당**합니다.  
  
4.  세부 정보 창에서 두 번 클릭 **도메인에 워크스테이션 추가**합니다.  
  
5.  선택 된 **이 정책 설정 정의** 확인란을 선택한 다음 클릭 **사용자 또는 그룹 추가**합니다.  
  
6.  사용자 권한을 부여 하 고 클릭 하려는 계정의 이름을 입력 **확인** 두 번입니다.  
  
## <a name="BKMK_ODKSxS"></a>오프 라인 도메인 가입 프로세스  
컴퓨터 계정 메타 데이터를 프로 비전 하려면 관리자 권한 명령 프롬프트에서 Djoin.exe를 실행 합니다. 프로 비전 하는 명령을 실행 하는 경우 컴퓨터 계정 메타 데이터 명령의 일부로 지정 하는 이진 파일에 만들어집니다.  
  
오프 라인 도메인 가입을 하는 동안 컴퓨터 계정을 프로 비전 하는 데 사용 되는 NetProvisionComputerAccount 함수에 대 한 자세한 내용은 참조 하세요. [NetProvisionComputerAccount 함수](https://go.microsoft.com/fwlink/?LinkId=162426) (https://go.microsoft.com/fwlink/?LinkId=162426)합니다. 대상 컴퓨터에서 로컬로 실행 되는 NetRequestOfflineDomainJoin 함수에 대 한 자세한 내용은 참조 하세요. [NetRequestOfflineDomainJoin 함수](https://go.microsoft.com/fwlink/?LinkId=162427) (https://go.microsoft.com/fwlink/?LinkId=162427)합니다.  
  
## <a name="BKMK_ODJSteps"></a>DirectAccess 오프 라인 도메인 가입을 수행 하기 위한 단계  
오프 라인 도메인 가입 프로세스에는 다음 단계가 포함 됩니다.  
  
1.  각 원격 클라이언트에 대 한 새 컴퓨터 계정을 만들고에서 Djoin.exe 명령을 사용 하 여 프로 비전 패키지를 생성을 이미 도메인 회사 네트워크의 컴퓨터를 조인 합니다.  
  
2.  DirectAccessClients 보안 그룹에 클라이언트 컴퓨터를 추가 합니다.  
  
3.  도메인 가입 하는 원격 컴퓨터 (s)에 안전 하 게 프로 비전 패키지를 전송 합니다.  
  
4.  프로 비전 패키지를 적용 하 고 클라이언트를 도메인에 가입 합니다.  
  
5.  도메인 가입을 완료 하 고 연결을 설정 하려면 클라이언트를 다시 부팅 합니다.  
  
두 가지 옵션을 클라이언트에 대 한 프로 비전 패킷을 만들 때 고려해 야 합니다. 시작 마법사를 사용 하는 PKI 없이 DirectAccess를 설치할 경우 1 아래 옵션을 사용 해야 합니다. 고급 설정 마법사를 사용 하는 PKI를 사용 하 여 DirectAccess를 설치할 경우 아래의 옵션 2를 사용 해야 합니다.  
  
오프 라인 도메인 가입을 수행 하려면 다음 단계를 완료 합니다.  
  
##### <a name="option1-create-a-provisioning-package-for-the-client-without-pki"></a>옵션 1: PKI 없이 클라이언트에 대 한 프로 비전 패키지 만들기  
  
1.  원격 액세스 서버의 명령 프롬프트에서 컴퓨터 계정을 프로 비전 하려면 다음 명령을 입력 합니다.  
  
    ```  
    Djoin /provision /domain <your domain name> /machine <remote machine name> /policynames DA Client GPO name /rootcacerts /savefile c:\files\provision.txt /reuse  
    ```  
  
##### <a name="option2-create-a-provisioning-package-for-the-client-with-pki"></a>옵션 2: PKI 사용 하 여 클라이언트에 대 한 프로 비전 패키지 만들기  
  
1.  원격 액세스 서버의 명령 프롬프트에서 컴퓨터 계정을 프로 비전 하려면 다음 명령을 입력 합니다.  
  
    ```  
    Djoin /provision /machine <remote machine name> /domain <Your Domain name> /policynames <DA Client GPO name> /certtemplate <Name of client computer cert template> /savefile c:\files\provision.txt /reuse  
    ```  
  
##### <a name="add-the-client-computer-to-the-directaccessclients-security-group"></a>DirectAccessClients 보안 그룹에 클라이언트 컴퓨터를 추가 합니다.  
  
1.  도메인 컨트롤러에서에서 **시작** 화면에서 입력 **활성** 선택한 **Active Directory Users and Computers** 에서 **앱** 화면 .  
  
2.  도메인에 아래의 트리를 확장 하 고 선택 합니다 **사용자** 컨테이너입니다.  
  
3.  세부 정보 창에서 마우스 오른쪽 단추로 클릭 **DirectAccessClients**, 클릭 **속성**합니다.  
  
4.  **구성원** 탭에서 **추가**를 클릭합니다.  
  
5.  클릭 **개체 유형**를 선택 **컴퓨터**를 클릭 하 고 **확인**합니다.  
  
6.  을 추가 하 고 클릭 한 다음 클라이언트 이름을 입력 **확인**합니다.  
  
7.  클릭 **확인** 닫으려면 합니다 **DirectAccessClients** 속성 대화 상자를 닫은 다음 **Active Directory Users and Computers**합니다.  
  
##### <a name="copy-and-then-apply-the-provisioning-package-to-the-client-computer"></a>복사한 다음 클라이언트 컴퓨터에 프로 비전 패키지 적용  
  
1.  저장 된 위치, c:\provision\provision.txt 클라이언트 컴퓨터에 원격 액세스 서버에서 c:\files\provision.txt에서 프로 비전 패키지를 복사 합니다.  
  
2.  클라이언트 컴퓨터의 관리자 권한 명령 프롬프트를 열고 도메인 가입을 요청 하려면 다음 명령을 입력 합니다.  
  
    ```  
    Djoin /requestodj /loadfile C:\provision\provision.txt /windowspath %windir% /localos  
    ```  
  
3.  클라이언트 컴퓨터를 다시 부팅 합니다. 컴퓨터는 도메인에 가입 됩니다. 다시 부팅 한 다음 클라이언트는 도메인에 가입 됩니다와 DirectAccess 사용 하 여 회사 네트워크에 연결 합니다.  
  
## <a name="see-also"></a>관련 항목  
[NetProvisionComputerAccount 함수](https://go.microsoft.com/fwlink/?LinkId=162426)  
[NetRequestOfflineDomainJoin 함수](https://go.microsoft.com/fwlink/?LinkId=162427)  
  


