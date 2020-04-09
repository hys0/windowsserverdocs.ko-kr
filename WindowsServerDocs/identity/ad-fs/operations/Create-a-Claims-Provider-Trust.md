---
ms.assetid: a4f7842c-cfca-4d78-916e-023d12a9cdf0
title: 클레임 공급자 트러스트 만들기
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: bd5c13dbdf4258b6a87dcf599299dd7969da5acd
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80817066"
---
# <a name="create-a-claims-provider-trust"></a>클레임 공급자 트러스트 만들기

에서 AD FS 관리 스냅인\-사용 하 여 새 클레임 공급자 트러스트를 추가 하 고 설정을 수동으로 구성 하려면 리소스 파트너 조직의 리소스 파트너 페더레이션 서버에서 다음 절차를 수행 합니다.  
  
멤버 자격이 **관리자**, 또는 이와 동등한 로컬 컴퓨터에서 최소한이이 절차를 완료 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
## <a name="to-create-a-claims-provider-trust-manually"></a>클레임 공급자 트러스트를 수동으로 생성하려면  
  
1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  **작업**아래에서 **클레임 공급자 트러스트 추가**를 클릭 합니다.  
![클레임 공급자 트러스트](media/Create-a-Claims-Provider-Trust/addclaim1.PNG)   
  
3.  **시작** 페이지에서 **시작**을 클릭합니다. 
![클레임 공급자 트러스트](media/Create-a-Claims-Provider-Trust/addclaim2.PNG)    
  
4.  **데이터 원본 선택** 페이지에서 **수동으로 클레임 공급자 트러스트 데이터 입력**을 클릭한 후 **다음**을 클릭합니다.  
![클레임 공급자 트러스트](media/Create-a-Claims-Provider-Trust/addclaim3.PNG)     

5.  **표시 이름 지정** 페이지에서 **메모** 아래에 **표시 이름**을 입력하고 이 클레임 공급자 트러스트에 대한 설명을 입력한 후 **다음**을 클릭합니다.  
![클레임 공급자 트러스트](media/Create-a-Claims-Provider-Trust/addclaim4.PNG)     

6.  **URL 구성** 페이지에서 **ws-federation 수동 URL** (해당 하는 경우)을 지정 하 고 **다음**을 클릭 합니다.
![클레임 공급자 트러스트](media/Create-a-Claims-Provider-Trust/addclaim5.PNG)     

8. **클레임 공급자 트러스트 식별자** 아래의 **식별자 구성** 페이지에 적절한 식별자를 입력하고 **다음**을 클릭합니다.  
![클레임 공급자 트러스트](media/Create-a-Claims-Provider-Trust/addclaim6.PNG)    

9. **인증서 구성** 페이지에서 **추가**를 클릭하여 인증서 파일을 찾아서 인증서를 인증서 목록에 추가하고 **다음**을 클릭합니다.  
![클레임 공급자 트러스트](media/Create-a-Claims-Provider-Trust/addclaim7.PNG)    

10. **트러스트 추가 준비 완료** 페이지에서 **다음**을 클릭하여 클레임 공급자 트러스트 정보를 저장합니다.  
![클레임 공급자 트러스트](media/Create-a-Claims-Provider-Trust/addclaim8.PNG)    

11. **Finish(마침)** 페이지에서 **Close(닫기)** 를 클릭합니다. 이 작업을 통해 **클레임 규칙 편집** 대화 상자가 자동으로 표시됩니다. 이 클레임 공급자 트러스트에 대 한 클레임 규칙 추가를 진행 하는 방법에 대 한 자세한 내용은 다음 추가 참조를 참조 하세요.  
![클레임 공급자 트러스트](media/Create-a-Claims-Provider-Trust/addclaim9.PNG)

## <a name="to-create-a-claims-provider-trust-using-federation-metadata"></a>페더레이션 메타 데이터를 사용 하 여 클레임 공급자 트러스트를 만들려면
AD FS 관리 스냅인을 사용 하 여 새 클레임 공급자 트러스트를 추가 하려면 파트너가 로컬 네트워크 또는 인터넷에 게시 한 페더레이션 메타 데이터에서 파트너에 대 한 구성 데이터를 자동으로 가져와서 리소스 파트너 조직의 페더레이션 서버에서 다음 절차를 수행 합니다.

>[!NOTE]
>일반적으로 https:\//myserver와 같이 정규화 되지 않은 호스트 이름으로 인증서를 사용 하는 것이 일반적 이지만 이러한 인증서에는 보안 값이 없으며 공격자가 페더레이션 메타 데이터를 게시 하는 페더레이션 서비스 가장할 수 있습니다. 따라서 페더레이션 메타 데이터를 쿼리 하는 경우 `https://myserver.contoso.com`같은 정규화 된 도메인 이름만 사용 해야 합니다.

1.  서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  **작업**아래에서 **클레임 공급자 트러스트 추가**를 클릭 합니다.  
![클레임 공급자 트러스트](media/Create-a-Claims-Provider-Trust/addclaim1.PNG)   
  
3.  **시작** 페이지에서 **시작**을 클릭합니다. 
![클레임 공급자 트러스트](media/Create-a-Claims-Provider-Trust/addclaim2.PNG)    
  
4.  **데이터 원본 선택** 페이지에서 **온라인으로 또는 로컬 네트워크로 게시한 클레임 공급자 관련 데이터 가져오기**를 클릭합니다. 페더레이션 메타 데이터 주소 (호스트 이름 또는 URL)에 파트너에 대 한 **페더레이션 메타 데이터 URL** 또는 호스트 이름을 입력 하 고 **다음**을 클릭 합니다.
![클레임 공급자 트러스트](media/Create-a-Claims-Provider-Trust/addclaim10.PNG)    

5.  표시 이름 지정 페이지에서 메모 아래에 **표시 이름을**입력 하 고이 클레임 공급자 트러스트에 대 한 설명을 입력 한 후 **다음**을 클릭 합니다.

6.  트러스트 추가 준비 페이지에서 **다음** 을 클릭 하 여 클레임 공급자 트러스트 정보를 저장 합니다.

7.  마침 페이지에서 클릭 **닫기**합니다. 그러면 클레임 규칙 편집 대화 상자가 자동으로 표시 됩니다. 이 클레임 공급자 트러스트에 대 한 클레임 규칙 추가를 진행 하는 방법에 대 한 자세한 내용은 아래의 추가 참조 섹션을 참조 하세요.



    
## <a name="additional-references"></a>추가 참조  
[검사 목록: 리소스 파트너 조직 구성](../../ad-fs/deployment/Checklist--Configuring-the-Resource-Partner-Organization.md)  
  
[검사 목록: 클레임 공급자 트러스트에 대 한 클레임 규칙 만들기](../../ad-fs/deployment/Checklist--Creating-Claim-Rules-for-a-Claims-Provider-Trust.md)  
  
## <a name="see-also"></a>관련 항목  
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md) 
  
