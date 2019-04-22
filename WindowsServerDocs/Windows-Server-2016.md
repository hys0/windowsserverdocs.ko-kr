---
redirect_url: /windows-server/windows-server
ms.openlocfilehash: 6f6e0d21fdf43ce3cf9f713d5731cfea5bb069de
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812274"
---
# <a name="windows-server-2016"></a>Windows Server 2016

이 라이브러리는 IT 전문가가 Windows Server 2016을 평가, 계획, 배포, 보호 및 관리하는 데 필요한 정보를 제공합니다.

> [!Note] 
> Windows Server의 다음 버전은 변하고 있습니다! 곧 적용될 변화에 대한 자세한 내용은 [Windows Server 반기 채널 개요](./get-started/semi-annual-channel-overview.md)에서 찾을 수 있습니다. 

[![Windows Server 2016 개요 비디오](media/front-page-video.png)](https://www.youtube-nocookie.com/embed/V8oF0JpDzaM)

<table border="0" width="100%" align='center'>
  <tr style="text-align:center;">
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/get-started/what-s-new-in-windows-server-2016">
        <img height=145 src="media/whats-new-highlight.png" alt="What's new icon" title="Windows Server 16의 새로운 기능"/></a>
        <br/>새로운 기능?
    </td>
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/get-started/server-basics">
        <img height=145 src="media/1-getstarted.png" alt="get started icon" title="Windows Server 16 시작" /></a>
      <br/>시작 </td>
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/administration/index">
        <img height=145 src="media/8-management.png" alt="administer icon" title="Windows Server 관리" /></a>
      <br/>관리 </td>
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/failover-clustering/failover-clustering-overview">
        <img height=145 src="media/3-failover.png" alt="Failover clustering icon" title="Windows Server 장애 조치(failover) 클러스터링" /></a>
      <br/>장애 조치(failover) 클러스터링 </td>
  </tr>
  <tr style="text-align:center;">
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/identity/identity-and-access">
        <img height=145 src="media/4-identity.png" alt="Identity and access icon" title="Windows Server ID 및 액세스" /></a>
      <br>ID 및 액세스 </td>
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/networking/networking">
        <img height=145 src="media/6-networking.png" alt="Networking icon" title="Windows Server 네트워킹" />
        </a>
      <br/>네트워킹 </td>
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/remote/index">
        <img height=145 src="media/remote.png" alt="remote icon" title="원격 액세스 및 서버 관리" />
        </a>
      <br/>원격 액세스 </td>
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/security/security-and-assurance">
        <img height=145 src="media/5-security.png" alt="Security icon" title="Windows Server 보안 및 보증" />
      </a>
      <br/>보안 및 보증 </td>
  </tr>
  <tr style="text-align:center;">
    <td align='center' style="width:25%; border:0;">&nbsp;</td>
    <td align='center' style="width:25%; border:0;"><br>
      <a href="/windows-server/storage/storage">
        <img height=145 src="media/7-storage.png" alt="Storage icon" title="Windows Server 저장소" />
      </a>
      <br/>스토리지 </td>
   <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/virtualization/virtualization">
        <img height=145 src="media/virtualization.png" alt="virtualization icon" title="Windows Server 가상화" /></a>
      <br/>가상화 </td>
    <td align='center' style="width:25%; border:0;">&nbsp; </td>
  </tr>
</table>

<br/>

> [!Note] 
> Windows Server 2016에서 제공되는 새로운 기능을 직접 경험해 보려면 [Windows Server 평가판](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016)을 방문하여 평가판 버전을 다운로드할 수 있습니다 


## <a name="windows-server-2016-editions"></a>Windows Server 2016 버전

Windows Server 2016은 Standard, Datacenter 및 Essentials 버전으로 제공됩니다. Windows Server 2016 Datacenter에는 무제한 가상화 권한과 소프트웨어 정의 데이터 센터를 구축하는 새로운 기능이 포함됩니다. Windows Server 2016 Standard는 제한된 가상화 권한과 함께 엔터프라이즈급 기능을 제공합니다. Windows Server Essentials는 이상적인 클라우드로 연결된 최초 서버입니다. 고유의 [광범위한 문서](https://go.microsoft.com/fwlink/?LinkID=827171)를 포함하며 여기에서는 Standard 및 Datacenter 버전에 대해 주로 다룹니다. 다음 표에서는 Standard 및 Datacenter 에디션 간의 주요 차이점을 간략히 요약하여 보여 줍니다.

|기능|Datacenter|Standard|  
|-------------------|----------|-----------------------|  
|Windows Server의 핵심 기능| 예| 예|
|OSE / Hyper-V 컨테이너|제한 없음|   2|
|Windows Server 컨테이너|제한 없음|   제한 없음|
|호스트 보호 서비스| 예| 예|
|Nano Server 설치 옵션| 예| 예|
|저장소 공간 다이렉트 및 저장소 복제본을 포함한 저장소 기능| 예| no|
|보호된 가상 컴퓨터| 예| no|
|소프트웨어 방식 네트워킹 인프라(네트워크 컨트롤러, 소프트웨어 부하 분산 장치, 다중 테넌트 게이트웨이)| 예| no|

자세한 내용은 [Windows Server 2016의 가격 및 라이선싱](https://www.microsoft.com/en-us/cloud-platform/windows-server-pricing) 및 [Windows Server 버전의 기능 비교](https://www.microsoft.com/en-us/cloud-platform/windows-server-comparison)를 참조하세요.

## <a name="installation-options"></a>설치 옵션

Standard 및 Datacenter 버전은 세 가지 설치 옵션을 제공합니다.

- **Server Core:** 디스크에 필요한 공간과 잠재적인 공격 노출 영역이 줄어들고, 특히 서비스 요구 사항이 줄어듭니다. 추가 사용자 인터페이스 요소 및 그래픽 관리 도구에 대한 특정 요구가 없는 경우 **권장되는** 옵션입니다.
- **데스크톱 환경 포함 서버:** Windows Server 2012 R2에 별도 설치해야 하는 클라이언트 환경 기능을 포함하여 표준 사용자 인터페이스 및 모든 도구가 설치됩니다. 서버 역할과 기능은 서버 관리자 또는 다른 메서드를 통해 설치됩니다.
- **Nano Server:** 사설 클라우드 및 데이터 센터에 최적화된 원격 관리 서버 운영 체제입니다. Server Core 모드의 Windows Server와 유사하지만 훨씬 작고 로컬 로그온 기능이 없으며 64비트 응용 프로그램, 도구 및 에이전트에만 지원합니다. 다른 옵션보다 훨씬 적은 디스크 공간을 차지하고, 훨씬 빠르게 설치되며, 필요한 업데이트 및 다시 시작 횟수도 훨씬 적습니다.

>[!Note]
> 일부 이전 릴리스의 Windows Server와 달리 설치 후 Server Core와 데스크톱 경험 기능이 설치된 서버 간에 변환할 수 없습니다. 예를 들어 Server Core를 설치하고 나중에 데스크톱 경험이 설치된 서버를 사용하기로 결정하는 경우에는 새로 설치를 수행해야 하고, 그 반대의 경우도 마찬가지입니다.


이제 적합한 버전 및 설치 옵션에 대해 알았으므로 아래를 클릭하여 Windows Server 2016을 시작합니다.
<br/>
<br/>

<table border="0" width="100%" align='center'>
  <tr style="text-align:center;">
    <td align='center' style="width:33%; border:0;">
      <a  href="/windows-server/get-started/getting-started-with-nano-server"> <img width="175" src="media/nano.png" alt="Icon representing Nano server" title="Nano 서버 - 가장 간단한 버전" /><br/>Nano 서버 - <br/>낮은 가중치가</a>
    </td>
    <td align='center' style="width:33%; border:0;"><a href="/windows-server/get-started/getting-started-with-server-core"> <img width="175" src="media/servercore.png" alt="Icon representing the Server Core installation" title="Server Core - 권장" /><br/>Server Core - <br/>권장</a></td>
   <td align='center' style="width:33%; border:0;"><a href="/windows-server/get-started/getting-started-with-server-with-desktop-experience"><img width="175" src="media/desktop.png" alt="Icon representing the full desktop experience installation option for Windows Server" title="데스크톱 환경 - 전체 환경" /><br/>데스크톱 환경 - <br/>전체 인터페이스</a></td>
  </tr>
</table>

## <a name="windows-server-software-defined-datacenter-sddc"></a>Windows Server SDDC(소프트웨어 정의 데이터 센터)

가상화된 저장소, 네트워킹, 보안 및 관리 기술은 Windows SDDC(소프트웨어 정의 데이터 센터)의 구성 요소입니다.
<br/>
<br/>

<table border="0" width="100%" align='center'>
  <tr style="text-align:center;">
    <td align='center' style="width:10%; border:0;"></td>
    <td align='center' style="width:50%; border:0;"><a href="/windows-server/sddc"><img width="400" src="media/sddc/WS16-heading.png" alt="Icon representing SDDC" title="Windows Server SDDC(소프트웨어 정의 데이터 센터)" /><br/>Windows Server 소프트웨어 정의 데이터 센터 (SDDC)</a></td>
    <td align='center' style="width:10%; border:0;"></td>
  </tr>
</table>
