---
ms.assetid: 13fe87d9-75cf-45bc-a954-ef75d4423839
title: "부록 I-보호 계정과 Active Directory에 있는 그룹에 대 한 관리 계정 만들기"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 666180adca691d6c9783a43063df76877115fc40
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="appendix-i-creating-management-accounts-for-protected-accounts-and-groups-in-active-directory"></a>부록 i: 보호 계정과 Active Directory에 있는 그룹에 대 한 계정을 만들 관리

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

  
## <a name="appendix-i-creating-management-accounts-for-protected-accounts-and-groups-in-active-directory"></a>부록 i: 보호 계정과 Active Directory에 있는 그룹에 대 한 계정을 만들 관리  

매우 권한이 있는 그룹의 영구 구성원에 의존 하지 않는 한 Active Directory 모델을 구현에서 문제 중 하나는 메커니즘을 그룹의 회원 임시 필요할 때 이러한 그룹을 채울 여야 합니다. 일부 id 권한 관리 솔루션 필요 소프트웨어의 서비스 계정 영구 그룹 구성원에 DA 등 각 도메인 숲에서 관리자 권한이 부여 됩니다. 그러나 기술적 필요는 없습니다 권한이 높은 이러한 상황에서 해야만 서비스를 실행 하려면 신원을 권한 관리 (PIM) 해결 방법입니다.  
  
이 부록 기본적으로 구현 또는 제 3 자 PIM 해결 방법에 대 한 권한이 제한 엄격 제어할 수 있습니다 있지만 임시 상승 필요할 때 Active Directory에 권한이 있는 그룹 채울 데 사용할 수 있는 계정 만들기를 사용할 수 있는 정보를 제공 합니다. 임시 그룹 인구 수행 하려면 관리 담당자가 이러한 계정을 사용할 수 기본 솔루션으로 PIM 구현 하는 경우 및 타사 소프트웨어를 통해 PIM를 구현 하는 경우 서비스 계정으로 작동 하는 데이 계정을 대응할 수 있습니다.  
  
> [!NOTE]  
> 이 부록에 설명 된 절차 관리 매우 권한이 있는 그룹 Active Directory에의 한 가지 방법을 제공 합니다. 이 절차를 필요에 따라 추가 제한 사항이 추가 조정 하거나 일부는 여기에 설명 된 제한 생략 수 있습니다.  
  
### <a name="creating-management-accounts-for-protected-accounts-and-groups-in-active-directory"></a>보호 된 계정과 Active Directory에 있는 그룹에 대 한 계정을 만들 관리  
과도 하 게 권한을 부여 관리 계정을 않고도 권한이 있는 그룹의 회원 관리에 사용할 수 있는 계정 만들기와 권한을 단계별 지침에 따라 있는에 대해 설명 하는 네 일반 활동의 구성 같습니다.  
  
1.  첫째, 이러한 계정은 신뢰할 수 있는 사용자의 제한 된 집합으로 관리 해야 하기 때문에, 계정을 관리 하는 그룹을 만들 해야 있습니다. 아직 OU 구조 레이어에서 권한 및 보호 계정과 시스템 도메인에 있는 일반 인구에서 제공 하는 없는 경우 만들어야 합니다. 특정 명령을이 부록에를 제공 하지 않은 하지만 스크린샷 OU 계층의 예를 표시 됩니다.  
  
2.  관리 계정을 만듭니다. 이러한 계정은 "일반" 사용자 계정으로 작성 하 고 이미 기본적으로 사용자에 게 부여 된 이상 없이 사용자 권한이 부여 해야 합니다.  
  
3.  제한 된 생성 된 뿐 아니라 사용 하도록 설정 하 고 계정을 (그룹 첫 번째 단계에서 만든) 사용할 수 있는 사람 특수 용도로 사용할 수 있도록 관리 계정에 구현 합니다.  
  
4.  권한을 관리 계정을 도메인에 있는 권한이 있는 그룹 구성원을 변경할 수 있도록 각각 도메인에 있는 AdminSDHolder 개체의 구성 합니다.  
  
