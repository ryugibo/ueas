+++
title = "설치"
weight = 10
+++

# 설치
## 1. Unreal Engine 소스 접근 권한 얻기
Angelscript 통합이 작동하려면 Unreal Engine 코드를 직접 변경해야 합니다.
이 프로젝트에서 사용하는 엔진 버전에 접근하려면 Unreal Engine 소스 코드 접근 권한이 필요합니다.

소스 코드 접근 권한을 얻으려면 Epic Games의 다음 안내를 따르세요.
[https://www.unrealengine.com/en-US/ue-on-github](https://www.unrealengine.com/en-US/ue-on-github)


## 2. UnrealEngine-Angelscript 다운로드
Unreal 소스 코드 접근 권한을 얻은 다음 [UnrealEngine-Angelscript GitHub 저장소](https://github.com/Hazelight/UnrealEngine-Angelscript)를 복제하고,
평소와 같이 Visual Studio를 사용해 Unreal Editor를 빌드하세요.

엔진에 추가하려는 모든 플러그인도 소스에서 빌드해야 합니다.
이 포크는 미리 빌드된 바이너리 플러그인과 호환되지 않습니다.


## 3. Visual Studio Code 확장 프로그램 설치
자동 완성과 디버깅을 지원하는 Visual Studio Code 확장 프로그램을 사용할 수 있습니다.

[https://code.visualstudio.com/](https://code.visualstudio.com/)에서 Visual Studio Code를 설치하세요.

그런 다음 마켓플레이스에서 [Unreal Angelscript 확장 프로그램](https://marketplace.visualstudio.com/items?itemName=Hazelight.unreal-angelscript)을 설치하거나,
Visual Studio Code의 확장 사이드바에서 'Unreal Angelscript'를 검색하세요.
