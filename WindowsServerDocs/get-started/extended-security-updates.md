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
ms.date: 01/23/2020
ms.openlocfilehash: 0f3ea0dacc200adaaec5064d19754ad6de0042a6
ms.sourcegitcommit: ff0db5ca093a31034ccc5e9156f5e9b45b69bae5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2020
ms.locfileid: "76725778"
---
# <a name="how-to-use-windows-server-2008-and-2008-r2-extended-security-updates-esu"></a>Windows Server 2008 및 2008 R2 ESU(Extended Security Updates)를 사용하는 방법

>적용 대상: Windows Server 2008 / 2008 R2

Windows Server 2008 및 Windows Server 2008 R2는 2020년 1월 14일에 지원 주기가 끝났습니다. Windows Server LTSC(Long Term Servicing Channel)는 주요 지원 5년, 연장 지원 5년으로 최소 10년 동안 지원됩니다. 이 지원에는 정기적인 보안 업데이트가 포함됩니다.

지원이 종료되면 보안 업데이트도 종료됩니다. 이렇게 되면 보안 또는 규정 준수 문제를 야기하고 비즈니스 애플리케이션이 위험에 노출될 수 있습니다. 가장 고급 보안, 성능 및 혁신을 위해 [현재 버전의 Windows Server로 업그레이드](modernize-windows-server-2008.md)하는 것이 좋습니다.

지원 주기 마감일까지 모든 서버를 업그레이드할 수 없는 경우, 업그레이드 전환 중 애플리케이션 및 데이터를 보호하는 데 다음 옵션이 도움이 됩니다.

* 기존 Windows Server 2008 및 2008 R2 워크로드를 그대로 Azure VM(Virtual Machines)으로 마이그레이션합니다.
    * Azure로 마이그레이션하면 자동으로 3년 동안 ESU(Extended Security Updates)가 제공됩니다. Azure VM 비용에 확장 보안 업데이트에 대한 추가 비용이 없으며 추가 구성도 필요하지 않습니다.
* 서버에 대한 확장 보안 업데이트 구독을 구매하여 최신 Windows Server 버전으로 업그레이드할 준비가 될 때까지 보호합니다.
    * 이 업데이트는 지원 주기 종료 날짜 후 최대 3년 동안 제공됩니다.

3년 연장 업데이트 이후에는 컴퓨터가 받을 수 있는 추가 업데이트 옵션은 없습니다.

## <a name="what-are-extended-security-updates-for-windows-server"></a>Windows Server의 확장 보안 업데이트는 무엇입니까?

Windows Server의 ESU(Extended Security Updates)는 2020년 1월 14일 이후 최대 3년 동안 *위험* 및 *중요* 등급의 보안 업데이트 및 게시판이 포함되어 있습니다. 확장 보안 업데이트는 다음을 포함하지 않습니다.

* 새로운 기능
* 고객이 요청한 비보안 핫픽스
* 디자인 변경 요청