철저 하 게이 절차의 모든 테스트 하 고 생산 환경에서 구현 하기 전에 필요한 귀하의 환경에 대 한 수정 해야 합니다. 모든 설정 예상 대로 작동 하는지 확인 해야 (일부 테스트 절차를 제공 되는이 부록에) 관리 계정은 복구 목적을 위해 보호 된 그룹을 사용할 수 없습니다 장애 복구 시나리오 테스트 해야 합니다. For more information about backing up and restoring Active Directory, see the [AD DS Backup and Recovery Step-by-Step Guide](https://technet.microsoft.com/library/cc771290(v=ws.10).aspx).  
  
> [!NOTE]  
> 이 부록에 설명 된을 구현 하 여 각 도메인으로 보호 되는 모든 그룹, EAs, DAs BAs 등 가장 높은 권한 Active Directory 그룹 뿐만 아니라 구성원을 관리할 수 있는 계정을 만듭니다. 보호 된 그룹 Active Directory에 대 한 자세한 내용은 참조 [부록 c: 보호 계정 및 Active Directory에 그룹](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)합니다.  
  
#### <a name="step-by-step-instructions-for-creating-management-accounts-for-protected-groups"></a>보호 된 그룹에 대 한 관리 계정을 만드는 데 단계별 지침  
  
##### <a name="creating-a-group-to-enable-and-disable-management-accounts"></a>및 계정 관리 해제 하는 그룹 만들기  
계정 관리가 암호를 사용 하 여 각에서 초기화 해야 하며 하는가 작업을 완료 했으면 않도록 합니다. 이러한 계정에 대해 스마트 카드 로그온 요구 사항을 구현 수도, 있지만 선택적 구성 하며이 지침 가정 최소 컨트롤로 관리 계정의 사용자 이름 및 암호 복잡 하 고 긴으로 구성할 수 됩니다. 이 단계에서 관리 계정의 암호를 다시 사용 하도록 설정 하 고 계정을 사용할 수 없게 수 있는 권한이 있는 그룹을 만듭니다.  
  
활성화 하 고 관리 계정 사용 중지 그룹을 만든 다음 단계를 수행 합니다.  
  
1.  위치 사용자는 수 주택 관리 계정 OU 구조 그룹을 만들려면 OU 마우스 오른쪽 단추로 클릭 클릭 **새로** 클릭 **그룹**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_115.png)  
  
2.  **새 개체-그룹** 대화 상자에서 그룹의 이름을 입력 합니다. 이 그룹에 숲 속의 모든 관리 계정 "정품 인증"을 사용 하려는 경우 범용 보안 그룹을 확인 합니다. 단일 도메인 숲 하는 경우 각 도메인에 있는 그룹을 만들 하려는 경우에 전 세계 보안 그룹을 만들 수 있습니다. 클릭 **확인** 그룹을 만들 수 있습니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_116.png)  
  
3.  Right-click the group you just created, click **Properties**, and click the **Object** tab. In the group's **Object property** dialog box, select **Protect object from accidental deletion**, which will not only prevent otherwise-authorized users from deleting the group, but also from moving it to another OU unless the attribute is first deselected.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_117.png)  
  
    > [!NOTE]  

    > 그룹의 부모 관리 제한 된 집합 사용자를 제한 하려면 Ou에서 이미 사용 권한을 구성 하는 경우 다음 단계를 수행 해야 없습니다. 이러한 제공 여기이 그룹 만든 OU 구조 대 한 제한 된 관리 제어 아직 구현 되지 있는 경우에 수정에 대 한 그룹을 보호할 수 있도록 권한 없는 사용자나 합니다.  
  
4.  클릭는 **회원** 탭 하 고 관리 계정을 사용 하거나 채우기 책임이 팀의 구성원 보호 필요할 때 그룹에 대 한 계정을 추가 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_118.png)  
  
5.  수행 하지 않은 이미,의 경우는 **Active Directory 사용자와 컴퓨터** 콘솔를 클릭 **보기** 선택한 **고급 기능**합니다. Right-click the group you just created, click **Properties**, and click the **Security** tab. On the **Security** tab, click **Advanced**.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_119.png)  
  
6.  에 **[그룹]에 대 한 고급 보안 설정을** 대화 상자를 클릭 **상속 사용 안 함**합니다. 메시지가 표시 되 면 클릭 **변환이이 개체의 명시적인 권한이에 사용 권한을 상속**를 클릭 하 고 **확인** 그룹의 돌아가려면 **보안** 대화 상자 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_120.png)  
  
