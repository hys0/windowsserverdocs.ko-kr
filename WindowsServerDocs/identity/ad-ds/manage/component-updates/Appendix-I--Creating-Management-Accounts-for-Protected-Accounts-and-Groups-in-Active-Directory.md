---
ms.assetid: 13fe87d9-75cf-45bc-a954-ef75d4423839
title: 부록 I-Active Directory의 보호 된 계정 및 그룹에 대 한 관리 계정 만들기
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c71b96f6c44cfc2b14b4c5d203f876e55cc728ec
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855634"
---
# <a name="appendix-i-creating-management-accounts-for-protected-accounts-and-groups-in-active-directory"></a>부록 i: Active Directory의 보호 된 계정 및 그룹에 대 한 계정 관리

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

높은 권한 있는 그룹에서 영구 멤버 자격에 의존 하지 않는 한 Active Directory 모델을 구현 하는의 과제 중 하나는 임시 그룹의 멤버 자격이 필요 하는 경우 이러한 그룹을 채울 수 있는 메커니즘 이어야 합니다. 일부 권한 있는 id 관리 솔루션 소프트웨어의 서비스 계정에 DA 또는 포리스트의 각 도메인의 관리자와 같은 그룹에서 영구 멤버 자격을 부여 되어 있는지 필요 합니다. 그러나 기술적으로 필요 없는 이러한 높은 권한이 필요한 컨텍스트에서 서비스를 실행 하는 권한 있는 Identity 관리 (PIM) 솔루션에 대 한 합니다.  
  
이 부록에서는 기본적으로 구현 된 또는 타사 PIM 솔루션에 대 한 권한을 제한 하는 고 엄격 하 게 제어할 수 있지만 임시 권한 상승이 필요한 경우 Active Directory의 권한 있는 그룹을 채우는 데 사용할 수 있는 계정 만들기를 사용할 수 있는 정보를 제공 합니다. PIM 네이티브 솔루션으로 구현 하는 경우 이러한 계정을 사용할 수 있습니다 관리 담당자 임시 그룹 채우기를 수행 하지 하 고 타사 소프트웨어를 통해 PIM를 구현 하는 경우 이러한 계정은 서비스 계정으로 작동 하는 데 활용할 수 있습니다.  
  
> [!NOTE]  
> 이 부록에서 설명 하는 절차는 Active Directory에서 높은 권한 있는 그룹의 관리 하는 접근 방식을 제공 합니다. 필요에 따라, 추가 제한을 추가 하려면이 절차를 조정 하거나 여기에 설명 되어 있는 제한의 일부를 생략할 수 있습니다.  
  
## <a name="creating-management-accounts-for-protected-accounts-and-groups-in-active-directory"></a>Active Directory의 보호 된 계정 및 그룹에 대 한 계정 관리

과도 한 권한 부여 관리 계정을 요구 하지 않고 권한 있는 그룹의 구성원을 관리에 사용할 수 있는 계정 만들기 및 사용 권한 구성 이어지는 단계별 지침에 설명 된 네 가지 일반 작업:  
  
1.  첫째, 만들어야 하는 계정을 관리 하는 그룹의 관계를 이러한 계정은 제한 된 신뢰할 수 있는 사용자 집합으로 관리 해야 하기 때문에 합니다. 따로 저장 권한 및 보호 된 계정 및 도메인의 일반적인 인구에서 시스템을 수용 하는 OU 구조 아직 없는 경우 만들어야 합니다. 이 부록에 구체적인 지침은 제공 되지 않으면 있지만 스크린 샷을 OU 계층의 예를 보여 줍니다.  
  
2.  관리 계정을 만듭니다. 이러한 계정은 "일반" 사용자 계정으로 작성 하 고 기본적으로 사용자에 게 이미 부여 된 것 이외의 없는 사용자 권한이 부여 해야 합니다.  
  
3.  만들어진 사용 하도록 설정 하 고 계정 (첫 번째 단계에서 만든 그룹)를 사용할 수 있는 제어 하는 것 외에도 특별 한 용도로 사용할 수 있도록 하는 관리 계정에 제한을 구현 합니다.  
  
4.  AdminSDHolder 개체 관리 계정이 도메인에서 권한 있는 그룹의 구성원 자격을 변경할 수 있도록 각 도메인에서 권한을 구성 합니다.  
  
