---
title: Windows Server 2008 및 2008 R2 확장 보안 업데이트
description: 지원 주기가 끝난 후 Windows Server 2008 및 2008 R2에 대해 ESU(Extended Security Updates)를 사용하는 방법을 알아봅니다.
ms.prod: windows-server
ms.technology: server-general
ms.mktglfcycl: manage
author: iainfoulds
ms.author: iainfou
ms.topic: get-started-article
ms.localizationpriority: high
ms.date: 02/21/2020
ms.openlocfilehash: 6c9d732b6ec3d8ceb65c691ab143f09dd8f10f23
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "77552526"
---
# <a name="how-to-use-windows-server-2008-and-2008-r2-extended-security-updates-esu"></a>Windows Server 2008 및 2008 R2 ESU(Extended Security Updates)를 사용하는 방법

>적용 대상: Windows Server 2008 및 Windows Server 2008 R2

Windows Server 2008 및 Windows Server 2008 R2는 2020년 1월 14일에 지원 수명 주기가 종료되었습니다. Windows Server LTSC(장기 서비스 채널)는 최소 10년간 지원됩니다(일반 지원 5년 및 확장 지원 5년). 이 지원에는 정기적인 보안 업데이트가 포함됩니다.

지원이 종료되면 보안 업데이트도 종료됩니다. 이렇게 되면 보안 또는 규정 준수 문제를 야기하고 비즈니스 애플리케이션이 위험에 노출될 수 있습니다. 가장 고급 보안, 성능 및 혁신을 위해 [현재 버전의 Windows Server로 업그레이드](modernize-windows-server-2008.md)하는 것이 좋습니다.

서버를 아직 업그레이드하지 않은 경우 다음 옵션을 사용하면 전환 중에 앱과 데이터를 보호할 수 있습니다.

* 기존 Windows Server 2008 및 2008 R2 워크로드를 그대로 Azure VM(Virtual Machines)으로 마이그레이션합니다.
  * Azure로 마이그레이션하면 자동으로 3년 동안 ESU(Extended Security Updates)가 제공됩니다. Azure VM 비용에 확장 보안 업데이트에 대한 추가 비용이 없으며 추가 구성도 필요하지 않습니다.
* 서버에 대한 확장 보안 업데이트 구독을 구매하여 최신 Windows Server 버전으로 업그레이드할 준비가 될 때까지 보호합니다.
  * 이 업데이트는 지원 주기 종료 날짜 후 최대 3년 동안 제공됩니다.

3년 기간의 확장 업데이트가 끝나면 Windows Server 2008 및 2008 R2에 대한 업데이트가 중지됩니다. Windows Server 버전을 최대한 빨리 최신 버전으로 업데이트하는 것이 좋습니다.

## <a name="what-are-extended-security-updates-for-windows-server"></a>Windows Server의 확장 보안 업데이트는 무엇입니까?

Windows Server의 ESU(Extended Security Updates)는 2020년 1월 14일 이후 최대 3년 동안 *위험* 및 *중요* 등급의 보안 업데이트 및 게시판이 포함되어 있습니다. 확장 보안 업데이트는 다음을 포함하지 않습니다.

* 새로운 기능
* 고객이 요청한 비보안 핫픽스
* 디자인 변경 요청

