---
title: AD FS를 사용 하는 id 위임 시나리오
description: 이 시나리오에서는 id 위임 체인이 액세스 제어 검사를 수행 해야 하는 백 엔드 리소스에 액세스 해야 하는 응용 프로그램을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: c36de1c3565be7f0f0e6c6203a21345f3d227e96
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857326"
---
# <a name="identity-delegation-scenario-with-ad-fs"></a>AD FS를 사용 하는 id 위임 시나리오


[.NET Framework 4.5부터 Windows Identity Foundation (WIF)이 .NET Framework에 완전히 통합 되었습니다. WIF 3.5에 설명 된 WIF 버전은 더 이상 사용 되지 않으며 .NET Framework 3.5 SP1 또는 .NET Framework 4에 대해 개발 하는 경우에만 사용 해야 합니다. WIF 4.5이 라고도 하는 .NET Framework 4.5의 WIF에 대 한 자세한 내용은 .NET Framework 4.5 개발 가이드의 Windows Identity Foundation 설명서를 참조 하십시오.] 

이 시나리오에서는 id 위임 체인이 액세스 제어 검사를 수행 해야 하는 백 엔드 리소스에 액세스 해야 하는 응용 프로그램을 설명 합니다. 일반적으로 단순 id 위임 체인은 초기 호출자의 정보와 직접 실행 호출자의 id로 구성 됩니다.

현재 Windows 플랫폼의 Kerberos 위임 모델을 사용 하 여 백 엔드 리소스는 초기 호출자의 id가 아니라 직접 호출자의 id에만 액세스할 수 있습니다. 이 모델을 일반적으로 신뢰할 수 있는 하위 시스템 모델 이라고 합니다. WIF는 행위자 속성을 사용 하 여 초기 호출자의 id와 위임 체인의 직접 실행 호출자를 유지 관리 합니다.

다음 다이어그램에서는 Fabrikam 직원이 Contoso.com 응용 프로그램에 노출 된 리소스에 액세스 하는 일반적인 id 위임 시나리오를 보여 줍니다.

![Identity](media/ad-fs-identity-delegation/id1.png)

이 시나리오에 참여 하는 가상 사용자는 다음과 같습니다.

- Frank: Contoso 리소스에 액세스 하려는 Fabrikam 직원입니다.
- Daniel: 응용 프로그램에서 필요한 변경 내용을 구현 하는 Contoso 응용 프로그램 개발자입니다.
- Adam: Contoso IT 관리자.

이 시나리오와 관련 된 구성 요소는 다음과 같습니다.

- web1: 초기 호출자의 위임 된 id를 필요로 하는 백 엔드 리소스에 대 한 링크가 포함 된 웹 응용 프로그램입니다. 이 응용 프로그램은 ASP.NET를 사용 하 여 빌드됩니다.
- 직접 실행 호출자의 위임 된 id가 필요한 SQL Server에 액세스 하는 웹 서비스입니다. 이 서비스는 WCF를 사용 하 여 빌드됩니다.
- sts1: 클레임 공급자의 역할에 있는 STS 이며 응용 프로그램에서 예상 하는 클레임 (web1)을 내보냅니다. Fabrikam.com와 응용 프로그램을 사용 하 여 트러스트를 설정 했습니다.
- sts2: Fabrikam.com에 대 한 id 공급자의 역할에 있는 STS 이며 Fabrikam 직원이 인증 하는 데 사용 하는 끝점을 제공 합니다. Fabrikam 직원이 Contoso.com의 리소스에 액세스할 수 있도록 Contoso.com와 트러스트를 설정 했습니다.

>[!NOTE] 
>이 시나리오에서 자주 사용 되는 "ActAs token" 이라는 용어는 STS에서 발급 한 토큰을 나타내며 사용자의 id를 포함 합니다. 행위자 속성은 STS의 id를 포함 합니다.

위의 다이어그램에 표시 된 것 처럼이 시나리오의 흐름은 다음과 같습니다.


