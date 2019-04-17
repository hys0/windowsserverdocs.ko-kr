---
title: "광고 숲 복구 DNS 서버 구성 서비스"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f24570965fd8b3f3e050779c42758865cbee2728
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---configuring-the-dns-server-service"></a>DNS 서버 서비스 구성-광고 숲 복구 

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.
 
DNS 서버 역할 백업에서 복원 DC에 설치 되어 있지 않으면를 설치 하 고 DNS 서버를 구성 해야 합니다.  
  

## <a name="install-and-configure-the-dns-server-service"></a>설치 및 구성 DNS 서버 서비스  
복원이 완료 된 후 DNS 서버가로 실행 하지 않는 복원된 DC 각에 대 한이 단계를 완료 합니다.  
  
> [!NOTE]
>  DC 백업에서 복원 하는 Windows Server 2008 R2을 실행 중인 경우 DNS 서버를 설치 하려면 DC 격리 된 네트워크에 연결 해야 있습니다. 그런 다음 각 복원된 DNS 서버 상호 공유, 격리 된 네트워크에 연결 합니다. Repadmin 실행 /replsum 복원된 DNS 서버 복제가 정상적으로 확인할 수 있습니다. 복제 확인 한 후 DNS 서버 역할이 이미 설치 된 경우 복원된 Dc 프로덕션 네트워크에 연결할 수 있습니다, DNS 서버를 시작 하는 동안 서버 모든 네트워크에 연결 되지 않은 수 있게 해 주는 핫픽스 적용할 수 있습니다. 빌드 자동된 프로세스 동안 운영 체제 설치 이미지에 핫픽스를 slipstream 해야 합니다. 핫픽스에 대 한 자세한 내용은 참조 [975654 문서](https://go.microsoft.com/fwlink/?LinkId=184691) 에 Microsoft 기술 자료 (https://go.microsoft.com/fwlink/?LinkId=184691). 

아래 설치 및 구성 단계를 완료 합니다.
  
### <a name="to-install-and-the-dns-server-service-using-server-manager"></a>설치 및 서버 관리자를 사용 하 여 DNS 서버 서비스를  
  
1.  클릭 하 고 서버 관리자 연 **역할 및 기능을 추가**합니다.  
2.  역할 추가 마법사에서 하는 경우는 **시작 하기 전에** 클릭 페이지가 나타나면 **다음**합니다.  
3.  에 **설치 유형을** 선택 화면 **역할 기반 기능 기반 설치 또는** 클릭 **다음**합니다.
4.  에 **서버 선택** 화면 서버를 선택 하 고 클릭 **다음**합니다.
5.  에 **서버 역할** 선택 화면 **DNS 서버**클릭 메시지가 표시 되 면, **기능 추가** 클릭 **다음**합니다.
6.  에 **기능** 화면 클릭 **다음**합니다.
7.  정보를 읽고 있는 **DNS 서버** 페이지, 클릭 한 다음 한 **다음**합니다.
![DNS 서버](media/AD-Forest-Recovery-Configure-DNS/dns1.png)  
8.  에 **확인** 페이지에서 DNS 서버 역할을 설치를 클릭 한 다음 확인 **설치**합니다.  
  
     
### <a name="to-configure-the-dns-server-service"></a>DNS 서버 서비스 구성 하려면 
1.  서버 관리자를 열을 클릭 **도구** 클릭 **DNS**합니다.
![DNS 서버](media/AD-Forest-Recovery-Configure-DNS/dns2.png)    
2.  중요 한 오작동 전에 DNS 서버에서 된 호스트 하는 동일한 DNS 도메인 이름에 대 한 DNS 영역을 만듭니다. 자세한 내용은 참조 추가 앞 조회 영역이 ([https://go.microsoft.com/fwlink/?LinkId=74574](https://go.microsoft.com/fwlink/?LinkId=74574)).  
3.  중요 한 오작동 전의 DNS 데이터 구성 합니다. 예를 들어:  
  
    -   DNS AD DS에 저장 되는 영역을 구성 합니다. 자세한 내용은 참조 변경 영역 종류 ([https://go.microsoft.com/fwlink/?LinkId=74579](https://go.microsoft.com/fwlink/?LinkId=74579)).  
  
    -   DNS 도메인 컨트롤러 locator (DC Locator) 수 있도록 리소스 레코드 동적 보안 업데이트를 신뢰할 수 있는 영역을 구성 합니다. 자세한 내용은 참조 허용만 보안 동적 업데이트 ([https://go.microsoft.com/fwlink/?LinkId=74580](https://go.microsoft.com/fwlink/?LinkId=74580)).  
  
4. 부모 DNS 영역 위임 리소스 레코드 (이름을 서버 (NS) 및 리소스 붙이기 호스트 레코드)이 DNS 서버에서 호스트 하는 자녀 영역에 대 한 포함 되어 있는지 확인 합니다. 자세한 내용은 참조 만들기 영역 위임 ([https://go.microsoft.com/fwlink/?LinkId=74562](https://go.microsoft.com/fwlink/?LinkId=74562)).  
5. DNS 구성 하 고 나면 NETLOGON 기록의 등록을 줄일 수 있습니다.  
  
    > [!NOTE]
    >  보안 동적 업데이트 드 서버를 사용할 수 있는 경우에 작동 합니다.  
  
     명령 프롬프트에서 다음 명령을 입력 하 고 enter 다음과 같습니다.  
  
     **Net 중지 netlogon**  
  
6. 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
     **Net 시작 netlogon**  

![DNS 서버](media/AD-Forest-Recovery-Configure-DNS/dns3.png)  

## <a name="next-steps"></a>다음 단계

- [광고 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)
