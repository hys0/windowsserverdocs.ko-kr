---
ms.assetid: 7b7ae389-5032-44f7-9c0a-94398c3e4d88
title: 비 클레임 인식 신뢰 당사자 트러스트 만들기
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: c6886145e910b76edbe99549266d651cdd7c3edf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816926"
---
# <a name="create-a-non-claims-aware-relying-party-trust"></a>비 클레임 인식 신뢰 당사자 트러스트 만들기


AD FS 관리 스냅인에서\-비에서\-클레임\-인식 신뢰 당사자 트러스트를 페더레이션 서비스와 단일 웹 간의 트러스트를 나타내는 생성 된 개체는\-기반 클레임 되지 않는 응용 프로그램\-인식 웹 응용 프로그램 프록시를 통해 액세스 하는 고 합니다.  
  
비\-클레임\-신뢰 당사자 트러스트는 신뢰 당사자 트러스트에 웹 응용 프로그램 프록시를 통해 액세스할 때 식별자, 이름 및 인증 및 권한 부여에 대 한 규칙의 구성 된 신뢰 당사자 트러스트를 인식 합니다. 이러한 웹\-기반 클레임, 즉, 이러한 Windows 통합 인증에 사용 하지 않는 응용 프로그램\-기반된 응용 프로그램 액세스는 웹 응용 프로그램 프록시를 통해 회사 네트워크 외부의 경우 클레임 기반 액세스를 적용 하는 권한 부여 규칙을 가질 수 있습니다.  
  
새 추가 하려면 비\-클레임\-AD FS 관리 스냅인을 사용 하 여 인식 신뢰 당사자 트러스트\-다음 절차를 수행 합니다.  
  
이 절차를 완료하려면 최소한 로컬 컴퓨터의 **Administrators** 구성원 자격 또는 동급의 권한이 필요합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
## <a name="to-create-a-non-claims-aware-relying-party-trust-manually"></a>비 클레임 인식 신뢰 당사자 트러스트를 수동으로 만들려면 
1. 서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다.  
  
2.  아래에서 **작업**, 클릭 **신뢰 당사자 트러스트 추가**합니다.  
![신뢰 당사자](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3.  에 **시작** 페이지에서 선택 **비 클레임 인식** 클릭 **시작**합니다.  
![신뢰 당사자](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon1.PNG) 
  
4.  에 **표시 이름 지정** 페이지에 이름을 입력 합니다 **표시 이름**, 아래 **메모** 이 신뢰 당사자 트러스트에 대 한 설명을 입력 한 다음 클릭 **다음**합니다.  
![신뢰 당사자](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon2.PNG)

5. **식별자 구성** 페이지에서 이 신뢰 당사자에 대한 식별자를 하나 이상 지정하고 **추가**를 클릭하여 목록에 추가한 후 **다음**을 클릭합니다.  
![신뢰 당사자](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon3.PNG)

6.  에 **액세스 제어 정책 선택** 정책을 선택 하 고 클릭 **다음**합니다.  액세스 제어 정책에 대 한 자세한 내용은 참조 [AD FS에서 액세스 제어 정책](Access-Control-Policies-in-AD-FS.md)합니다. 
![신뢰 당사자](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon4.PNG)

7. **트러스트 추가 준비 완료** 페이지에서 설정을 검토한 후 **다음**을 클릭하여 신뢰 당사자 트러스트 정보를 저장합니다.  
   ![신뢰 당사자](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon5.PNG) 

8. **Finish(마침)** 페이지에서 **Close(닫기)** 를 클릭합니다. 이 작업을 통해 **클레임 규칙 편집** 대화 상자가 자동으로 표시됩니다.  
![신뢰 당사자](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon6.PNG)  
  
## <a name="see-also"></a>관련 항목  
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md) 
