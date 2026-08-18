+++
title = "자동 바인딩"
weight = 10
+++

# 자동 바인딩

엔진이 시작되면 Angelscript 플러그인이 Unreal의 모든 리플렉션 데이터를 자동으로 탐색합니다.

C++의 관련 타입, 프로퍼티, 함수는 스크립트에서 사용할 수 있도록 Angelscript에 자동으로 바인딩됩니다.

자동 바인딩의 기본 원칙은 다음과 같습니다.
블루프린트에서 사용할 수 있다면 Angelscript에서도 사용할 수 있어야 합니다.

## 클래스 바인딩

C++에서 `UCLASS()`로 표시된 클래스는 `BlueprintType` 지정자가 있거나 `BlueprintCallable` 함수가 하나라도 있으면 자동으로 바인딩됩니다.

`NotInAngelscript` 메타데이터를 추가하면 클래스를 자동 바인딩에서 제외할 수 있습니다.

## 구조체 바인딩

C++에서 `USTRUCT()`로 표시된 구조체는 `BlueprintType` 지정자가 있거나 블루프린트에서 접근 또는 편집할 수 있는 프로퍼티가 하나라도 있으면 자동으로 바인딩됩니다.

`NoAutoAngelscriptBind` 메타데이터를 추가하면 구조체를 자동 바인딩에서 제외할 수 있습니다.

## 프로퍼티 바인딩

### 읽기/쓰기 플래그

`BlueprintReadWrite` 또는 `BlueprintReadOnly`로 선언된 C++ `UPROPERTY`는 스크립트에 자동으로 바인딩됩니다.

프로퍼티가 `BlueprintReadOnly`이면 `const`가 되어 스크립트에서 변경할 수 없습니다.

프로퍼티를 블루프린트에 노출하지 않고 Angelscript에만 노출하려면 `ScriptReadWrite` 또는 `ScriptReadOnly` 지정자를 사용할 수 있습니다.

### 편집 가능 플래그

편집 가능 플래그(`EditAnywhere`, `EditInstanceOnly`, `EditDefaultsOnly`) 중 하나로 선언된 프로퍼티도 스크립트에 노출됩니다.

> **참고:** 프로퍼티에 편집 가능 플래그는 있지만 블루프린트 접근 플래그가 없다면, 클래스의 `default` 문 안에서만 스크립트로 접근할 수 있습니다.
> _[기본값 문](@/scripting/actors-components.md#default-statements)을 참고하세요._

### 프로퍼티 제외

블루프린트에서 접근할 수 있는 프로퍼티라도 `NotInAngelscript` 메타데이터를 추가하면 Angelscript 바인딩에서 제외할 수 있습니다.

## 함수 바인딩

### 호출 가능 플래그

`BlueprintCallable` 또는 `BlueprintPure`가 지정된 모든 C++ `UFUNCTION`은 스크립트에 자동으로 바인딩됩니다.

함수를 블루프린트에 노출하지 않고 Angelscript에만 노출하려면 `ScriptCallable` 지정자를 사용할 수 있습니다.

### 블루프린트 이벤트

`BlueprintImplementableEvent` 및 `BlueprintNativeEvent` 지정자가 있는 `UFUNCTION`은 블루프린트뿐 아니라 스크립트에서도 오버라이드할 수 있습니다.

> [C++의 BlueprintEvent 오버라이드](@/scripting/functions-and-events.md#overriding-blueprintevents-from-c)를 참고하세요.

### 함수 제외

블루프린트에서 접근할 수 있는 함수라도 `NotInAngelscript` 메타데이터를 추가하면 Angelscript 바인딩에서 제외할 수 있습니다.

### 사용 중단된 함수

사용 중단으로 표시된 함수는 스크립트에 전혀 바인딩되지 않습니다.

스크립트에는 사용 중단 경고 기능이 없으므로, Epic이 특정 API의 사용을 중단하면 엔진 업그레이드 시 스크립트를 변경해야 할 수 있습니다.

## 정적 함수

`UCLASS`에 선언된 정적 함수는 스크립트에서 네임스페이스가 있는 전역 함수로 바인딩됩니다.

정적 함수를 바인딩할 때만 클래스 이름에 [네임스페이스 단순화](@/scripting/function-libraries.md#namespace-simplification)가 적용됩니다.

## 열거형 바인딩

C++에 선언된 모든 `UENUM()`은 스크립트에서 자동으로 사용할 수 있습니다.
