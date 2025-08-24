# AssemblyAI CLI

![Release](https://img.shields.io/github/v/release/assemblyai/assemblyai-cli)
![Build](https://img.shields.io/github/actions/workflow/status/assemblyai/assemblyai-cli/release.yml)
![License](https://img.shields.io/github/license/assemblyai/assemblyai-cli)

AssemblyAI CLI는 터미널에서 바로 최신 AI 모델을 빠르게 테스트할 수 있도록 도와주는 도구입니다. 최소한의 설치만으로 사용할 수 있습니다.

![Thumbnail](./assets/thumbnail.png)

## 설치 방법

CLI는 설치가 간단하며, macOS, Windows, Linux 등 다양한 운영 체제를 지원합니다. AssemblyAI를 사용한 개발을 더욱 원활하게 만들어줍니다.

### Homebrew를 사용한 설치

macOS를 사용하는 경우 Homebrew를 통해 설치할 수 있습니다:

```bash
brew tap assemblyai/assemblyai
brew install assemblyai
```

### macOS 또는 Linux

Homebrew가 설치되어 있지 않거나 Linux를 사용하는 경우:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/AssemblyAI/assemblyai-cli/main/install.sh)"
```

### Windows

Windows에서는 Scoop 또는 스크립트를 통해 CLI를 사용할 수 있습니다.

Scoop을 통한 설치:

```powershell
scoop bucket add assemblyai https://github.com/assemblyai/scoop-assemblyai.git
scoop install assemblyai
```

또는 관리자 권한으로 PowerShell을 통한 설치:

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
irm https://raw.githubusercontent.com/AssemblyAI/assemblyai-cli/main/install.ps1 | iex
New-Alias -Name assemblyai -Value $Env:Programfiles/AssemblyAI/assemblyai.exe
```

## 시작하기

AssemblyAI 토큰으로 CLI를 구성하여 시작하세요. 아직 계정이 없다면 [여기](https://www.assemblyai.com/app)에서 생성할 수 있습니다.

```bash
assemblyai config [token]
```

이 명령은 계정을 검증하고 토큰을 `~/.config/assemblyai/config.toml`에 안전하게 저장하여 나중에 파일을 전사할 때 사용됩니다.

이제 로컬 파일과 원격 URL을 전사할 수 있습니다.

```bash
assemblyai transcribe ./file.mp3 --auto_highlights --entity_detection
```

## 사용법

CLI를 설치하면 `assemblyai` 명령에 액세스할 수 있습니다:

```bash
assemblyai [command] [--flags]
```

## 명령어

### Transcribe (전사)

CLI를 사용하여 로컬 파일과 원격 URL을 전사할 수 있습니다.

```bash
assemblyai transcribe [로컬 파일 | 원격 URL] [--flags]
```

<details>
  <summary>플래그 옵션</summary>
  
  > **-j, --json**  
  > 기본값: false  
  > 예시: `-j` 또는 `--json`  
  > true로 설정하면 CLI가 JSON을 출력합니다.

> **-p, --poll**  
> 기본값: true  
> 예시: `-p` 또는 `--poll`  
> CLI가 전사가 완료될 때까지 3초마다 폴링합니다.

> **-s, --auto_chapters**  
> 기본값: false  
> 예시: `-s` 또는 `--auto_chapters`  
> 전사된 오디오 파일에 대한 "시간별 요약"을 생성합니다.

> **-a, --auto_highlights**  
> 기본값: false  
> 예시: `-a` 또는 `--auto_highlights`  
> 텍스트에서 중요한 구문과 단어를 자동으로 감지합니다.

> **-c, --content_moderation**  
> 기본값: false  
> 예시: `-c` 또는 `--content_moderation`  
> 파일에서 민감한 내용이 포함되어 있는지 감지합니다.

> **-d, --dual_channel**  
> 기본값: false  
> 예시: `-d` 또는 `--dual_channel`  
> 듀얼 채널 활성화

> **-D, --disfluencies**  
> 기본값: false  
> 예시: `-D` 또는 `--disfluencies`  
> 전사에 채움말(Filler Words) 포함

> **-e, --entity_detection**  
> 기본값: false  
> 예시: `-e` 또는 `--entity_detection`  
> 오디오 파일에서 언급된 다양한 개체를 식별합니다.

> **-f, --format_text**  
> 기본값: true  
> 예시: `-f=false` 또는 `--format_text=false`  
> 텍스트 서식 활성화

> **-u, --punctuate**  
> 기본값: true  
> 예시: `-u=false` 또는 `--punctuate=false`  
> 자동 구두점 활성화

> **-r, --redact_pii**  
> 기본값: false  
> 예시: `-r` 또는 `--redact_pii`  
> 전사에서 개인 식별 정보를 제거합니다.

> **-i, --redact_pii_policies**  
> 기본값: drug,number_sequence,person_name  
> 예시: `-i medical_process,nationality` 또는 `--redact_pii_policies medical_process,nationality`  
> 편집할 PII 정책 목록 ([소스](https://www.assemblyai.com/docs/Models/pii_redaction)), 쉼표로 구분. redact_pii 플래그가 true인 경우 필수입니다.

> **-x, --sentiment_analysis**  
> 기본값: false  
> 예시: `-x` 또는 `--sentiment_analysis`  
> 파일에서 각 문장의 감정을 감지합니다.

> **-l, --speaker_labels**  
> 기본값: true  
> 예시: `-l=false` 또는 `--speaker_labels=false`  
> 파일에서 화자 수를 자동으로 감지합니다.

> **-t, --topic_detection**  
> 기본값: false  
> 예시: `-t` 또는 `--topic_detection`  
> 파일에서 언급된 주제에 레이블을 지정합니다.

> **-w, --webhook_url**  
> 예시: `--webhook_url "https://example.com/"`  
> 전사가 완료되면 웹훅을 받습니다.

> **-b, --webhook_auth_header_name**  
> 예시: `--webhook_auth_header_name "Authorization"`  
> 웹훅 요청에 삽입될 헤더 이름을 포함합니다.

> **-o, --webhook_auth_header_value**  
> 예시: `--webhook_auth_header_value "foo:bar"`  
> 웹훅 요청에 포함될 헤더 값입니다.

> **-n, --language_detection**  
> 기본값: false  
> 예시: `-n` 또는 `--language_detection`  
> 오디오 파일에서 주로 사용되는 언어를 자동으로 식별합니다.
> [여기](https://www.assemblyai.com/docs/Models/speech_recognition#automatic-language-detection)에서 지원되는 언어에 대한 ALD 목록을 볼 수 있습니다.

> **-g, --language_code**  
> 예시: `-g es` 또는 `--language_code es`  
> 오디오 파일의 음성 언어를 수동으로 지정합니다.
> [여기](https://www.assemblyai.com/docs/Concepts/faq#supported-languages)를 클릭하여 지원되는 모든 언어를 확인하세요.

> **-m, --summarization**  
> 기본값: false  
> 예시: `-m` 또는 `--summarization`  
> 전체 오디오의 단일 추상적 요약을 생성합니다.

> **-q, --summary_model**
> 기본값: bullets  
> 예시: `-q conversational` 또는 `--summary_model conversational`  
> 생성되는 요약의 유형입니다.
> [여기](https://www.assemblyai.com/docs/Models/summarization)를 클릭하여 지원되는 모든 유형을 확인하세요.

> **-y, --summary_type**
> 기본값: bullets  
> 예시: `-y paragraph` 또는 `--summary_type paragraph`  
> 생성되는 요약의 모델입니다.
> [여기](https://www.assemblyai.com/docs/Models/summarization)를 클릭하여 지원되는 모든 유형을 확인하세요.

> **-k, --word_boost**
> 예시: `-k "sally mcmanus,the IQEZ iPhone app"` 또는 `--word_boost "sally mcmanus,the IQEZ iPhone app"`  
> 포함된 모든 용어의 전사 가능성이 높아집니다.

> **-z, --boost_param**
> 예시: `-z high` 또는 `--boost_param high`  
> 부스트된 키워드/구문에 적용할 가중치를 제어합니다. 이 값은 low, default 또는 high가 될 수 있습니다.

> **--custom_spelling**
> 예시: `--custom_spelling "[{\"from\": [\"ariana\"], \"to\": \"Arianna\"}]"` 또는 `--custom_spelling ./custom_spelling.json`
> 전사 텍스트에서 단어의 철자나 형식을 지정합니다.

> **--srt**  
> 기본값: false  
> 예시: `--srt`  
> 현재 디렉토리에 `[id].srt` 파일을 생성합니다.

</details>

### Get (가져오기)

전사를 폴링하지 않는 경우 나중에 가져올 수 있습니다:

```bash
assemblyai get [id]
```

<details>
  <summary>플래그 옵션</summary>
  
  > **-j, --json**  
  > 기본값: false  
  > 예시: `--json` 또는 `--json=true`  
  > true로 설정하면 CLI가 JSON을 출력합니다.

> **-p, --poll**  
> 기본값: true  
> 예시: `--poll=false`  
> CLI가 전사가 완료될 때까지 3초마다 폴링합니다.

> **--srt**  
> 기본값: false  
> 예시: `--srt`  
> 현재 디렉토리에 `[id].srt` 파일을 생성합니다.

</details>

### 출력을 파일로 내보내기

[셸 리디렉션](https://www.gnu.org/software/bash/manual/html_node/Redirections.html)을 사용하여 AssemblyAI CLI 명령의 출력을 파일로 내보낼 수 있습니다. 출력을 텍스트 파일로 내보내려면 `>` 연산자와 생성하려는 파일 이름을 사용합니다.

```bash
assemblyai get [id] > transcript.txt
```

API의 원시 JSON 응답을 저장하려면 다음과 같이 할 수 있습니다:

```bash
assemblyai get [id] -j > transcript.json
```

내보내는 파일이 이미 존재하는 경우 해당 내용이 덮어쓰여집니다. 기존 파일에 출력을 추가하려면 `>` 대신 `>>` 연산자를 사용하세요.

## 기여하기

새로운 기여자를 환영합니다. 수정하거나 개선하고 싶은 것이 있다면 먼저 [이슈를 생성](https://github.com/AssemblyAI/assemblyai-cli/issues)해 주세요. [행동 강령](https://github.com/AssemblyAI/assemblyai-cli/blob/main/CODE_OF_CONDUCT.md)을 준수해 주시기 바랍니다.

## 원격 측정

AssemblyAI CLI에는 사용 데이터를 수집하는 원격 측정 기능이 포함되어 있으며 기본적으로 활성화되어 있습니다.

원격 측정을 비활성화하려면 `config.toml` 파일의 telemetry 변수를 false로 설정하세요.

## 업그레이드

저희 팀은 세계적인 수준의 서비스를 보장하기 위해 정기적으로 업데이트를 릴리스하므로 새 릴리스가 있을 때 CLI를 업데이트하세요. [설치](#설치-방법) 섹션에 표시된 것과 동일한 명령을 실행하거나 brew를 사용하여 설치한 경우 다음을 실행합니다:

```bash
brew upgrade assemblyai
```

## 피드백

[의견을 알려주세요](https://forms.gle/oQgktMWyL7xStH2J8)!

## 제거

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/AssemblyAI/assemblyai-cli/main/uninstall.sh)"
```

CLI를 제거하는 이유와 개선할 수 있는 부분을 알고 싶습니다. [연락 주세요](https://forms.gle/oQgktMWyL7xStH2J8).

## 라이선스

Copyright (c) AssemblyAI. All rights reserved.

[Apache License 2.0 라이선스](https://github.com/AssemblyAI/assemblyai-cli/blob/main/LICENSE)에 따라 라이선스가 부여됩니다.