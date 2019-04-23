---
title: AD 포리스트 복구를 발생 시키는 RID 풀
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: c37bc129-a5e0-4219-9ba7-b4cf3a9fc9a4
ms.technology: identity-adds
ms.openlocfilehash: c8f91226e10ea6681933d5a5dc00b92f5ab2179c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862984"
---
# <a name="ad-forest-recovery---raising-the-value-of-available-rid-pools"></a>사용 가능한 RID 풀의 값을 발생 시키는 AD 포리스트 복구- 

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

상대 ID (RID)의 값을 발생 시키는 다음 절차는 DC를 복원한 후 RID 작업 마스터를 할당 풀을 사용 합니다. 사용 가능한 RID 풀의 값을 생성 하 여 DC가 없는 도메인을 복원 하는 데 사용 된 백업 이후에 만든 보안 주체에 대 한 RID 할당을 확인할 수 있습니다. 

## <a name="about-active-directory-rid-pools-and-ridavailablepool"></a>Active Directory RID 풀 및 rIDAvailablePool 하는 방법에 대 한

각 도메인에 개체 **CN = RID Manager$, CN = System, DC**=<*domain_name*>. 이 개체에 명명 된 특성 **rIDAvailablePool**합니다. 이 특성 값이 전역 RID 공간의 전체 도메인에 대 한 유지 관리합니다. 값에는 상한 및 하 한 파트를 사용 하 여 큰 정수입니다. 위쪽 (0x3FFFFFFF 또는 1 십억 약간 넘은) 각 도메인에 대 한 할당 될 수 있는 보안 주체를 정의 합니다. 아래쪽에는 도메인에 할당 된 Rid의 수입니다. 
  
> [!NOTE]
> Windows Server 2016 및 2012에서 할당 될 수 있는 보안 주체의 수가 2 십억 약간 넘은 증가 됨. 자세한 내용은 [관리 RID 발급](https://technet.microsoft.com/library/jj574229.aspx)합니다. 
  
- 샘플 값: 4611686014132422708  
- 낮은 부: 2100 (할당할 다음 RID 풀의 시작 부분)  
- 위 부: 1073741823 (도메인에 만들 수 있는 Rid 총 수)  
  
큰 정수 값을 늘리면 늘려야 낮은 부분의 값입니다. 예를 들어, 4611686014132422708 4611686014132522708의 합계에 대 한 샘플 값 100000을 추가 하는 경우 새 하위 부분 102100입니다. 이 다음 RID 풀 할당 되는 RID 마스터에서 102100 2100 대신 시작 됩니다 것을 나타냅니다. 
  
### <a name="to-raise-the-value-of-available-rid-pools-using-adsiedit-and-the-calculator"></a>Adsiedit 및 계산기를 사용 하 여 사용 가능한 RID 풀의 값을 시키려면

1. 서버 관리자를 열고 **도구가** 클릭 **ADSI 편집**합니다.
2. 마우스 오른쪽 단추로 선택한 **연결할** 연결 및 기본 명명 컨텍스트를 수행 하 고 클릭 **확인**합니다.
   ![ADSI 편집](media/AD-Forest-Recovery-Raise-RID-Pool/adsi1.png) 
3. 고유 이름 경로를 찾습니다. **CN=RID Manager$,CN=System,DC=<domain name>**.
   ![ADSI 편집](media/AD-Forest-Recovery-Raise-RID-Pool/adsi2.png) 
3. 마우스 오른쪽 단추로 클릭 하 고 cn 속성 선택 = RID Manager$입니다. 
4. 특성 선택 **rIDAvailablePool**, 클릭 **편집**, 큰 정수 값을 클립보드에 복사 합니다.
   ![ADSI 편집](media/AD-Forest-Recovery-Raise-RID-Pool/adsi3.png)  
5. 계산기를 시작 및 합니다 **보기** 메뉴에서 **공학용 모드**. 
6. 현재 값 100000을 추가 합니다.
   ![ADSI 편집](media/AD-Forest-Recovery-Raise-RID-Pool/adsi4.png) 
7. Ctrl + c를 사용 하 여 또는 **복사** 에서 명령을 합니다 **편집** 메뉴에서 값을 클립보드에 복사 합니다. 
8. Adsiedit의 편집 대화 상자에서이 새 값을 붙여넣습니다. 
   ![ADSI 편집](media/AD-Forest-Recovery-Raise-RID-Pool/adsi5.png) 
9. 클릭 **확인** 대화 상자에서 및 **적용** 업데이트 하 고 속성 시트에는 **rIDAvailablePool** 특성입니다. 
  
### <a name="to-raise-the-value-of-available-rid-pools-using-ldp"></a>LDP를 사용 하 여 사용 가능한 RID 풀의 값을 시키려면  
  
1. 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다.  
   **ldp**  
2. 클릭 **연결**, 클릭 **Connect**RID 관리자의 이름을 입력 하 고 클릭 **확인**합니다. 
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp1.png)
3. 클릭 **연결**, 클릭 **바인딩할**를 선택 **자격 증명을 사용 하 여 바인딩** 관리 자격 증명을 입력 하 고 클릭 **확인**합니다. 
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp2.png)
4. 클릭 **뷰**, 클릭 **트리** 다음 고유 이름 경로 입력 합니다.  CN=RID Manager$,CN=System,DC=*domain name*  
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp3.png)
5. 클릭 **찾아보기**를 클릭 하 고 **수정**합니다. 
6. 현재 100,000 추가할 **rIDAvailablePool** 값을 다음으로 합계를 입력 **값**합니다. 
7. **Dn**, 형식 `cn=RID Manager$,cn=System,dc=` *< 도메인 이름\>* 합니다. 
8. **항목 편집 특성**, 형식 `rIDAvailablePool`합니다. 
9. 선택 **바꿉니다** 작업 및 클릭 **Enter**합니다.
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp4.png) 
10. 클릭 **실행** 작업을 실행 합니다. **닫기**를 클릭합니다.
11. 변경의 유효성을 검사 하려면 클릭 **뷰**, 클릭 **트리**, 고유 이름 경로 입력 합니다.   CN = RID Manager$, CN = System, DC =*도메인 이름*합니다.   확인 합니다 **rIDAvailablePool** 특성입니다. 
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp5.png)

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 절차](AD-Forest-Recovery-Procedures.md)