철저 하 게 모든이 절차를 테스트 하 고 사용자 환경에 프로덕션 환경에서 구현 하기 전에 필요에 따라이 수정 해야 합니다. 모든 설정이 예상 대로 작동 하는지 확인 해야 (일부 테스트 절차는이 부록의 내용 제공), 하 고는 관리 계정을 사용할 수 없는 복구를 위해 보호 그룹을 채우는 데 사용할 재해 복구 시나리오를 테스트 해야 합니다. 백업 및 Active Directory를 복원 하는 방법에 대 한 자세한 내용은 참조는 [AD DS 백업 및 복구 단계별 가이드](https://technet.microsoft.com/library/cc771290(v=ws.10).aspx)합니다.  
  
> [!NOTE]  
> 이 부록에서 설명 하는 단계를 구현 하 여 EAs, DAs, BAs 등 가장 높은 권한 Active Directory 그룹 뿐만 아니라, 각 도메인의 모든 보호 된 그룹의 구성원을 관리할 수 있는 계정을 만듭니다. Active Directory의 보호 된 그룹에 대 한 자세한 내용은 참조 하세요. [부록 c: 보호 된 계정 및 Active Directory에서 그룹](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)합니다.  
  
### <a name="step-by-step-instructions-for-creating-management-accounts-for-protected-groups"></a>보호 그룹에 대 한 관리 계정을 만들기 위한 단계별 지침  
  
#### <a name="creating-a-group-to-enable-and-disable-management-accounts"></a>설정 및 관리 계정을 해제 하는 그룹 만들기

관리 계정 암호에 사용할 때마다 다시 설정 해야 하 고 것을 요구 하는 활동 완료 되 면 해제 되어야 합니다. 또한 이러한 계정에 대 한 스마트 카드 로그온 요구 사항을 구현 하는 것이 좋습니다, 있지만 선택적 구성 이며 이러한 지침 최소 컨트롤로 관리 계정을 사용자 이름 및 길고 복잡 한 암호 사용 하 여 구성할 수는 가정입니다. 이 단계에서는 관리 계정에서 암호 재설정을 사용 하도록 설정 하 고 계정을 사용할 수 없게 하는 권한이 있는 그룹을 만들게 됩니다.  
  
설정 및 관리 계정을 해제 하는 그룹을 만들려면 다음 단계를 수행 합니다.  
  
1.  위치 하는 수 보유할 수 있도록 관리 계정 OU 구조에서 그룹을 만들려면 원하는 OU를 마우스 오른쪽 단추로 클릭 하 여 **새로** 클릭 **그룹**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_115.png)  
  
2.  에 **새 개체-그룹** 대화 상자에서 그룹의 이름을 입력 합니다. 이 그룹 "모든 관리 계정 포리스트에서 활성화"을 사용 하려는 경우 유니버설 보안 그룹을 확인 합니다. 단일 도메인 포리스트가 있는 경우 각 도메인에서 그룹을 만들려는 경우에 글로벌 보안 그룹을 만들 수 있습니다. **확인**을 클릭하여 그룹을 만듭니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_116.png)  
  
3.  방금 만든 그룹을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭하고 **개체** 탭을 클릭합니다. 그룹의 **개체 속성** 대화 상자에서 **실수로 삭제 되지 않도록에서 개체 보호**, 입니다만 공인한 그렇지 않으면 사용자가 그룹을 삭제 수 있지만 하지 않는 한 다른 OU로 이동 특성을 먼저 선택 해제 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_117.png)  
  
    > [!NOTE]  
    > 그룹의 부모 관리 사용자의 제한 된 집합을 제한 하는 Ou에 사용 권한을 이미 구성한 경우 다음 단계를 수행 해야 하지 않습니다. 제공 여기 하므로 제한 된 관리 제어권이이 그룹 만든 OU 구조를 아직 구현 하지 않았기 하는 경우에 수정할 수 없도록 그룹을 보호할 수 있습니다 권한이 없는 사용자가 있습니다.  
  
4.  클릭 하 고 **멤버** 탭을 팀 멤버에 대 한 관리 계정을 사용 하도록 설정 하거나 채우는 담당할 필요할 때 그룹 보호에 대 한 계정을 추가 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_118.png)  
  
5.  이미 않았다면 등에 하는 경우는 **Active Directory 사용자 및 컴퓨터** 콘솔 **보기** 선택한 **고급 기능**합니다. 방금 만든 그룹을 마우스 오른쪽 단추로 클릭 합니다. **속성**, 를 클릭 하 고는 **보안** 탭 합니다. **보안** 탭에서 **고급**을 클릭합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_119.png)  
  
6.  에 **[그룹]에 대 한 고급 보안 설정** 대화 상자를 클릭 하 여 **상속 사용 안 함**합니다. 대화 상자가 나타나면 클릭 **변환에는이 개체에 대 한 명시적 사용 권한으로 사용 권한을 상속 받은**, 클릭 하 고 **확인** 그룹의 돌아가려면 **보안** 대화 상자입니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_120.png)  
  
