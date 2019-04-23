---
title: 작업 마스터 역할 점유 AD 포리스트 복구-
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 7e6bb370-f840-4416-b5e2-86b0ba715f4f
ms.technology: identity-adds
ms.openlocfilehash: 1994d49652ee9eb10f6afc73cf5b4630b4718e77
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858464"
---
# <a name="ad-forest-recovery---seizing-an-operations-master-role"></a>작업 마스터 역할 점유 AD 포리스트 복구-  

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

다음 절차를 사용 하 여 작업 마스터 역할 (라고도 신축 단일 마스터 작업 (FSMO) 역할)을 확보 합니다. Ntdsutil.exe, 모든 Dc에서 자동으로 설치 되는 명령줄 도구를 사용할 수 있습니다.  
  
## <a name="to-seize-an-operations-master-role"></a>작업 마스터 역할 점유에  
  
1. 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다.  

   ```  
   ntdsutil  
   ```  

2. 에 **ntdsutil:** 프롬프트을 다음 명령을 입력 한 다음 enter 키를 눌러:  

   ```  
   roles  
   ```  

3. 에 **FSMO 유지 관리:** 프롬프트을 다음 명령을 입력 한 다음 enter 키를 눌러:  

   ```  
   connections  
   ```  

4. 에 **서버 연결:** 프롬프트을 다음 명령을 입력 한 다음 enter 키를 눌러:  

   ```  
   Connect to server ServerFQDN  
   ```  

   여기서 *ServerFQDN* 예를 들어이 DC의 정규화 된 도메인 이름 (FQDN)는: **server nycdc01.example.com 연결할**합니다.  

   하는 경우 *ServerFQDN* 성공, DC의 NetBIOS 이름을 사용 하지 않습니다.  

5. 에 **서버 연결:** 프롬프트을 다음 명령을 입력 한 다음 enter 키를 눌러:  

   ```  
   quit  
   ```  

6. 역할을 점유 하 고, 원하는 따라에 **FSMO 유지 관리:** , 메시지를 표시 하 고, 다음 표에 설명 된 대로 적절 한 명령을 입력 하 고, 다음 ENTER를 누릅니다.  
  
|역할|자격 증명|Command|  
|----------|-----------------|-------------|  
|도메인 명명 마스터|Enterprise Admins|**명명 마스터를 점유 합니다.**|  
|스키마 마스터|Schema Admins|**스키마 마스터를 점유 합니다.**|  
|인프라 마스터 **참고 합니다.**  인프라 마스터 역할을 점유 하기 후 오류가 발생할 수 있습니다는 나중에 Adprep /Rodcprep을 실행 하는 경우. 자세한 내용은 기술 자료 문서를 참조 하십시오 [949257](https://support.microsoft.com/kb/949257)합니다.|Domain Admins|**인프라 마스터를 점유 합니다.**|  
|PDC 에뮬레이터 마스터|Domain Admins|**Pdc를 점유 합니다.**|  
|RID 마스터|Domain Admins|**Rid 마스터를 점유 합니다.**|  

요청을 확인 한 후 Active Directory 또는 AD DS 역할을 전송 하려고 시도 합니다. 전송에 실패 하면 오류 정보가 표시 되 고 확보를 사용 하 여 Active Directory 또는 AD DS에서 진행 됩니다. 확보를 완료 한 후 역할 및 각 역할을 현재 보유 하는 서버의 이름을 액세스 프로토콜 LDAP (Lightweight Directory)의 목록이 표시 됩니다. 실행할 수도 있습니다 **Netdom Query FSMO** 현재 역할 소유자를 확인 하려면 관리자 권한 명령 프롬프트에서.  
  
> [!NOTE]
> 이 컴퓨터는 장애 전의 RID 마스터 없었으며 RID 마스터 역할을 중단 하려는 경우 컴퓨터에서는이 역할을 수락 하기 전에 복제 파트너와 동기화 하려고 합니다. 그러나 컴퓨터를 격리 하는 경우이 단계를 수행 하면 때문에 성공 하지 파트너와 동기화 합니다. 따라서 대화 상자를 파트너와 동기화 할 수 없는이 컴퓨터에도 불구 하 고 작업을 계속할 것인지 묻는 나타납니다. **예**를 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 절차](AD-Forest-Recovery-Procedures.md)
