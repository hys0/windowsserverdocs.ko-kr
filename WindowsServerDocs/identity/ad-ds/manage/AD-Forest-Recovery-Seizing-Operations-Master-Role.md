---
title: AD 포리스트 복구-작업 마스터 역할 점유
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 7e6bb370-f840-4416-b5e2-86b0ba715f4f
ms.technology: identity-adds
ms.openlocfilehash: b229215eb7dde23bd1c17e6023b1c5eace0a56bf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823536"
---
# <a name="ad-forest-recovery---seizing-an-operations-master-role"></a>AD 포리스트 복구-작업 마스터 역할 점유  

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

작업 마스터 역할 (FSMO (신축 단일 마스터 작업) 역할)을 점유 하려면 다음 절차를 따르십시오. 모든 Dc에 자동으로 설치 되는 명령줄 도구인 Ntdsutil.exe를 사용할 수 있습니다.  
  
## <a name="to-seize-an-operations-master-role"></a>작업 마스터 역할을 점유 하려면  
  
1. 명령 프롬프트에서 다음 명령을 입력한 다음 Enter 키를 누릅니다.  

   ```  
   ntdsutil  
   ```  

2. **Ntdsutil:** 프롬프트에서 다음 명령을 입력 한 후 enter 키를 누릅니다.  

   ```  
   roles  
   ```  

3. **FSMO 유지 관리:** 프롬프트에서 다음 명령을 입력 한 후 enter 키를 누릅니다.  

   ```  
   connections  
   ```  

4. **서버 연결:** 프롬프트에서 다음 명령을 입력 한 후 enter 키를 누릅니다.  

   ```  
   Connect to server ServerFQDN  
   ```  

   여기서 *Serverfqdn* 은이 DC의 fqdn (정규화 된 도메인 이름)입니다. 예를 들어 **nycdc01.example.com server에 연결**합니다.  

   *Serverfqdn* 이 실패 하면 DC의 NetBIOS 이름을 사용 합니다.  

5. **서버 연결:** 프롬프트에서 다음 명령을 입력 한 후 enter 키를 누릅니다.  

   ```  
   quit  
   ```  

6. 점유 하려는 역할에 따라 다음 표에 설명 된 대로 적절 한 명령을 입력 하 고 ENTER 키를 **누릅니다.**  
  
|Role|자격 증명|명령|  
|----------|-----------------|-------------|  
|도메인 명명 마스터|Enterprise Admins|**이름 지정 마스터 확보**|  
|스키마 마스터|Schema Admins|**스키마 마스터 확보**|  
|인프라 마스터 **참고:** 인프라 마스터 역할을 점유 하 고 나면 나중에 Adprep/Rodcprep.를 실행 해야 하는 경우 오류 메시지가 표시 될 수 있습니다. 자세한 내용은 기술 자료 문서 [949257](https://support.microsoft.com/kb/949257)를 참조 하십시오.|Domain Admins|**인프라 마스터 확보**|  
|PDC 에뮬레이터 마스터|Domain Admins|**Pdc 점유**|  
|RID 마스터|Domain Admins|**Rid 마스터 점유**|  

요청을 확인 한 후 Active Directory 또는 AD DS 역할을 전송 하려고 시도 합니다. 전송에 실패 하면 일부 오류 정보가 표시 되 고 Active Directory 또는 AD DS은 확보를 진행 합니다. 점유를 완료 한 후에는 역할 목록과 현재 각 역할을 보유 하 고 있는 서버의 LDAP (Lightweight Directory Access Protocol) 이름이 표시 됩니다. 관리자 권한 명령 프롬프트에서 **Netdom QUERY FSMO** 를 실행 하 여 현재 역할 소유자를 확인할 수도 있습니다.  
  
> [!NOTE]
> 오류가 발생 하기 전에이 컴퓨터가 RID 마스터가 아닌 경우 RID 마스터 역할을 점유 하려고 하면 컴퓨터는이 역할을 수락 하기 전에 복제 파트너와 동기화를 시도 합니다. 그러나이 단계는 컴퓨터가 격리 될 때 수행 되므로 파트너와의 동기화에 성공 하지 못합니다. 따라서이 컴퓨터를 파트너와 동기화 할 수 없는 경우에도 작업을 계속할지 여부를 묻는 대화 상자가 나타납니다. **예**를 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)