7.  에 **보안** 탭에서이 그룹에 액세스를 허용 되지 않은 그룹을 제거 합니다. 예를 들어 인증 된 사용자 그룹의 이름 및 일반 속성을 읽을 수 있으려면 하지 않으려면 해당 ACE를 제거할 수 있습니다. 계정 운영자 및 이전 windows 2000 Server 액세스를 위한 호환 가능한 것과 같은 Ace를 제거할 수도 있습니다. 그러나 위치에 최소 개체 사용 권한 집합을 유지 해야 합니다. 다음 Ace를 그대로 둡니다.  
  
    -   자체  
  
    -   시스템  
  
    -   Domain Admins  
  
    -   Enterprise Admins  
  
    -   Administrators  
  
    -   Windows Authorization Access Group (있는 경우)  
  
    -   엔터프라이즈 도메인 컨트롤러  
  
    이 그룹을 관리 하려면 Active Directory에서 가장 높은 권한 있는 그룹을 허용 하 게 들릴 수 있습니다, 있지만 이러한 설정을 구현할 목표 하지 않으려면 해당 그룹의 구성원 권한이 부여 된 변경입니다. 대신, 매우 높은 수준의 권한 필요로 하는 경우, 있는 경우 권한이 부여 된 변경 내용을 성공 합니다 되도록 목표가입니다. 중첩 그룹, 권한, 권한 있는 기본값을 변경 하 고이 문서 전체에서 사용 권한을 권장 하지 않습니다.이 때문입니다. 기본 구조를 수정 하지 않고 디렉터리에서 가장 높은 권한 그룹의 멤버 자격을 비우고 초기값을 여전히 예상 대로 작동 하는 보다 안전한 환경을 만들 수 있습니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_121.png)  
  
    > [!NOTE]  
    > 이 그룹을 만든 OU 구조에는 개체에 대 한 감사 정책을 아직 구성 하지 않은 경우 구성 해야 감사 변경 내용을 기록할를이 그룹.  
  
8.  "체크 아웃" 하는 그룹의 구성을 완료 했습니다 "체크 인" 계정을 해당 작업을 완료 한 후 필요한 경우 관리 계정.  
  
#### <a name="creating-the-management-accounts"></a>관리 계정 만들기

Active Directory 설치의 권한 있는 그룹의 멤버 자격을 관리 하는 데 사용 될 하나 이상의 계정 및 가급적 백업으로 사용할 수 있는 두 번째 계정을 만들어야 합니다. 그룹, 보호 된 포리스트에 단일 도메인에 관리 계정을 만들고 모든 도메인에 대 한 관리 기능 권한을 부여 하도록 선택 하 든 또는 포리스트의 각 도메인에서 관리 계정을 구현 하 든 절차는 효과적으로 동일 합니다.  
  
> [!NOTE]  
> 이 문서의 단계는 아직 구현 하지 역할 기반 액세스 제어 및 Active Directory에 대 한 권한 있는 id 관리 하는 것으로 가정 합니다. 따라서 일부 절차는 계정이 해당 도메인에 대 한 Domain Admins 그룹의 멤버인 사용자가 수행 되어야 합니다.  
>   
> DA 권한을 가진 계정을 사용 하는 경우 구성 작업을 수행 하는 도메인 컨트롤러에 로그온 할 수 있습니다. 관리 워크스테이션에 로그온 하는 권한이 적은 계정에서 DA 권한이 필요 하지 않은 단계를 수행할 수 있습니다. 밝은 파란색 테두리가 있는 대화 상자를 보여 주는 스크린 샷을 도메인 컨트롤러에서 수행할 수 있는 활동을 나타냅니다. 어두운 파란색에서 대화 상자를 보여 주는 스크린 샷을 계정 권한을 제한 하는 관리 워크스테이션에서 수행할 수 있는 활동을 나타냅니다.  
  
관리 계정을 만들려면 다음 단계를 수행 합니다.  
  
1. 도메인의 DA 그룹의 구성원 인 계정으로 도메인 컨트롤러에 로그온 합니다.  

2. 시작 **Active Directory 사용자 및 컴퓨터** 관리 계정을 만들어야 OU로 이동 합니다.  

3. OU를 마우스 오른쪽 단추로 클릭 하 고 클릭 **새로** 클릭 **사용자**합니다.  

4. 에 **새 개체-사용자** 대화 상자를 원하는 명명 된 계정에 대 한 정보를 입력 한 다음 클릭 **다음**합니다.  

   ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_122.png)  
  
5. 분명 사용자 계정에 대 한 초기 암호를 제공 **사용자는 다음 로그온 할 때 암호를 변경 해야**, 선택, **사용자 암호를 변경할 수 없습니다** 및 **계정이 비활성화 되어**, 클릭 하 고 **다음**합니다.  

   ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_123.png)  

6. 확인 올바른지 계정 세부 정보를 클릭 **마침**합니다.  

7. 방금 만든 사용자 개체를 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다.  

8. 클릭 하 고 **계정** 탭 합니다.  

