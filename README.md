# nhn-cloud-drawio

말로 설명하면 **NHN Cloud 아키텍처 구성도**를 그려 주는 Claude Code 스킬입니다.
도형은 전부 [NHN Cloud 아이콘 라이브러리](https://nhn-cloud.github.io/Icons/)에서 가져옵니다.

> 사내 파일럿 중입니다. 쓰시다 막히거나 어색한 점이 있으면 이슈로 남겨 주세요.

## 준비물

| 항목 | 확인 |
| --- | --- |
| Claude Code | 설치돼 있어야 합니다 |
| Python 3.9 이상 | `python --version` |
| PyYAML | `pip install pyyaml` |

## 설치 — 한 줄

**Windows (PowerShell)**

```powershell
git clone https://github.com/TOAST-DOCS/Icons "$env:USERPROFILE\.claude\skills\nhn-cloud-drawio"
```

**macOS · Linux**

```bash
git clone https://github.com/TOAST-DOCS/Icons ~/.claude/skills/nhn-cloud-drawio
```

폴더 이름 `nhn-cloud-drawio` 가 곧 스킬 이름입니다. **그대로 두세요.**
Claude Code 를 새로 열면 목록에 나타납니다.

## 쓰는 법

구성도를 그리고 싶은 폴더에서 Claude Code 를 열고, 평소처럼 말하면 됩니다.

> 판교 리전 VPC에 퍼블릭 서브넷 LB 한 대, 프라이빗 서브넷에 웹 서버 2대,
> DB는 Master/Replica로 구성도 그려줘

진행 순서는 이렇습니다.

1. 아이콘 이름을 라이브러리에서 **실제로 조회**합니다. 없는 아이콘은 지어내지 않고 되묻습니다.
2. YAML 명세를 먼저 보여 줍니다. 확인하거나 고쳐 달라고 하세요.
3. `.drawio` 를 만들고 브라우저 draw.io 로 엽니다.
4. 세밀한 배치는 draw.io 에서 직접 손보시면 됩니다.

### 고친 그림을 다시 바꿀 때도 그냥 말하세요

> DB를 하나 더 추가해 줘

**draw.io 에서 옮겨 둔 위치는 그대로 두고 바뀐 부분만 반영합니다.** 처음부터 다시 그리지 않습니다.

## 알아 두실 것

- 자동 배치는 **초안 수준**입니다. 선이 겹치거나 그룹 경계를 지나는 건 draw.io 에서 밀어 주세요.
- 처음 열었을 때 왼쪽 도형 패널에 NHN Cloud 팔레트가 없으면,
  <https://nhn-cloud.github.io/Icons/> 를 한 번 열어 주세요. 설정이 브라우저에 저장됩니다.
- draw.io 웹에서 `Ctrl+S` 는 다운로드입니다. 제자리 저장을 원하면
  draw.io 의 `파일 > 열기 > 디바이스` 로 `.drawio` 를 직접 여세요.
- 아이콘 팔레트는 실행할 때마다 원격에서 받아옵니다. 아이콘이 추가되면 바로 반영됩니다.

## 업데이트

```powershell
cd "$env:USERPROFILE\.claude\skills\nhn-cloud-drawio"
git pull
```

## 제거

폴더를 지우면 끝입니다.

```powershell
Remove-Item -Recurse "$env:USERPROFILE\.claude\skills\nhn-cloud-drawio"
```

## 직접 실행 (스킬 없이)

Claude 를 거치지 않고 명령으로도 쓸 수 있습니다.

```powershell
$SKILL = "$env:USERPROFILE\.claude\skills\nhn-cloud-drawio"

python "$SKILL\nhn_diagram.py" --list 로드밸런        # 아이콘 이름 찾기
python "$SKILL\nhn_diagram.py" spec.yaml out.drawio   # 명세 -> 그림
python "$SKILL\drawio_edit.py" out.drawio list        # 도형 목록
python "$SKILL\drawio_open.py" out.drawio             # 브라우저로 열기
```

명세 형식은 `examples/3tier.yaml` 과 `SKILL.md` 의 "명세 형식" 을 보세요.

## 구성

| 파일 | 내용 |
| --- | --- |
| `SKILL.md` | 스킬 본체. Claude 가 따르는 절차 |
| `nhn_diagram.py` | 팔레트 조회 + 명세 → `.drawio` 생성 |
| `drawio_edit.py` | 기존 `.drawio` 제자리 수정 (손편집 보존) |
| `drawio_open.py` | 브라우저 draw.io 로 열기 |
| `examples/3tier.yaml` | 3-Tier 구성 예시 명세 |

아이콘 원본과 팔레트는 <https://github.com/nhn-cloud/Icons> 에서 관리합니다.
