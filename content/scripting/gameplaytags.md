+++
title = "게임플레이 태그"
weight = 105
sort_by = "weight"
+++

# 게임플레이 태그

게임플레이 태그는 여러 Unreal 시스템에서 사용됩니다. 자세한 내용은 [게임플레이 태그 Unreal 문서](https://docs.unrealengine.com/5.1/en-US/using-gameplay-tags-in-unreal-engine/)를 참고하세요.

모든 `FGameplayTag`는 전역 네임스페이스 `GameplayTags`에 자동으로 바인딩됩니다. 점 구분자를 포함해 영숫자가 아닌 모든 문자는 밑줄 `_`로 변환됩니다.

<div class="code_block" style="color: #d4d4d4;background-color: #1e1e1e;font-family: 'Terminus (TTF) for Windows', Consolas, 'Courier New', monospace;font-weight: normal;font-size: 14px;line-height: 19px;white-space: pre;"><div><span style="color: #6a9955;">// Assuming there is a GameplayTag named "UI.Action.Escape"</span></div><div><span style="color: #4ec9b0;">FGameplayTag</span><span style="color: #d4d4d4;"> </span><span style="color: #9cdcfe;">TheTag</span><span style="color: #d4d4d4;"> = <span style="color: #4ec9b0">GameplayTags</span></span><span style="color: #d4d4d4;">::</span><span style="color: #9cdcfe;">UI_Action_Escape<span style="color: #d4d4d4">;</span></span></div></div>