7.  에 **보안** 이 그룹에 액세스 하도록 허용 되지 않을 그룹 제거를 탭 합니다. 예를 들어, 그룹의 이름 및 일반 속성에 읽을 수를 인증 된 사용자를 하지 않을 경우 해당 ACE를 제거할 수 있습니다. 액세스를 위해 계정 연산자 및 이전 windows 2000 Server 호환 되는 것과 같은 제거할 수도 있습니다. 그러나 곳에서 최소한의 개체 권한이 유지 해야 합니다. 다음 Ace 그대로 둡니다.  
  
    -   자체  
  
    -   시스템  
  
    -   도메인 관리  
  
    -   엔터프라이즈 관리  
  
    -   관리자  
  
    -   Windows 인증 액세스 그룹 (가능한 경우)  
  
    -   엔터프라이즈 도메인 컨트롤러  
  
    Active directory 관리이 그룹에 높은 권한이 있는 그룹 수 있도록 들릴 수, 있지만 해당 그룹의 회원 공인된 변경 하지 못하도록 하려면 하지 구현 이러한 설정의 목표가입니다. 대신, 매우 높은 수준의 권한이 필요한 경우를 사용 하는 경우 공인된 변경 성공는 되도록 목표가입니다. 것은 이런 이유 때문 그룹 중첩 권리를 변경 기본 권한 및 사용 권한을이 문서 전체의 권장 하지 않습니다. 기본 구조 그대로 디렉터리에 있는 가장 높은 권한 그룹의 회원 비우기을 여전히 예상 대로 작동 하는 보안이 환경을 만들 수 있습니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_121.png)  
  
    > [!NOTE]  
    > 이 그룹을 만든 OU 구조에 감사 정책 개체를 아직 구성 하지 않은 경우 구성 해야 감사 로그 변경 하려면이 그룹입니다.  
  
8.  "확인" 하는 데 사용 될 그룹의 구성을 완료 관리 필요한 경우 "체크 인"는 계정 자녀의 활동 완료 되 면 계정 합니다.  
  
##### <a name="creating-the-management-accounts"></a>관리 계정 만들기  
Active Directory에 권한이 있는 그룹의 회원 관리 하는 데 사용 될 수 있는 하나 이상의 계정 고 백업으로 처리 하기 위해 두 번째 계정 가능 만들어야 합니다. 각 도메인 숲에서 계정 관리 구현 하 든 절차는 효과적으로 동일한 또는 그룹을 보호 사용자가 선택 하 고 숲 속의 단일 도메인에 있는 관리 계정을 만들고 관리 기능을 모두 도메인에 대 한 권한을 부여.  
  
> [!NOTE]  
> 이 문서에 있는 단계는 아직 구현 하지 역할 기반 액세스 컨트롤과 Active Directory에 대 한 권한 있는 id 관리 가정 합니다. 따라서 해당 도메인에 있는 도메인 관리자 그룹 구성원 계정은 사용자가 일부 절차를 수행 합니다.  
>   
> DA 권한을 사용 하 여 계정을 사용 하면 구성 활동을 수행 하는 도메인 컨트롤러에 로그온 할 수 있습니다. 관리 워크스테이션 로그온 권한이 적은 계정에서 DA 권한이 필요 하지 않은 단계를 수행할 수 있습니다. 스크린샷을 가벼운 파란색에서 테두리 대화 상자를 표시 하는 도메인 컨트롤러에서 수행할 수 있는 활동을 나타냅니다. 스크린샷을 더 어두운 파란색에서 대화 상자를 표시 하는 권한을 제한 된 계정 관리 워크스테이션에서 수행할 수 있는 활동을 나타냅니다.  
  
관리 계정을 만들려면 다음 단계를 수행 합니다.  
  
1.  도메인 컨트롤러 도메인의 DA 그룹의 회원은는 계정에 로그인 합니다.  
  
2.  시작 **Active Directory 사용자와 컴퓨터** 관리 계정을 만들어야를 이동 합니다.  
  
3.  OU 마우스 오른쪽 단추로 클릭 한 **새로** 클릭 **사용자**합니다.  
  
4.  에 **새 개체-사용자** 대화 상자에 원하는 명명 계정에 대 한 정보를 입력 한 클릭 **다음**합니다.  
  
5.  도메인 컨트롤러 도메인의 DA 그룹의 회원은는 계정에 로그인 합니다.  
  
6.  시작 **Active Directory 사용자와 컴퓨터** 관리 계정을 만들어야를 이동 합니다.  
  
7.  OU 마우스 오른쪽 단추로 클릭 한 **새로** 클릭 **사용자**합니다.  
  
8.  에 **새 개체-사용자** 대화 상자에 원하는 명명 계정에 대 한 정보를 입력 한 클릭 **다음**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_122.png)  
  
9. 확인란의 선택을 취소 사용자 계정에 대 한 초기 암호를 제공 **사용자 다음 로그온 할 때 암호를 변경 해야**선택 **사용자 암호를 변경할 수 없는** 및 **계정이 비활성화 되어**, 클릭 하 고 **다음**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_123.png)  
  
10. 계정 세부 정보 정확 하 고 클릭 확인 **완료**합니다.  
  
11. 방금 만든 사용자 개체를 마우스 오른쪽 단추로 클릭 한 **속성**합니다.  
  
12. 클릭 하 고 **계정** 탭 합니다.  
  
