---
title: Windows Server에서 AD FS에 대 한 사용자 지정 인증 방법 빌드
description: 이 시나리오에서는 Windows Server에서 AD FS에 대 한 사용자 지정 인증 방법을 빌드하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 05/23/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 53bbc2bd30f7ede3fc9e4f3580a96514068a7d5f
ms.sourcegitcommit: d669d4af166b9018bcf18dc79cb621a5fee80042
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2020
ms.locfileid: "82037162"
---
# <a name="build-a-custom-authentication-method-for-ad-fs-in-windows-server"></a>Windows Server에서 AD FS에 대 한 사용자 지정 인증 방법 빌드

이 연습에서는 Windows Server 2012 r 2에서 AD FS에 대 한 사용자 지정 인증 방법을 구현 하기 위한 지침을 제공 합니다. 자세한 내용은 [추가 인증 방법](https://msdn.microsoft.com/library/dn758113\(v=msdn.10\))을 참조 하세요.


> [!WARNING]
> 여기에서 빌드할 수 있는 예제는 교육용&nbsp;으로만 사용 됩니다. &nbsp;이러한 지침은 모델의 필수 요소를 노출할 수 있는 가장 간단한 구현에 대 한 것입니다. &nbsp; 인증 백 엔드, 오류 처리 또는 구성 데이터가 없습니다. 
> <P></P>



## <a name="setting-up-the-development-box"></a>개발 상자를 설정합니다.

이 연습에서는 Visual Studio 2012을 사용 합니다.  Windows 용 .NET 클래스를 만들 수 있는 개발 환경을 사용 하 여 프로젝트를 빌드할 수 있습니다. **Beginauthentication** 및 **tryendauthentication** 메서드에서 .NET Framework 버전 4.5의 일부를 사용 하기 때문에 프로젝트에서 .net **4.5를 대상**으로 해야 합니다. 프로젝트에 필요한 참조가 하나 있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>참조 dll</strong></p></td>
<td><p><strong>찾는 위치</strong></p></td>
<td><p><strong>소프트웨어가 사용되는 구성 요소</strong></p></td>
</tr>
<tr class="even">
<td><p>IdentityServer.</p></td>
<td><p>Dll은 AD FS가 설치 된 Windows Server 2012 R2 서버에 있는%windir%\ADFS에 있습니다.</p>
<p></p>
<p>이 dll을 개발 컴퓨터에 복사 하 고 프로젝트에서 명시적 참조를 만들어야 합니다.</p></td>
<td><p>IAuthenticationContext, IProofData를 포함 한 인터페이스 형식</p></td>
</tr>
</tbody>
</table>


## <a name="create-the-provider"></a>공급자 만들기

1.  Visual Studio 2012: 파일-\>새로 만들기-\>프로젝트 ...를 선택 합니다.

2.  클래스 라이브러리를 선택 하 고 .NET 4.5를 대상으로 해야 합니다.

    ![공급자 만들기](media/ad-fs-build-custom-auth-method/Dn783423.71a57ae1-d53d-462b-a846-5b3c02c7d3f2(MSDN.10).jpg "공급자 만들기")

3.  AD FS 설치 된 Windows **Microsoft.IdentityServer.Web.dll** Server 2012 R2 서버 에서% windir%\\ADFS의 IdentityServer 복사본을 만들어 개발 컴퓨터의 프로젝트 폴더에 붙여 넣습니다.

4.  **솔루션 탐색기**에서 **참조** 를 마우스 오른쪽 단추로 클릭 하 고 **참조 추가** ...를 클릭 합니다.

5.  **IdentityServer** 의 로컬 복사본으로 이동 하 여 다음을 **추가** 합니다.

6.  **확인** 을 클릭 하 여 새 참조를 확인 합니다.

    ![공급자 만들기](media/ad-fs-build-custom-auth-method/Dn783423.f18df353-9259-4744-b4b6-dd780ce90951(MSDN.10).jpg "공급자 만들기")

    이제 공급자에 필요한 모든 형식을 확인 하도록를 설정 해야 합니다. 

7.  프로젝트에 새 클래스를 추가 합니다. 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 추가 ...를 클릭 합니다. ** 클래스 ...**) 아래에 표시 된 **Myadapter**와 같은 이름을 지정 합니다.

    ![공급자 만들기](media/ad-fs-build-custom-auth-method/Dn783423.6b6a7a8b-9d66-40c7-8a86-a2e3b9e14d09(MSDN.10).jpg "공급자 만들기")

