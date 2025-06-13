# 오리엔테이션

<div class="video-wrapper">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/G3CV-FcV-rc?si=nyLvwhrSB2m1NPc5&amp;list=PLPZ8WHdZGxmXiHf8B26oB_fTfoKQdhlik" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

/// caption
:fontawesome-brands-youtube:{ .youtube } [Nextflow YouTube 채널](https://www.youtube.com/playlist?list=PLPZ8WHdZGxmXiHf8B26oB_fTfoKQdhlik)에서 전체 재생목록을 확인할 수 있습니다.

:green_book: 영상 자막은 [여기](./transcripts/00_orientation.md)에서 확인할 수 있습니다.
///

!!! tip

    YouTube 동영상에는 몇 가지 유용한 기능이 있습니다!

    - :fontawesome-solid-closed-captioning: 고품질(수동으로 관리된) 자막이 제공됩니다. :material-subtitles: 아이콘을 클릭해 자막을 켤 수 있습니다.
    - :material-bookmark: 동영상 타임라인에 페이지 제목과 일치하는 챕터가 표시됩니다.

## GitHub Codespaces

GitHub Codespaces 환경에는 이 교육 과정을 진행하는 데 필요한 모든 소프트웨어, 코드, 데이터가 포함되어 있으므로 별도의 설치가 필요하지 않습니다.
단, 로그인하려면 (무료) GitHub 계정이 필요하며, 인터페이스에 익숙해지는 데 몇 분 정도 시간을 투자하는 것이 좋습니다.

아직 환경 설정을 완료하지 않았다면, 계속 진행하기 전에 [환경 설정](../../envsetup/) 미니 코스를 먼저 완료해 주세요.

## 작업 디렉토리

이 교육 과정 전반에 걸쳐 `hello-nextflow/` 디렉토리에서 작업하게 됩니다.

터미널에서 다음 명령어를 실행하여 지금 디렉토리를 변경하세요:

```bash
cd hello-nextflow/
```

!!!tip

    혹시 디렉터리에서 벗어나게 되더라도, GitHub Codespaces 교육 환경 내에서 작업 중이라면 전체 경로를 입력하여 언제든지 다시 이 디렉터리로 돌아올 수 있습니다.

    ```bash
    cd /workspaces/training/hello-nextflow
    ```

이제 이 디렉토리의 내용을 살펴보겠습니다.

## 제공된 자료

교육 작업공간 왼쪽에 있는 파일 탐색기를 사용하여 이 디렉토리의 내용을 탐색할 수 있습니다.
또는 `tree` 명령어를 사용할 수 있습니다.

이 교육 과정에서는 디렉터리 구조와 파일 내용을 보다 쉽게 전달하기 위해 `tree` 명령어의 출력 결과를 사용하며, 때때로 설명을 명확히 하기 위해 일부 내용을 간단히 수정할 수 있습니다.

여기서는 두 번째 수준까지의 목차를 생성합니다:

```bash
tree . -L 2
```

이 명령어를 `hello-nextflow` 내에서 실행하면 다음과 같은 출력을 볼 수 있습니다:

```console title="디렉터리의 구성 항목"
.
├── greetings.csv
├── hello-channels.nf
├── hello-config.nf
├── hello-containers.nf
├── hello-modules.nf
├── hello-workflow.nf
├── hello-world.nf
├── nextflow.config
├── solutions
│   ├── 1-hello-world
│   ├── 2-hello-channels
│   ├── 3-hello-workflow
│   ├── 4-hello-modules
│   ├── 5-hello-containers
│   └── 6-hello-config
└── test-params.json

7 directories, 9 files
```

**시작 전 꼭 알아야 할 핵심 요약:**

- **`.nf` 파일**은 과정의 각 단계에서 사용하는 워크플로우 스크립트이며, 해당 단계에 맞춰 이름이 지정되어 있습니다.

- **`nextflow.config` 파일**은 최소한의 환경 설정을 정의하는 구성 파일입니다. 지금은 신경 쓰지 않으셔도 됩니다.

- **`greetings.csv` 파일**은 과정 대부분에서 사용할 입력 데이터를 포함하고 있습니다. 이는 첫 번째로 소개되는 1부에서 설명됩니다.

- **`test-params.json` 파일**은 6부에서 사용할 파일입니다. 지금은 신경 쓰지 않으셔도 됩니다.

- **`solutions` 디렉토리**는 각 단계에서 완성된 워크플로우 스크립트가 들어 있습니다.
  이는 작업 결과를 확인하거나 문제를 해결할 때 참고용으로 활용할 수 있습니다.
  파일 이름과 번호는 해당하는 과정의 단계와 연결되어 있습니다.
  예를 들어, `hello-world-4.nf` 파일은 1부: Hello World의 1단계부터 4단계까지 완료했을 때의 예상 결과입니다.

**이제, 과정을 시작하려면 이 페이지 오른쪽 하단의 화살표를 클릭하세요.**