13. **계정 옵션** 필드를는 **계정은 중요 한 위임 수 없습니다** 플래그를 선택 하 고 있는 **이 계정 Kerberos AES 128 약간 암호화를 지 원하는** 및/또는 **이 계정 Kerberos AES 256 암호화를 지 원하는** 플래그 지정, 클릭 한 **확인**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_124.png)  
  
    > [!NOTE]  
    > 와 같은 다른 계정으로이 계정, 제한 된 하지만 강력한 기능은 하므로, 계정 보안 관리 호스트에만 사용 해야 합니다. 귀하의 환경에 있는 모든 안전 하 게 관리 호스트를 고려해 야 구현 하는 그룹 정책 설정을 **네트워크 보안: Kerberos에 대 한 암호화 구성 형식을 허용** 가장 안전한 암호화 종류를 허용 하도록 안전한 호스트 구현할 수 있습니다.  
    >   
    > 하지만 호스트에 대 한 보안을 강화 암호화 유형 구현 방지할 수 없습니다 도난 공격 자격 증명을 사용 하 여 적절 한 및 보안 호스트 구성 않습니다. 강력한 암호화 유형 권한이 있는 계정 으로만 사용 되는 호스트 설정을 컴퓨터 전체적인 공격 간단히 줄일 수 있습니다.  
    >   
    > 시스템 및 계정 암호화 유형 구성에 대 한 자세한 내용은 참조 [Kerberos 지원 암호화 형식에 대 한 Windows 구성](http://blogs.msdn.com/b/openspecification/archive/2011/05/31/windows-configurations-for-kerberos-supported-encryption-type.aspx)합니다.  
    >   
    > **참고** 이러한 설정은 Windows Server 2012, Windows Server 2008 R2, Windows 8 또는 Windows 7을 실행 하는 컴퓨터에만 지원 됩니다.  
  
14. 에 **개체** 탭을 선택 하 고 **실수로 삭제 되지 않도록에서 보호 개체**합니다. 이 되더라도 개체 (도 권한이 있는 사용자의 경우)으로 삭제 되지 발생 하지만 것을 AD DS 계층을에서 다른 OU로 이동 하는 것 특성을 변경할 수 있는 권한이 있는 사용자가 있는 확인란의 선택을 취소 먼저 하지 않는 한 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_125.png)  
  
15. 클릭 하 고 **원격 제어** 탭 합니다.  
  
16. 지우기는 **원격 제어를 사용 하도록 설정** 플래그. 절대 구현 수정에 대 한이 계정 세션에 연결 하는 지원 담당자에 게 해야 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_126.png)  
  
    > [!NOTE]  
    > 모든 개체 Active Directory에 지정된 된 IT 소유자와 해야 지정된 비즈니스 소유자에 설명 된 대로 [손상에 대 한 계획](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md)합니다. 외부 데이터베이스) (반대로 Active Directory에 AD DS 개체의 소유권을 추적 하는 경우이 개체 속성에서 소유권 적절 한 정보를 입력 해야 합니다.  
    >   
    > 이 경우 비즈니스 소유자는 IT 부서 가능성이 높습니다를 andthere도 IT 소유자 되 고 비즈니스 소유자에 금지 없습니다. 개체의 소유권을 설정 하는 지점 변경 해야 할 개체에 아마도 년 초기 생성에서 하는 경우 연락처를 식별할 수 있도록 하는 것입니다.  
  
17. 클릭 하 고 **조직** 탭 합니다.  
  
18. AD DS 개체 표준에 필요한 정보를 입력 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_127.png)  
  
19. 클릭는 **전화 접속** 탭 합니다.  
  
20. 에 **네트워크 액세스 권한을** 필드를 **액세스 거부**합니다. 이 계정 해야 원격 연결을 통해 연결할 필요가 없습니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_128.png)  
  
    > [!NOTE]  
    > 가능성이이 계정 읽기 전용 Rodc (도메인 컨트롤러) 귀하의 환경에에 로그인 하는 것은 아닙니다. 그러나 해야 환경에서 필요한 계정에 로그온 RODC에 설정 된를 추가 해야이 계정을 RODC 거부 암호 복제 그룹 암호에 RODC 캐시 되지 않도록 합니다.  
    >   
    > 사용할 때마다 후 계정의 암호를 다시 설정 해야 하 고 계정을 사용 하지 않도록 설정 해야 하지만이 설정을 구현 악영향은 계정에 없고 관리자 계정 암호 다시 설정 하 고 비활성화가 잊어버린 경우에 도움이 될 수 있습니다.  
  
21. 클릭 하 고 **소속** 탭 합니다.  
  
22. 클릭 **추가**합니다.  
  
23. 입력 **RODC 암호 복제 그룹 거부** 에 **선택 사용자, 연락처, 컴퓨터** 대화 상자와 클릭 **이름 확인**합니다. 그룹의 이름을 개체 선택기에서 밑줄이 그어진를 클릭 **확인** 계정을 다음 화면에 표시 되는 두 가지 그룹의 회원 이제 인지 확인 하 고 있습니다. 계정을 보호 그룹에 추가 하지 마십시오.  
  