8.  새 파일 MyAdapter.cs에서 기존 코드를 다음 코드로 바꿉니다.

        using System;
         using System.Collections.Generic;
         using System.Linq;
         using System.Text;
         using System.Threading.Tasks;
         using System.Globalization;
         using System.IO;
         using System.Net;
         using System.Xml.Serialization;
         using Microsoft.IdentityServer.Web.Authentication.External;
         using Claim = System.Security.Claims.Claim;

         namespace MFAadapter
         {
         class MyAdapter : IAuthenticationAdapter
         {

         }
         }

    이제 IAuthenticationAdapter에서 F12 키를 마우스 오른쪽 단추로 클릭 하 여 (정의로 이동) 필요한 인터페이스 멤버 집합을 볼 수 있습니다. 

    다음으로 이러한 작업을 간단 하 게 구현할 수 있습니다.

9.  클래스의 전체 내용을 다음으로 바꿉니다.

        namespace MFAadapter
         {
         class MyAdapter : IAuthenticationAdapter
         {
         public IAuthenticationAdapterMetadata Metadata
         {
         //get { return new <instance of IAuthenticationAdapterMetadata derived class>; }
         }

         public IAdapterPresentation BeginAuthentication(Claim identityClaim, HttpListenerRequest request, IAuthenticationContext authContext)
         {
         //return new instance of IAdapterPresentationForm derived class

         }

         public bool IsAvailableForUser(Claim identityClaim, IAuthenticationContext authContext)
         {
         return true; //its all available for now

         }

         public void OnAuthenticationPipelineLoad(IAuthenticationMethodConfigData configData)
         {
         //this is where AD FS passes us the config data, if such data was supplied at registration of the adapter

         }

         public void OnAuthenticationPipelineUnload()
         {

         }

         public IAdapterPresentation OnError(HttpListenerRequest request, ExternalAuthenticationException ex)
         {
         //return new instance of IAdapterPresentationForm derived class

         }

         public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
         {
         //return new instance of IAdapterPresentationForm derived class

         }

         }
         }

10. 아직 빌드할 준비가 되지 않았습니다 ... 이동할 인터페이스가 두 개 더 있습니다.

    하나 이상의 클래스를 프로젝트에 추가 합니다. 하나는 메타 데이터를 위한 것이 고 다른 하나는 프레젠테이션 폼입니다.  위의 클래스와 동일한 파일 내에 이러한 내용을 추가할 수 있습니다.

        class MyMetadata : IAuthenticationAdapterMetadata
         {

         }

         class MyPresentationForm : IAdapterPresentationForm
         {

         }

