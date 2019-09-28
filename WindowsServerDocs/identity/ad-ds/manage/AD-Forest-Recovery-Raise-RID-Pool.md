---
title: AD 포리스트 복구-RID 풀 발생
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: c37bc129-a5e0-4219-9ba7-b4cf3a9fc9a4
ms.technology: identity-adds
ms.openlocfilehash: aa1f5e8b40aa43fa2601bc6f11efe2fcd4ccd05e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369063"
---
# <a name="ad-forest-recovery---raising-the-value-of-available-rid-pools"></a>AD 포리스트 복구-사용 가능한 RID 풀의 값을 발생 시킵니다. 

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

다음 절차를 사용 하 여 해당 DC가 복원 된 후 RID 작업 마스터가 할당 하는 RID (상대 ID) 풀의 값을 증가 시킵니다. 사용 가능한 RID 풀의 값을 높여 도메인을 복원 하는 데 사용 된 백업 이후에 생성 된 보안 주체에 대 한 RID를 DC가 할당 하지 않도록 할 수 있습니다. 

## <a name="about-active-directory-rid-pools-and-ridavailablepool"></a>Active Directory RID 풀 및 rIDAvailablePool 정보

각 도메인에는 **cn = RID Manager $, CN = System, DC**=<*domain_name*> 개체가 있습니다. 이 개체에는 이름이 **rIDAvailablePool**인 특성이 있습니다. 이 특성 값은 전체 도메인에 대 한 전역 RID 공간을 유지 합니다. 값은 상한 및 하 한을 포함 하는 양의 정수입니다. 상단 부분은 각 도메인에 대해 할당할 수 있는 보안 주체의 수 (0x3FFFFFFF 또는 10억 이상)를 정의 합니다. 낮은 부분은 도메인에 할당 된 Rid의 수입니다. 
  
> [!NOTE]
> Windows Server 2016 및 2012에서는 할당 될 수 있는 보안 주체의 수가 20억을 초과 하는 것으로 증가 합니다. 자세한 내용은 [RID 발급 관리](https://technet.microsoft.com/library/jj574229.aspx)를 참조 하세요. 
  
- 샘플 값: 4611686014132422708  
- 낮은 부분: 2100 (할당할 다음 RID 풀의 시작)  
- 위쪽 부분: 1073741823 (도메인에서 만들 수 있는 Rid의 총 수)  
  
큼 정수 값을 늘리면 하위 부분의 값이 증가 합니다. 예를 들어 4611686014132522708의 합계를 4611686014132422708의 샘플 값에 10만 추가 하는 경우 새 낮은 부분은 102100입니다. 이는 RID 마스터에 의해 할당 되는 다음 RID 풀이 2100 대신 102100로 시작 됨을 나타냅니다. 
  
### <a name="to-raise-the-value-of-available-rid-pools-using-adsiedit-and-the-calculator"></a>Adsiedit 및 계산기를 사용 하 여 사용 가능한 RID 풀의 값을 높이려면

1. 서버 관리자 열고 **도구** 를 클릭 한 다음 **ADSI 편집**을 클릭 합니다.
2. 마우스 오른쪽 단추를 클릭 하 고 **연결 대상** 을 선택 하 고 연결을 선택한 다음 **확인**을 클릭 합니다.
   ![ADSI Edit @ no__t-1 
3. 다음 고유 이름 경로를 찾습니다. **Cn = RID Manager $, CN = System, DC = <domain name>** .
   ![ADSI Edit @ no__t-1 
3. 마우스 오른쪽 단추를 클릭 하 고 CN = RID Manager $의 속성을 선택 합니다. 
4. **RIDAvailablePool**특성을 선택 하 고 **편집**을 클릭 한 다음, 긴 정수 값을 클립보드에 복사 합니다.
   ![ADSI Edit @ no__t-1  
5. 계산기를 시작 하 고 **보기** 메뉴에서 **공학용 모드**를 선택 합니다. 
6. 현재 값에 10만을 추가 합니다.
   ![ADSI Edit @ no__t-1 
7. Ctrl + c를 사용 하거나 **편집** 메뉴의 **복사** 명령을 사용 하 여 값을 클립보드에 복사 합니다. 
8. Adsiedit의 편집 대화 상자에서이 새 값을 붙여넣습니다. 
   ![ADSI Edit @ no__t-1 
9. 대화 상자에서 **확인** 을 클릭 하 고 속성 시트에서를 **적용** 하 여 **rIDAvailablePool** 특성을 업데이트 합니다. 
  
### <a name="to-raise-the-value-of-available-rid-pools-using-ldp"></a>LDP를 사용 하 여 사용 가능한 RID 풀의 값을 높이려면  
  
1. 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다.  
   **ldp**  
2. **연결**을 클릭 하 고 **연결**을 클릭 한 다음 RID 관리자의 이름을 입력 하 고 **확인**을 클릭 합니다. 
   ![LDP @ NO__T-1
3. **연결**, **바인딩**을 차례로 클릭 하 고 **자격 증명을 사용 하 여 바인딩** 을 선택 하 고 관리자 자격 증명을 입력 한 다음 **확인**을 클릭 합니다. 
   ![LDP @ NO__T-1
4. **보기**를 클릭 하 고 **트리** 를 클릭 한 후 다음 고유 이름 경로를 입력 합니다.  CN = RID Manager $, CN = System, DC =*도메인 이름*  
   ![LDP @ NO__T-1
5. **찾아보기**를 클릭 한 다음 **수정**을 클릭 합니다. 
6. 현재 **rIDAvailablePool** 값에 10만을 추가한 다음 **값**에 합계를 입력 합니다. 
7. **Dn**에 `cn=RID Manager$,cn=System,dc=` *< 도메인 이름 @ no__t-3*을 입력 합니다. 
8. **항목 편집 특성**에 `rIDAvailablePool`을 입력 합니다. 
9. 작업으로 **바꾸기** 를 선택 하 고 **enter 키**를 누릅니다.
   ![LDP @ NO__T-1 
10. **실행** 을 클릭 하 여 작업을 실행 합니다. **닫기**를 클릭합니다.
11. 변경 내용의 유효성을 검사 하려면 **보기**를 클릭 하 고 **트리**를 클릭 한 후 다음 고유 이름 경로를 입력 합니다.   CN = RID Manager $, CN = System, DC =*도메인 이름*입니다.   **RIDAvailablePool** 특성을 확인 합니다. 
   ![LDP @ NO__T-1

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)