24. 클릭 **확인**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_129.png)  
  
25. 클릭 하 고 **보안** 탭 및 클릭 **고급**합니다.  
  
26. 에 **고급 보안 설정을** 대화 상자를 클릭 **상속 사용할 수 없게** 명시적인 권한이으로 사용 권한이 상속된 복사 및 클릭 **추가**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_130.png)  
  
27. 에 **[계정]에 대 한 권한 항목** 대화 상자에서 클릭 **주체 선택** 이전 단계에서 만든 그룹을 추가 합니다. 대화 상자 아래쪽으로 스크롤하고 클릭 **모두 지우기** 모든 기본 권한을 제거 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_131.png)  
  
28. 스크롤의 맨 위에 있는 **권한 항목** 대화 상자 합니다. 되도록는 **유형** 드롭다운 목록에서로 설정 되어 **허용**의 **에 적용 됩니다** 드롭다운 목록 **만이 개체**합니다.  
  
29. 에 **권한을** 필드를 **모든 속성 읽기**, **읽기 권한이**, 및 **암호 재설정**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_132.png)  
  
30. 에 **속성** 필드를 **userAccountControl 읽기** 및 **userAccountControl 쓰기**합니다.  
  
31. 클릭 **확인**, **확인** 다시에 **고급 보안 설정을** 대화 상자가 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_133.png)  
  
    > [!NOTE]  
    > **userAccountControl** 특성 제어 여러 계정 구성 옵션이 있습니다. 특성 쓰기 권한을 부여 하면 구성 옵션 중 일부를 변경 하는 데 사용 권한을 부여할 수 없습니다.  
  
32. 에 **그룹 또는 사용자 이름** 필드에서 **보안** 탭, 있는 그룹에 액세스 하거나 계정 관리 허용 되지 않은 제거 합니다. 모든 그룹와 자체 계산 계정와 같은 거부가로 구성 되어 있는 모든 그룹을 제거 하지 않습니다 (때 해당 ACE 설정 된는 **사용자 암호를 변경할 수 없는** 계정 만드는 동안 플래그를 사용할 수 있습니다. 또한 방금 추가한 그룹, 시스템 계정을 또는 EA, DA, 모음, Windows 인증 액세스 그룹 등 그룹 제거 되지 않습니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_134.png)  
  
33. 클릭 **고급** 고급 보안 설정 대화 상자 다음 스크린샷와 유사 있는지 확인 합니다.  
  
34. 클릭 **확인**, 및 **확인** 다시 계정의 속성 대화 상자를 닫습니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_135.png)  
  
35. 첫 번째 관리 계정 설정이 완료 됩니다. 이후 절차에 계정을 테스트 합니다.  
  
###### <a name="creating-additional-management-accounts"></a>추가 관리 계정 만들기  
이전 단계를 반복 하 여, 방금 만든 계정을 복사 하 여 또는 원하는 구성 설정으로 계정을 만드는 데 필요한 스크립트 만들어 추가 관리 계정을 만들 수 있습니다. 그러나 방금 만든 계정을 복사 하는 경우 새로운 계정으로 복사 되지는 대부분의 사용자 지정된 설정 및 Acl 및 대부분의 구성 단계를 반복 하는 note 합니다.  
  
대신을 구성 하 고 보호 그룹 unpopulate 권한 있는 위임 그룹을 만들 수 있지만 그룹과에 배치 계정 보호를 위해 해야 합니다. 보호 되는 그룹의 회원 관리 하는 기능은 허가 된 계정을 디렉터리에 매우 몇 가지 있어야, 하므로 개별 계정을 만드는 가장 간단한 방법은 수 있습니다.  
  
어떻게 관리 계정 넣을 그룹을 만들려면 선택에 관계 없이 앞에서 설명한 대로 각 계정 보안 확인 해야 합니다. GPO 제한에 설명 된 것과 비슷합니다 구현 고려해 야 [Active Directory에 부록 d: 보안 기본 제공 관리자 계정](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)합니다.  
  
###### <a name="auditing-management-accounts"></a>계정 관리 감사합니다.  
최소한 모든 쓰기 계정에 로그인 하는 계정에 대 한 감사 구성 해야 합니다. 그러면 성공 계정을 사용 하 고 허가 된 사용 하는 동안 하지만 하 여 권한 없는 사용자나 조작 하려고 계정을 식별 하기 위해 암호 재설정 뿐만 아니라 사용자의 신원을 확인 합니다. 실패 한 쓰기 계정에 보안 정보 및 이벤트 모니터링 (SIEM) 시스템에 해당 하는 경우, 캡처하고 잠재적인 타협점 조사에 대해 책임 지지 직원에 게 알림을 제공 하는 알림 실행 됩니다.  
  
