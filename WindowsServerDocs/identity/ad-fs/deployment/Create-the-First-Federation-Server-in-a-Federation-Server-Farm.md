---
ms.assetid: 5e334c4e-75a7-453c-83e8-5ab4243cc685
title: "첫 번째 Federation 서버 Federation 서버 팜에서 만들기"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: af0aa61f0d16d4ca567b140c95d74445d09f1cf3
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="create-the-first-federation-server-in-a-federation-server-farm"></a>첫 번째 Federation 서버 Federation 서버 팜에서 만들기

 >적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Federation 서비스 역할을 설치 하 고 컴퓨터에 필요한 인증서를 구성 후 컴퓨터를 federation 서버 구성 준비가 됩니다. 다음 절차 컴퓨터를 사용 하 여 광고 FS Federation 서버 구성 마법사 새 federation 서버 팜의 첫 번째 federation 서버 설정에 사용할 수 있습니다.  
  
농장의 첫 번째 federation 서버를 만드는 새 Federation 서비스를 만들고이 컴퓨터의 기본 federation 서버는 합니다. 즉,이 컴퓨터는 ADFS 구성 데이터베이스 read\/쓰기 복사본으로 구성 됩니다. 이 그룹에 다른 모든 federation 서버 로컬로 저장 하는 ADFS 구성 데이터베이스 read\ 전용 복사본 기본 federation 서버에서 변경 내용이 복제 해야 합니다. 이 복제 프로세스에 대 한 자세한 내용은 참조 [AD FS 구성 데이터베이스의 The 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)합니다.  
  
