---
title: ADBA 클라이언트 문제 해결
description: Windows 정품 인증 문제에 대한 문제 해결 프로세스를 안내합니다.
ms.topic: troubleshooting
ms.date: 09/24/2019
ms.technology: server-general
author: Teresa-Motiv
ms.author: v-tea
manager: dcscontentpm
ms.localizationpriority: medium
ms.openlocfilehash: b4e31cfa892019e4f3bbcd3b67dbb42751cc58dd
ms.sourcegitcommit: 9855d6b59b1f8722f39ae74ad373ce1530da0ccf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71963039"
---
# <a name="example-troubleshooting-active-directory-based-activation-adba-clients-that-do-not-activate"></a>예제: 정품 인증되지 않은 ADBA(Active Directory 기반 정품 인증) 클라이언트 문제 해결

> [!NOTE]
> 이 문서는 원래 2018년 3월 26일에 TechNet 블로그로 게시되었습니다.

여러분 안녕하세요! 제 이름은 Mike Kammer이며, Microsoft에서 플랫폼 PFE로 근무한지 2년이 조금 넘었습니다. 최근에 Windows Server 2016을 자신의 환경에 배포하는 고객에게 도움을 주었습니다. 또한 이 기회를 통해 정품 인증 방법론을 KMS 서버에서 [Active Directory 기반 정품 인증](https://docs.microsoft.com/previous-versions/windows/hh852637(v=win.10))으로 마이그레이션했습니다.

모든 변경을 수행하기 위한 적절한 절차로 고객의 테스트 환경에서 마이그레이션을 시작했습니다. 우리는 Charity Shelbourne의 훌륭한 블로그 게시물인 [Active Directory 기반 정품 인증 및 키 관리 서비스]의](https://techcommunity.microsoft.com/t5/Core-Infrastructure-and-Security/Active-Directory-Based-Activation-vs-Key-Management-Services/ba-p/256016)' 지침에 따라 배포를 시작했습니다. 테스트 환경의 도메인 컨트롤러는 모두 Windows Server 2012 R2를 실행하고 있었으므로 포리스트를 준비할 필요가 없었습니다. 역할을 Windows Server 2012 R2 도메인 컨트롤러에 설치하고, 볼륨 정품 인증 방법으로 Active Directory 기반 정품 인증을 선택했습니다. KMS 키를 설치하고, "KMS AD 정품 인증( ** LAB)"이라는 이름을 지정했습니다. 블로그 게시물을 단계별로 자세히 수행했습니다.

먼저 4개의 가상 머신, 2개의 Windows 2016 Standard, 2개의 Windows 2016 Datacenter를 구축하여 시작했습니다. 이제 모든 것이 잘 되었고 모든 사람이 만족할 것입니다. Windows 2016 Standard를 실행하는 물리적 서버를 구축했으며, 이 머신이 제대로 작동했습니다. 여기서 우리의 이야기는 끝납니다.

하하! 농담이에요! 어느 것도 쉽지 않습니다. 사실, 설정과 구성이 매우 쉬웠으므로 해당 부분은 간단하고 직접적이었습니다. 월요일에는 사무실로 돌아왔으며, 1주일 전에 구축한 모든 가상 머신이 정품 인증되지 않은 것으로 나타났습니다. 이봐요! 그건 옳지 않아요! 나는 물리적 머신을 살펴보았지만 괜찮았어요. 고객과 함께 무슨 일이 있었는지 논의했습니다. 물론, 첫 번째 질문은 "주말에 무엇이 바뀌었나요?"였습니다. 그리고 평소와 같이 대답은 "아무것도 바꾸지 않았어요!"였습니다. 이번에는 실제로 아무것도 바꾸지 않았고, 무슨 일이 발생했는지 파악해야 했습니다.

문제 서버 중 하나로 이동하여 명령 프롬프트를 열고, **slmgr /ao-list** 명령의 출력을 확인했습니다. **/ao-list** 스위치는 Active Directory의 모든 정품 인증 개체를 표시합니다.

![slmgr 명령을 보여 주는 이미지](./media/032618_1700_Troubleshoo1.png)

![slmgr 명령의 결과를 보여 주는 이미지](./media/032618_1700_Troubleshoo2.png)

결과에서는 서버 2012 R2에 대한 정품 인증 및 Windows Server 2016 라이선스인 새로 만든 KMS AD 정품 인증(* LAB)의 두 정품 인증 개체가 있음을 보여 줍니다. 이는 Windows KMS 클라이언트를 정품 인증하도록 Active Directory가 올바르게 구성되었음을 나타냅니다.

**slmgr** 명령이 라이선스 정품 인증을 위한 친구라는 것을 알고 있으므로 다른 옵션을 계속 사용했습니다. 자세한 라이선스 정보가 표시되는 **/dlv** 스위치를 사용해 보았습니다. 이 스위치는 괜찮은 것으로 생각했습니다. Windows Server 2016 Standard 버전을 실행하고 있었으며, 정품 인증 ID, 설치 ID, 유효성 검사 URL, 심지어 부분 제품 키도 있었습니다.

![slmgr /dlv의 결과를 보여 주는 이미지](./media/ActivationTroubleshoot2b.jpg)

이 시점에서 제가 놓친 것을 아는 사람이 있나요? 다른 문제 해결 단계를 수행한 후에 다시 돌아올 수 있겠지만, 이 스크린샷에 문제에 대한 답변이 있다고 말하기에 충분합니다.

이제 몇 가지 이유로 키가 손상되었다고 생각하므로 현재 키를 제거하는 **/upk** 스위치를 사용합니다. 키를 제거하는 데 효과적인 방법이었지만, 일반적으로는 이 작업을 수행하는 가장 좋은 방법이 아닙니다. 새 키를 가져오기 전에 서버를 다시 부팅하면 서버가 잘못된 상태로 있을 수 있습니다. **/ipk** 스위치를 사용하는 것(나중의 문제 해결에서 수행)이 기존 키를 덮어쓰고 훨씬 더 안전하게 수행할 수 있는 경로입니다. 제 실수에서 알아보세요!

![slmgr /upk 명령 및 해당 결과를 보여 주는 이미지](./media/032618_1700_Troubleshoo3.png)

**/dlv** 스위치를 다시 실행하여 자세한 라이선스 정보를 확인했습니다. 아쉽게도 제게 도움이 되는 정보를 제공하지 않았으며, 제품 키를 찾을 수 없음 오류만 발생했습니다. 제가 방금 키를 제거했으므로 해당 키가 없는 것이 당연합니다!

![slmgr /dlv 명령 및 해당 결과를 보여 주는 이미지](./media/032618_1700_Troubleshoo4.png)

모험인 줄 알았지만 알려진 KMS 서버(또는 경우에 따라 Active Directory)에 대해 Windows를 정품 인증하는 **/ato** 스위치를 사용해 보았습니다. 제품을 찾을 수 없음 오류가 다시 발생했습니다.

![slmgr /ato 명령 및 해당 결과를 보여 주는 이미지](./media/032618_1700_Troubleshoo5.png)

다음으로, 때로는 서비스를 중지하고 시작하는 것이 좋은 방법일 수도 있다고 생각했습니다. 그래서 저는 다음 작업으로 이를 시도했습니다. Microsoft Software Protection Platform Service(SPPSvc 서비스)를 중지하고 시작해야 합니다. 관리 명령 프롬프트에서 신뢰할 수 있는 **net stop** 및 **net start** 명령을 사용합니다. 처음에는 서비스가 실행되고 있지 않다는 것을 알고 있었으므로 이것이 틀림없다고 생각합니다!

![net stop 및 net start 명령의 결과를 보여 주는 이미지](./media/032618_1700_Troubleshoo6.png)

하지만 아니었어요. 서비스를 시작하고 Windows 정품 인증을 다시 시도한 후에도 여전히 제품을 찾을 수 없음 오류가 발생합니다.

그런 다음, 문제 서버 중 하나에서 애플리케이션 이벤트 로그를 살펴보았습니다. 8198 이벤트 ID의 라이선스 정품 인증과 관련된 오류(0x8007007B 코드)가 발견되었습니다.

![8198 이벤트 ID의 세부 정보를 보여 주는 이미지](./media/032618_1700_Troubleshoo7.png)

이 코드를 조회하는 동안 오류 코드에서 파일 이름, 디렉터리 이름 또는 볼륨 레이블 구문이 잘못되었음을 나타내는 문서를 찾았습니다. 이 문서에서 설명하는 방법을 읽어본 결과 제 상황에 맞지 않는 것 같았습니다. **nslookup -type=all _vlmcs._tcp** 명령을 실행했을 때 기존 KMS 서버(환경에 아직도 많은 Windows 7 및 Windows Server 2008 머신이 있으므로 유지해야 함) 및 5개의 도메인 컨트롤러도 찾았습니다. 이는 DNS 문제가 아니며 내 문제가 다른 곳에 있음을 나타냅니다.

![nslookup 명령의 결과를 보여 주는 이미지](./media/032618_1700_Troubleshoo8.png)

그래서 DNS는 괜찮다는 것을 알고 있습니다. Active Directory는 KMS 정품 인증 원본으로 올바르게 구성되어 있습니다. 내 물리적 서버는 올바르게 정품 인증되었습니다. VM만 관련된 문제일까요? 이 시점에서 흥미로운 측면으로, 다른 부서의 누군가가 12개 이상의 Windows Server 2016 가상 머신도 구축하기로 결정했다고 고객이 알려주는 것입니다. 이제 제가 정품 인증되지 않도록 처리해야 하는 또 다른 12개의 서버가 있다고 가정합니다. 하지만 아니었어요! 이러한 서버는 정상적으로 정품 인증되었습니다.

**slmgr** 명령으로 돌아가서 이러한 몬스터를 정품 인증하는 방법을 알아보았습니다. 이번에는 제품 키를 설치할 수 있는 **/ipk** 스위치를 사용해 보겠습니다. [이 사이트](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj612867(v=ws.11))로 이동하여 Windows Server 2016 Standard 버전에 적합한 키를 가져왔습니다. 서버 중 일부는 Datacenter이지만, 먼저 이 서버를 수정해야 합니다.

![KMS 클라이언트 설정 키의 목록을 보여 주는 이미지](./media/032618_1700_Troubleshoo9.png)

**/ipk** 스위치를 사용하여 제품 키를 설치하고 Windows Server 2016 Standard 키를 선택했습니다.

![slmgr /ipk 명령 및 해당 결과를 보여 주는 이미지](./media/032618_1700_Troubleshoo10.png)

여기서는 Datacenter 환경에서 발생한 결과만 수집했지만 결과는 동일했습니다. **/ato** 스위치를 사용하여 정품 인증을 적용했습니다. 제품이 성공적으로 정품 인증되었다는 놀라운 메시지가 표시됩니다!

![slmgr /ato 명령 및 해당 결과를 보여 주는 이미지](./media/032618_1700_Troubleshoo11.png)

**/dlv** 스위치를 다시 사용하면 이제 Active Directory에서 정품 인증했음을 알 수 있습니다.

![slmgr /dlv 명령 및 해당 결과를 보여 주는 이미지](./media/032618_1700_Troubleshoo12.png)

이제, 무엇이 잘못되었을까요? 이러한 머신이 제대로 정품 인증되도록 설치된 키를 제거하고 이러한 일반 키를 추가하는 이유는 무엇일까요? 다른 12개 정도의 머신이 아무 문제 없이 정품 인증되는 이유는 무엇일까요? 앞에서 설명한 대로 문제를 살펴보는 초기 단계에서 중요한 사항을 놓쳤습니다. 저는 완전히 혼란스러웠으므로 앞서의 블로그 게시물에서 Charity가 제게 도움을 줄 수 있는지 알아보기 위해 그녀에게 연락했습니다. 그녀는 해당 문제를 바로 확인하여 제가 초기에 놓친 사항을 이해하는데 도움을 주었습니다.

첫 번째 **/dlv** 스위치를 실행했을 때 설명에는 키가 있었습니다. 이 설명은 Windows® 운영 체제, RETAIL 채널입니다. 저는 이를 살펴본 후 RETAIL 채널이 구매되었고 유효한 키라는 것을 의미한다고 생각했습니다.

![채널 정보가 강조 표시된 slmgr /dlv의 결과를 보여 주는 이미지](./media/032618_1700_Troubleshoo13.png)

올바르게 정품 인증된 서버에서 **/dlv** 스위치의 출력을 살펴보면 이제 VOLUME_KMSCLIENT 채널이 설명에 표시되어 있습니다. 이를 통해 실제로 볼륨 라이선스임을 알 수 있습니다.

![채널 정보가 강조 표시된 slmgr /dlv의 결과를 보여 주는 이미지](./media/032618_1700_Troubleshoo14.png)

그러면 이 RETAIL 채널은 무엇을 의미할까요? 이는 운영 체제를 설치하는 데 사용된 미디어가 MSDN ISO임을 의미합니다. 고객에게 돌아가서 어떤 기회에 두 번째 Windows Server 2016 ISO가 네트워크 주위에서 작동하고 있는지 물어보았습니다. 예, 다른 ISO가 네트워크에 있었고 다른 12개의 머신을 만드는 데 사용되었습니다. 두 개의 ISO를 비교했으며, 가상 서버를 구축하기 위해 저에게 제공된 것은 실제로 MSDN ISO였습니다. 네트워크에서 MSDN ISO를 제거했으며, 이제 기존 서버를 모두 정품 인증했으며, 이후 구축에서 정품 인증 실패에 대해 더 이상 걱정할 필요가 없습니다.

이를 통해 도움이 되었으면 좋겠고, 앞으로 시간을 절약할 수 있기를 바랍니다!

Mike