SIEM 솔루션 이벤트 정보 (예: 이벤트 로그, 응용 프로그램 데이터, 네트워크 스트림, 맬웨어 방지 제품을 및 침입 검색 원본)와 관련 된 보안 소스에서 수행 하 고 대조 데이터를 지능형 보기 및 사전 조치를 시도해 보세요. 많은 상용 SIEM 솔루션 되며 많은 기업 만들기 개인 구현 합니다. 보안 모니터링 및 인시던트 응답 기능 하도록 설계 되 고 적절히 구현 SIEM 크게 향상 시킬 수 있습니다. 그러나 기능과 정확도 가격은 매우 다양 솔루션 간에 합니다. 이 문서에서는 범위를 벗어나는 SIEMs는 있지만 특정 이벤트 권장 사항을 포함 하 여 모든 SIEM 구현자 고려해 야 합니다.  
  
도메인 컨트롤러에 대 한 권장된 감사 구성 설정에 대 한 자세한 내용은 참조 [손상 기호에 대 한 Active Directory 모니터링](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)합니다. 도메인 컨트롤러 관련 구성 설정이에 제공 된 [손상 기호에 대 한 Active Directory 모니터링](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)합니다.  
  
##### <a name="enabling-management-accounts-to-modify-the-membership-of-protected-groups"></a>계정을 보호 그룹의 회원 수정 관리 활성화  
이 절차를 새로 만든된 관리 계정을 보호 되는 도메인에 있는 그룹 구성원을 수정할 수 있도록 AdminSDHolder 개체 도메인에 사용 권한을 구성 합니다. 이 절차는 그래픽 GUI (사용자 인터페이스)을 통해 수행할 수 없습니다.  
  
설명한 대로 [부록 c: 보호 계정 및 그룹 Active Directory에](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md), ACL 개체를 효과적으로 "복사" 하는 도메인의 AdminSDHolder에 SDProp 작업이 실행 되 면 개체를 보호 합니다. 보호 된 그룹과 계정 권한을 상속 하지 않는 자신의 AdminSDHolder 개체;에서 자녀가 사용 권한은 AdminSDHolder 개체에 맞게 명시적으로 설정 됩니다. 따라서 AdminSDHolder 개체에 대 한 권한을 수정 하는 경우 수정 해야 하는 대상으로 보호 된 개체의 종류에 적합 한 특성.  
  
이 경우 사용자는 수 부여 읽는 데와 개체 그룹에서 쓰기 구성원 특성 수 있도록 새로 만든된 관리 계정 합니다. 그러나 AdminSDHolder 개체 그룹 개체 아니며 그룹 특성 그래픽 ACL 편집기에 노출 되지 않습니다. 사용 권한 변경 내용을 Dsacls 명령줄 유틸리티를 통해을 구현는 이런 이유이 때문입니다. (사용할 수 없음된) 관리에 보호 그룹의 회원 수정할 계정 권한을 부여 하려면 다음 단계를 수행 합니다.  
  
1.  도메인 컨트롤러의 경우 가능 된 내용이 DA 그룹의 회원 도메인에 있는 사용자 계정의 자격 증명은 에뮬레이터 PDC (PDCE) 역할 도메인 컨트롤러에 로그인 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_136.png)  
  
2.  마우스 오른쪽 단추로 클릭 하 여 관리자 명령 프롬프트를 열고 **명령 프롬프트** 클릭 **관리자 권한으로 실행**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_137.gif)  
  