11. 다음에는 각에 필요한 멤버를 추가할 수 있습니다. 첫 번째, 메타 데이터 (유용한 인라인 주석 포함)

        class MyMetadata : IAuthenticationAdapterMetadata
         {
         //Returns the name of the provider that will be shown in the AD FS management UI (not visible to end users)
         public string AdminName
         {
         get { return "My Example MFA Adapter"; }
         }

         //Returns an array of strings containing URIs indicating the set of authentication methods implemented by the adapter 
         /// AD FS requires that, if authentication is successful, the method actually employed will be returned by the
         /// final call to TryEndAuthentication(). If no authentication method is returned, or the method returned is not
         /// one of the methods listed in this property, the authentication attempt will fail.
         public virtual string[] AuthenticationMethods 
         {
         get { return new[] { "http://example.com/myauthenticationmethod1", "http://example.com/myauthenticationmethod2" }; }
         }

         /// Returns an array indicating which languages are supported by the provider. AD FS uses this information
         /// to determine the best language\locale to display to the user.
         public int[] AvailableLcids
         {
         get
         {
         return new[] { new CultureInfo("en-us").LCID, new CultureInfo("fr").LCID};
         }
         }

         /// Returns a Dictionary containing the set of localized friendly names of the provider, indexed by lcid. 
         /// These Friendly Names are displayed in the "choice page" offered to the user when there is more than 
         /// one secondary authentication provider available.
         public Dictionary<int, string> FriendlyNames
         {
         get
         {
         Dictionary<int, string> _friendlyNames = new Dictionary<int, string>();
         _friendlyNames.Add(new CultureInfo("en-us").LCID, "Friendly name of My Example MFA Adapter for end users (en)");
         _friendlyNames.Add(new CultureInfo("fr").LCID, "Friendly name translated to fr locale");
         return _friendlyNames;
         }
         }

         /// Returns a Dictionary containing the set of localized descriptions (hover over help) of the provider, indexed by lcid. 
         /// These descriptions are displayed in the "choice page" offered to the user when there is more than one 
         /// secondary authentication provider available.
         public Dictionary<int, string> Descriptions
         {
         get 
         {
         Dictionary<int, string> _descriptions = new Dictionary<int, string>();
         _descriptions.Add(new CultureInfo("en-us").LCID, "Description of My Example MFA Adapter for end users (en)");
         _descriptions.Add(new CultureInfo("fr").LCID, "Description translated to fr locale");
         return _descriptions; 
         }
         }

         /// Returns an array indicating the type of claim that the adapter uses to identify the user being authenticated.
         /// Note that although the property is an array, only the first element is currently used.
         /// MUST BE ONE OF THE FOLLOWING
         /// "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"
         /// "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"
         /// "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"
         /// "https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"
         public string[] IdentityClaims
         {
         get { return new[] { "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn" }; }
         }

         //All external providers must return a value of "true" for this property.
         public bool RequiresIdentity
         {
         get { return true; }
         }
        }

    다음으로 프레젠테이션 양식:

        class MyPresentationForm : IAdapterPresentationForm
         {
         /// Returns the HTML Form fragment that contains the adapter user interface. This data will be included in the web page that is presented
         /// to the cient.
         public string GetFormHtml(int lcid)
         {
         string htmlTemplate = Resources.FormPageHtml; //todo we will implement this
         return htmlTemplate;
         }

         /// Return any external resources, ie references to libraries etc., that should be included in 
         /// the HEAD section of the presentation form html. 
         public string GetFormPreRenderHtml(int lcid)
         {
         return null;
         }

         //returns the title string for the web page which presents the HTML form content to the end user
         public string GetPageTitle(int lcid)
         {
         return "MFA Adapter";
         }


~~~
     }
~~~

12. 위의 **resources. FormPageHtml** 요소에 대 한 ' todo '를 적어둡니다. 

   1 분 이내에 수정할 수 있지만, 처음에는 새로 구현 된 형식을 기반으로 하는 최종 필수 return 문을 초기 MyAdapter 클래스에 추가 하겠습니다.  이렇게 하려면 아래 *기울임꼴로* 된 항목을 기존 IAuthenticationAdapter 구현에 추가 합니다.

       클래스 MyAdapter: IAuthenticationAdapter {public IAuthenticationAdapterMetadata Metadata {/get {return new <instance of IAuthenticationAdapterMetadata derived class>;}     get {return new MyMetadata ();}     }

        public IAdapterPresentation BeginAuthentication(Claim identityClaim, HttpListenerRequest request, IAuthenticationContext authContext)
        {
        //return new instance of IAdapterPresentationForm derived class
        return new MyPresentationForm();
        }

        public bool IsAvailableForUser(Claim identityClaim, IAuthenticationContext authContext)
        {
        return true; //its all available for now
        }

        public void OnAuthenticationPipelineLoad(IAuthenticationMethodConfigData configData)
        {
        //this is where AD FS passes us the config data, if such data was supplied at registration of the adapter

        }

        public void OnAuthenticationPipelineUnload()
        {

        }

        public IAdapterPresentation OnError(HttpListenerRequest request, ExternalAuthenticationException ex)
        {
        //return new instance of IAdapterPresentationForm derived class
        return new MyPresentationForm();
        }

        public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
        {
        //return new instance of IAdapterPresentationForm derived class
        outgoingClaims = new Claim[0];
        return new MyPresentationForm();
        }

        }

13. 이제 html 조각을 포함 하는 리소스 파일입니다. 다음 내용을 사용 하 여 프로젝트 폴더에 새 텍스트 파일을 만듭니다.

       <div id="loginArea">
        <form method="post" id="loginForm" >
        <!-- These inputs are required by the presentation framework. Do not modify or remove -->
        <input id="authMethod" type="hidden" name="AuthMethod" value="%AuthMethod%"/>
        <input id="context" type="hidden" name="Context" value="%Context%"/>
        <!-- End inputs are required by the presentation framework. -->
        <p id="pageIntroductionText">이 콘텐츠는 MFA 샘플 어댑터에서 제공 됩니다. 챌린지 입력은 아래에 표시 되어야 합니다.</p>
        <label for="challengeQuestionInput" class="block">질문 텍스트</label>
        <input id="challengeQuestionInput" name="ChallengeQuestionAnswer" type="text" value="" class="text" placeholder="Answer placeholder" />
        <div id="submissionArea" class="submitMargin">
        <input id="submitButton" type="submit" name="Submit" value="Submit" onclick="return AuthPage.submitAnswer()"/>
        </div>
        </form>
        <div id="intro" class="groupMargin">
        <p id="supportEmail">지원 정보</p>
        </div>
        <script type="text/javascript" language="JavaScript">
        //<![CDATA[
        function AuthPage() { }
        AuthPage.submitAnswer = function () { return true; };
        //]]>
        </script></div>