자세한 내용은 [확장 보안 업데이트 FAQ(질문과 대답)](https://www.microsoft.com/cloud-platform/extended-security-updates)를 참조하세요.

## <a name="how-to-use-extended-security-updates"></a>확장 보안 업데이트 사용 방법

Azure에서 Windows Server 2008/2008 R2 VM을 실행하는 경우 확장 보안 업데이트가 자동으로 사용하도록 설정됩니다. 어느 것도 구성할 필요가 없으며 Azure VM에서 확장 보안 업데이트를 사용하는 데 대한 추가 비용이 없습니다. 확장 보안 업데이트는 업데이트를 수신하도록 구성된 Azure VM에 자동으로 배달됩니다.

온-프레미스 VM 또는 물리적 서버와 같은 다른 환경의 경우에는 확장 보안 업데이트를 수동으로 요청하고 구성해야 합니다. EA(기업계약), EAS(기업계약 구독), EES(교육 솔루션 등록), SCE(서버 및 클라우드 등록)와 같은 볼륨 라이선싱 프로그램을 통해 사용할 수 있는 확장 보안 업데이트를 이미 구매한 경우 다음 단계 중 하나를 사용하여 활성화 키를 가져올 수 있습니다.

* 활성화 키를 보고 가져오려면 [Microsoft 볼륨 라이선싱 서비스 센터](https://www.microsoft.com/Licensing/servicecenter/default.aspx)에 로그인합니다.
* Azure Portal에서 확장 보안 업데이트를 등록하여 Windows Server 2008/R2 활성화 키를 가져옵니다.
    * 이 프로세스를 완료하는 방법에 대한 설명은 이 문서의 다음 단계를 참조하세요.

## <a name="register-for-extended-security-updates"></a>확장 보안 업데이트 등록

확장 보안 업데이트를 사용하려면 MAK(복수 정품 인증 키)를 만들어 Windows Server 2008 및 2008 R2 컴퓨터에 적용합니다. 이 키는 Windows Update 서버가 보안 업데이트를 계속 받을 수 있음을 알려줍니다. 온-프레미스 컴퓨터만 사용하더라도 확장 보안 업데이트를 등록하고 Azure Portal을 사용하여 이 키를 관리합니다.

> [!NOTE]
>
> Azure VM에서 Windows Server 2008 및 2008 R2를 실행 중인 경우 확장 보안 업데이트를 등록할 필요가 없습니다. 온-프레미스 VM 또는 물리적 서버와 같은 다른 환경의 경우에는 [확장 보안 업데이트를 구매](https://www.microsoft.com/licensing/how-to-buy/how-to-buy)한 후에 등록하고 사용해야 합니다.

> [!IMPORTANT]
>
> 볼륨 라이선싱 프로그램을 통해 확장 보안 업데이트를 구매하려면 이전 단계를 수행했는지 확인합니다. 아래 단계를 수행하기 전에 [winsvresuchamps@microsoft.com](mailto:winsvresuchamps@microsoft.com)으로 다음 정보가 포함된 이메일을 보내 기능 사용 승인을 받으세요.
>
> * 고객 이름:
> * Azure 구독:
> * EA 계약 번호(ESU의 경우):
> * ESU 서버 수:
>
> 담당 팀이 제공된 정보를 검토하고 사용자/구독을 승인된 목록에 추가합니다.
>
> 요청자가 승인되지 않은 경우 다음과 같은 오류가 발생할 수 있습니다.
>
> [네임스페이스 'Microsoft.WindowsESU'에서 리소스 종류를 찾을 수 없습니다.](https://social.msdn.microsoft.com/Forums/office/94b16a89-3149-43da-865d-abf7dba7b977/the-resource-type-could-not-be-found-in-the-namespace-microsoftwindowsesu-for-api-version)

확장 보안 업데이트를 위해 비 Azure VM을 등록하고 키를 만들려면 Azure Portal에서 다음 단계를 완료합니다.

1. [Azure Portal](https://portal.azure.com/)에 로그인합니다.
1. Azure Portal 상단의 검색 상자에서 **확장 보안 업데이트**를 검색하고 선택합니다.

    ![Azure Portal에서 확장 보안 업데이트 검색](media/extended-security-updates/esu-portal-search.png)

    이전에 확장 보안 업데이트를 사용하지 않은 경우, 확장 보안 업데이트 리소스 **+ 만들기**를 먼저 선택합니다. 그렇지 않으면 목록에서 리소스를 선택합니다.

1. **확장 서비스 업데이트 등록**에서 **시작**를 선택합니다.

    ![Azure Portal에서 확장 보안 업데이트 시작](media/extended-security-updates/get-started-with-esu.png)

1. 첫 번째 키를 만들려면 **키 가져오기**를 선택합니다.

    ![Azure Portal에서 키를 만들도록 선택](media/extended-security-updates/get-key.png)

    > [!NOTE]
    > 확장 보안 업데이트 리소스 및 키를 만들려면 계정과 연결된 Azure 구독이 필요합니다. 계정과 연결된 Azure 구독이 없는 경우 다른 사용자 계정으로 로그인하거나 포털에 표시된 안내 단계를 사용하여 Azure 구독을 만듭니다.

1. **Azure 세부 정보**에서 Azure 구독, 리소스 그룹 및 키 위치를 선택합니다.

    **등록 세부 정보**에서 다음 정보를 입력합니다.

    | 설정             | Value |
    |---------------------|-------|
    | 키 이름            | 키의 표시 이름(예: *Agreement01*)입니다. |
    | 계약 번호    | 볼륨 라이선싱 계약 관리 시스템 또는 MSLicense for Enterprise Agreement 프로그램에서 생성된 계약 번호입니다. |
    | 컴퓨터 수 | 이 키를 사용하여 확장 보안 업데이트를 설치하려는 컴퓨터 수를 선택합니다. |
    | 운영 체제    | 이 키를 사용할 운영 체제(예: Windows Server 2008 또는 Windows Server 2008 R2)를 선택합니다. |

    준비가 되면 **검토 + 등록**을 선택합니다.

1. 유효성 검사가 성공하면 새 레지스트리 리소스에 대한 선택 사항 요약이 표시됩니다. 필요한 경우 유효성 검사 오류를 수정하거나 구성 선택 사항을 업데이트합니다. Azure [이용 약관](https://azure.microsoft.com/support/legal/) 및 [개인 정보 취급 방침](https://privacy.microsoft.com/privacystatement)를 사용할 수 있습니다.

    적격 컴퓨터가 있고 키가 조직 내에서만 사용되는지 확인란을 선택하여 확인합니다.

    ![키가 조직에서만 사용되는지 확인합니다.](media/extended-security-updates/confirm-key-usage.png)

    준비가 되면 **만들기**를 선택하여 MAK를 생성합니다.

이제 컴퓨터에서 확장 보안 업데이트 등록을 사용할 수 있습니다. 생성된 키는 보안 업데이트를 받을 수 있는 Windows Server 2008 및 2008 R2 컴퓨터에 적용해야 합니다.

## <a name="download-and-apply-extended-security-updates"></a>확장 보안 업데이트 다운로드 및 적용

Windows Server용 확장 보안 업데이트의 전송, 다운로드 및 적용은 기존 배포 프로세스와 다르지 않습니다. 확장 보안 업데이트를 통해 제공되는 업데이트는 *보안*에 대해서만 제공되며 화요일 패치마다 릴리스됩니다.

이미 존재하는 도구 및 프로세스를 사용하여 업데이트를 설치할 수 있습니다. 유일한 차이점은 업데이트를 다운로드하여 설치하려면 이전 섹션에서 생성된 키를 사용하여 시스템을 등록해야 한다는 것입니다.

Azure VM의 경우 확장 보안 업데이트를 위해 컴퓨터를 활성화하는 프로세스가 자동으로 완료됩니다. 추가 구성없이 업데이트를 다운로드하여 설치해야 합니다.
