---
title: Active Directory Domain Services에서 클러스터 컴퓨터 개체 사전 준비
description: Active Directory Domain Services에서 클러스터 컴퓨터 개체 사전 준비 하는 방법입니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.manager: daveba
ms.technology: storage-failover-clustering
ms.date: 05/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: 151f02572d7595776539af163831b4a7a060c1c7
ms.sourcegitcommit: 75f257d97d345da388cda972ccce0eb29e82d3bc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65613172"
---
# <a name="prestage-cluster-computer-objects-in-active-directory-domain-services"></a>Active Directory Domain Services에서 클러스터 컴퓨터 개체 사전 준비

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 AD DS(Active Directory 도메인 서비스)에서 클러스터 컴퓨터 개체를 사전 준비하는 방법을 보여 줍니다. 이 절차를 사용하여 사용자 또는 그룹이 AD DS에서 컴퓨터 개체를 만들 권한이 없는 경우 장애 조치(failover) 클러스터를 만들 수 있도록 할 수 있습니다.

클러스터 만들기 마법사 또는 Windows PowerShell을 사용하여 장애 조치(failover) 클러스터를 만들 때는 클러스터 이름을 지정해야 합니다. 클러스터를 만들 때 충분한 권한이 있으면 클러스터 만들기 프로세스에서 클러스터 이름과 일치하는 컴퓨터 개체를 AD DS에 자동으로 만듭니다. 이 개체를 *클러스터 이름 개체* 또는 CNO라고 합니다. 클라이언트 액세스 지점을 사용하는 클러스터된 역할을 구성할 때 CNO를 통해 VCO(가상 컴퓨터 개체)가 자동으로 만들어집니다. 예를 들어 이름이 *FileServer1*인 클라이언트 액세스 지점을 통해 항상 사용 가능한 파일 서버를 만든 경우 CNO는 AD DS에 해당 VCO를 만듭니다.

>[!NOTE]
>AD DS에서 CNO 또는 Vco 없습니다 만들어진 Active Directory 분리 클러스터를 만들 수가 있습니다. 이는 특정 유형의 클러스터 배포를 대상으로 합니다. 자세한 내용은 [Active Directory 분리 클러스터 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v%3dws.11)>)를 참조하십시오.

CNO를 자동으로 만들려면 장애 조치(failover) 클러스터를 만드는 사용자에게 클러스터를 구성할 서버가 있는 컨테이너 또는 OU(조직 구성 단위)에 대한 **컴퓨터 개체 만들기** 권한이 있어야 합니다. 이 권한 없이 사용자 또는 그룹이 클러스터를 만들 수 있도록 하려면 AD DS에서 적절한 권한을 가진 사용자(일반적으로 도메인 관리자)가 AD DS에서 CNO를 사전 준비하면 됩니다. 또한 이 경우 클러스터에 사용되는 명명 규칙과 클러스터 개체가 만들어지는 OU에 대한 도메인 관리자의 제어 권한이 강화됩니다.

## <a name="step-1-prestage-the-cno-in-ad-ds"></a>1단계: AD DS에서 CNO를 사전 준비

시작하기 전에 다음 사항을 알아야 합니다.

- 클러스터를 할당 하려는 이름
- 사용자 계정 또는 클러스터를 만들 수 있는 권한을 부여 하려는 그룹의 이름

클러스터 개체에 대한 OU를 만드는 것이 가장 좋습니다. 사용하려는 OU가 이미 있는 경우 이 단계를 완료하려면 최소한 **Account Operators** 그룹의 구성원이어야 합니다. 클러스터 개체에 대한 OU를 만들어야 하는 경우 이 단계를 완료하려면 최소한 **Domain Admins** 그룹의 구성원이거나 이와 동등한 자격을 갖추고 있어야 합니다.

>[!NOTE]
>OU 대신 기본 컴퓨터 컨테이너에 CNO를 만드는 경우에는 이 항목의 3단계를 완료하지 않아도 됩니다. 이 시나리오에서는 클러스터 관리자가 추가 구성 없이 최대 10개의 VCO를 만들 수 있습니다.

### <a name="prestage-the-cno-in-ad-ds"></a>AD DS에서 CNO를 사전 준비

1. 원격 서버 관리 도구에서 AD DS 도구를 설치한 컴퓨터 또는 도메인 컨트롤러에서 **Active Directory 사용자 및 컴퓨터**를 엽니다. 서버에서이 작업을 수행 하려면 서버 관리자를 시작 한 후 합니다 **도구** 메뉴에서 **Active Directory Users and Computers**합니다.
2. 컴퓨터 개체는 클러스터에 대 한 OU를 만들려면 도메인 이름 또는 기존 OU를 마우스 오른쪽 단추로 클릭, 가리킨 **새로 만들기**를 선택한 후 **조직 구성 단위**합니다. 에 **이름을** 상자에 OU의 이름을 입력 한 다음 선택 **확인**합니다.
3. 콘솔 트리에서 CNO를 만들려는 OU를 마우스 오른쪽 단추로 가리킵니다 **새로 만들기**를 선택한 후 **컴퓨터**합니다.
4. 에 **컴퓨터 이름** 상자에 장애 조치 클러스터를 사용할지 선택한 후 이름을 입력 합니다 **확인**합니다.

  >[!NOTE]
  >이 이름은 클러스터를 만드는 사용자가 클러스터 만들기 마법사의 **클러스터 관리 액세스 지점** 페이지에서 지정하거나 *–Name* Windows PowerShell cmdlet에서 **New-Cluster** 매개 변수 값으로 지정할 클러스터 이름입니다.

