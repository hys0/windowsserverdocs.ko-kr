---
title: "광고 숲 복구 풀 발생 제거"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: c37bc129-a5e0-4219-9ba7-b4cf3a9fc9a4
ms.technology: identity-adfs
ms.openlocfilehash: e6b5dc8b9c0b701fe2cd1b0c88f7edc22802c393
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---raising-the-value-of-available-rid-pools"></a>사용 가능한 RID 풀의 값 발생-광고 숲 복구 

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.
 
 사용 값의는 관련 ID (RID)를 다음 절차 풀 해당 DC 복원 된 후 RID 작업 마스터 할당 합니다. 사용 가능한 RID 풀의 값 제기, DC 후 도메인 복원 하는 데 사용 된 백업을 만든 보안 사용자에 대 한 RID 할당 있는지 확인할 수 있습니다.  
 
## <a name="about-active-directory-rid-pools-and-ridavailablepool"></a>RIDAvailablePool Active Directory 제거 풀에 대 한
 각 도메인에 있는 개체 **CN = RID 관리자 $CN 시스템, DC =**=<*domain_name*> 합니다. 이 개체의 이라는 특성 **rIDAvailablePool**합니다. 이 특성 값 전체 도메인에 대 한 전 세계 RID 공간을 유지합니다. 값 위쪽 및 아래쪽 부분과 큰 정수입니다. 위쪽 정의 각 도메인 (0x3FFFFFFF 또는 1 십억만 이상)에 할당 될 수 있는 보안 사용자의 수 있습니다. 아래쪽은 도메인에 할당 된 rid 수입니다.  
  
> [!NOTE]
>  Windows Server 2016 및 2012에 할당 될 수 있는 보안 사용자의 수는만 넘는 2 십억 증가 합니다. 자세한 내용은 참조 [제거 관리 발급](https://technet.microsoft.com/library/jj574229.aspx)합니다.  
  
-   4611686014132422708 샘플 값:  
  
-   낮은 단계: 2100 (할당 다음 RID 풀의 시작 부분)  
  
-   위 단계: 1073741823 (도메인에 만들 수 있는 rid 총)  
  
 큰 형식은 가치를 늘리는 경우 낮은 일부 값을 늘립니다. 예를 들어 100, 000 샘플 4611686014132422708 4611686014132522708 총에 대 한 값으로 추가 하면 새 낮은 부품 102100입니다. 이 나타냅니다 102100 2100 대신로 다음 RID 풀 RID 마스터 할당을 시작 합니다.  
  
### <a name="to-raise-the-value-of-available-rid-pools-using-adsiedit-and-the-calculator--"></a>발생 하는 가치 adsiedit 및 계산기를 사용 하 여 사용 가능한 RID 풀에 '  
1.  서버 관리자를 열을 클릭 **도구** 클릭 **ADSI 편집**합니다.    
2.  마우스 오른쪽 단추를 선택 하 고 **연결할** 연결 및 기본 이름 지정 컨텍스트를 수행 하 고 클릭 **확인**합니다.
![ADSI 편집](media/AD-Forest-Recovery-Raise-RID-Pool/adsi1.png) 
3. 다음과 같은 고유 이름 경로를 찾아: **CN = RID 관리자 $CN 시스템, DC = =<domain name>**합니다.
![ADSI 편집](media/AD-Forest-Recovery-Raise-RID-Pool/adsi2.png) 
3.  마우스 오른쪽 단추로 클릭 하 고 CN 속성을 선택 하 고 RID 관리자 $= 합니다.  
4.  특성 **rIDAvailablePool**, 클릭 **편집**, 큰 정수값 클립보드에 복사 합니다.
![ADSI 편집](media/AD-Forest-Recovery-Raise-RID-Pool/adsi3.png)  
5.  계산기, 시작 및에서 **보기** 메뉴를 선택 하 고 **공학용 모드**합니다.  6.  100, 000 현재 금액을 추가 합니다.  
![ADSI 편집](media/AD-Forest-Recovery-Raise-RID-Pool/adsi4.png) 
7.  Ctrl c를 사용 하 여 또는 **복사** 명령을 **편집** 메뉴 값 클립보드에 복사 합니다.  
8.  Adsiedit의 편집 대화 상자에서이 새 값을 붙여 넣습니다. 
![ADSI 편집](media/AD-Forest-Recovery-Raise-RID-Pool/adsi5.png) 
9. 클릭 **확인** 대화 상자에서 및 **적용** 속성 시트 업데이트에 **rIDAvailablePool** 특성 합니다.  
  
### <a name="to-raise-the-value-of-available-rid-pools-using-ldp"></a>발생 하는 가치 LDP 사용 하 여 사용 가능한 RID 풀에  
  
1.  명령 프롬프트에서 다음 명령을 입력 하 고 enter 다음과 같습니다.  
  
     **ldp**  
  
2.  클릭 **연결**, 클릭 **연결**RID 관리자의 이름을 입력 한 다음, **확인**합니다.  
![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp1.png)
3.  클릭 **연결**, 클릭 **연결**선택 **자격 증명으로 연결** 관리자 자격 증명을 입력 하 고 클릭 한 다음 **확인**합니다.  
![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp2.png)
4.  클릭 **보기**, 클릭 **트리** 후 다음과 같은 고유 이름을 경로 입력 하 고: CN RID CN 관리자 $= 시스템, DC = =*도메인 이름*  
![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp3.png)
5.  클릭 **찾아보기**을 차례로 클릭 하 고 **수정**합니다.  
6.  현재 100, 000 추가 **rIDAvailablePool** 값을 다음에 합계 입력 **값**합니다.  
7.  **Dn**, 입력 `cn=RID Manager$,cn=System,dc=`*< 도메인 name\ >*합니다.  
8.  **항목 특성 편집**, 입력 `rIDAvailablePool`합니다.  
9. 선택 **교체** 작업을 선택한 다음 클릭 **Enter**합니다. </br>
![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp4.png) 
10. 클릭 **실행** 여 작업을 실행 합니다.  클릭 **닫기**합니다.
11. 변경 사항을 확인을 클릭 **보기**, 클릭 **트리**, 후 다음과 같은 고유 이름을 경로 입력 하 고: CN = RID 관리자 $CN 시스템, DC = =*도메인 이름*합니다.    검사는 **rIDAvailablePool** 특성 합니다.  
![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp5.png)

## <a name="next-steps"></a>다음 단계

- [광고 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)
 
