---
ms.assetid: 5b9fc9c1-5d12-4ad4-8ddc-3b8a6d45b217
title: 신뢰 당사자 트러스트 추가
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b000d4cfd4ded7ad37dbb235a9d33c83d8951707
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444366"
---
# <a name="create-a-relying-party-trust"></a>신뢰 당사자 트러스트 추가


다음 문서에서는 신뢰 당사자 트러스트를 수동으로 만들고 페더레이션 메타 데이터를 사용 하 여 설명 합니다.
  
## <a name="to-create-a-claims-aware-relying-party-trust-manually"></a>만들려면 클레임 인식 신뢰 당사자 트러스트 수동으로 

AD FS 관리 스냅인을 사용 하 여 새 신뢰 당사자 트러스트를 추가 하려면\-수동으로 설정을 구성, 페더레이션 서버에서 다음 절차를 수행 합니다.  

로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.
  
1. 서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  아래에서 **작업**, 클릭 **신뢰 당사자 트러스트 추가**합니다.  
![신뢰 당사자](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3.  에 **시작** 페이지에서 선택 **클레임 인식** 클릭 **시작**합니다.  
![신뢰 당사자](media/Create-a-Relying-Party-Trust/addtrust2.PNG) 
  
4.  **데이터 원본 선택** 페이지에서 **수동으로 신뢰 당사자 트러스트 데이터 입력**을 클릭한 후 **다음**을 클릭합니다.  
![신뢰 당사자](media/Create-a-Relying-Party-Trust/addtrust3.PNG) 
  
5.  에 **표시 이름 지정** 페이지에 이름을 입력 합니다 **표시 이름**, 아래 **메모** 이 신뢰 당사자 트러스트에 대 한 설명을 입력 한 다음 클릭 **다음**합니다.  
![신뢰 당사자](media/Create-a-Relying-Party-Trust/addtrust4.PNG) 

6. 에 **인증서 구성** 페이지를 클릭 하 여 선택적 토큰 암호화 인증서가 있는 경우 **찾아보기** 를 인증서 파일을 찾아 클릭 한 다음 **다음**합니다.  
![신뢰 당사자](media/Create-a-Relying-Party-Trust/addtrust5.PNG) 

7.  에 **URL 구성** 페이지에서 다음 중 하나 이상을 수행을 클릭 **다음**, 8 단계로 이동:  
  
    -   선택 된 **WS에 대 한 지원을 사용 하도록 설정\-패시브 페더레이션 프로토콜** 확인란입니다. 아래에서 **신뢰 당사자 WS\-페더레이션 Passive 프로토콜 URL**, 이 신뢰 당사자 트러스트에 대 한 URL을 입력 하 고 클릭 한 다음 **다음**합니다.  
  
    -   **SAML 2.0 WebSSO 프로토콜에 대한 지원 사용** 확인란을 선택합니다. 아래 **신뢰 당사자 SAML 2.0 SSO 서비스 URL**, Security Assertion Markup Language 입력 \(SAML\) 클릭 하 고 서비스 끝점 URL이 신뢰 당사자 트러스트에 대 한 **다음**.  
![신뢰 당사자](media/Create-a-Relying-Party-Trust/addtrust6.PNG)   

8. **식별자 구성** 페이지에서 이 신뢰 당사자에 대한 식별자를 하나 이상 지정하고 **추가**를 클릭하여 목록에 추가한 후 **다음**을 클릭합니다.  
![신뢰 당사자](media/Create-a-Relying-Party-Trust/addtrust8.PNG)
  
9.  에 **액세스 제어 정책 선택** 정책을 선택 하 고 클릭 **다음**합니다.  액세스 제어 정책에 대 한 자세한 내용은 참조 [AD FS에서 액세스 제어 정책](Access-Control-Policies-in-AD-FS.md)합니다. 
![신뢰 당사자](media/Create-a-Relying-Party-Trust/addtrust9.PNG)

10. **트러스트 추가 준비 완료** 페이지에서 설정을 검토한 후 **다음** 을 클릭하여 신뢰 당사자 트러스트 정보를 저장합니다.  
   ![신뢰 당사자](media/Create-a-Relying-Party-Trust/addtrust10.PNG) 
11. **Finish(마침)** 페이지에서 **Close(닫기)** 를 클릭합니다. 이 작업을 통해 **클레임 규칙 편집** 대화 상자가 자동으로 표시됩니다.  
![신뢰 당사자](media/Create-a-Relying-Party-Trust/addtrust11.PNG) 

## <a name="to-create-a-claims-aware-relying-party-trust-using-federation-metadata"></a>만들려면 클레임 인식 신뢰 당사자 페더레이션 메타 데이터를 사용 하 여 신뢰

새 신뢰 당사자 트러스트, AD FS 관리 스냅인을 사용 하 여 로컬 네트워크 또는 인터넷에 게시 하는 페더레이션 메타 데이터에서 파트너에 대 한 구성 데이터를 자동으로 가져와서 추가 하려면 계정 파트너 조직의 페더레이션 서버에서 다음 절차를 수행 합니다.

>[!NOTE]
>와 같은 비 정규화 된 호스트 이름으로 인증서를 사용 하는 것이 오래 된 있지만 https://myserver, 이러한 인증서는 보안 가치가 없으므로 및 공격자가 페더레이션 메타 데이터를 게시 하는 페더레이션 서비스를 가장할 수 있습니다. 따라서 페더레이션 메타 데이터를 쿼리할 때만 사용 해야는 정규화 된 도메인 이름 같은 https://myserver.contoso.com합니다.

로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.


1. 서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2. 아래에서 **작업**, 클릭 **신뢰 당사자 트러스트 추가**합니다.  
   ![신뢰 당사자](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3. 에 **시작** 페이지에서 선택 **클레임 인식** 클릭 **시작**합니다.  
   ![신뢰 당사자](media/Create-a-Relying-Party-Trust/addtrust2.PNG) 
  
4. 에 **데이터 원본 선택** 페이지에서 <strong>온라인 이나 로컬 네트워크 *에 게시 한 신뢰 당사자 관련 데이터 가져오기. * * 페더레이션 메타 데이터 주소 (호스트 이름 또는 URL)</strong>파트너에 대 한 페더레이션 메타 데이터 URL 또는 호스트 이름을 입력 하 고 클릭 **다음**합니다.  
   ![신뢰 당사자](media/Create-a-Relying-Party-Trust/addtrust12.PNG) 

5. 표시 이름 지정 페이지에서 이름을 입력 **표시 이름**, 정보 아래에서이 신뢰 당사자 트러스트에 대 한 설명을 입력 하 고 클릭 한 다음, **다음**합니다.

6. 발급 권한 부여 규칙 선택 페이지에서 하나를 선택 **모든 사용자가이 신뢰 당사자에 액세스 하도록 허용** 또는 **이 신뢰 당사자에 게 모든 사용자의 액세스 거부**, 를 클릭 하 고 **다음**합니다.

7. 트러스트 추가 페이지를 준비에서 설정을 검토 한 다음 클릭 **다음** 신뢰 당사자를 저장 하려면 정보를 신뢰 합니다.

8. 마침 페이지에서 클릭 **닫기**합니다. 이 작업에는 클레임 규칙 편집 대화 상자를 사용 하 여 자동으로 표시 됩니다. 이 신뢰 당사자 트러스트에 대한 클레임 규칙을 추가하는 방법에 대한 자세한 내용은 추가 참조 섹션을 참조하세요.




## <a name="see-also"></a>관련 항목  
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md) 