9. 에 **계정 옵션** 필드를 선택한는 **계정이 민감하여 위임할 수 없음** 플래그를는 **이 계정은 Kerberos AES 128 비트 암호화를 지원** 및/또는 **이 계정은 Kerberos AES 256 암호화를 지 원하는** 플래그를 클릭 하 고 **확인**.  

   ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_124.png)  

   > [!NOTE]  
   > 다른 계정과 마찬가지로이 계정에는 제한 하지만 강력한 함수가 포함 되므로 계정은 보안 관리 호스트에만 사용 해야 합니다. 사용자 환경에서 모든 보안 관리 호스트에 대 한 구현을 고려해 그룹 정책 설정을 **네트워크 보안: Kerberos에 허용 된 암호화 유형 구성** 만 가장 안전한 암호화 종류를 허용 하도록 보안 호스트에 구현할 수 있습니다.  
   >
   > 호스트에 대 한 보다 안전한 암호화 종류를 구현 하는 경우에 자격 증명 도난 공격 완화 되지 않습니다, 하지만 적절 한 사용 및 보안 호스트의 구성에서는 않습니다. 컴퓨터의 전반적인 공격 노출을 줄입니다만 권한 있는 계정에서 사용 되는 호스트에 대 한 더 강력한 암호화 유형을 설정 합니다.  
   >
   > 시스템 및 계정에서 암호화 종류를 구성 하는 방법에 대 한 자세한 내용은 참조 [Kerberos 지원 암호화 유형에 대 한 Windows 구성](http://blogs.msdn.com/b/openspecification/archive/2011/05/31/windows-configurations-for-kerberos-supported-encryption-type.aspx)합니다.  
   >
   > 이러한 설정은 Windows Server 2012, Windows Server 2008 R2, Windows 8 또는 Windows 7을 실행 하는 컴퓨터 에서만 지원 됩니다.  
  
10. 에 **개체** 탭을 선택 **실수로 삭제 되지 않도록에서 개체 보호**합니다. 이 개체도 (권한 있는 사용자의 경우) 하 여 삭제를 수 있지만 방해 하 여 AD DS 계층 구조에서 다른 OU로 이동 되지 특성을 변경할 수 있는 권한이 있는 사용자는 확인란의 선택을 취소 먼저 하지 않는 한 합니다.  

   ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_125.png)  

11. 클릭 하 고 **원격 제어** 탭 합니다.  

12. 지우기는 **원격 제어 사용** 플래그입니다. 지원 담당자가이 계정 수정 프로그램을 구현 하는이 세션에 연결 하는 데 필요한 안 있습니다.  

   ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_126.png)  

   > [!NOTE]  
   > Active Directory 모든 개체에에서 지정된 된 IT 소유자 및 있어야 지정 된 비즈니스 소유자가에 설명 된 대로 [손상에 대 한 계획](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md)합니다. (외부 데이터베이스)가 아니라 Active Directory에서 AD DS 개체의 소유권을 추적 하는 경우에이 개체의이 속성에 적절 한 소유권 정보를 입력 해야 합니다.  
   >
   > 이 경우 비즈니스 소유자는 대개 IT 부서는 andthere 비즈니스 소유자가 있는 IT 소유자에 대 한 금지 없습니다. 개체의 소유권을 설정 하는 점은 변경 해야 할 개체에 아마도 년 초기 생성에서 하는 경우 연락처를 식별할 수 있도록 하는 것입니다.  

13. 클릭 된 **조직** 탭 합니다.  

14. AD DS 개체 표준 프로그램에 필요한 모든 정보를 입력 합니다.  

   ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_127.png)  

15. 클릭 된 **전화 접속** 탭 합니다.  

16. 에 **네트워크 액세스 권한** 필드를 선택한 **액세스 거부**합니다. 이 계정은 해야 원격 연결을 통해 연결할 필요는 없습니다.  

   ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_128.png)  

   > [!NOTE]  
   > 이 계정은 사용자 환경에서 읽기 전용 도메인 컨트롤러 (Rodc)에 로그온 하는 많지 않습니다. 그러나 해야 상황에서 필요한 계정에 로그온 RODC에 로그온 추가 해야이 계정이 Denied RODC Password Replication Group에 해당 암호는 RODC에 캐시 되지 않도록 합니다.  
   >
   > 각 사용 후 계정 암호를 다시 설정 해야 하 고 계정을 사용 하지 않도록 설정 해야 하지만이 설정을 구현 하는 계정에 나쁜 영향 없고 관리자 계정의 암호를 다시 설정 하 고 비활성화가 잊어버린 경우에 도움이 될 수 있습니다.  

17. 클릭 하 고 **소속** 탭 합니다.  

18. **추가**를 클릭합니다.  

19. 형식 **Denied RODC Password Replication Group** 에 **선택 사용자, 연락처, 컴퓨터** 대화 상자를 클릭 하 고 **이름 확인**합니다. 개체 선택기에서 그룹의 이름에 밑줄이 클릭 **확인** 이제 계정이 다음 스크린 샷에 표시 되는 두 그룹의 구성원 인지 확인 합니다. 보호 그룹에 계정을 추가 하지 마십시오.  

