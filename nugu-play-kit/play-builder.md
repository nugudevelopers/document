# Play Builder

Play Builder는 Play를 만드는 도구입니다. 사용자의 발화를 이해하는 User Utterance Model, 그리고 이를 기반으로 기능을 수행하는 Action들을 조합하여 하나의 완결된 Play를 만듭니다.

하나의 Play를 완성하기 위해서는 크게

1. 사용자의 발화를 정확하게 분석하도록 Intent/Entity를 정의하여 NLU 엔진을 학습시키고,
2. Intent별로 Action을 정의하여 사용자의 요청에 대해 적절한 응답과 동작을 처리할 수 있어야 하며,
3. 실질적으로 사용자 발화에 대해 응답하거나 동작할 수 있는 Backend proxy API를 연동하는 것이 필요합니다.

Play Builder는 이 모든 기능들을 하나의 통합된 환경에서 GUI 기반으로 제공하고 있습니다. 따라서 개발자가 아니어도 Play Builder를 활용하여 자신만의 Play를 개발할 수 있습니다.

