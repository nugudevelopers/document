Release Notes
==================
## Version 1.4.0

업데이트일 : 2019년 7월 11일


####1. 새로운 기능
* 실패 발화 분석 도구 추가 : [자세히 알아보기](/create-plays-with-play-builder/log-mining.md)


####2. 향상/변경된 기능
* Translator, Normalizer의 Source/Target 최대 글자수를 50에서 200으로 변경



####3. 버그 수정
* Prompt 입력창에서 백스페이스 글자 삭제 버그 수정 
* Translator 이름 중복 버그 수정 및 정렬 수정
* 학습 문장 분석 도구 내 Intent 미노출 현상 수정
* Play 구조에서 Common Action 하위 브랜치 노출
  
<br>
<br>

## Version 1.3.0

업데이트일 : 2019년 4월 23일


####1. 새로운 기능
* Utterance Model 학습 문장 분석 도구 추가 : [자세히 알아보기](/create-plays-with-play-builder/corpus-inspection.md)
* 합성음 목소리 '벨' 추가 : [자세히 알아보기](/create-plays-with-play-builder/customize-a-play.md#setting)


####2. 향상/변경된 기능
* 자동 처리 조사 추가 '예요/이에요'
* Common Action 내에서 Utterance Parameter 정의할 수 있도록 수정
* 학습문장 Export 파일 이름 변경
* Action의 Prompt 하나를 Silent Prompt로 지정하면, 모두 Silent Prompt로 변경되도록 수정
* Root Common Action끼리 Parameter 공유되지 않도록 변경



####3. 버그 수정
* Intent 리스트 최종 수정 시간이 정확히 표시 안되는 현상 수정 
* 자동완성 UI 수정
* 일부 단어 Entity 검색 안되는 버그 수정
* 여러 개의 Response Filter를 적용할 때 멈추는 현상 수정
  
<br>
<br>
## Version 1.2.0

업데이트일 : 2019년 3월 12일


####1. 새로운 기능
* Action 중복 생성을 줄이기 위한 Common Action 추가 : [자세히 알아보기](/create-plays-with-play-builder/use-common-actions.md)
* Play 내에서 공통으로 사용할 수 있는 Global Backend Parameter 추가 : [자세히 알아보기](/create-plays-with-play-builder/customize-a-play.md#setting-backend-proxy)
* Response에서 효과음 추가 : [자세히 알아보기](/create-plays-with-play-builder/use-prompts.md#skml-tag)


####2. 향상/변경된 기능
* Utterance Parameter에 Entity mapping 방식 변경 : [자세히 알아보기](/create-plays-with-play-builder/multi-entity-mapping.md)
* Entity value 및 동의어 입력 시 허용 특수기호 추가
  ' (Apostrophe), & (Ampersand), - (Hyphen) 
* 저장 버튼 동작 수정
* Entity value 및 동의어 입력 시 띄어쓰기 허용
* 여러 Prompt 등록 후 하나를 Silent prompt로 지정하면 모두 Silent prompt로 변경
* 히스토리에 Snapshot ID 노출
* Exception prompt 3개 이상 입력 허용


####3. 버그 수정
* Entity Type의 BID_QT에 숫자 보강
* Utterance parameter에 mapping할 Entity 사라지는 현상 수정
 


<br>
<br>
## Version 1.1.0

업데이트일 : 2018년 12월 13일


####1. 새로운 기능
* 멀티턴 대화 지원 (Response + Branch Action) : [자세히 알아보기](/create-plays-with-play-builder/response-with-branch-actions.md) 
* AudioPlayer Interface용 Display Interface 추가 : [자세히 알아보기](/create-plays-with-play-builder/display-interface.md)
* 다른 Intent 에서 Entity type 더 가져오기 기능 추가 : [자세히 알아보기](/create-plays-with-play-builder/response-with-branch-actions.md#multi-turn-branch)
* Silent Prompt : [자세히 알아보기](/create-plays-with-play-builder/use-prompts.md#silent-prompt)


####2. 향상/변경된 기능
* Entity value 및 동의어 입력 시 특수기호 허용 제외 
 _ (Underbar)
* Entity value 및 동의어 입력 시 띄어쓰기 허용

####3. 버그 수정
* Fallback 처리 되어야 하는 발화들이 특정 Custom Intent로 분석되는 현상 수정
* 상세 페이지에서 Ctrl(Cmd) + A 키가 동작하지 않는 현상 수정
 


####4. 다음 업데이트 추가 예정 기능
* Entity value 및 동의어 입력 시 허용 특수기호 추가
  ' (Apostrophe), & (Ampersand), - (Hyphen) 