3.  를 상승 승인 하 라는 메시지가 나타나면 클릭 **예**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_138.gif)  
  
    > [!NOTE]  
    > For more information about elevation and user account control (UAC) in Windows, see [UAC Processes and Interactions](https://technet.microsoft.com/library/dd835561(v=WS.10).aspx) on the TechNet website.  
  
4.  명령 프롬프트 (도메인 관련 정보를 대체) 유형 **Dsacls [도메인에 있는 AdminSDHolder 개체의 고유 이름] /G [관리 계정 UPN]: RPWP; 회원**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_139.gif)  
  
    이전 명령 (대/소문자 구분 되지 않음)은 다음과 같습니다.  
  
    -   Dsacls 설정 하거나 Ace directory 개체에 표시 됩니다.  
  
    -   CN CN AdminSDHolder = 시스템, DC = 명인 = msft 수정 개체를 식별 합니다.  
  
    -   /G 부여 ACE 구성 되어 있는지를 나타냅니다.  
  
    -   PIM001@tailspintoys.msft이 사용자 이름 UPN (계정) Ace 부여할 수 보안 사용자의  
  
    -   RPWP 부여 속성 읽기 / 쓰기 속성 권한이  
  
    -   (특성) 속성의 이름을 사용 권한을 설정할 수 켜져 회원  
  
    사용에 대 한 자세한 내용은 **Dsacls**, Dsacls 매개 변수 명령 프롬프트에 입력 합니다.  
  
    도메인에 대 한 여러 관리 계정을 만든 경우 각 계정의 Dsacls 명령을 실행 해야 합니다. AdminSDHolder 개체에 ACL 구성을 완료 했으면, 실행 또는 그 예약된 실행 완료 될 때까지 기다렸다가 SDProp 강제로 합니다. 실행 SDProp 강제로 대 한 정보, "실행 SDProp 수동으로 참조"에서 [부록 c: 보호 계정 및 Active Directory에 그룹](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)합니다.  
  
    SDProp 실행 되 면 보호 되는 도메인에 있는 그룹에 AdminSDHolder 개체 내용을 변경 내용이 적용 된 것을 확인할 수 있습니다. 앞에서 설명한 이유로 ACL AdminSDHolder 개체를 확인 하 여이 확인할 수 없는 하지만 Acl 보호 되는 그룹에서 확인 하 여 권한을 적용 된 것을 확인할 수 있습니다.  
  
5.  **Active Directory 사용자와 컴퓨터**를 설정 했는지 확인 **고급 기능**합니다. 이렇게 하기 위해 클릭 **보기**를 찾아는 **도메인 관리자** 그룹 그룹을 마우스 오른쪽 단추로 클릭 한 **속성**합니다.  
  
6.  클릭는 **보안** 탭 및 클릭 **고급** 열려면는 **도메인 관리자에 대 한 고급 보안 설정을** 대화 상자 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_140.gif)  
  
7.  선택 **관리 계정에 대 한 ACE 허용** 클릭 **편집**합니다. 해당 계정에만 부여 확인 **읽기 회원** 및 **쓰기 회원** 누른 DA 그룹에 대 한 권한을 **확인**합니다.  
  
8.  클릭 **확인** 에 **고급 보안 설정을** 대화 상자를 클릭 하 고 **확인** DA 그룹에 대 한 속성 대화 상자를 닫고를 다시 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_141.gif)  
  
9. 이전 단계를 반복 다른 보호 되는; 도메인에 있는 그룹에 대 한 사용 권한 보호 되는 모든 그룹에 대 한 동일 해야 합니다. 이제 생성 하 고 관리 계정 보호 되는이 도메인에 있는 그룹에 대 한 구성 완료 했습니다.  
  
    > [!NOTE]  
    > 그룹의 회원 Active Directory에 쓸 수 있는 모든 계정에 추가할 수도 자체 그룹입니다. 이 동작으로 설계 이며 비활성화할 수 없습니다. 이러한 이유로 사용 하지를 사용 하지 않도록 설정 관리 계정 항상 고 해제 하 고 사용에 있을 때 계정을 모니터링 밀접 하 게 해야 합니다.  
  
##### <a name="verifying-group-and-account-configuration-settings"></a>그룹 하 고 계정 구성 설정 확인  
이제는 만들고 (권한이 가장 높은 EA, DA, 및 모음 그룹 포함)는 도메인의 보호 된 그룹 구성원을 수정할 수 있는 관리 계정을 구성, 하 고 계정 및 관리 그룹의 만든 제대로 확인 해야 합니다. 일반 작업 인증 구성 됩니다.  
  
1.  사용 하도록 설정 하 고 확인 하 그룹 캔의 회원 사용 하도록 설정 하 고 계정을 사용할 수 없게의 암호 재설정 있지만 관리 계정 관리 기타 작업을 수행할 수 없는 계정 관리를 사용 하지 않도록 설정할 수 있는 그룹을 테스트 합니다.  
  
2.  관리 계정을 추가할 수 있고 제거 멤버 도메인에 있는 그룹 보호 하지만 계정 보호 및 그룹의 다른 속성 변경할 수 없는 확인 테스트 합니다.  
  
###### <a name="test-the-group-that-will-enable-and-disable-management-accounts"></a>테스트 그룹을 사용 하도록 설정 관리 계정 사용 안 함  
  
1.  관리 계정을 사용 하 고 해당 암호를 재설정할 때 테스트를 하려면 안전 하 게 관리 워크스테이션 그룹 구성원에 해당 하는 계정에서 만든에 로그온 [부록 i: 관리 계정 만들기 보호 계정과 Active Directory에 있는 그룹에 대 한](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_142.gif)  
  
2.  열기 **Active Directory 사용자와 컴퓨터**관리 계정 마우스 오른쪽 단추로 클릭 하 고 클릭 **계정**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_143.gif)  
  