1. Contoso 응용 프로그램은 행위자 속성에 Fabrikam 직원의 id와 직접 실행 호출자의 id를 모두 포함 하는 ActAs 토큰을 가져오도록 구성 됩니다. Daniel는 이러한 변경 내용을 응용 프로그램에 구현 했습니다.
2. Contoso 응용 프로그램은 백 엔드 서비스에 ActAs 토큰을 전달 하도록 구성 되어 있습니다. Daniel는 이러한 변경 내용을 응용 프로그램에 구현 했습니다.
3. Contoso 웹 서비스는 sts1를 호출 하 여 ActAs 토큰의 유효성을 검사 하도록 구성 됩니다. Adam은 위임 요청을 처리 하기 위해 sts1를 사용 하도록 설정 했습니다.
4. Fabrikam 사용자 Frank는 Contoso 응용 프로그램에 액세스 하 고 백 엔드 리소스에 대 한 액세스 권한을 부여 합니다.

## <a name="set-up-the-identity-provider-ip"></a>IP (Id 공급자) 설정

Fabrikam.com 관리자는 Frank에 대해 세 가지 옵션을 사용할 수 있습니다.


1. AD FS (Active Directory&reg; Federation Services)와 같은 STS 제품을 구매 하 고 설치 합니다.
2. LiveID STS와 같은 클라우드 STS 제품을 구독 합니다.
3. WIF를 사용 하 여 사용자 지정 STS를 빌드합니다.

이 샘플 시나리오에서는 Frank가 옵션 1 마이그레이션를 선택 하 고 AD FS를 IP STS로 설치 한다고 가정 합니다. 또한 \windowsauth 라는 끝점을 구성 하 여 사용자를 인증 합니다. AD FS 제품 설명서를 참조 하 고, Contoso IT 관리자는 Contoso.com 도메인과의 트러스트를 설정 합니다.

## <a name="set-up-the-claims-provider"></a>클레임 공급자 설정

Contoso.com 관리자, Adam에 사용할 수 있는 옵션은 이전에 id 공급자에 대해 설명한 것과 같습니다. 이 샘플 시나리오에서는 Adam이 옵션 1을 선택 하 고 AD FS 2.0를 RP STS로 설치 한다고 가정 합니다.

## <a name="set-up-trust-with-the-ip-and-application"></a>IP 및 응용 프로그램을 사용 하 여 트러스트 설정

AD FS 설명서를 참조 하 여 Adam은 Fabrikam.com와 응용 프로그램 간에 신뢰를 설정 합니다.

## <a name="set-up-delegation"></a>위임 설정

AD FS는 위임 처리를 제공 합니다. Adam은 AD FS 설명서를 참조 하 여 ActAs 토큰을 처리할 수 있도록 합니다.

## <a name="application-specific-changes"></a>응용 프로그램별 변경 내용

기존 응용 프로그램에 id 위임에 대 한 지원을 추가 하려면 다음과 같이 변경 해야 합니다. Daniel는 WIF를 사용 하 여 이러한 변경을 수행 합니다.


- Sts1에서 web1 받은 부트스트랩 토큰을 캐시 합니다.
- CreateChannelActingAs를 발급 된 토큰과 함께 사용 하 여 백 엔드 웹 서비스에 대 한 채널을 만듭니다.
- 백 엔드 서비스의 메서드를 호출 합니다.

## <a name="cache-the-bootstrap-token"></a>부트스트랩 토큰 캐시

부트스트랩 토큰은 STS에서 발급 한 초기 토큰으로, 응용 프로그램에서 클레임을 추출 합니다. 이 샘플 시나리오에서는 사용자 Frank에 대해 sts1에서이 토큰을 발급 하 고 응용 프로그램에서이 토큰을 캐시 합니다. 다음 코드 샘플에서는 ASP.NET 응용 프로그램에서 부트스트랩 토큰을 검색 하는 방법을 보여 줍니다.

