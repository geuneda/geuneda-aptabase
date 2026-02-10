# Geuneda Aptabase SDK

[Aptabase](https://aptabase.com)의 Unity SDK입니다. 모바일, 데스크톱, 웹 앱을 위한 오픈소스, 프라이버시 우선 분석 도구입니다.

> 원본 저장소: [CoderGamester/aptabase-unity](https://github.com/CoderGamester/aptabase-unity)

## 설치

[Unity Package Manager](https://docs.unity3d.com/Manual/upm-ui.html)를 통해 설치할 수 있습니다.

`Window` > `Package Manager` > `+` > `Add Package from git URL`에서 다음 URL을 입력하세요:

```
https://github.com/geuneda/geuneda-aptabase.git
```

## 프로젝트 설정

1. Aptabase에서 `App Key`를 발급받으세요. 좌측 메뉴의 `Instructions`에서 확인할 수 있습니다.
2. `Aptabase/Resources/AptabaseSettings.Asset` 설정 파일의 `App Key` 필드에 키를 입력하세요.
3. 키에 따라 `Host`가 자동으로 선택됩니다. 셀프 호스팅 버전의 경우 `SelfHostURL` 필드가 추가로 나타납니다.

앱 버전은 자동으로 감지되지만, `AppVersion` 필드로 수동 설정할 수 있습니다. 플랫폼별 빌드 번호가 다를 수 있으므로 `AppBuildNumber`를 제공하여 정확한 버전 추적이 가능합니다.

이벤트는 프로덕션에서 60초, 개발 환경에서 2초마다 배치 전송됩니다. `FlushInterval` 필드에 밀리초 단위로 원하는 값을 입력하여 변경할 수 있습니다.

## 사용법

Aptabase SDK는 앱이 시작되면 자동으로 백그라운드에서 실행됩니다. 이벤트를 기록하려면 다음 코드를 사용하세요. Props 매개변수는 선택 사항입니다.

```csharp
Aptabase.TrackEvent("app_started", new Dictionary<string, object>
{
    {"hello", "world"}
});
```

이벤트 큐를 수동으로 플러시하려면 다음을 사용하세요:

```csharp
Aptabase.Flush();
```

### 참고 사항

1. SDK는 OS, 앱 버전 등 유용한 정보를 자동으로 이벤트에 추가합니다.
2. Aptabase로 전송되는 데이터는 사용자가 직접 제어합니다. SDK는 자동으로 이벤트를 추적하지 않으며, 수동으로 기록해야 합니다.
   - 따라서 최소한 앱 시작 시 이벤트를 추적하는 것을 권장합니다.
3. 이벤트 기록 호출을 await할 필요가 없습니다. 백그라운드에서 실행됩니다.
4. 커스텀 속성에는 문자열과 숫자 값만 허용됩니다.

## Apple App Store 제출 준비

Apple App Store에 앱을 제출할 때 `App Privacy` 양식을 작성해야 합니다. [Aptabase 사용 시 Apple App Privacy 작성 가이드](https://aptabase.com/docs/apple-app-privacy)를 참고하세요.

## 라이선스

원본 저장소의 라이선스를 따릅니다. [LICENSE](LICENSE) 파일을 참고하세요.
