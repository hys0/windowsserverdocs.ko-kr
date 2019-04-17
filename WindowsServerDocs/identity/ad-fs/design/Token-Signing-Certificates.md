---
ms.assetid: 98c5ef45-2bcb-4f87-86c8-5ac6c16a6097
title: "토큰 서명 인증서"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 84e106ec87861960d7de651b4aaa0e88c952aa79
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="token-signing-certificates"></a>토큰 서명 인증서

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Federation 서버 변경 하거나 보안 토큰 연합된 리소스에는 무단 액세스 하기 위해에서 위조 악의적인 token\ 서명 인증서 필요 합니다. 즉 페어링 private\ 월 공개 키 token\ 서명 인증서를 사용 하는 가장 중요 한 유효성 검사 메커니즘 모든 연합된 간 산학 협동의 보안 토큰 유효한 파트너 federation 서버에서 발급 되었습니다 및 토큰 전송 중 수정 되지 않았습니다 이러한 키를 확인 하기 때문에.  
  
## <a name="token-signing-certificate-requirements"></a>Token\ 서명 인증서 요구 사항  
Token\ 서명 인증서 ADFS 작업할 다음 요구 사항을 충족 해야 합니다.  
  
-   보안 토큰 성공적으로 로그인 하는 token\ 서명 인증서를 token\ 서명 인증서 개인 키가 있어야 합니다.  
  
-   ADFS 서비스 계정 로컬 컴퓨터의 개인 스토어에서 개인 키 token\ 서명 인증서에 액세스할 수 있어야 합니다. 이의 처리 하 여 설치 합니다. 또한 이후에 token\ 서명 인증서를 변경 하면이 액세스할 수 있도록 snap\에서 AD FS 관리를 사용할 수 있습니다.  
  
> [!NOTE]  
> 것 공개 키 인프라 \(PKI\) 가장 좋은 방법은 여러 용도로 개인 키를 공유 하지에 있습니다. 따라서로 token\ 서명 인증서에 설치 된 서비스 통신 인증서를 사용 하지 마십시오.  
  
## <a name="how-token-signing-certificates-are-used-across-partners"></a>파트너 전체 token\ 서명 인증서를 사용 하는 방법  
모든 token\ 서명 인증서 개인 암호화 키와에 디지털 서명 하는 데 사용 되는 공개 키를 포함 \ (개인 key\)을 통해 보안 토큰 합니다. 나중에 파트너 federation 서버 받은, 후 이러한 키의 유효성을 검사 신뢰성 \ (공개 key\)를 통해 암호화 보안 토큰 합니다.  
  
각 보안 토큰 계정 파트너가 디지털 서명이 때문에 리소스 파트너 보안 토큰 계정 파트너가 사실 발급 및 수정 되지 않았음을 확인할 수 있습니다. 디지털 서명은 파트너의 token\ 노래 인증서의 공개 키 부분으로 확인 됩니다. 서명이 확인 한 후 리소스 federation 서버 해당 조직에 대 한 보안 토큰 생성 하 고 고유한 token\ 서명 인증서를 보안 토큰 서명 합니다.  
  
Federation 파트너 환경에 대 한 token\ 서명 인증서가는 캘리포니아 하 여 발급 때 있는지 확인 합니다.  
  
1.  인증서 인증서 해지 목록을 \(CRLs\)는 신뢰 당사자 및 federation 서버 신뢰 하는 웹 서버에 액세스할 수 있습니다.  
  
2.  캘리포니아 루트 인증서 신뢰 당사자 및 federation 서버 신뢰 하는 웹 서버에서 신뢰할 수 있습니다.  
  
리소스 파트너의 웹 서버 token\ 서명 인증서 공개 키를 사용 하 여 보안 토큰 리소스 federation 서버에 의해 서명 되었는지 확인 합니다. 다음 웹 서버 클라이언트에 적절 한 액세스할 수 있게합니다.  
  
## <a name="deployment-considerations-for-token-signing-certificates"></a>배포 고려 token\ 서명 인증서에 대 한  
새로운 ADFS 설치의 첫 번째 federation 서버를 배포 token\ 서명 인증서를 얻는 하 고 해당 federation 서버에서 로컬 컴퓨터 개인 인증서 스토어에서 설치 해야 합니다. Token\ 서명 받을 수 있는 엔터프라이즈의 요청으로 인증서 캘리포니아 또는 공개 캘리포니아 또는 self\ 서명 인증서를 만들고 있습니다.  
  
ADFS 농장 배포할 때 token\ 서명 인증서 서버 팜 만드는 방법에 따라 다르게 설치 됩니다.  
  
배포에 대 한 token\ 서명 인증서를 얻는 경우 고려할 수 있는 팜 옵션 서버 두 가지가 있습니다.  
  
-   개인 키 하나 token\ 서명 인증서를 농장의 모든 federation 서버 간에 공유 됩니다.  
  
    Federation 서버 농장 환경에서 모든 federation 서버 \(or reuse\) 동일한 token\ 서명 인증서를 공유 하는 것이 좋습니다. 캘리포니아 federation 서버에에서 단일 token\ 서명 인증서를 설치 하 고 발급 된 인증서를 내보낼는으로 개인 키를 누른 다음 내보내기 수 있습니다.  
  
    다음 그림와 같이 농장의 모든 federation 서버에 개인 키 단일 token\ 서명 인증서를 공유할 수 있습니다. 이 옵션을 다음 "고유한 token\ 서명 인증서"에 비해 많음 옵션-공개 캘리포니아에서 token\ 서명 인증서를 얻는 하려는 경우 비용을 절감 됩니다.  
  
![토큰 서명](media/adfs2_fedserver_certstory_3.gif)  
  
-   농장의 각 federation 서버에 대 한 고유한 token\ 서명 인증서가 있습니다.  
  
    여러를 사용 하면 해당 농장의 각 서버에 농장 전체 고유한 인증서 고유한 개인 키로 토큰 서명 합니다.  
  
    다음 그림와 같이 그룹의 모든 단일 federation 서버에 대 한 별도 token\ 서명 인증서를 얻을 수 있습니다. 이 옵션은 공개 캘리포니아에서 token\ 서명 인증서를 얻는 하려는 경우 저렴 합니다.  
  
![토큰 서명](media/adfs2_fedserver_certstory_4.gif)  
  
캘리포니아 엔터프라이즈도 Microsoft 인증서 서비스를 사용 하면 인증서를 설치에 대 한 정보를 참조 하세요. [IIS 7.0: 도메인 서버 인증서 IIS 7.0에서 만들기](https://go.microsoft.com/fwlink/?LinkId=108548)합니다.  
  
공용 캐나다의 인증서를 설치에 대 한 정보를 참조 하세요. [IIS 7.0: 인터넷 서버 인증서를 요청](https://go.microsoft.com/fwlink/?LinkId=108549)합니다.  
  
Self\ 서명 인증서를 설치에 대 한 정보를 참조 하세요. [IIS 7.0: Self\-Signed 서버 인증서 IIS 7.0에서 만들기](https://go.microsoft.com/fwlink/?LinkID=108271)합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