20. **확인**을 클릭합니다.  

   ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_129.png)  

21. 클릭 하 고 **보안** 탭을 클릭 **고급**합니다.  

22. 에 **고급 보안 설정** 대화 상자를 클릭 하 여 **상속 사용 안 함** 명시적 권한이 상속된 된 사용 권한을 복사 하 고을 클릭 **추가**합니다.  

   ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_130.png)  

23. 에 **[Account]에 대 한 사용 권한 항목** 대화 상자를 클릭 **보안 주체 선택** 이전 절차에서 만든 그룹을 추가 합니다. 대화 상자의 아래쪽으로 스크롤하여 클릭 **모두 지우기** 모든 기본 권한을 제거 합니다.  

   ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_131.png)  

24. 맨 위에 있는 스크롤은 **권한 항목** 대화 상자입니다. 확인는 **형식** 드롭다운 목록이로 설정 되어 **허용**, 및는 **에 적용 됩니다** 드롭 다운 목록에서 **이 개체만**합니다.  

25. 에 **권한을** 필드를 선택한 **모든 속성 읽기**, **대 한 읽기 권한이**, 및 **암호 재설정**합니다.  

   ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_132.png)  

26. 에 **속성** 필드를 선택한 **userAccountControl 읽기** 및 **userAccountControl 쓰기**합니다.  

27. 클릭 **확인**, **확인** 다시는 **고급 보안 설정** 대화 상자입니다.  

   ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_133.png)  

   > [!NOTE]  
   > **userAccountControl** 특성 여러 계정 구성 옵션을 제어 합니다. 특성에 대 한 쓰기 권한을 부여 하는 경우 일부 구성 옵션을 변경할 수 있는 권한을 부여할 수 없습니다.  

28. 에 **그룹 또는 사용자 이름** 필드는 **보안** 탭에서 액세스 계정을 관리 하거나 허용 되지 않은 모든 그룹을 제거 합니다. Everyone 그룹 및 자체 계산 계정 등 Deny Ace를 사용 하 여 구성 된 모든 그룹을 제거 하지 마십시오 (해당 ACE 때 설정 된는 **사용자 암호를 변경할 수 없음** 플래그 계정 작성 하는 동안 활성화 되었습니다. 또한 방금 추가한 그룹, 시스템 계정 또는 EA, DA, BA, 또는 Windows Authorization Access Group 같은 그룹 제거 하지 마십시오.  

   ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_134.png)  

29. 클릭 **고급** 및 고급 보안 설정 대화 상자는 다음 스크린샷과 유사 표시 되는지 확인 합니다.  

30. 클릭 **확인**, 및 **확인** 다시 계정 속성 대화 상자를 닫습니다.  

   ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_135.png)  

31. 첫 번째 관리 계정의 설치가 이제 완료 됩니다. 이후 절차에서 계정을 테스트 합니다.  

##### <a name="creating-additional-management-accounts"></a>추가 관리 계정 만들기

이전 단계를 반복 하 여, 방금 만든 계정에 복사 하 여 또는 원하는 구성 설정을 사용 하 여 계정을 만들 수 있는 스크립트를 만들어 추가 관리 계정을 만들 수 있습니다. 그러나 방금 만든 계정을 복사 하는 경우 새 계정으로 복사 되지 것입니다 다 수의 사용자 지정된 설정 및 Acl 및 대부분의 구성 단계를 반복 해야 note 합니다.  
  
대신 채우고 unpopulate 보호 된 그룹에 대 한 권한을 위임할 수 있는 그룹을 만들지만 보안 그룹 및 계정에 배치 해야 합니다. 보호 그룹의 구성원을 관리 하는 기능을 허용 하는 매우 적은 계정을 디렉터리에 있을 것 때문에 개별 계정을 만드는 가장 간단한 방법은 수 있습니다.  
  
관리 계정의 넣을 있는 그룹을 만들려면 원하는 방법에 관계 없이 앞에서 설명한 대로 각 계정에 보안을 확인 해야 합니다. GPO의 제한 사항에 설명 된 것과 유사한 구현도 고려해 야 [부록 d: Active Directory에서 기본 제공 관리자 계정 보안](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)합니다.  
  
##### <a name="auditing-management-accounts"></a>감사 관리 계정

최소한 계정에 대 한 모든 쓰기를 기록 하려면 계정에 대 한 감사를 구성 해야 합니다. 이 성공적으로 계정을 사용 하도록 설정 하 고 권한이 부여 된 사용 중 하지만 식별 하는 데도 권한이 없는 사용자가 조작 하려고 계정 암호 재설정 식별 뿐만 아니라 수 있습니다. 실패 한 쓰기는 계정에 보안 정보 및 이벤트 모니터링 SIEM () 시스템에 해당 하는 경우, 캡처하고 잠재적인 단점을 조사 하는 일을 담당 직원에 게 알림을 제공 하는 경고를 트리거해야 합니다.  
  
