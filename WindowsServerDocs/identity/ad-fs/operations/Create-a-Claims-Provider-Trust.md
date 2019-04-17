---
ms.assetid: a4f7842c-cfca-4d78-916e-023d12a9cdf0
title: "청구 공급자 신뢰 만들기"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b4dc20713fdd137b019a072037e35e9219e02fa9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-claims-provider-trust"></a>청구 공급자 신뢰 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

Snap\에 AD FS 관리를 사용 하 여 새 클레임 공급자 신뢰를 추가 하는 설정을 수동으로 구성 리소스 파트너 조직에서 리소스 파트너 federation 서버에 다음 절차를 수행 합니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 최소 요구 사항을 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
## <a name="to-create-a-claims-provider-trust-manually"></a>수동으로 클레임 공급자 신뢰를 만들려면  
  
1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  아래에서 **작업**, 클릭 **클레임 공급자 신뢰 추가**합니다.  
![청구 공급자 보안](media/Create-a-Claims-Provider-Trust/addclaim1.PNG)   
  
3.  에 **시작** 페이지, 클릭 **시작**합니다. 
![청구 공급자 보안](media/Create-a-Claims-Provider-Trust/addclaim2.PNG)    
  
4.  에 **데이터 소스를 선택** 페이지, 클릭 **Enter 클레임 수동으로 공급자 신뢰 데이터**을 차례로 클릭 하 고 **다음**합니다.  
![청구 공급자 보안](media/Create-a-Claims-Provider-Trust/addclaim3.PNG)     

5.  에 **표시 이름 지정** 페이지를 입력 합니다는 **표시 이름**, **노트**공급자 신뢰 하는 클레임이 대 한 설명을 입력 하 고 클릭 한 다음 **다음**합니다.  
![청구 공급자 보안](media/Create-a-Claims-Provider-Trust/addclaim4.PNG)     

6.  에 **구성 URL** 페이지에서 지정는 **WS Federation 수동 URL** 해당 하는 경우를 클릭 하 고 **다음**합니다.
![청구 공급자 보안](media/Create-a-Claims-Provider-Trust/addclaim5.PNG)     

8. 에 **구성 식별자** 페이지의 **클레임 공급자 신뢰 식별자**적절 한 식별자를 입력 하 고 클릭 한 다음 **다음**합니다.  
![청구 공급자 보안](media/Create-a-Claims-Provider-Trust/addclaim6.PNG)    

9. 에 **구성 인증서** 페이지, 클릭 **추가** 인증서 파일을 찾아 인증서를 목록에 추가 하 고 클릭 한 다음 **다음**합니다.  
![청구 공급자 보안](media/Create-a-Claims-Provider-Trust/addclaim7.PNG)    

10. 에 **추가 보안 준비가** 페이지, 클릭 **다음** 여 클레임 공급자 보안 정보를 저장 하도록 합니다.  
![청구 공급자 보안](media/Create-a-Claims-Provider-Trust/addclaim8.PNG)    

11. 에 **완료** 페이지, 클릭 **닫기**합니다. 이 작업은 자동으로 표시는 **편집 클레임 규칙** 대화 상자가 합니다. 추가 진행 하는 방법에 대 한 자세한 내용은 규칙 클레임 공급자 신뢰가에 대 한 주장 다음과 같은 추가 참조 참조 하십시오.  
![청구 공급자 보안](media/Create-a-Claims-Provider-Trust/addclaim9.PNG)

## <a name="to-create-a-claims-provider-trust-using-federation-metadata"></a>Federation 메타 데이터를 사용 하 여 클레임 공급자 신뢰를 만들려면
새 클레임 공급자를 추가 하려면 AD FS 관리 스냅인를 사용 하 여 자동으로 파트너는 로컬 네트워크 또는 인터넷에 게시 federation 메타 데이터를 파트너에 대 한 구성 데이터를 가져오는 방법으로 보안 리소스 파트너 조직에서 federation 서버에 다음 절차를 수행 합니다.

>[!NOTE]
>https://myserver 등 호스트 자격이 없는 이름으로 인증서를 사용 하 여 일반적으로 오랫동안, 있지만 이러한 인증서 보안 값이 없는 및 공격자 가장 federation 메타 데이터를 게시 하는 Federation 서비스를 사용 하도록 설정할 수 있습니다. 따라서 federation 메타 데이터를 쿼리를 https://myserver.contoso.com 등 정식된 도메인 이름을 사용만 해야 합니다.

1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  아래에서 **작업**, 클릭 **의존 파티 신뢰 추가**합니다.  
![청구 공급자 보안](media/Create-a-Claims-Provider-Trust/addclaim1.PNG)   
  
3.  에 **시작** 페이지, 클릭 **시작**합니다. 
![청구 공급자 보안](media/Create-a-Claims-Provider-Trust/addclaim2.PNG)    
  
4.  에 **선택 데이터 소스** 페이지, 클릭 **클레임 공급자에 대 한 데이터 가져오기 게시 로컬 네트워크 또는 온라인**합니다. (호스트 이름이 나 URL) 메타 데이터 주소를 입력 연합에서는 **federation 메타 데이터 URL** 또는 호스트 파트너에 이름을 지정 하 고 클릭 한 다음 **다음**합니다.
![청구 공급자 보안](media/Create-a-Claims-Provider-Trust/addclaim10.PNG)    

5.  페이지 표시 이름 지정에 입력 한 **표시 이름**노트 한 설명을 입력이 주장 공급자 보안에 대 한을 클릭 한 다음 **다음**합니다.

6.  준비 추가 보안 페이지, 클릭 **다음** 여 클레임 공급자 보안 정보를 저장 하도록 합니다.

7.  마침 페이지, 클릭 **닫기**합니다. 이 청구 규칙 편집 대화 상자에서 자동으로 표시 됩니다. 추가 진행 하는 방법에 대 한 자세한 내용은 규칙 클레임 공급자 신뢰가에 대 한 주장 추가 참조 섹션 아래를 참조 하십시오.



    
## <a name="additional-references"></a>추가 참조  
[구성 리소스 파트너 조직 검사:](../../ad-fs/deployment/Checklist--Configuring-the-Resource-Partner-Organization.md)  
  
[청구 공급자에 대 한 청구 규칙 만들기 신뢰 검사:](../../ad-fs/deployment/Checklist--Creating-Claim-Rules-for-a-Claims-Provider-Trust.md)  
  
## <a name="see-also"></a>참조 하십시오  
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md) 
  