자세한 내용은 [확장 보안 업데이트 FAQ(질문과 대답)](https://www.microsoft.com/cloud-platform/extended-security-updates)를 참조하세요.

## <a name="how-to-use-extended-security-updates"></a>확장 보안 업데이트를 사용하는 방법

Azure에서 Windows Server 2008 또는 2008 R2 VM을 실행하는 경우 확장 보안 업데이트를 사용하도록 자동으로 설정됩니다. 아무 것도 구성할 필요가 없으며 Azure VM에서 확장 보안 업데이트를 사용하는 데 들어가는 추가 비용이 없습니다. Azure VM에서 업데이트를 받도록 구성된 경우 확장 보안 업데이트가 해당 VM에 자동으로 제공됩니다.

온-프레미스 VM 또는 물리적 서버와 같은 다른 환경의 경우 확장 보안 업데이트를 수동으로 요청하고 구성해야 합니다. 확장 보안 업데이트는 EA(기업계약), EAS(기업계약 구독), EES(교육 솔루션용 등록계약), SCE(서버 및 클라우드 등록계약)와 같은 볼륨 라이선스 프로그램을 통해 구입할 수 있습니다.

확장 보안 업데이트를 구입한 경우 다음 방법 중 하나를 사용하여 키를 가져올 수 있습니다.

* Azure Portal에서 확장 보안 업데이트 키를 가져오려면 [Azure Portal에서 확장 보안 업데이트를 등록](#register-for-extended-security-updates-on-azure-portal)할 수 있습니다.
* Azure Portal을 사용하지 않고 [Microsoft 볼륨 라이선스 서비스 센터에 로그인](#sign-in-to-the-microsoft-volume-licensing-service-center)하여 키를 가져올 수도 있습니다.

### <a name="register-for-extended-security-updates-on-azure-portal"></a>Azure Portal에서 확장 보안 업데이트 등록

비 Azure VM에서 확장 보안 업데이트를 사용하려면 MAK(복수 정품 인증 키)를 만들어 Windows Server 2008 및 2008 R2 컴퓨터에 적용합니다. MAK 키를 사용하면 Windows Update 서버에서 보안 업데이트를 계속 받을 수 있는지 알 수 있습니다. 온-프레미스 컴퓨터만 사용하는 경우에도 Azure Portal을 사용하여 확장 보안 업데이트를 등록하고 이러한 키를 관리할 수 있습니다.

> [!NOTE]
> Azure VM에서 Windows Server 2008 및 2008 R2를 실행하는 경우 확장 보안 업데이트를 등록할 필요가 없습니다. 온-프레미스 VM 또는 물리적 서버와 같은 다른 환경의 경우 먼저 [확장 보안 업데이트를 구입](https://www.microsoft.com/licensing/how-to-buy/how-to-buy)한 후에 등록하고 사용해야 합니다.

확장 보안 업데이트를 위해 VM을 등록하고 키를 만들려면 Azure Portal을 열고 다음 지침을 따르세요.

1. [Azure Portal](https://portal.azure.com/)에 로그인합니다.
2. Azure Portal 위쪽의 검색 상자에서 **확장 보안 업데이트**를 검색하고 선택합니다.

    ![Azure Portal에서 확장 보안 업데이트 검색](media/extended-security-updates/esu-portal-search.png)

    이전에 확장 보안 업데이트를 사용하지 않은 경우 먼저 **+ 만들기**를 선택하여 확장 보안 업데이트 리소스를 만듭니다. 그렇지 않으면 목록에서 리소스를 선택합니다.

3. **확장 서비스 업데이트 등록**에서 **시작**를 선택합니다.

    ![Azure Portal에서 확장 보안 업데이트 시작](media/extended-security-updates/get-started-with-esu.png)

4. 첫 번째 키를 만들려면 **키 가져오기**를 선택합니다.

    ![Azure Portal에서 키를 만들도록 선택](media/extended-security-updates/get-key.png)

    확장 보안 업데이트 리소스 및 키를 만들려면 계정과 연결된 Azure 구독이 필요합니다. 계정과 연결된 Azure 구독이 없는 경우 다른 사용자 계정으로 로그인하거나 Azure Portal에서 Azure 구독을 만듭니다.

    보안 업데이트가 작동하려면 Azure 구독에도 기여자 역할을 할당해야 합니다. 역할을 확인하려면 검색 상자에서 "구독"을 입력합니다. 구독 ID 및 이름 옆에 해당 역할을 보여 주는 테이블이 표시됩니다.

    기여자가 아닌 경우 구독 소유자에게 역할을 변경하도록 요청할 수 있습니다. 구독을 소유한 사용자를 확인하려면 이전 단락에서 설명한 역할 테이블로 이동하여 구독 이름을 선택합니다. 다음으로, 페이지 왼쪽의 메뉴로 이동하여 **액세스 제어(IAM)**  > **역할 할당**을 차례로 선택하고, 테이블에서 "소유자" 섹션을 확인합니다.

5. "복수 정품 인증 키를 가져오기 위해 등록"이라는 페이지가 표시되는 경우 이는 확장 보안 업데이트를 사용하기 전에 프라이빗 미리 보기에 대한 액세스를 요청해야 한다는 것을 의미합니다. 이 페이지가 표시되지 않으면 6단계로 건너뜁니다.

   액세스를 요청하려면 **프라이빗 미리 보기 조인**을 선택합니다. 이메일 메시지 창이 열립니다. 이 이메일은 제품 팀에 대한 액세스 요청입니다.
  
    요청에 포함되는 정보는 다음과 같습니다.

    * 고객 이름
    * Azure 구독 ID
    * 계약 번호(ESU의 경우)
    * ESU 서버 수

    완료되면 이메일을 보내세요.

    팀에서 요청 이메일에 제공된 정보를 검토합니다. 모든 항목이 양호하면 승인된 목록에 추가됩니다.

    팀이 요청을 승인하지 않으면 다음 오류 메시지가 표시됩니다.

    [네임스페이스 'Microsoft.WindowsESU'에서 리소스 종류를 찾을 수 없습니다.](https://social.msdn.microsoft.com/Forums/office/94b16a89-3149-43da-865d-abf7dba7b977/the-resource-type-could-not-be-found-in-the-namespace-microsoftwindowsesu-for-api-version)

6. **Azure 세부 정보**에서 Azure 구독, 리소스 그룹 및 키 위치를 선택합니다.

    **등록 세부 정보**에서 다음 정보를 입력합니다.

    | 설정             | Value |
    |---------------------|-------|
    | 키 이름            | 키의 표시 이름(예: *Agreement01*)입니다. |
    | 계약 번호    | 볼륨 라이선싱 계약 관리 시스템 또는 MSLicense for Enterprise Agreement 프로그램에서 생성된 계약 번호입니다. |
    | 컴퓨터 수 | 이 키를 사용하여 확장 보안 업데이트를 설치하려는 컴퓨터 수를 선택합니다. |
    | 운영 체제    | 이 키를 사용할 운영 체제(예: Windows Server 2008 또는 Windows Server 2008 R2)를 선택합니다. |

    준비가 되면 **검토 + 등록**을 선택합니다.

    >[!NOTE]
    >글로벌 필터에서 프라이빗 미리 보기에 조인한 Azure 구독을 선택했는지 확인합니다. Azure Portal 리본 메뉴에서 **필터** 단추를 선택하여 글로벌 구독 필터를 확인합니다.
    >
    > ![필터 단추가 선택된 Azure Portal 리본 메뉴의 이미지](media/azure-ribbon-filter.png)

7. 유효성 검사가 성공하면 새 레지스트리 리소스에 대한 선택 사항 요약이 표시됩니다. 필요한 경우 유효성 검사 오류를 수정하거나 구성 선택 사항을 업데이트합니다. Azure [이용 약관](https://azure.microsoft.com/support/legal/) 및 [개인 정보 취급 방침](https://privacy.microsoft.com/privacystatement)를 사용할 수 있습니다.

    적격 컴퓨터가 있고 키가 조직 내에서만 사용되는지 확인란을 선택하여 확인합니다.

    ![키가 조직에서만 사용되는지 확인합니다.](media/extended-security-updates/confirm-key-usage.png)

    준비가 되면 **만들기**를 선택하여 MAK를 생성합니다.

이제 컴퓨터에서 확장 보안 업데이트 등록을 사용할 수 있습니다. 생성된 키는 보안 업데이트를 받을 수 있는 Windows Server 2008 및 2008 R2 컴퓨터에 적용해야 합니다.

### <a name="sign-in-to-the-microsoft-volume-licensing-service-center"></a>Microsoft 볼륨 라이선스 서비스 센터에 로그인

Azure Portal에 액세스할 수 없는 경우 볼륨 라이선스 서비스 센터를 사용하여 정품 인증 키를 보고 다운로드할 수 있습니다.

볼륨 라이선스 서비스 센터에서 키를 가져오려면 다음을 수행합니다.

1. [볼륨 라이선스 서비스 센터 페이지](https://www.microsoft.com/vlsc)로 이동하여 Azure 자격 증명을 사용하여 로그인합니다.

2. **라이선스** > **관계 요약** > **라이선스 ID** > **제품 키**를 차례로 선택합니다.

적합한 Windows 디바이스에 대한 확장 보안 업데이트를 가져오는 방법에 대한 자세한 내용은 [Tech Community 게시물](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/obtaining-extended-security-updates-for-eligible-windows-devices/ba-p/1167091#)을 참조하세요.

## <a name="download-and-apply-extended-security-updates"></a>확장 보안 업데이트 다운로드 및 적용

Windows Server용 확장 보안 업데이트의 전송, 다운로드 및 적용은 기존 배포 프로세스와 동일합니다. 확장 보안 업데이트를 통해 제공되는 업데이트는 *보안*에만 해당되며, 모든 화요일 패치에서 릴리스됩니다.

이미 존재하는 도구 및 프로세스를 사용하여 업데이트를 설치할 수 있습니다. 유일한 차이점은 업데이트를 다운로드하여 설치하려면 이전 섹션에서 생성된 키를 사용하여 시스템을 등록해야 한다는 것입니다.

Azure VM의 경우 컴퓨터에서 확장 보안 업데이트를 사용하도록 설정하는 프로세스가 자동으로 완료됩니다. 추가 구성없이 업데이트를 다운로드하여 설치해야 합니다.