메뉴 및 도구 모음을 SIEM 솔루션 관련 된 보안 원본 (예를 들어: 이벤트 로그, 응용 프로그램 데이터, 네트워크 스트림, 맬웨어 방지 제품 및 침입 검색 원본)에서 이벤트 정보를 가져올 데이터를 정렬할 지능형 보기와 자동 관리 작업을 확인 하려고 합니다. 많은 상용 SIEM 솔루션이 있으며 많은 기업이 프라이빗 구현을 만듭니다. 보안 모니터링 및 문제 대응 기능 하도록 설계 되 고 적절 하 게 구현 된 SIEM 대폭 향상 시킬 수 있습니다. 그러나 기능과 정확도 다릅니다 단시간 솔루션입니다. 이 문서의 범위를 벗어나는으로 SIEMs 하지만 모든 SIEM 구현자에 의해 포함 된 특정 이벤트 권장 사항을 고려해 야 합니다.  
  
도메인 컨트롤러에 대 한 권장된 감사 구성 설정에 대 한 자세한 내용은 참조 [손상의 기호에 대 한 Active Directory 모니터링](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)합니다. 도메인 컨트롤러 관련 구성 설정에 제공 된 [손상의 기호에 대 한 Active Directory 모니터링](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)합니다.  
  
#### <a name="enabling-management-accounts-to-modify-the-membership-of-protected-groups"></a>보호 되는 그룹의 멤버 자격을 수정 하는 관리 계정을 사용 하도록 설정

이 절차에서는 새로 만든된 관리 계정이 도메인의 보호 된 그룹의 멤버 자격을 수정할 수 있도록 도메인의 AdminSDHolder 개체에 사용 권한을 구성 합니다. 이 절차는 그래픽 사용자 인터페이스 (GUI)를 통해 수행할 수 없습니다.  
  
에 설명 된 대로 [부록 c: 보호 된 계정 및 Active Directory에서 그룹](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md), SDProp 작업이 실행 될 때 도메인의 AdminSDHolder 개체를 효과적으로 "복사"에 대 한 ACL 개체를 보호 합니다. 보호 되는 그룹 및 계정에서에서 상속 하지 않는 사용 권한을 AdminSDHolder 개체입니다. AdminSDHolder 개체에 일치 하도록 해당 권한은 명시적으로 설정 합니다. 따라서 AdminSDHolder 개체에 대 한 권한을 수정 하면 대상으로 하는 보호 된 개체의 형식에 적절 한 특성에 대 한 수정할 해야 있습니다.  
  
이 경우 있습니다 됩니다 수 부여에 새로 만든된 관리 계정을 읽기 위해 및 멤버 특성에 대 한 쓰기 그룹 개체를 허용 합니다. 그러나 AdminSDHolder 개체 그룹 개체 아니며 그룹 특성 그래픽 ACL 편집기에 표시 되지 않습니다. Dsacls 명령줄 유틸리티를 통해 사용 권한 변경 내용을 구현 하는 이러한 이유 때문입니다. (사용 안 함된) 관리 계정 권한 보호 되는 그룹의 구성원 자격 수정에 부여 하려면 다음 단계를 수행 합니다.  
  
1.  도메인 컨트롤러는 PDC 에뮬레이터 (PDCE) 역할 이루어졌습니다 DA 그룹의 멤버인 도메인 사용자 계정의 자격 증명으로 도메인 컨트롤러 가급적에 로그온 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_136.png)  
  
2.  관리자 권한 명령 프롬프트를 마우스 오른쪽 단추로 클릭 하 여 **명령 프롬프트** 클릭 **관리자 권한으로 실행**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_137.gif)  
  