> [!NOTE]  
> 웹 Single\-Sign\-On 연방 \(SSO\) 디자인에 대 한 계정 파트너 조직에서 하나 이상의 federation 서버 및 리소스 파트너 조직에서 하나 이상의 federation 서버 있어야 합니다. 자세한 내용은 참조 [위치 Federation 서버를](https://technet.microsoft.com/library/dd807127.aspx)합니다.  
  
도메인 관리자 또는 쓰기 프로그램 데이터 컨테이너 Active Directory에 대 한 액세스 권한이 부여 된 위임된 도메인 계정에 등록이이 절차를 수행 하는 데 필요한 최소입니다.  
  
### <a name="to-create-the-first-federation-server-in-a-federation-server-farm"></a>Federation 서버 농장의 첫 번째 federation 서버를 만들려면  
  
1.  두 가지 방법으로 AD FS Federation 서버 구성 마법사를 시작 합니다. 마법사를 시작 하려면 다음 중 하나를 수행 합니다.  
  
    -   Federation 서비스 역할 서비스 설치가 완료 되 면에서 snap\ AD FS 관리 열고 클릭는 **광고 FS Federation 서버 구성 마법사** 에 연결는 **개요** 페이지 또는 **작업** 창 합니다.  
  
    -   설치 마법사를 완료 한 개방형 Windows 탐색기, 후 언제 든 지 탐색 하 고 **C:\\Windows\\ADFS** 폴더 double\ 클릭 한 다음 **FsConfigWizard.exe**합니다.  
  
2.  에 **시작** 페이지에서 다음을 확인 **새 Federation 서비스 만들기** 을 선택한 다음 클릭 **다음**합니다.  
  
3.  에 **선택 Stand\ 번만 또는 농장 배포** 페이지, 클릭 **새 federation 서버 팜**을 차례로 클릭 하 고 **다음**합니다.  
  
4.  에 **해당 Federation 서비스 이름을 지정** 페이지에서 다음을 확인는 **SSL 인증서** 올바른 표시 되는 합니다. 올바른 인증서 없는 경우 해당 인증서를 선택는 **SSL 인증서** 목록입니다.  
  
    기본 웹 사이트에 대 한 주소 \(SSL\) 설정에서이 인증서를 생성 됩니다. 기본 웹 사이트 구성 하나만 SSL 인증서 있으면 해당 인증서 제공 하 고 사용 하기 위해 자동으로 선택 합니다. 여러 개의 SSL 인증서를 기본 웹 사이트에 대 한 구성 된 경우 이러한 모든 인증서 여기 나열 되 고을 중에서 선택 해야 합니다. 기본 웹 사이트에 대해 구성 되지 SSL 설정을 인 목록 로컬 컴퓨터의 개인 인증서 스토어에서 사용할 수 있는 인증서를 생성 됩니다.  
  
    > [!NOTE]  
    > 마법사가 SSL 인증서 iis 구성 된 인증서를 무시 수 없습니다. 이렇게 하면 의도 모든 SSL 인증서 이전 IIS 구성을 유지 됩니다. 이 제한은 해결 하기 위해 인증서를 제거 하거나 IIS Management Console로 수동으로 재구성 수 있습니다.  
  
5.  이미 선택한 ADFS 데이터베이스 있는 경우 홈 그룹의 **기존 광고 FS 구성 데이터베이스 감지** 페이지가 나타납니다. 이 페이지에 표시 되 면 클릭 **삭제 데이터베이스**을 차례로 클릭 하 고 **다음**합니다.  
  
    > [!CAUTION]  
    > 이 ADFS 데이터베이스의 데이터에에서는 중요 하지 못하도록 프로덕션 federation 서버 그룹에 사용 되지 않는 경우에이 옵션을 선택 합니다.  
  
6.  에 **서비스 계정을 지정** 페이지, 클릭 **찾아보기**합니다. 에 **찾아보기** 대화 상자를 찾아 서비스 계정에서이 새 federation 서버 팜으로 사용할 수 있는 클릭 한 다음 도메인 계정을 **확인**합니다. 이 계정에 대 한 암호를 입력을 확인을 클릭 한 다음 **다음**합니다.  
  
    > [!NOTE]  
    > 참조 [수동으로 서비스 계정을 Federation 서버 팜에 대 한 구성](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md) 지정 federation 서버 팜에 대 한 서비스 계정에 대 한 자세한 내용은 합니다. 각 federation 서버에 federation 서버 팜 같은 서비스 계정을 그룹이 작동 하려면 지정 해야 합니다. 예를 들어, contoso\\ADFS2SVC 서비스 계정을 만든 경우 federation 서버 역할을 구성 하 고 하는 동일한 팜에 참여 하는 각 컴퓨터 해야 contoso\\ADFS2SVC이이 단계에서 작동 하려면 그룹에 대 한 Federation 서버 구성 마법사에서 지정 됩니다.  
  
7.  에 **설정 적용 준비가** 페이지에서 세부 정보를 확인 합니다. 설정을 올바르게 표시를 클릭 **다음** 이러한 설정을 통해 ADFS 구성 시작 합니다.  
  
8.  에 **구성 결과** 페이지에서 검색 결과 검토 합니다. 모든 구성 단계가 완료 되 면 클릭 **닫기** 마법사를 종료 합니다.  
  
    > [!IMPORTANT]  
    > 안전 하 게 배포를 위해 광고 FS Federation 서버 구성 마법사를 사용 하 여 federation 서버 농장 구성 아티팩트 해상도 및 회신 감지 사용 되지 않습니다. 이 마법사를 자동으로 서비스 구성 데이터를 저장 하기 위한 Windows 내부 데이터베이스 구성 합니다. 하지만 중 하나를 사용 하 여 아티팩트 해상도 끝점을 사용 하 여 이러한 변경 실수로 취소할, 수도 있는 **끝점** 노드 snap\에서 AD FS 관리 또는에서 Windows PowerShell cmdlet Enable\ ADFSEndpoint 합니다. 하지 federation 서버 팜와 Windows 내부 데이터베이스를 함께 사용할 때이 끝점 사용할 수 없는 되지 않도록 기본 설정을 다시 구성 주의 해야 합니다.  
  
## <a name="additional-references"></a>추가 참조  
[Federation 서버 설정 검사:](Checklist--Setting-Up-a-Federation-Server.md)  
  

