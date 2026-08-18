+++
title = "개발 현황"
weight = 10
+++

# 개발 현황
[Hazelight](http://hazelight.se)는 2018년 초부터 이 프로젝트의 Angelscript 통합을 게임 개발에 적극적으로 사용해 왔습니다.
현재 팀 내 30명 이상의 개발자가 매일 사용하고 있습니다.

최근 출시한 두 게임 [Split Fiction](https://www.ea.com/games/split-fiction/split-fiction)과 [It Takes Two](https://www.ea.com/games/it-takes-two)는 모두 게임플레이 대부분을 Angelscript로 작성했습니다.
Split Fiction에는 16,000개가 넘는 스크립트 파일에 170만 줄 이상의 Angelscript 코드가 포함되어 있습니다.

Hazelight는 이 사이트에서 이미 제공하는 것 이상의 유지보수나 지원을 보장하지 않습니다.
상용 프로젝트에서 Angelscript 통합 사용을 고려하고 있다면, 사용 중 발생할 수 있는 문제를 조사할 수 있는 엔진 프로그래머를 확보하기를 강력히 권장합니다.


## 플랫폼 지원
Hazelight에서는 Windows, PS5, Xbox Series X|S 플랫폼에서 이 플러그인을 정기적으로 사용하고 테스트합니다.
다른 스튜디오에서는 Hazelight가 내부적으로 테스트하지 않은 플랫폼에서도 성공적으로 빌드하고 실행했습니다.

다른 플랫폼에 관해 궁금한 점이 있다면 [Discord 서버](https://discord.gg/39wmC2)에 참여해 자유롭게 질문하세요.


## 알려진 제한 사항
* `Super::Function()` 호출은 Angelscript의 부모 함수에만 사용할 수 있습니다. `BlueprintNativeEvent`를 오버라이드할 때 C++의 부모 함수를 호출할 수 없습니다.
* Unreal 인터페이스(`IInterface`/`UInterface`)는 Angelscript에서 사용할 수 없습니다.