3.  권한 상승을 승인를 묻는 메시지가 나타나면 클릭 **예**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_138.gif)  
  
    > [!NOTE]  
    > 권한 상승 및 사용자 계정 컨트롤 (UAC) Windows에서에 대 한 자세한 내용은 참조 [UAC 프로세스 및 상호 작용](https://technet.microsoft.com/library/dd835561(v=WS.10).aspx) TechNet 웹 사이트입니다.  
  
4.  명령 프롬프트 (도메인 관련 정보로 대체) 하는 형식 **Dsacls [사용자 도메인에 있는 AdminSDHolder 개체의 고유 이름] [관리 계정 UPN] /G: RPWP; 구성원**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_139.gif)  
  
    이전 명령 (대/소문자 구분 하지 않음)은 다음과 같습니다.  
  
    -   Dsacls 설정 하거나 Ace 디렉터리 개체에 표시 됩니다.  
  
    -   CN AdminSDHolder, CN = System, DC = 명인 = msft 수정할 개체를 식별 합니다.  
  
    -   /G은 ACE 권한 부여 구성 되어 있는지 나타냅니다.  
  
    -   PIM001@tailspintoys.msft 이름 UPN (사용자 계정)의 Ace 부여 보안 주체는  
  
    -   RPWP 부여 속성 읽기 및 쓰기 권한을 속성  
  
    -   멤버의 이름인 속성 (특성)에 사용 권한을 설정할 수  
  
    사용에 대 한 자세한 내용은 **Dsacls**, 명령 프롬프트에서 매개 변수 없이 Dsacls를 입력 합니다.  
  
    도메인 관리 계정을 여러 개를 만든 경우 각 계정에 대해 Dsacls 명령을 실행 해야 합니다. AdminSDHolder 개체에서 ACL 구성을 완료 했으면, 실행 또는 예약 된 실행이 완료 될 때까지 대기 하도록 SDProp를 강제로 수행 해야 합니다. 실행 하는 SDProp 강제 적용에 대 한 내용은 "실행 SDProp Manually"를 참조 [부록 c: 보호 된 계정 및 Active Directory에서 그룹](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)합니다.  
  
    SDProp이 실행 될 때 도메인의 보호 된 그룹에는 AdminSDHolder 개체에 대 한 변경 내용이 적용 된 것을 확인할 수 있습니다. 앞에서 설명한 이유 때문에 AdminSDHolder 개체에 ACL을 확인 하 여이 확인할 수 없는 있지만 보호 된 그룹에 Acl을 확인 하 여 사용 권한이 적용 된 것을 확인할 수 있습니다.  
  
5.  **Active Directory 사용자 및 컴퓨터**, 를 설정 했는지 확인 **고급 기능**합니다. 이렇게 하려면 클릭 **보기**, 를 찾아는 **Domain Admins** 그룹의 그룹을 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다.  
  
6.  클릭 된 **보안** 탭을 클릭 **고급** 를 열려면는 **도메인 관리자에 대 한 고급 보안 설정** 대화 상자.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_140.gif)  
  
7.  선택 **관리 계정에 대 한 ACE 허용** 클릭 **편집**합니다. 해당 계정에만 부여 확인 **읽기 구성원** 및 **쓰기 구성원** DA 그룹과 클릭에 대 한 권한을 **확인**합니다.  
  
8.  클릭 **확인** 에 **고급 보안 설정** 대화 상자를 클릭 하 고 **확인** DA 그룹에 대 한 속성 대화 상자를 다시 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_141.gif)  
  
9. 이전 단계를 반복 하 여 도메인;에서 보호 되는 다른 그룹에 대 한 사용 권한을 모든 보호 그룹에 대해 동일 해야 합니다. 이제이 도메인의 보호 된 그룹에 대 한 관리 계정의 생성 및 구성 완료 했습니다.  
  
    > [!NOTE]  
    > 그룹의 구성원이 Active Directory에 쓰기 권한이 있는 계정을 그룹에 자신을 추가할 수도 수 있습니다. 이 동작은 의도적으로 설계 비활성화할 수 없습니다. 이러한 이유로 때 사용 중이 아님, 사용 하지 않도록 설정 하는 관리 계정을 항상 보존 해야와 밀접 하 게 모니터링 하는 계정 사용 안 함 하 고 사용 되기 합니다.  
  
#### <a name="verifying-group-and-account-configuration-settings"></a>그룹 및 계정 구성 설정 확인

만들어졌으며 (포함 하는 가장 높은 권한이 필요한 EA, DA 및 BA 그룹)는 도메인의 보호 된 그룹의 멤버 자격을 수정할 수 있는 관리 계정 구성 했으므로 계정 및 해당 관리 그룹 만들어졌는지 제대로 확인 해야 합니다. 확인이 일반 작업으로 이루어집니다.  
  
1.  테스트를 사용 하도록 설정 하 고 되었는지 확인 하 수 있는 그룹의 멤버를 사용 하도록 설정 하 고 계정을 사용할 수 없게 하 고 자신의 암호를 재설정할 관리 계정에서 다른 관리 작업을 수행할 수 없습니다 관리 계정을 사용 하지 않도록 설정할 수 있는 그룹입니다.  
  
2.  테스트를 추가할 수 및 멤버 제거는 도메인에서 그룹을 보호 하지만 보호 된 계정 및 그룹의 다른 속성을 변경할 수 없습니다 확인 하려면 관리 계정이 있습니다.  
  
##### <a name="test-the-group-that-will-enable-and-disable-management-accounts"></a>테스트 그룹을 설정 하 고 관리 계정 사용 안 함
  
1.  관리 계정을 사용 하도록 설정 하 고 해당 암호를 재설정를 테스트 하려면 워크스테이션에 로그온 한 보안 관리 그룹의 구성원 인 계정으로에서 만든 [부록 i: 계정 및 Active Directory에서 그룹 보호에 대 한 관리 계정을 만드는](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_142.gif)  
  