```
// Get the Bootstrap Token
SecurityToken bootstrapToken = null;

IClaimsPrincipal claimsPrincipal = Thread.CurrentPrincipal as IClaimsPrincipal;
if ( claimsPrincipal != null )
{
    IClaimsIdentity claimsIdentity = (IClaimsIdentity)claimsPrincipal.Identity;
    bootstrapToken = claimsIdentity.BootstrapToken;
}
```
WIF는 지정 된 보안 토큰을 사용 하 여 토큰 발급 요청을 ActAs 요소로 보강 하는 지정 된 형식의 채널을 만드는 [CreateChannelActingAs](https://msdn.microsoft.com/library/ee733863.aspx)메서드를 제공 합니다. 부트스트랩 토큰을이 메서드에 전달 하 고 반환 된 채널에서 필요한 서비스 메서드를 호출할 수 있습니다. 이 샘플 시나리오에서 Frank의 id는 [행위자](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.iclaimsidentity.actor.aspx) 속성이 web1's identity로 설정 되어 있습니다.

다음 코드 조각에서는 [CreateChannelActingAs](https://msdn.microsoft.com/library/ee733863.aspx) 를 사용 하 여 웹 서비스를 호출 하 고 반환 된 채널에서 서비스 메서드 ComputeResponse 중 하나를 호출 하는 방법을 보여 줍니다.

```
// Get the channel factory to the backend service from the application state
ChannelFactory<IService2Channel> factory = (ChannelFactory<IService2Channel>)Application[Global.CachedChannelFactory];

// Create and setup channel to talk to the backend service
IService2Channel channel;
lock (factory)
{
// Setup the ActAs to point to the caller's token so that we perform a 
// delegated call to the backend service
// on behalf of the original caller.
    channel = factory.CreateChannelActingAs<IService2Channel>(callerToken);
}

string retval = null;

// Call the backend service and handle the possible exceptions
try
{
    retval = channel.ComputeResponse(value);
    channel.Close();
} catch (Exception exception)
{
    StringBuilder sb = new StringBuilder();
    sb.AppendLine("An unexpected exception occurred.");
    sb.AppendLine(exception.StackTrace);
    channel.Abort();
    retval = sb.ToString();
}

```
## <a name="web-service-specific-changes"></a>웹 서비스 관련 변경 내용

웹 서비스는 WCF를 사용 하 여 빌드되고 WIF에 대해 사용 하도록 설정 되어 있으므로, 올바른 발급자 주소를 사용 하 여 IssuedSecurityTokenParameters를 사용 하 여 바인딩을 구성 하면 ActAs의 유효성 검사가 WIF에서 자동으로 처리 됩니다. 

웹 서비스는 응용 프로그램에 필요한 특정 메서드를 노출 합니다. 서비스에는 특정 코드 변경이 필요 하지 않습니다. 다음 코드 샘플에서는 IssuedSecurityTokenParameters를 사용 하 여 웹 서비스를 구성 하는 방법을 보여 줍니다.

```
// Configure the issued token parameters with the correct settings
IssuedSecurityTokenParameters itp = new IssuedSecurityTokenParameters( "http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1" );
itp.IssuerMetadataAddress = new EndpointAddress( "http://localhost:6000/STS/mex" );
itp.IssuerAddress = new EndpointAddress( "http://localhost:6000/STS" );

// Create the security binding element
SecurityBindingElement sbe = SecurityBindingElement.CreateIssuedTokenForCertificateBindingElement( itp );
sbe.MessageSecurityVersion = MessageSecurityVersion.WSSecurity11WSTrust13WSSecureConversation13WSSecurityPolicy12BasicSecurityProfile10;

// Create the HTTP transport binding element
HttpTransportBindingElement httpBE = new HttpTransportBindingElement();

// Create the custom binding using the prepared binding elements
CustomBinding binding = new CustomBinding( sbe, httpBE );

using ( ServiceHost host = new ServiceHost( typeof( Service2 ), new Uri( "http://localhost:6002/Service2" ) ) )
{
    host.AddServiceEndpoint( typeof( IService2 ), binding, "" );
    host.Credentials.ServiceCertificate.SetCertificate( "CN=localhost", StoreLocation.LocalMachine, StoreName.My );

// Enable metadata generation via HTTP GET
    ServiceMetadataBehavior smb = new ServiceMetadataBehavior();
    smb.HttpGetEnabled = true;
    host.Description.Behaviors.Add( smb );
    host.AddServiceEndpoint( typeof( IMetadataExchange ), MetadataExchangeBindings.CreateMexHttpBinding(), "mex" );

// Configure the service host to use WIF
    ServiceConfiguration configuration = new ServiceConfiguration();
    configuration.IssuerNameRegistry = new TrustedIssuerNameRegistry();

    FederatedServiceCredentials.ConfigureServiceHost( host, configuration );

    host.Open();

    Console.WriteLine( "Service2 started, press ENTER to stop ..." );
    Console.ReadLine();

    host.Close();
}
```

## <a name="next-steps"></a>다음 단계
[AD FS 개발](../../ad-fs/AD-FS-Development.md)  