5. 모범 사례로, 방금 만든 컴퓨터 계정을 마우스 오른쪽 단추로 클릭 한 다음를 선택 합니다 **속성**를 선택한 후 합니다 **개체** 탭 합니다. 에 **개체** 탭을 선택 합니다 **실수로 삭제 되지 않도록에서 개체 보호** 확인란을 선택한 후 **확인**합니다.
6. 컴퓨터 계정을 방금 만든 단추로 선택한 **계정 사용 안 함**합니다. 선택 **Yes** 여 확인 하 고 선택한 **확인**합니다.

  >[!NOTE]
  >계정을 사용하지 않도록 설정해야 클러스터를 만드는 동안 클러스터 만들기 프로세스에서 도메인의 기존 컴퓨터 또는 클러스터가 해당 계정을 현재 사용하고 있지 않은지 확인할 수 있습니다.

![예제 Clusters OU에서 사용하지 않도록 설정된 CNO](media/prestage-cluster-adds/disabled-cno-in-the-example-clusters-ou.png)

**그림 1입니다. 예제 Clusters OU에서에서 CNO를 사용 안 함된**

## <a name="step-2-grant-the-user-permissions-to-create-the-cluster"></a>2단계: 클러스터를 만드는 사용자 권한 부여

장애 조치(failover) 클러스터를 만드는 데 사용할 사용자 계정에 CNO에 대한 모든 권한이 부여되도록 사용 권한을 구성해야 합니다.

이 단계를 완료하려면 최소한 **Account Operators** 그룹의 구성원이어야 합니다.

클러스터를 만들 수 있는 사용자 권한을 부여 하는 방법을 다음과 같습니다.

1. Active Directory 사용자 및 컴퓨터의 **보기** 메뉴에서 **고급 기능**이 선택되어 있는지 확인합니다.
2. 찾을 CNO를 마우스 오른쪽 단추로 클릭 하 고 선택한 **속성**합니다.
3. 에 **Security** 탭을 선택 **추가**합니다.
4. 에 **사용자, 컴퓨터 또는 그룹 선택** 대화 상자에서 사용자 계정 또는 그룹에 권한을 부여 하 고 클릭 하려는 지정 **확인**합니다.
5. 방금 추가한 사용자 계정 또는 그룹을 선택한 다음 **모든 권한**옆에서 **허용** 확인란을 선택합니다.
  
  ![클러스터를 만들 사용자 또는 그룹에 모든 권한 부여](media/prestage-cluster-adds/granting-full-control-to-the-user-create-the-cluster.png)
  
  **그림 2입니다. 사용자 또는 클러스터에 만든 그룹에 모든 권한 부여**
6. **확인**을 선택합니다.

이 단계를 완료하면 권한을 부여받은 사용자가 장애 조치(failover) 클러스터를 만들 수 있습니다. 그러나 CNO가 OU에 있는 경우 사용자는 3단계를 완료할 때까지 클라이언트 액세스 지점이 필요한 클러스터된 역할을 만들 수 없습니다.

>[!NOTE]
>CNO가 기본 컴퓨터 컨테이너에 있는 경우 클러스터 관리자는 추가 구성 없이 최대 10개의 VCO를 만들 수 있습니다. 10개가 넘는 VCO를 추가하려면 컴퓨터 컨테이너의 CNO에 **컴퓨터 개체 만들기** 권한을 명시적으로 부여해야 합니다.

## <a name="step-3-grant-the-cno-permissions-to-the-ou-or-prestage-vcos-for-clustered-roles"></a>3단계: OU에 CNO 권한을 부여 하거나 클러스터 된 역할에 대 한 Vco를 사전 준비

클라이언트 액세스 지점이 있는 클러스터된 역할을 만들면 클러스터에서 CNO와 동일한 OU에 VCO를 만듭니다. 이 작업이 자동으로 수행되려면 CNO에는 OU에 컴퓨터 개체를 만들 수 있는 권한이 있어야 합니다.

AD DS에서 CNO를 사전 준비한 경우 다음 중 하나를 수행하여 VCO를 만들 수 있습니다.