2.  열기 **Active Directory 사용자 및 컴퓨터**, 관리 계정을 마우스 오른쪽 단추로 클릭 하 고 클릭 **계정 사용**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_143.gif)  
  
3.  계정이 설정 되어 있는지 확인 하는 대화 상자가 표시 됩니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_144.gif)  
  
4.  다음으로, 관리 계정에서 암호를 다시 설정 합니다. 이렇게 하려면 계정 다시 마우스 오른쪽 단추로 클릭 하 고 클릭 **암호 재설정**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_145.gif)  
  
5.  계정에 대 한 새 암호를 입력의 **새 암호** 및 **암호 확인** 필드 및 클릭 **확인**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_146.gif)  
  
6.  계정의 암호 다시 설정 되었는지 확인 하는 대화 상자가 나타납니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_147.gif)  
  
7.  이제 관리 계정의 추가 속성을 수정 하려고 합니다. 계정을 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**, 를 클릭 하 고는 **원격 제어** 탭 합니다.  
  
8.  선택 **원격 제어 사용** 클릭 **적용**합니다. 작업 실패와 **액세스가 거부 되었습니다.** 오류 메시지가 표시 됩니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_148.gif)  
  
9. 클릭 된 **계정** 는 계정에 대 한 탭 하 고 계정의 이름, 로그온 시간 또는 로그온 워크스테이션을 변경 하려고 합니다. 실패 하 고 계정 옵션을 통해 제어 되지 않으므로 해야 모든는 **userAccountControl** 특성 수정 하기 위해 사용할 수 없으며 흐리게 표시 해야 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_149.gif)  
  
10. DA 그룹과 같은 보호 그룹에 관리 그룹을 추가 하려고 했습니다. 클릭할 때 **확인**, 그룹을 수정할 권한이 사용자에 게 알리는 메시지가 표시 됩니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_150.gif)  
  
11. 구성할 수 없음을 아무 것도 제외 하 고 관리 계정에 확인 하는 데 필요한 만큼 추가 테스트를 수행 **userAccountControl** 설정 및 암호를 다시 설정 합니다.  
  
    > [!NOTE]  
    > **userAccountControl** 특성 여러 계정 구성 옵션을 제어 합니다. 특성에 대 한 쓰기 권한을 부여 하는 경우 일부 구성 옵션을 변경할 수 있는 권한을 부여할 수 없습니다.  
  
##### <a name="test-the-management-accounts"></a>테스트 관리 계정

보호 그룹의 구성원을 변경할 수 있는 하나 이상의 계정을 사용 하도록 설정한 했으므로 계정을 확인은 보호 그룹 구성원 자격을 수정할 수 있지만 보호 된 계정 및 그룹에서 기타 수정 작업을 수행할 수 없습니다를 테스트할 수 있습니다.  
  
1.  보안 관리 호스트에 첫 번째 관리 계정으로 로그온 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_151.gif)  
  
2.  시작 **Active Directory 사용자 및 컴퓨터** 찾아서는 **Domain Admins 그룹**합니다.  
  
3.  마우스 오른쪽 단추로 클릭는 **Domain Admins** 묶고 클릭 **속성**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_152.gif)  
  
4.  에 **도메인 관리자 속성**, 를 클릭 하는 **멤버** 탭 및 **클릭** 추가 합니다. 임시 도메인 관리자 권한이 주어 집니다을 클릭 하는 계정의 이름을 입력 **이름 확인**합니다. 계정 이름에 밑줄이 클릭 **확인** 돌아가려면는 **멤버** 탭 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_153.gif)  
  
5.  에 **멤버** 탭을 **도메인 관리자 속성** 대화 상자를 클릭 하 여 **적용**합니다. 클릭 한 후 **적용**, 계정 DA 그룹의 구성원 상태를 유지 해야 하 고 없음 오류 메시지를 받아야 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_154.gif)  
  
6.  클릭는 **하 여 관리 되는** 탭에 **도메인 관리자 속성** 대화 상자 모든 필드에 텍스트를 입력할 수 없는 모든 단추는 회색으로 확인 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_155.gif)  
  
7.  클릭 된 **일반** 탭에 **도메인 관리자 속성** 대화 상자의 해당 탭에 대 한 정보를 수정할 수 없음을 확인 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_156.gif)  
  
8.  필요에 따라 보호 되는 추가 그룹에 대해 이러한 단계를 반복 합니다. 완료 되 면 로그 설정 및 관리 계정을 사용 하지 않도록 설정 하기 위해 만든 보안 관리 호스트 그룹의 구성원 인 계정으로 로그온 합니다. 그런 다음 방금 테스트 하 고 계정을 사용 하지 않도록 설정 하는 관리 계정에 암호를 다시 설정 합니다. 관리 계정 및 그룹 계정을 설정 하거나 해제 하는 일을 담당 될의 설치를 완료 했습니다.  