3.  대화 상자 계정을 활성화 되어 있는 확인 표시 됩니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_144.gif)  
  
4.  그런 다음, 암호 관리 계정에 다시 설정 합니다. 이렇게 하기 위해 계정을 다시 마우스 오른쪽 단추로 클릭 하 고 클릭 **암호 재설정**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_145.gif)  
  
5.  계정에 대 한 새 암호를 입력 하 고 **새 암호** 및 **암호 확인** 필드 및 클릭 **확인**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_146.gif)  
  
6.  계정에 대 한 암호 다시 설정 되었는지 확인 대화 상자가 나타납니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_147.gif)  
  
7.  이제 수정 관리 계정 추가 속성 하려고 합니다. 계정을 마우스 오른쪽 단추로 클릭 한 **속성**를 클릭 하 고 있는 **원격 제어** 탭 합니다.  
  
8.  선택 **원격 제어를 사용 하도록 설정** 클릭 **적용**합니다. 작업을 중지 해야 및 **액세스 거부** 오류 메시지가 표시 됩니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_148.gif)  
  
9. 클릭 하 고 **계정** 계정에 대해 탭 하 고는 계정 이름, 로그온 시간이 또는 로그온 워크스테이션 변경 하려고 합니다. 모든 실패 하 고 계정 옵션으로 제어 되지 않는 해야는 **userAccountControl** 서 수정 하기 위해 사용할 수 없게 특성 회색으로 표시 될 해야 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_149.gif)  
  
10. 관리 그룹 보호 그룹 DA 그룹 등을 추가 하려고 합니다. 클릭 하면 **확인**, 그룹 수정 권한이 알리는 메시지가 표시 됩니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_150.gif)  
  
11. 수 없는 구성 하는 항목 제외 하 고 관리 계정에서 확인 하는 데 필요한 추가 테스트 수행 **userAccountControl** 설정 및 암호 재설정 합니다.  
  
    > [!NOTE]  
    > **userAccountControl** 특성 제어 여러 계정 구성 옵션이 있습니다. 특성 쓰기 권한을 부여 하면 구성 옵션 중 일부를 변경 하는 데 사용 권한을 부여할 수 없습니다.  
  
###### <a name="test-the-management-accounts"></a>계정 관리 테스트  
이제 보호 그룹의 회원 변경할 수 있는 하나 이상의 계정을 사용 하면는 계정을 보호 그룹 구성원을 수정할 수 있습니다 하지만 계정 보호 및 그룹에 다른 수정 작업을 수행할 수 없습니다 테스트할 수 있습니다.  
  
1.  안전 하 게 관리 호스트 첫 번째 관리 계정으로 로그온 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_151.gif)  
  
2.  시작 **Active Directory 사용자와 컴퓨터** 찾습니다는 **도메인 관리자 그룹**합니다.  
  
3.  마우스 오른쪽 단추로 클릭는 **도메인 관리자** 그룹화 하 고 클릭 **속성**합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_152.gif)  
  
4.  에 **도메인 관리자 속성**를 클릭는 **회원** 탭 하 고 **클릭** 추가 합니다. 클릭 하 고 임시 도메인 관리자 권한이 부여 됩니다 하는 계정 이름을 입력 **이름 확인**합니다. 계정 이름을 밑줄이 그어져 있으면을 클릭 **확인** 돌아가려면는 **회원** 탭 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_153.gif)  
  
5.  에 **회원** 탭에 대 한는 **도메인 관리자 속성** 대화 상자를 클릭 **적용**합니다. 클릭 한 후 **적용**계정을 DA 그룹의 회원 상태를 유지 해야 하 고 없이 오류 메시지가 표시 됩니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_154.gif)  
  
6.  클릭는 **관리 하 여** 탭의 **도메인 관리자 속성** 대화 상자에서 모든 텍스트를 입력할 수 없는 및 모든 단추 회색 있는지 확인 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_155.gif)  
  
7.  클릭는 **일반** 탭의 **도메인 관리자 속성** 대화 상자 및 수정할 수 없습니다 해당 탭에 대 한 정보를 확인 합니다.  
  
    ![관리 계정 만들기](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_156.gif)  
  
8.  필요에 따라 추가 보호 그룹에 대 한 다음이 단계를 반복 합니다. 완료 되 면 기록 사용 하도록 설정 하 고 관리 계정 사용 중지 하기 위해 만든 그룹 구성원에 해당 하는 계정 보안 관리 호스트 로그온 합니다. 다음에서 방금 테스트 하 고는 계정 사용 안 함 관리 계정 암호 다시 설정 합니다. 관리 계정과 계정을 설정 하거나 해제 책임이 그룹의 설치를 완료 했습니다.  
  


