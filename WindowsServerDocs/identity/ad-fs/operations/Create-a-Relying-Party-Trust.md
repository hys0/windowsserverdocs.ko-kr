---
ms.assetid: 5b9fc9c1-5d12-4ad4-8ddc-3b8a6d45b217
title: "신뢰 파티 신뢰 만들기"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 14e1cc732ed60b7f05a9a4a9aac9037c48b702f2
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-relying-party-trust"></a>신뢰 파티 신뢰 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

다음 문서를 수동으로 신뢰 파티 신뢰를 만들고 federation 메타 데이터를 사용 하 여 정보를 제공 합니다.
  
## <a name="to-create-a-claims-aware-relying-party-trust-manually"></a>클레임을 만들려면 인식 Relying 파티 신뢰 수동으로 

snap\ AD FS 관리를 사용 하 여 새 신뢰 파티 신뢰를 추가 하 고 설정을 수동으로 구성를 federation 서버에 다음 절차를 수행 합니다.  

회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.
  
1. 서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  아래에서 **작업**, 클릭 **의존 파티 신뢰 추가**합니다.  
![당사자에](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3.  에 **시작** 페이지에서 선택 **인식 클레임** 클릭 **시작**합니다.  
![당사자에](media/Create-a-Relying-Party-Trust/addtrust2.PNG) 
  
4.  에 **데이터 소스를 선택** 페이지, 클릭 **당사자에 대 한 데이터를 직접 입력**을 차례로 클릭 하 고 **다음**합니다.  
![당사자에](media/Create-a-Relying-Party-Trust/addtrust3.PNG) 
  
5.  에 **표시 이름 지정** 페이지에서에 이름을 입력 **표시 이름**, **노트** 이 신뢰 파티 보안에 대 한 설명을 입력 한 다음 **다음**합니다.  
![당사자에](media/Create-a-Relying-Party-Trust/addtrust4.PNG) 

6. 에 **구성 인증서** 페이지, 클릭 옵션 토큰 암호화 인증서가 있는 경우 **검색** 인증서 파일을 찾은 다음을 클릭 하려면 **다음**합니다.  
![당사자에](media/Create-a-Relying-Party-Trust/addtrust5.PNG) 

7.  에 **구성 URL** 페이지를 다음 중 하나 이상을 수행를 클릭 **다음**, 하 고 8 단계로 이동 합니다.  
  
    -   선택는 **WS\ Federation 수동 프로토콜에 대 한 지원을** 확인란을 선택 합니다. 아래에서 **Relying 파티 WS\ Federation 수동 프로토콜 URL**신뢰 파티 신뢰가에 대 한 URL을 입력 한 다음, **다음**합니다.  
  
    -   선택는 **SAML 2.0 WebSSO 프로토콜에 대 한 지원을** 확인란을 선택 합니다. 아래에서 **Relying 파티 SAML 2.0 SSO 서비스 URL**신뢰 파티 신뢰가에 대 한 보안 설정 Markup Language \(SAML\) 서비스 endpoint URL을 입력 한 다음, **다음**합니다.  
![당사자에](media/Create-a-Relying-Party-Trust/addtrust6.PNG)   

8. 에 **구성 식별자** 페이지이 당사자에 대 한 식별자 하나 또는 여러 개의 지정를 클릭 **추가** 목록에 추가를 클릭 한 다음 **다음**합니다.  
![당사자에](media/Create-a-Relying-Party-Trust/addtrust8.PNG)
  
9.  에 **액세스 제어 정책 선택** 정책을 선택 하 고 클릭 **다음**합니다.  액세스 제어 정책에 대 한 자세한 내용은 참조 [adfs에서 액세스 제어 정책을](Access-Control-Policies-in-AD-FS.md)합니다. 
![당사자에](media/Create-a-Relying-Party-Trust/addtrust9.PNG)

10. 에 **추가 보안 준비가** 페이지를 설정을 검토 하 고, 클릭 한 다음 **다음** 당사자에 저장 하려면 정보를 신뢰 합니다.  
   ![당사자에](media/Create-a-Relying-Party-Trust/addtrust10.PNG) 
11. 에 **완료** 페이지, 클릭 **닫기**합니다. 이 작업은 자동으로 표시는 **편집 클레임 규칙** 대화 상자가 합니다.  
![당사자에](media/Create-a-Relying-Party-Trust/addtrust11.PNG) 

## <a name="to-create-a-claims-aware-relying-party-trust-using-federation-metadata"></a>클레임을 만들려면 인식 Relying 파티 신뢰 federation 메타 데이터를 사용 하 여

새로운 신뢰 파티 신뢰를 AD FS 관리 스냅인 federation 메타 데이터를 파트너 게시 로컬 네트워크 또는 인터넷의 파트너에 대 한 구성 데이터를 자동으로 가져오는 방법으로 사용 하 여 추가 계정 파트너 조직에서 federation 서버에 다음 절차를 수행 합니다.

>[!NOTE]
>https://myserver 등 호스트 자격이 없는 이름으로 인증서를 사용 하 여 일반적으로 오랫동안, 있지만 이러한 인증서 보안 값이 없는 및 공격자 가장 federation 메타 데이터를 게시 하는 Federation 서비스를 사용 하도록 설정할 수 있습니다. 따라서 federation 메타 데이터를 쿼리를 https://myserver.contoso.com 등 정식된 도메인 이름을 사용만 해야 합니다.

회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.


1. 서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  아래에서 **작업**, 클릭 **의존 파티 신뢰 추가**합니다.  
![당사자에](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3.  에 **시작** 페이지에서 선택 **인식 클레임** 클릭 **시작**합니다.  
![당사자에](media/Create-a-Relying-Party-Trust/addtrust2.PNG) 
  
4.  에 **선택 데이터 소스** 페이지, 클릭 **당사자에 대 한 데이터 가져오기 게시 로컬 네트워크 또는 온라인*합니다. **Federation 메타 데이터 주소 (호스트 이름이 나 URL)**파트너, federation 메타 데이터 URL 이나 호스트 이름을 입력 한 클릭 한 다음 **다음**합니다.  
![당사자에](media/Create-a-Relying-Party-Trust/addtrust12.PNG) 

5.  표시 이름 지정 페이지에 이름을 입력 **표시 이름**노트에서이 신뢰 파티 보안에 대 한 설명을 입력 하 고 클릭 한 다음, **다음**합니다.

6.  선택 발급 승인 규칙 페이지 중 하나를 선택 **모든 사용자가이 당사자에 액세스 하도록 허용** 또는 **모든 사용자의이 당사자에 대 한 액세스 거부**을 차례로 클릭 하 고 **다음**합니다.

7.  추가 보안 페이지 준비가 설정을 검토 하 고 클릭 한 다음 **다음** 당사자에 저장 하려면 정보를 신뢰 합니다.

8.  마침 페이지, 클릭 **닫기**합니다. 자동으로이 작업을이 수행 편집 클레임 규칙 대화 상자를 표시합니다. 계속이 신뢰 파티 보안에 대 한 청구 규칙을 추가 하는 방법에 대 한 자세한 내용은 대 한 추가 참조 참조 하십시오.




## <a name="see-also"></a>참조 하십시오  
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md) 
