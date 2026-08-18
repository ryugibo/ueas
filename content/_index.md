+++
title = "홈"
+++

# Unreal Engine Angelscript

UnrealEngine-Angelscript는 완전한 기능을 갖춘 스크립팅 언어를 UE5에 통합하는 엔진 수정 사항과 플러그인 모음입니다.
게임플레이 대부분을 Angelscript로 작성해 출시한 [Split Fiction](https://www.ea.com/games/split-fiction/split-fiction)과 [It Takes Two](https://www.ea.com/games/it-takes-two)의 개발사 [Hazelight](http://hazelight.se)가 활발히 개발하고 있습니다.
[여러 다른 스튜디오](@/project/resources.md)에서도 UnrealEngine-Angelscript를 사용한 게임을 출시했습니다.

Angelscript를 통합하는 Unreal 플러그인은 오픈 소스이며, 스톡홀름을 비롯한 전 세계 스튜디오에서 기여를 받고 있습니다.

스크립팅 언어에 대한 소개는 [스크립팅 입문](@/getting-started/introduction.md)을 참고하세요.

관심이 있거나 궁금한 점이 있다면 [Discord 서버](https://discord.gg/39wmC2e)에서 이야기해 주세요!

## 목표

복잡한 게임플레이 시스템을 만들 때 블루프린트 비주얼 스크립팅은 유지 관리하기 어려운 스파게티 코드로 이어지기 쉽습니다.
반면 이러한 시스템을 C++로 만들면 반복 작업 시간이 길어지고, 디자이너나 게임플레이 스크립터가 사용하기 부담스러울 수 있습니다.

이 플러그인을 사용하면 단순하면서도 강력한 스크립팅 언어인 [Angelscript](https://www.angelcode.com/angelscript/)의 커스텀 버전으로 게임플레이를 작성할 수 있습니다.

이 플러그인이 제공하는 주요 이점은 다음과 같습니다.

- **빠른 반복 작업** - 에디터에서 스크립트를 즉시 다시 불러올 수 있으므로, 컴파일과 에디터 재시작을 기다리지 않고 멋진 기능을 만드는 데 집중할 수 있습니다.
- **향상된 협업** - 프로그래머와 디자이너가 더 이상 C++과 블루프린트로 나뉘지 않으므로, 같은 시스템과 도구를 사용해 긴밀하게 협업할 수 있습니다.
- **성능** - Angelscript는 게임 스크립팅에서 블루프린트보다 훨씬 뛰어난 성능을 제공하며, 출시 빌드에서 [트랜스파일된 스크립트](@/cpp-bindings/precompiled-data.md)를 사용하면 네이티브 C++에 근접한 성능을 냅니다.

## 기능

### 익숙하지만 더 단순한 문법

{{ img(path="scripting.png") }}

Unreal C++에 익숙한 프로그래머라면 곧바로 친숙함을 느낄 수 있으며, 디자이너가 쉽게 사용하고 흔한 C++ 함정을 피할 수 있도록 여러 핵심 요소를 단순화했습니다.

### 빠른 반복 작업을 위한 스크립트 핫 리로드

저장하는 즉시 스크립트 액터와 컴포넌트의 변경 사항을 확인할 수 있습니다.

Unreal Editor를 재시작하지 않고도 모든 스크립트 변경 사항을 다시 불러올 수 있습니다.
PIE(Play In Editor)로 게임을 실행하는 동안에도 플레이 세션을 종료하지 않고 구조에 영향을 주지 않는 스크립트 코드 변경 사항을 다시 불러올 수 있습니다!

{{ img(path="properties.png", alt="프로퍼티") }}

### 완전한 에디터 지원을 제공하는 스크립팅

더 편리한 스크립팅을 위해 Language Server Protocol을 완전히 지원하는 [Visual Studio Code 확장 프로그램](https://marketplace.visualstudio.com/items?itemName=Hazelight.unreal-angelscript)을 제공합니다.

다음과 같은 다양한 에디터 기능을 지원합니다.

- 코드 자동 완성
- 오류 진단
- 심볼 이름 변경
- 모든 참조 찾기
- 의미론적 강조 표시

{{ img(path="timer.png") }}

### 기존 C++ 및 블루프린트 작업 흐름과 통합

Angelscript 클래스는 C++에서 노출한 모든 `BlueprintImplementableEvent`를 오버라이드할 수 있으며,
자식 블루프린트의 부모 클래스로도 자연스럽게 사용할 수 있습니다.

작업 흐름에 가장 잘 맞는 도구 조합을 자유롭게 사용하세요.

{{ img(path="functions.png", alt="함수") }}

### Visual Studio Code를 통한 디버깅 지원

Visual Studio Code 확장 프로그램으로 스크립트 코드를 디버깅할 수 있습니다.
중단점을 설정하고 변수를 살펴보거나 스크립트를 단계별로 실행하여 문제를 찾을 수 있습니다.

{{ img(path="debug.png", alt="디버깅") }}
