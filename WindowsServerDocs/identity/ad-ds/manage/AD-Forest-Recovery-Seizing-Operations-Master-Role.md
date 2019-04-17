---
title: "광고 숲 복구-작업 마스터 역할 중단"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 7e6bb370-f840-4416-b5e2-86b0ba715f4f
ms.technology: identity-adfs
ms.openlocfilehash: 7ca6e3746586feeb3573b1ad6ba02831d1f5addd
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---seizing-an-operations-master-role"></a>광고 숲 복구-작업 마스터 역할 중단  

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.

 다음 절차를 사용 하 여 작업 마스터 역할 (유연한 단일 마스터 작업 (FSMO) 역할) 중단 됩니다. Ntdsutil.exe, 모든 Dc에 자동으로 설치 되는 명령줄 도구를 사용할 수 있습니다.  
  
## <a name="to-seize-an-operations-master-role"></a>작업 마스터 역할 중단  
  
1.  명령 프롬프트에서 다음 명령을 입력 하 고 enter 다음과 같습니다.  
  
    ```  
    ntdsutil  
    ```  
  
2.  에 **ntdsutil:** 라는 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
    ```  
    roles  
    ```  
  
3.  에 **FSMO 유지 관리:** 라는 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
    ```  
    connections  
    ```  
  
4.  에 **서버 연결:** 라는 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
    ```  
    Connect to server ServerFQDN  
    ```  
  
     여기서 *ServerFQDN* 는 정식된 FQDN (도메인 이름)이이 DC의 예는: **nycdc01.example.com 서버에 연결**합니다.  
  
     하는 경우 *ServerFQDN* 성공, dc NetBIOS 이름을 사용 되지 않습니다.  
  
5.  에 **서버 연결:** 라는 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
    ```  
    quit  
    ```  
  
6.  역할을 중단 하 고 싶은 따라에 **FSMO 유지 관리:** 라는 아래에 설명 된 대로 적절 한 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
    |역할|자격 증명|명령|  
    |----------|-----------------|-------------|  
    |도메인 이름 지정 마스터|엔터프라이즈 관리|**명명 마스터 중단**|  
    |스키마 마스터|스키마 관리|**스키마 마스터 중단**|  
    |Infrastructure 마스터 **참고:** 후 infrastructure 마스터 역할을 중단 나타날 수 있습니다 오류가 나중에 Adprep 실행 해야 하는 경우 /Rodcprep 합니다. 자세한 내용은 참조 KB 문서 [949257](https://support.microsoft.com/kb/949257)합니다.|도메인 관리|**Infrastructure 마스터 중단**|  
    |Pdc 에뮬레이터|도메인 관리|**Pdc 중단**|  
    |마스터 제거|도메인 관리|**제거 마스터 중단**|  
  
     요청을 확인 한 후 Active Directory 또는 AD DS 하려고 역할을 전송 합니다. 전송 실패 하면 일부 오류 정보가 나타나고 Active Directory 또는 AD DS 확보도 진행 됩니다. 확보 완료 되 면 현재 각 역할을 보유 서버가 LDAP(Lightweight Directory Access Protocol) (LDAP) 이름과 역할 목록이 표시 됩니다. 실행할 수도 있습니다 **Netdom 쿼리 FSMO** 현재 역할 소유자 확인 하려면 관리자 명령 프롬프트에 있습니다.  
  
    > [!NOTE]
    >  이 컴퓨터에서 오류가 발생 하기 전에 RID 마스터 없습니다 RID 마스터 역할을 중단 하려는 경우이 역할을 받기 전에 복제 파트너와 동기화 하는 컴퓨터 시도 합니다. 그러나 컴퓨터가 격리 된 경우이 단계를 수행 하세요 하기 때문에 동기화 하는 파트너와 하지 성공 됩니다. 따라서이 컴퓨터 파트너와 동기화 할 수 없는 불구 하 고 작업을 계속할 것인지 묻는 대화 상자가 나타납니다. 클릭 **예**합니다.  
  
## <a name="next-steps"></a>다음 단계

- [광고 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)