- 옵션 1: [사용 권한을 부여 합니다 CNO에 OU에](#grant-the-cno-permissions-to-the-ou)입니다. 이 옵션을 사용하면 클러스터에서 VCO를 AD DS에 자동으로 만들 수 있습니다. 따라서 장애 조치(failover) 클러스터의 관리자는 AD DS에서 VCO를 사전 준비하도록 요청하지 않고도 클러스터된 역할을 만들 수 있습니다.

>[!NOTE]
>이 옵션에 대한 단계를 완료하려면 최소한 **Domain Admins** 그룹의 구성원이거나 이와 동등한 자격을 갖추고 있어야 합니다.

- 옵션 2: [클러스터 된 역할에 대 한 VCO를 사전 준비](#prestage-a-vco-for-a-clustered-role)합니다. 조직의 요구 사항으로 인해 클러스터된 역할에 대한 계정을 사전 준비해야 하는 경우 이 옵션을 사용합니다. 예를 들어 명명 규칙을 제어하거나 만들어지는 클러스터된 역할을 제어할 수 있습니다.

>[!NOTE]
>이 옵션에 대한 단계를 완료하려면 최소한 **Account Operators** 그룹의 구성원이어야 합니다.

### <a name="grant-the-cno-permissions-to-the-ou"></a>사용 권한을 부여 합니다 CNO에 OU에

1. Active Directory 사용자 및 컴퓨터의 **보기** 메뉴에서 **고급 기능**이 선택되어 있는지 확인합니다.
2. CNO를 만든 OU를 마우스 오른쪽 단추로 클릭 [1 단계: AD DS에서 CNO를 사전 준비할](#step-1-prestage-the-cno-in-ad-ds)를 선택한 후 **속성**합니다.
3. 에 **Security** 탭을 선택 **고급**합니다.
4. 에 **Advanced Security Settings** 대화 상자에서 **추가**합니다.
5. 옆에 **주체**를 선택 **보안 주체 선택**합니다.
6. 에 **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 대화 상자에서 **개체 유형**를 선택 합니다 **컴퓨터** 확인란을 선택한 후 **확인** .
7. 아래 **선택할 개체 이름을 입력 하십시오**cno 이름을 입력 **이름 확인**를 선택한 후 **확인**합니다. 사용할 수 없는 개체를 추가 하려고 한다는 경고 메시지에 대 한 응답으로 선택 **확인**합니다.
8. **권한 항목** 대화 상자에서 **유형** 목록이 **허용**으로 설정되고, **적용 대상** 목록이 **이 개체 및 모든 하위 개체**로 설정되어 있는지 확인합니다.
9. **사용 권한**에서 **컴퓨터 개체 만들기** 확인란을 선택합니다.

  ![CNO에 컴퓨터 개체 만들기 권한 부여](media/prestage-cluster-adds/granting-create-computer-objects-permission-to-the-cno.png)

  **그림 3입니다. CNO에 컴퓨터 만들기 개체 권한 부여**
10. 선택 **확인** 돌아가게 Active Directory 사용자 및 컴퓨터 스냅인 될 때까지 합니다.

이제 장애 조치(failover) 클러스터의 관리자가 클라이언트 액세스 지점이 있는 클러스터된 역할을 만들고 리소스를 온라인 상태로 전환할 수 있습니다.

### <a name="prestage-a-vco-for-a-clustered-role"></a>클러스터 된 역할에 대 한 VCO를 사전 준비

1. 시작하기 전에 클러스터의 이름과 클러스터된 역할에 사용할 이름을 알아야 합니다.
2. Active Directory 사용자 및 컴퓨터의 **보기** 메뉴에서 **고급 기능**이 선택되어 있는지 확인합니다.
3. Active Directory 사용자 및 컴퓨터에 있는 CNO 클러스터에 대 한 가리킨 OU를 마우스 오른쪽 단추로 **새로 만들기**를 선택한 후 **컴퓨터**합니다.
4. 에 **컴퓨터 이름** 상자에 클러스터 된 역할에 대 한 사용을 선택 하는 이름을 입력 합니다 **확인**합니다.
5. 모범 사례로, 방금 만든 컴퓨터 계정을 마우스 오른쪽 단추로 클릭 한 다음를 선택 합니다 **속성**를 선택한 후 합니다 **개체** 탭 합니다. 에 **개체** 탭을 선택 합니다 **실수로 삭제 되지 않도록에서 개체 보호** 확인란을 선택한 후 **확인**합니다.
6. 컴퓨터 계정을 방금 만든 단추로 선택한 **속성**합니다.
7. 에 **Security** 탭을 선택 **추가**합니다.
8. 에 **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 대화 상자에서 **개체 유형**를 선택 합니다 **컴퓨터** 확인란을 선택한 후 **확인** .
9. 아래 **선택할 개체 이름을 입력 하십시오**cno 이름을 입력 **이름 확인**를 선택한 후 **확인**합니다. 사용할 수 없는 개체를 추가, 선택 하려고 한다는 경고 메시지가 표시 되 면 **확인**합니다.
10. CNO이 선택되어 있는지 확인한 다음 **모든 권한** 옆에서 **허용** 확인란을 선택합니다.
11. **확인**을 선택합니다.

이제 장애 조치(failover) 클러스터의 관리자가 사전 준비된 VCO 이름과 일치하는 클라이언트 액세스 지점이 있는 클러스터된 역할을 만들고 리소스를 온라인 상태로 전환할 수 있습니다.

## <a name="more-information"></a>자세한 정보

- [장애 조치(failover) 클러스터링](failover-clustering.md)
- [Active Directory에서 클러스터 계정 구성](configure-ad-accounts.md)