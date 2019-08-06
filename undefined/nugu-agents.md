# NUGU 에이전트

NUGU는 NUGU 스피커, T map, Btv 등 다양한 기기에서 서비스 되며, 이러한 기기들을 통해 사용자가 접하는 인공지능 소프트웨어를 NUGU 에이전트라고 합니다. 이 때의 NUGU 에이전트에 대한 사용자 경험은 NUGU 플랫폼을 이용하는 모든 사용자들에게 일관적일 수 있도록 다음의 기본 동작 프로세스를 따르게 됩니다.

## 에이전트 상태

NUGU 에이전트와 사용자간 대화 프로세스에서 NUGU 에이전트의 상태는 크게 Idle, Listening, Processing, Responding의 4단계로 나눠질 수 있습니다.

1. 대기 상태\(Idle State\): Wake-up 가능한 대기 상태에서 사용자가 호출어\(Invocation Word\)를 발화하거나 호출 버튼을 누르면,
2. NUGU 에이전트가 사용자의 명령을 받아들일 수 있는 상태\(Listening State\)로 변경됩니다. Listening 상태에서 
3. 사용자의 발화를 받아들여 동작을 결정하는 프로세스\(Process\)를 거친 후 
4. 명령에 대한 답변이나 동작을 수행\(Responding\)하게 됩니다. 각 상태의 정의 및 기본 흐름은 아래와 같습니다.

각 상태별 정의는 아래와 같습니다.

| 상태 | 설명 |
| :--- | :--- |
| **Idle** | Wake-up 가능한 대기 상태 |
| **Listening – Passive** | 사용자 발화 입력 대기 상태 |
| **Listening – Active** | 사용자 발화 입력 중 상태 |
| **Processing** | 입력된 사용자 발화를 분석하는 상태 |
| **Responding - Speaking** | 정보나 동작에 대해서 Prompt를 제공하는 상태 |
| **Responding - Playing** | 콘텐츠를 재생하는 상태 |
| **Responding - Error** | 에러로 인하여 정상 동작/답변을 할 수 없는 상태로 Speaking 상태 대신 발생 |

사용자가 Wake-up시키지 않더라도 NUGU 에이전트가 스스로 깨어나서 동작을 수행하는 경우가 있는데, 이를 Alert 상태라고 하며 아래와 같이 나뉠 수 있습니다.

**Alert - Message**

새로운 알림 메시지 수신 상태

**Alert - Sound**

사운드 알림 수신 상태\(알람, 타이머, 전화 수신\)

NUGU 에이전트의 각 상태에서 호출 버튼을 눌렀을 때의 상태 변화는 다음과 같습니다.

| 현재 상태 | 호출 버튼 눌렀을 때의 상태 변화 |
| :--- | :--- |
| **Listening – Passive** | Listening 상태가 해제되어 Idle 상태로 돌아감 |
| **Listening – Active** | 호출 버튼을 누르기 전까지 입력된 사용자 발화까지만 입력 받고 Processing 상태 진입 |
| **Alert – Message** | 수신된 메시지를 Prompt로 제공하는 Speaking 상태 진입 |
| **Alert – Sound** | 사운드 재생이 중지되고 Listening – Passive 상태 진입 |
| **Responding – Speaking** | TTS Prompt가 중지되고 Listening – Passive 상태 진입 |
| **Responding – Error** | 이후 이어지는 사용자 발화에 대해   Prompt가 아닌 동작\(볼륨 조절, 재생, 재시작 등\)을 수행하는 경우에는 그 동작을 먼저 수행한 후, 중지되었던 Prompt를 처음부터 재시작   사용자 발화에 대해 Prompt를 제공하는 경우에는 중지되었던 Prompt는 무시   1음절 발화, 소음, 무음 등 발화 미인식으로 처리된 경우에도 재생 중이었던 Prompt는 무시 |
| **Responding - Playing** | Playing을 일시 정지하고 Listening – Passive 상태 진입   이후 이어지는 사용자 발화에 대해 동작이나 Prompt를 제공한 후, Playing 상태로 돌아옴\(1음절 발화, 소음, 무음 등 발화 미인식으로 처리된 경우에도 동일\) |

