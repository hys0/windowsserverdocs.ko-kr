---
ms.assetid: 6ecf8d85-cd61-4c87-add8-00a679a6e3ff
title: "Federation 서버 Federation 서버 팜을 추가"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: d67f4c252ad25a05f11b88771f12fd01d13137d4
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="add-a-federation-server-to-a-federation-server-farm"></a>Federation 서버 Federation 서버 팜을 추가

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Federation 서비스 역할을 설치 하 고 컴퓨터에 필요한 인증서를 구성 후 컴퓨터를 federation 서버 구성 준비가 됩니다. 다음 절차는 컴퓨터에 새 federation 서버 팜 참가를 사용할 수 있습니다.  
  
컴퓨터 AD FS Federation 서버 구성 마법사 팜에 가입입니다. 이 마법사는 컴퓨터에는 기존 농장 참가를 사용 하 여 컴퓨터를 read\ 전용 ADFS 구성 데이터베이스의로 구성 하 고 기본 federation 서버에서 업데이트를 받을 해야 합니다.  
  
> [!NOTE]  
> 웹 Single\-Sign\-On 연방 \(SSO\) 디자인에 대 한 계정 파트너 조직에서 하나 이상의 federation 서버 및 리소스 파트너 조직에서 하나 이상의 federation 서버 있어야 합니다. 자세한 내용은 참조 [위치 Federation 서버를](https://technet.microsoft.com/library/dd807127.aspx)합니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) \ (http:///\/ go.microsoft.com\/fwlink\/있나요? LinkId\ 83477\ =).   
  
### <a name="to-add-a-federation-server-to-a-federation-server-farm"></a>Federation 서버 federation 서버 팜을 추가 하려면  
  
1.  두 가지 방법으로 AD FS Federation 서버 구성 마법사를 시작 합니다. 마법사를 시작 하려면 다음 중 하나를 수행 합니다.  
  
    -   Federation 서비스 역할 서비스 설치가 완료 되 면에서 snap\ AD FS 관리 열고 클릭는 **광고 FS Federation 서버 구성 마법사** 에 연결는 **개요** 페이지 또는 **작업** 창 합니다.  
  
    -   언제 든 지 설치 마법사를 완료 한 개방형 Windows 탐색기 되 면 탐색 하는 **C:\\Windows\\ADFS** 폴더 및 double\ 클릭 **FsConfigWizard.exe**합니다.  
  
2.  에 **시작** 페이지에서 다음을 확인 **federation 서버 기존 Federation 서비스를 추가** 을 선택한 다음 클릭 **다음**합니다.  
  
3.  이미 선택한 ADFS 데이터베이스 있는 경우 홈 그룹의 **기존 광고 FS 구성 데이터베이스 감지** 페이지가 나타납니다. 발생 하는 경우 클릭 **삭제 데이터베이스**을 차례로 클릭 하 고 **다음**합니다.  
  
    > [!CAUTION]  
    > 이 ADFS 데이터베이스의 데이터에에서는 중요 하지 못하도록 프로덕션 federation 서버 그룹에 사용 되지 않는 경우에이 옵션을 선택 합니다.  
  
4.  에 **주 Federation 서버 및 서비스 계정을 지정** 페이지의 **기본 federation 서버 이름**팜에서 기본 federation 서버의 컴퓨터 이름을 입력 하 고 클릭 한 다음 **찾아보기**합니다. 에 **찾아보기** 대화 상자에서 다른 모든 federation 서버에서 기존 federation 서버 농장 서비스 계정으로 사용 되는 도메인 계정 찾아 누릅니다 **확인**합니다. 암호를 입력 하 고 확인을 클릭 한 다음 **다음**:  
  
    > [!NOTE]  
    > 지정 federation 서버 팜에 대 한 서비스 계정에 대 한 자세한 내용은 참조 [수동으로 서비스 계정을 Federation 서버 팜에 대 한 구성](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md)합니다. 각 federation 서버에 federation 서버 팜 같은 서비스 계정을 그룹이 작동 하려면 지정 해야 합니다. 예를 들어, contoso\\ADFS2SVC 서비스 계정을 만든 경우 각 컴퓨터 federation 서버 역할을 구성 하 고 같은 팜에 참여할 해야 contoso\\ADFS2SVC이이 단계에서 작동 하려면 그룹에 대 한 Federation 서버 구성 마법사에서 지정 됩니다.  
  
5.  에 **설정 적용 준비가** 페이지에서 세부 정보를 확인 합니다. 설정을 올바르게 표시를 클릭 **다음** 이러한 설정을 통해 ADFS 구성 시작 합니다.  
  
6.  에 **구성 결과** 페이지에서 검색 결과 검토 합니다. 모든 구성 단계가 완료 되 면 클릭 **닫기** 마법사를 종료 합니다.  
  
## <a name="additional-references"></a>추가 참조  
[Federation 서버 설정 검사:](Checklist--Setting-Up-a-Federation-Server.md)  
  