14. 그런 다음 **프로젝트-\>구성 요소 추가 ...를 선택 합니다. 리소스** 파일 및 파일 **리소스**이름을로 추가 하 고 **추가** 를 클릭 합니다.

   ![공급자 만들기](media/ad-fs-build-custom-auth-method/Dn783423.3369ad8f-f65f-4f36-a6d5-6a3edbc1911a(MSDN.10).jpg "공급자 만들기")

15. 그런 다음 **리소스 .resx** 파일 내에서 리소스 추가 ...를 선택 합니다. ** 기존 파일을 추가**합니다.  위에서 저장 한 텍스트 파일 (html 조각 포함)로 이동 합니다.

   GetFormHtml 코드가 리소스 파일 (.resx 파일) 이름 접두사와 리소스 자체의 이름을 통해 새 리소스의 이름을 올바르게 확인 하는지 확인 합니다.

       public string GetFormHtml (int lcid) {string htmlTemplate = Resources. MfaFormHtml;//Resxfilename.resourcename는 htmlTemplate;을 반환 합니다.    }

   이제를 빌드할 수 있습니다.

## <a name="build-the-adapter"></a>어댑터 빌드

어댑터는 Windows의 GAC에 설치할 수 있는 강력한 이름의 .NET 어셈블리에 빌드해야 합니다.  Visual Studio 프로젝트에서이 작업을 수행 하려면 다음 단계를 완료 합니다.

1.  솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 합니다.

2.  **서명** 탭에서 **어셈블리 서명** 을 선택 하 고 ** \<새로 만들기 ...를 선택 합니다. \> ** **강력한 이름 키 파일 선택** 에서 키 파일 이름 및 암호를 입력 하 고 **확인**을 클릭 합니다.  그런 다음 **어셈블리 서명** 이 선택 되어 있고 **연기 서명만** 선택 취소 되어 있는지 확인 합니다.  속성 **서명** 페이지는 다음과 같습니다.

    ![공급자 빌드](media/ad-fs-build-custom-auth-method/Dn783423.0b1a1db2-d64e-4bb8-8c01-ef34296a2668(MSDN.10).jpg "공급자 빌드")

3.  그런 다음 솔루션을 빌드합니다.

## <a name="deploy-the-adapter-to-your-ad-fs-test-machine"></a>AD FS 테스트 컴퓨터에 어댑터 배포

AD FS에서 외부 공급자를 호출 하려면 먼저 시스템에 등록 되어 있어야 합니다.  어댑터 공급자는 GAC에 설치를 포함 하 여 필요한 설치 작업을 수행 하는 설치 관리자를 제공 해야 하며, 설치 관리자가 AD FS 등록을 지원 해야 합니다.  이렇게 하지 않으면 관리자가 아래의 Windows PowerShell 단계를 실행 해야 합니다.  이러한 단계는 랩에서 테스트 및 디버깅을 사용 하도록 설정 하는 데 사용할 수 있습니다.

### <a name="prepare-the-test-ad-fs-machine"></a>테스트 AD FS 컴퓨터 준비

파일을 복사 하 여 GAC에 추가 합니다.

1.  Windows Server 2012 R2 컴퓨터 또는 가상 머신이 있는지 확인 합니다.

2.  AD FS 역할 서비스를 설치 하 고 하나 이상의 노드를 사용 하 여 팜을 구성 합니다.

    랩 환경에서 페더레이션 서버를 설정 하는 자세한 단계는 [Windows server 2012 R2 AD FS Deployment Guide](https://msdn.microsoft.com/library/dn486820\(v=msdn.10\))를 참조 하세요.

3.  Gacutil.exe 도구를 서버에 복사 합니다.

    Gacutil.exe는 windows 8 컴퓨터의 **%\\homedrive% Program Files (x86)\\Microsoft sdk\\Windows\\v 8.0 a\\bin\\NETFX 4.0 도구\\ ** 에서 찾을 수 있습니다.  **NETFX 4.0 Tools** 위치 아래의 **1033**, **en-us**및 기타 지역화 된 리소스 폴더 뿐만 아니라 **gacutil.exe** 파일 자체가 필요 합니다.

4.  공급자 파일 (하나 이상의 강력한 이름의 서명 된 .dll 파일)을 gacutil.exe와 동일한 폴더 위치에 복사 **합니다.** 위치는 편의를 위한 것입니다.

5.  팜의 각 AD FS 페더레이션 서버에서 GAC에 .dll 파일을 추가 합니다.

    예: 명령줄 도구 Gacutil.exe를 사용 하 여 dll을 GAC에 추가 합니다.`C:\>.\gacutil.exe /if .\<yourdllname>.dll`

    GAC에서 결과 항목을 보려면 다음을 수행 합니다.`C:\>.\gacutil.exe /l <yourassemblyname>`

6.  

### <a name="register-your-provider-in-ad-fs"></a>AD FS에 공급자 등록

위의 필수 구성 요소가 충족 되 면 페더레이션 서버에서 Windows PowerShell 명령 창을 열고 다음 명령을 입력 합니다. Windows 내부 데이터베이스를 사용 하는 페더레이션 서버 팜을 사용 하는 경우 팜의 기본 페더레이션 서버에서 다음 명령을 실행 해야 합니다.

1.  `Register-AdfsAuthenticationProvider –TypeName YourTypeName –Name “AnyNameYouWish” [–ConfigurationFilePath (optional)]`

    여기서 해당 Typename은 .NET 강력한 형식 이름입니다. "해당 하는 Defaultnamespace. YourPublicKeyTokenValue, processorArchitecture = MSIL"은 해당 형식 이름입니다.

    그러면 AD FS에 외부 공급자가 등록 되 고,이 이름은 위의 AnyNameYouWish로 제공한 이름으로 등록 됩니다.

2.  예를 들어 Windows 서비스 스냅인을 사용 하 여 AD FS 서비스를 다시 시작 합니다.

3.  명령 `Get-AdfsAuthenticationProvider`를 실행합니다.

    이렇게 하면 공급자가 시스템의 공급자 중 하나로 표시 됩니다.

    예제:

        PS C:\>$typeName = "MFAadapter.MyAdapter, MFAadapter, Version=1.0.0.0, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”
        PS C:\>Register-AdfsAuthenticationProvider -TypeName $typeName -Name “MyMFAAdapter”
        PS C:\>net stop adfssrv
        PS C:\>net start adfssrv

    AD FS 환경에서 장치 등록 서비스를 사용 하도록 설정한 경우 다음도 실행 합니다.`PS C:\>net start drs`

    등록 된 공급자를 확인 하려면 다음 명령을 사용`PS C:\>Get-AdfsAuthenticationProvider`합니다.

    이렇게 하면 공급자가 시스템의 공급자 중 하나로 표시 됩니다.

### <a name="create-the-ad-fs-authentication-policy-that-invokes-your-adapter"></a>어댑터를 호출 하는 AD FS 인증 정책 만들기

#### <a name="create-the-authentication-policy-using-the-ad-fs-management-snap-in"></a>AD FS 관리 스냅인을 사용 하 여 인증 정책 만들기

1.  서버 관리자 **도구** 메뉴에서 AD FS 관리 스냅인을 엽니다.

2.  **인증 정책**을 클릭 합니다.

3.  가운데 창의 **Multi-Factor Authentication**에서 **전역 설정**의 오른쪽에 있는 **편집** 링크를 클릭 합니다.

4.  페이지 맨 아래에 있는 **추가 인증 방법 선택** 에서 공급자의 adminname에 대 한 확인란을 선택 합니다. **적용**을 클릭합니다.

5.  어댑터를 사용 하 여 MFA를 호출 하는 "트리거"를 제공 하려면 **위치** 아래에서 **엑스트라넷** 과 **인트라넷**을 모두 확인 합니다 (예:). **확인**을 클릭합니다. 신뢰 당사자 마다 트리거를 구성 하려면 아래의 "Windows PowerShell을 사용 하 여 인증 정책 만들기"를 참조 하세요.

6.  다음 명령을 사용 하 여 결과를 확인 합니다.

    먼저를 `Get-AdfsGlobalAuthenticationPolicy`사용 합니다. 공급자 이름이 AdditionalAuthenticationProvider 값 중 하나로 표시 됩니다.

    그런 다음 `Get-AdfsAdditionalAuthenticationRule`를 사용 합니다. 관리자 UI에서 정책 선택의 결과로 구성 된 엑스트라넷 및 인트라넷에 대 한 규칙이 표시 됩니다.

#### <a name="create-the-authentication-policy-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 인증 정책 만들기

1.  먼저 전역 정책에서 공급자를 사용 하도록 설정 합니다.

    `PS C:\>Set-AdfsGlobalAuthenticationPolicy -AdditionalAuthenticationProvider “YourAuthProviderName”`


~~~
> [!NOTE]
> Note that the value provided for the AdditionalAuthenticationProvider parameter corresponds to the value you provided for the “Name” parameter in the Register-AdfsAuthenticationProvider cmdlet above and to the “Name” property from Get-AdfsAuthenticationProvider cmdlet output. 
> <P></P>


Example:`PS C:\>Set-AdfsGlobalAuthenticationPolicy –AdditionalAuthenticationProvider “MyMFAAdapter”`
~~~

2. 다음으로, MFA를 트리거하기 위해 전역 또는 신뢰 당사자 관련 규칙을 구성 합니다.

   예 1: 외부 요청에 대해 MFA를 요구 하는 전역 규칙을 만들려면:`PS C:\>Set-AdfsAdditionalAuthenticationRule –AdditionalAuthenticationRules 'c:[type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type = "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn" );'`

   예 2: 특정 신뢰 당사자에 대 한 외부 요청에 MFA를 요구 하는 MFA 규칙을 만들려면  개별 공급자는 Windows Server 2012 r 2에서 AD FS의 개별 신뢰 당사자에 연결할 수 없습니다.

       PS C:\>$rp = Get-AdfsRelyingPartyTrust –Name <Relying Party Name>
       PS C:\>Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –AdditionalAuthenticationRules 'c:[type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type = "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn" );'

### <a name="authenticate-with-mfa-using-your-adapter"></a>어댑터를 사용 하 여 MFA로 인증

마지막으로, 아래 단계를 수행 하 여 어댑터를 테스트 합니다.

1.  AD FS 전역 기본 인증 유형이 엑스트라넷과 인트라넷 모두에 대해 폼 인증으로 구성 되어 있는지 확인 합니다 .이를 통해 데모를 특정 사용자로 더 쉽게 인증할 수 있습니다.

    1.  AD FS 스냅인의 **인증 정책**아래에 있는 **기본 인증** 영역에서 **전역 설정**옆의 **편집** 을 클릭 합니다.

        1.  또는 **다단계 정책** UI에서 **기본** 탭을 클릭 하면 됩니다.

2.  엑스트라넷 및 인트라넷 인증 방법 모두에 대해 **폼 인증이** 선택 되어 있는지 확인 합니다.  **확인**을 클릭합니다.

3.  IDP 시작 된 로그온 html 페이지 (https://\<fsname\>/adfs/ls/idpinitiatedsignon.htm)를 열고 테스트 환경에서 유효한 AD 사용자로 로그인 합니다.

4.  기본 인증에 대 한 자격 증명을 입력 합니다.

5.  예 고 챌린지 질문이 표시 된 MFA 양식 페이지가 표시 됩니다. 

    구성 된 어댑터가 둘 이상 있는 경우 위의 이름과 함께 MFA 선택 페이지가 표시 됩니다.

    ![어댑터로 인증](media/ad-fs-build-custom-auth-method/Dn783423.c98d2712-cbd3-4cb9-ac03-2838b81c4f63(MSDN.10).jpg "어댑터로 인증")

    ![어댑터로 인증](media/ad-fs-build-custom-auth-method/Dn783423.fd3aefc0-ef6c-4a8c-a737-4914c78ff2d2(MSDN.10).jpg "어댑터로 인증")

이제 인터페이스를 제대로 구현 했으며 모델의 작동 방식에 대 한 지식이 있습니다. BeginAuthentication에서 중단 지점과 나머지를 설정 하는 추가 예제로 m m을 사용할 수 있습니다.  사용자가 처음으로 MFA 폼에 들어가면 BeginAuthentication이 실행 되는 방식을 확인할 수 있습니다. 반면에는 각 폼 전송 시에는는 BeginAuthentication이 트리거됩니다.

## <a name="update-the-adapter-for-successful-authentication"></a>성공적인 인증을 위해 어댑터 업데이트

대기-예제 어댑터는 성공적으로 인증 되지 않습니다.\!  이는 코드에서 TryEndAuthentication에 대해 null을 반환 하지 않기 때문입니다.

위의 절차를 완료 하 여 기본 어댑터 구현을 만들고이를 AD FS 서버에 추가 했습니다.  MFA 양식 페이지를 가져올 수 있지만, 아직 인증 되지 않은 경우에는 아직 인증 되지 않았습니다.  이를 추가 해 보겠습니다.

다음과 같이 TryEndAuthentication 구현을 회수 합니다.

    public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
     {
     //return new instance of IAdapterPresentationForm derived class
     outgoingClaims = new Claim[0];
     return new MyPresentationForm();

     }

항상 MyPresentationForm ()를 반환 하지 않도록 업데이트 해 보겠습니다.  이를 위해 클래스 내에서 간단한 유틸리티 메서드를 하나 만들 수 있습니다.

    static bool ValidateProofData(IProofData proofData, IAuthenticationContext authContext)
     {
     if (proofData == null || proofData.Properties == null || !proofData.Properties.ContainsKey("ChallengeQuestionAnswer"))
     {
     throw new ExternalAuthenticationException("Error - no answer found", authContext);
     }

     if ((string)proofData.Properties["ChallengeQuestionAnswer"] == "adfabric")
     {
     return true;
     }
     else
     {
     return false;
     }
     }

그런 다음 아래와 같이 TryEndAuthentication을 업데이트 합니다.

    public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
     {
     outgoingClaims = new Claim[0];
     if (ValidateProofData(proofData, authContext))
     {
     //authn complete - return authn method
     outgoingClaims = new[] 
     {
     // Return the required authentication method claim, indicating the particulate authentication method used.
     new Claim( "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", 
     "http://example.com/myauthenticationmethod1" )
     };
     return null;
     }
     else
     {
     //authentication not complete - return new instance of IAdapterPresentationForm derived class
     return new MyPresentationForm();
     }
     }

이제 테스트 상자에서 어댑터를 업데이트 해야 합니다.  먼저 AD FS 정책을 실행 취소 한 다음 AD FS에서 등록을 취소 하 고 AD FS를 다시 시작한 다음 gac에서 .dll을 제거 하 고, gac에 새 .dll을 추가한 다음 AD FS에 등록 하 고 AD FS를 다시 시작한 후 AD FS 정책을 다시 구성 해야 합니다.

## <a name="deploy-and-configure-the-updated-adapter-on-your-test-ad-fs-machine"></a>테스트 AD FS 컴퓨터에 업데이트 된 어댑터 배포 및 구성

### <a name="clear-ad-fs-policy"></a>AD FS 정책 지우기

아래 표시 된 MFA UI에서 모든 MFA 관련 확인란의 선택을 취소 한 다음 확인을 클릭 합니다.

![정책 지우기](media/ad-fs-build-custom-auth-method/Dn783423.c111b4e7-5b05-413c-8b0f-222a0e91ac1f(MSDN.10).jpg "정책 지우기")

### <a name="unregister-provider-windows-powershell"></a>공급자 등록 취소 (Windows PowerShell)

`PS C:\> Unregister-AdfsAuthenticationProvider –Name “YourAuthProviderName”`

예:`PS C:\> Unregister-AdfsAuthenticationProvider –Name “MyMFAAdapter”`

"Name"에 대해 전달 하는 값은 Register-adfsauthenticationprovider cmdlet에 제공한 "Name"과 동일한 값입니다.  Register-adfsauthenticationprovider에서 출력 되는 "Name" 속성 이기도 합니다.

공급자 등록을 취소 하기 전에 AD FS 관리 스냅인에서 체크 인 한 확인란을 선택 취소 하거나 Windows PowerShell을 사용 하 여 AdfsGlobalAuthenticationPolicy에서 공급자를 제거 해야 합니다.

이 작업 후에는 AD FS 서비스를 다시 시작 해야 합니다.

### <a name="remove-assembly-from-gac"></a>GAC에서 어셈블리 제거

1.  먼저 다음 명령을 사용 하 여 항목의 정규화 된 강력한 이름을 찾습니다.`C:\>.\gacutil.exe /l <yourAdapterAssemblyName>`

    예:`C:\>.\gacutil.exe /l mfaadapter`

2.  그런 다음, 다음 명령을 사용 하 여 GAC에서 제거 합니다.`.\gacutil /u “<output from the above command>”`

    예:`C:\>.\gacutil /u “mfaadapter, Version=1.0.0.0, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”`

### <a name="add-the-updated-assembly-to-gac"></a>GAC에 업데이트 된 어셈블리 추가

먼저 업데이트 된 .dll을 로컬로 붙여넣어야 합니다. `C:\>.\gacutil.exe /if .\MFAAdapter.dll`

### <a name="view-assembly-in-the-gac-cmd-line"></a>GAC에서 어셈블리 보기 (cmd 줄)

`C:\> .\gacutil.exe /l mfaadapter`

### <a name="register-your-provider-in-ad-fs"></a>AD FS에 공급자 등록

1.  `PS C:\>$typeName = "MFAadapter.MyAdapter, MFAadapter, Version=1.0.0.1, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”`

2.  `PS C:\>Register-AdfsAuthenticationProvider -TypeName $typeName -Name “MyMFAAdapter1”`

3.  AD FS 서비스를 다시 시작합니다.

### <a name="create-the-authentication-policy-using-the-ad-fs-management-snap-in"></a>AD FS 관리 스냅인을 사용 하 여 인증 정책 만들기

1.  서버 관리자 **도구** 메뉴에서 AD FS 관리 스냅인을 엽니다.

2.  **인증 정책**을 클릭 합니다.

3.  **Multi-Factor Authentication**에서 **전역 설정**의 오른쪽에 있는 **편집** 링크를 클릭 합니다.

4.  **추가 인증 방법 선택**에서 공급자의 adminname에 대 한 확인란을 선택 합니다. **적용**을 클릭합니다.

5.  어댑터를 사용 하 여 MFA를 호출 하는 "트리거"를 제공 하려면 위치 아래에서 **엑스트라넷** 과 **인트라넷**을 모두 확인 합니다 (예:). **확인**을 클릭합니다.

### <a name="authenticate-with-mfa-using-your-adapter"></a>어댑터를 사용 하 여 MFA로 인증

마지막으로, 아래 단계를 수행 하 여 어댑터를 테스트 합니다.

1.  AD FS 전역 기본 인증 유형이 엑스트라넷과 인트라넷 모두에 대해 **폼 인증** 으로 구성 되어 있는지 확인 합니다. 이렇게 하면 특정 사용자로 쉽게 인증할 수 있습니다.

    1.  AD FS 관리 스냅인의 **인증 정책**아래에 있는 **기본 인증** 영역에서 **전역 설정**옆의 **편집** 을 클릭 합니다.

        1.  또는 다단계 정책 UI에서 **기본** 탭을 클릭 하면 됩니다.

2.  **엑스트라넷** 및 **인트라넷** 인증 방법 모두에 대해 **폼 인증이** 선택 되어 있는지 확인 합니다.  **확인**을 클릭합니다.

3.  IDP 시작 된 로그온 html 페이지 (https://\<fsname\>/adfs/ls/idpinitiatedsignon.htm)를 열고 테스트 환경에서 유효한 AD 사용자로 로그인 합니다.

4.  기본 인증에 대 한 자격 증명을 입력 합니다.

5.  예제 챌린지 텍스트가 표시 된 MFA 폼 페이지가 표시 됩니다.

    1.  구성 된 어댑터가 둘 이상 있는 경우 MFA 선택 페이지가 표시 됩니다.

MFA 인증 페이지에서 "adfabric"을 입력 하면 성공적인 로그인이 표시 됩니다.

![어댑터로 로그인](media/ad-fs-build-custom-auth-method/Dn783423.630d8a91-3bfe-4cba-8acf-03eae21530ee(MSDN.10).jpg "어댑터로 로그인")

![어댑터로 로그인](media/ad-fs-build-custom-auth-method/Dn783423.c340fa73-f70f-4870-b8dd-07900fea4469(MSDN.10).jpg "어댑터로 로그인")

## <a name="see-also"></a>참고 항목

#### <a name="other-resources"></a>관련 자료

[추가 인증 방법](https://msdn.microsoft.com/library/dn758113\(v=msdn.10\))  
[중요 애플리케이션에 추가 Multi-Factor Authentication을 사용하여 위험 관리](https://msdn.microsoft.com/library/dn280949\(v=msdn.10\))

