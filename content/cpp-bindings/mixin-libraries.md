+++
title = "스크립트 믹스인 라이브러리"
weight = 10
+++

# 스크립트 믹스인 라이브러리
스크립트에 네임스페이스가 있는 새 정적 함수를 추가하는 대신, 기존 타입에 추가 _메서드_ 를 제공하는 것이 유용할 수 있습니다.

이를 위해 정적 함수가 있는 C++ 클래스에 `ScriptMixin` 메타데이터를 사용합니다.
첫 번째 인수가 메타데이터에 지정된 타입과 일치하는 모든 정적 함수는 해당 타입의 메서드로 바인딩됩니다.

대표적인 용도는 `UFUNCTION`을 가질 수 없어 일반 자동 바인딩으로 메서드를 제공할 수 없는 `USTRUCT`에 메서드를 추가하는 것입니다.

## 구조체용 믹스인 라이브러리
예를 들어 다음 C++ 믹스인 라이브러리 클래스는 스크립트의 `FVector` 구조체에 두 개의 새 메서드를 추가합니다.

```cpp
UCLASS(Meta = (ScriptMixin = "FVector"))
class UFVectorScriptMixinLibrary : public UObject
{
	GENERATED_BODY()
public:

	// This will be accessible in script as
	//     FVector Vector;
	//     Vector.ResetTo(4.0);
	UFUNCTION(ScriptCallable)
	static void ResetTo(FVector& Vector, float NewValue)
	{
		Vector = FVector(NewValue, NewValue, NewValue);
	}

	// This will become a const method, as it takes
	// a const reference to the mixin type:
	//  Usable in script as both   Vector.SummedValue
	//                        or   Vector.GetSummedValue()
	UFUNCTION(ScriptCallable)
	static float GetSummedValue(const FVector& Vector)
	{
		return Vector.X+Vector.Y+Vector.Z;
	}
}
```

## 클래스용 믹스인 라이브러리
`UCLASS`에도 새 메서드를 추가할 수 있습니다. 이 경우 첫 번째 인수로 해당 타입의 포인터를 받습니다.

다음 C++ 믹스인 라이브러리는 스크립트의 모든 `AActor`에 새 메서드를 추가합니다.

```cpp
UCLASS(Meta = (ScriptMixin = "AActor"))
class UMyActorMixinLibrary : public UObject
{
	GENERATED_BODY()
public:

	// This can be used in script as:
	//  Actor.TeleportToOrigin();
	UFUNCTION(ScriptCallable)
	static void TeleportToOrigin(AActor* Actor)
	{
		Actor->SetActorLocation(FVector(0, 0, 0));
	}
}
```

> **참고:** Angelscript 플러그인에는 일반적으로 블루프린트에 노출되지 않는 C++ 기능을 노출하기 위한 여러 믹스인 라이브러리가 포함되어 있습니다.
> 예시는 [GameplayTagMixinLibrary](https://github.com/Hazelight/UnrealEngine-Angelscript/blob/angelscript-master/Engine/Plugins/Angelscript/Source/AngelscriptCode/Public/FunctionLibraries/GameplayTagMixinLibrary.h)를 참고하세요.
