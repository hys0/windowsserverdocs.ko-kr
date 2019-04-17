---
ms.assetid: ab97948a-c434-48f2-8313-c1a7a518e5f7
title: "독립 실행형 Federation 서버 만들기"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: fd075c5b7d1bfce89cc27c4917a016e7e5037ce5
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-stand-alone-federation-server"></a>독립 실행형 Federation 서버 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Federation 서비스 역할을 설치 하 고 컴퓨터에 필요한 인증서를 구성 후 컴퓨터를 federation 서버 구성 준비가 됩니다. 다음 절차 stand\만 federation 서버 될 수 있는 컴퓨터를 설정 하려면 사용할 수 있습니다. 또한 stand\만 federation 서버를 만드는 새로운 Federation 서비스를 만듭니다. Federation 서버 AD FS Federation 서버 구성 마법사를 받아서 만든 수행 합니다.  
  
> [!NOTE]  
> 웹 Single\-Sign\-On 연방 \(SSO\) 디자인에 대 한 계정 파트너 조직에서 하나 이상의 federation 서버 및 리소스 파트너 조직에서 하나 이상의 federation 서버 있어야 합니다. 자세한 내용은 참조 [위치 Federation 서버를](https://technet.microsoft.com/library/dd807127.aspx)합니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) \ (http:///\/ go.microsoft.com\/fwlink\/있나요? LinkId\ 83477\ =).   
  
### <a name="to-create-a-stand-alone-federation-server"></a>Stand\만 federation 서버를 만들려면  
  
1.  두 가지 방법으로 AD FS Federation 서버 구성 마법사를 시작 합니다. 마법사를 시작 하려면 다음 중 하나를 수행 합니다.  
  
    -   Federation 서비스 역할 서비스 설치가 완료 되 면에서 snap\ AD FS 관리 열고 클릭는 **광고 FS Federation 서버 구성 마법사** 에 연결는 **개요** 페이지 또는 **작업** 창 합니다.  
  
    -   언제 든 지 설치 마법사를 완료 한 개방형 Windows 탐색기 되 면 탐색 하는 **C:\\Windows\\ADFS** 폴더 double\ 클릭 한 다음 **FsConfigWizard.exe**합니다.  
  
2.  에 **시작** 페이지에서 다음을 확인 **새 Federation 서비스 만들기** 을 선택한 다음 클릭 **다음**합니다.  
  
3.  에 **선택 Stand\ 번만 또는 농장 배포** 페이지, 클릭 **Stand\만 federation 서버**을 차례로 클릭 하 고 **다음**합니다.  
  
    > [!IMPORTANT]  
    > AD FS Federation 서버 구성 마법사에서 Stand\만 federation 서버 옵션을 선택 하면이 Federation 서비스와 관련 된 서비스 계정은 서비스 네트워크 계정에 자동으로 지정 됩니다. ADFS 테스트 랩 환경에서 평가 하는 있는 경우에는 네트워크 서비스를 사용 하 여 서비스 계정으로만 것이 좋습니다. 생산 환경에서 federation 서버 배포할 수만 Stand\ federation 서버 옵션을 사용 하려는 경우에이 서비스 계정을 전용이 새로운 Federation 서비스에 대 한 요청을 처리으로 사용할 수 있는 더 적합 한 서비스 계정으로 변경 하는 것이 중요 합니다. 네트워크 서비스 이외의 다른 계정으로 서비스 계정을 변경는 그렇지 않으면 해당 federation 서버에 취약 해질 악의적인 공격 공격 도구로 줄일 수 있습니다.  
  
4.  에 **해당 Federation 서비스 이름을 지정** 페이지에서 다음을 확인는 **SSL 인증서** 올바른 표시 되는 합니다. 그렇지 않은 경우에서 적절 한 인증서 선택는 **SSL 인증서** 목록입니다.  
  
    기본 웹 사이트에 대 한 주소 \(SSL\) 설정에서이 인증서를 생성 됩니다. 기본 웹 사이트 구성 하나만 SSL 인증서 있으면 해당 인증서 제공 하 고 사용 하기 위해 자동으로 선택 합니다. 여러 개의 SSL 인증서를 기본 웹 사이트에 대 한 구성 된 경우 이러한 모든 인증서 여기 나열 되 고을 중에서 선택 해야 합니다. 기본 웹 사이트에 대해 구성 되지 SSL 설정을 인 목록 로컬 컴퓨터의 개인 인증서 스토어에서 사용할 수 있는 인증서를 생성 됩니다.  
  
    > [!NOTE]  
    > 마법사가 SSL 인증서 iis 구성 된 인증서를 무시 수 없습니다. 이렇게 하면 의도 모든 SSL 인증서 이전 IIS 구성을 유지 됩니다. 이 제한은 해결 하기 위해 인증서를 제거 하거나 다시 구성 수동으로 IIS Management Console와 수 있습니다.  
  
5.  이미 선택한 ADFS 데이터베이스 있는 경우 홈 그룹의 **기존 광고 FS 구성 데이터베이스 감지** 페이지가 나타납니다. 발생 하는 경우 클릭 **삭제 데이터베이스**을 차례로 클릭 하 고 **다음**합니다.  
  
    > [!CAUTION]  
    > 이 ADFS 데이터베이스의 데이터에에서는 중요 하지 못하도록 프로덕션 federation 서버 그룹에 사용 되지 않는 경우에이 옵션을 선택 합니다.  
  
6.  에 **설정 적용 준비가** 페이지에서 세부 정보를 확인 합니다. 설정을 올바르게 표시를 클릭 **다음** 이러한 설정을 통해 ADFS 구성 시작 합니다.  
  
7.  에 **구성 결과** 페이지에서 검색 결과 검토 합니다. 모든 구성 단계가 완료 되 면 클릭 **닫기** 마법사를 종료 합니다.  
  
## <a name="additional-references"></a>추가 참조  
[Federation 서버 설정 검사:](Checklist--Setting-Up-a-Federation-Server.md)  
  

