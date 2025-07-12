# 1부: Hello World

<div class="video-wrapper">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/8X2hHI-9vms?si=F0t9LFYLjAWoyRXj&amp;list=PLPZ8WHdZGxmXiHf8B26oB_fTfoKQdhlik" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

/// caption
:fontawesome-brands-youtube:{ .youtube } [Nextflow YouTube 채널](https://www.youtube.com/playlist?list=PLPZ8WHdZGxmXiHf8B26oB_fTfoKQdhlik)에서 전체 재생목록을 확인할 수 있습니다.

:green_book: 영상 자막은 [여기](./transcripts/01_hello_world.md)에서 확인할 수 있습니다.
///

Hello Nextflow 교육 과정의 첫 번째 파트에서는, 분야에 구애받지 않는 아주 기본적인 Hello World 예제를 통해 주제를 가볍게 시작합니다. 이 예제를 점차 확장해 나가며 Nextflow의 기본적인 로직과 구성 요소들의 사용법을 소개할 예정입니다.

!!! note

    "Hello World!"는 프로그래밍 언어나 소프트웨어 프레임워크의 기본 문법과 구조를 보여주기 위한 최소한의 예제입니다. 보통 'Hello, World!'라는 문구를 콘솔이나 터미널에 출력하거나 파일에 기록하는 방식으로 동작합니다.

---

## 0. 준비단계 Hello World 직접 실행하기

Nextflow로 감싸기 전에, 터미널에서 직접 간단한 명령어를 실행해 동작을 확인해봅니다.

!!! tip

    오리엔테이션에서 안내한 대로, 현재 `hello-nextflow/` 디렉터리 안에 있어야 합니다.

### 0.1. 터미널이 인사하도록 만들어 보기

```bash
echo 'Hello World!'
```

이 명령어는 'Hello World'라는 텍스트를 터미널에 출력합니다.

```console title="Output"
Hello World!
```

### 0.2. 이번에는 텍스트를 파일로 저장하기

```bash
echo 'Hello World!' > output.txt
```

이 명령어는 터미널에는 아무런 출력을 하지 않습니다.

```console title="Output"

```

### 0.3. 파일 내용 확인하기

```bash
cat output.txt
```

지정한 출력 파일에 'Hello World'라는 텍스트가 저장되었습니다.

```console title="output.txt" linenums="1"
Hello World!
```

!!! tip

    교육 환경에서는 파일 탐색기에서 출력 파일을 찾아보고, 클릭하여 내용을 확인할 수 있습니다. 또는 `code` 명령어를 사용하여 파일을 열어볼 수도 있습니다.

    ```bash
    code output.txt
    ```

### 요약

이제 텍스트를 출력하는 간단한 명령어를 터미널에서 실행하는 방법과, 선택적으로 그 출력을 파일에 저장하는 방법을 알게 되었습니다.

### 다음 단계는?

Nextflow 워크플로우로 작성했을 때의 모습을 알아봅시다.

---

## 1. Hello World 워크플로우 시작 스크립트 살펴보기

오리엔테이션에서 언급했듯이, 저희는 여러분에게 `hello-world.nf`라는 최소한의 구조를 갖춘 완전한 기능의 워크플로우 스크립트를 제공합니다. 이 스크립트는 앞에서 했던 것처럼 'Hello World!'를 출력하지만, 이번에는 Nextflow를 사용합니다.

시작하기에 앞서, 워크플로우 스크립트를 먼저 열어보면서 그 구조가 어떻게 되어 있는지 살펴보겠습니다.

### 1.1. 전체 코드 구조 살펴보기

편집기 창에서 `hello-world.nf` 스크립트를 열어봅시다.

!!! note

    파일은 `hello-nextflow` 디렉터리에 있으며, 현재 작업 디렉터리여야 합니다.
    파일 탐색기에서 파일을 클릭하거나, 터미널에서 `ls`를 입력한 후 파일을 Cmd+Click (MacOS) 또는 Ctrl+Click (PC)하여 열 수 있습니다.

```groovy title="hello-world.nf" linenums="1"
#!/usr/bin/env nextflow

/*
 * Use echo to print 'Hello World!' to a file
 */
process sayHello {

    output:
        path 'output.txt'

    script:
    """
    echo 'Hello World!' > output.txt
    """
}

workflow {

    // emit a greeting
    sayHello()
}
```

보시다시피, Nextflow 스크립트는 주로 두 가지 유형의 핵심 구성 요소로 이루어져 있습니다: 하나 이상의 **프로세스**와 **워크플로우** 자체입니다.
각 **프로세스**는 파이프라인의 해당 단계에서 수행해야 할 작업을 설명하고, **워크플로우**는 다양한 단계를 연결하는 데이터 흐름 논리를 설명합니다.

먼저 **프로세스** 블록을 자세히 살펴보고, 그 다음에 **워크플로우** 블록을 살펴보겠습니다.

### 1.2. `process(프로세스)` 정의

첫 번째 코드 블록은 **프로세스**를 설명합니다.
프로세스 정의는 `process` 키워드로 시작하여, 프로세스 이름이 뒤따르고, 마지막으로 중괄호로 구분된 프로세스 본체가 옵니다.
프로세스 본체에는 실행할 명령을 지정하는 스크립트 블록이 포함되어야 하며, 이는 커맨드 라인 터미널에서 실행할 수 있는 모든 것이 될 수 있습니다.

여기에는 `output.txt`라는 파일에 출력을 기록하는 **프로세스** `sayHello`가 있습니다.

```groovy title="hello-world.nf" linenums="3"
/*
 * Use echo to print 'Hello World!' to a file
 */
process sayHello {

    output:
        path 'output.txt'

    script:
    """
    echo 'Hello World!' > output.txt
    """
}
```

이것은 `output` 정의와 실행할 `script`만 포함된 매우 간단한 프로세스 정의입니다.

`output` 정의에는 `path` 한정자가 포함되어 있어, Nextflow에 이 출력이 경로(디렉터리 경로 및 파일 모두 포함)로 처리되어야 함을 알립니다.
또 다른 일반적인 한정자는 `val`입니다.

!!! note

    출력(output) 정의는 생성될 출력을 _결정_ 하지 않습니다.
    단지 어떤 출력이 나올 것으로 예상되는지를 _선언하는_ 역할을 하며, 실행이 완료된 후 Nextflow가 해당 출력을 찾아낼 수 있도록 도와줍니다.
    이는 명령이 성공적으로 실행되었는지 확인하고, 필요할 경우 출력 결과를 다음 단계의 프로세스로 전달하기 위해 필요합니다. 출력 블록에 선언된 것과 일치하지 않는 방식으로 생성된 출력은 다음 단계의 프로세스로 전달되지 않습니다.

!!! warning

    이 예제는 출력 파일 이름을 두 개의 별도 위치(스크립트와 출력 블록)에 하드코딩했기 때문에 다소 불안정 합니다.
    만약 한쪽만 수정하고 다른 쪽을 수정하지 않으면 스크립트가 작동하지 않게 됩니다.
    이후에 이러한 문제를 피하기 위해 변수를 사용하는 방법을 배우게 될 것입니다.

실제 파이프라인에서는 프로세스에 추가 블록(지시문 및 입력 등)이 포함되는 경우가 많으며, 이는 곧 소개할 것입니다.

### 1.3. `workflow(워크플로우)` 정의

두 번째 코드 블록은 **워크플로우** 자체를 설명합니다.
워크플로우 정의는 `workflow` 키워드로 시작하여 선택적 이름이 뒤따르고, 마지막으로 중괄호로 구분된 워크플로우 본체가 옵니다.

여기에는 `sayHello` 프로세스에 대한 호출이 하나만 있는 **워크플로우**가 있습니다.

```groovy title="hello-world.nf" linenums="17"
workflow {

    // emit a greeting
    sayHello()
}
```

이는 매우 최소한의 **워크플로우** 정의입니다.
실제 파이프라인에서는 워크플로우에 일반적으로 여러 **프로세스**에 대한 호출이 포함되며, 이들은 **채널(channels)**에 의해 연결되고 프로세스는 하나 이상의 가변 **입력(inputs)**을 기대합니다.

가변 입력을 추가하는 방법은 나중에 이 교육 모듈에서 배우게 될 것이며, 더 많은 프로세스를 추가하고 채널로 연결하는 방법은 이 과정의 3부에서 배우게 될 것입니다.

### 요약

이제 간단한 Nextflow 워크플로우가 어떻게 구성되어 있는지 알게 되었습니다.

### 다음 단계는?

워크플로우를 실행하고, 실행 모니터링 및 출력 결과를 찾는 방법을 배워봅시다.

---

## 2. 워크플로우 실행하기

코드를 보는 것만으로는 충분히 재미있지 않으니, 이를 실제로 시도해봅시다.

### 2.1. 워크플로우 실행 및 모니터링

터미널에서 다음 명령어를 실행합니다:

```bash
nextflow run hello-world.nf
```

콘솔 출력은 다음과 비슷하게 나타날 것입니다:

```console title="Output" linenums="1"
 N E X T F L O W   ~  version 25.04.3

Launching `hello-world.nf` [goofy_torvalds] DSL2 - revision: c33d41f479

executor >  local (1)
[a3/7be2fa] sayHello | 1 of 1 ✔
```

축하합니다. 첫 번째 Nextflow 워크플로우를 실행했습니다!

여기서 가장 중요한 출력은 마지막 줄(6행)입니다:

```console title="Output" linenums="6"
[a3/7be2fa] sayHello | 1 of 1 ✔
```

이는 `sayHello` 프로세스가 한 번(`1 of 1 ✔`) 성공적으로 실행되었음을 나타냅니다.

중요하게도, 이 줄은 또한 `sayHello` 프로세스 호출의 출력을 찾을 위치를 알려줍니다. 이제 그것을 살펴보겠습니다.

### 2.2. `work` 디렉터리에서 출력 및 로그 찾기

주어진 디렉터리에서 Nextflow를 처음 실행하면, 실행 과정에서 생성된 모든 파일(및 심볼릭 링크)을 기록할 `work`라는 디렉터리가 생성됩니다.

`work` 디렉터리 내에서, Nextflow는 프로세스 호출별로 출력 및 로그를 구성합니다.
각 프로세스가 실행될 때마다, Nextflow는 고유한 해시값을 이름으로 갖는 중첩된 하위 디렉토리를 생성합니다.
이 디렉토리에는 필요한 입력 파일들이 (기본적으로 심볼릭 링크를 사용하여) 준비되고, 보조 파일과 로그, 그리고 프로세스의 출력 결과가 저장됩니다.

이 하위 디렉토리의 경로는 콘솔 출력에서 대괄호로 감싸인 축약된 형태로 보여집니다.
위에서 보여준 실행 로그를 보면, `sayHello` 프로세스의 콘솔 로그 줄은 `[a3/7be2fa]`로 시작합니다. 이는 다음과 같은 디렉터리 경로에 해당합니다: `work/a3/7be2fad5e71e5f49998f795677fd68`

그 안에 무엇이 있는지 살펴보겠습니다.

!!! tip

    VSCode 파일 탐색기에서 작업 하위 디렉터리의 내용을 찾아보면 모든 파일을 즉시 볼 수 있습니다.
    그러나 터미널에서는 로그 파일이 보이지 않도록 설정되어 있으므로, 이를 보려면 관련 옵션을 설정해야 합니다.

    ```bash
    tree -a work
    ```

아래와 비슷한 형태가 출력될 것입니다. 다만, 실제 하위 디렉토리 이름은 사용자의 시스템에 따라 달라질 수 있습니다.

```console title="Directory contents"
work
└── a3
    └── 7be2fad5e71e5f49998f795677fd68
        ├── .command.begin
        ├── .command.err
        ├── .command.log
        ├── .command.out
        ├── .command.run
        ├── .command.sh
        ├── .exitcode
        └── output.txt
```

이들은 도우미 및 로그 파일입니다:

- **`.command.begin`**: 프로세스 호출의 실행 시작과 관련된 메타데이터
- **`.command.err`**: 프로세스 호출에 의해 생성된 오류 메시지(`stderr`)
- **`.command.log`**: 프로세스 호출에 의해 생성된 전체 로그 출력
- **`.command.out`**: 프로세스 호출에 의해 생성된 일반 출력(`stdout`)
- **`.command.run`**: 프로세스 호출을 실행하기 위해 Nextflow에 의해 실행된 전체 스크립트
- **`.command.sh`**: 프로세스 호출에 의해 실제로 실행된 명령
- **`.exitcode`**: 명령에서 생성된 종료 코드

특히 `.command.sh` 파일이 유용한데, 이는 Nextflow가 실제로 어떤 명령을 실행했는지를 알려줍니다.
이번 예제에서는 매우 단순하지만, 이후 과정에서는 변수 보간(interpolation)이 포함된 명령어들도 다루게 될 것입니다.
그럴 때는 특히 문제가 발생했을 때 어떤 명령이 실행되었는지 정확히 확인할 수 있어야 합니다.

`sayHello` 프로세스의 출력 결과는 `output.txt` 파일입니다.
이 파일을 열어보면, 최소한의 워크플로우에서 기대했던 결과인 Hello World! 인사말이 들어 있는 것을 확인할 수 있습니다.

```console title="output.txt" linenums="1"
Hello World!
```

### 요약

간단한 Nextflow 스크립트를 해독하고, 실행하며, 출력 및 관련 로그 파일을 작업 디렉터리에서 찾는 방법을 알게 되었습니다.

### 다음 단계는?

워크플로우 실행을 편리하게 관리하는 방법을 배워봅시다.

---

## 3. 워크플로우 실행 관리하기

워크플로우를 실행하고 출력 결과를 확인하는 것도 중요하지만, 특히 직접 워크플로우를 개발하는 경우에는 워크플로우 관리를 더 쉽게 만들어주는 몇 가지 핵심 요소들을 곧 접하게 될 것입니다.

이 섹션에서는 파이프라인의 주요 결과를 출력 폴더에 저장하는 `publishDir` 지시어의 사용법, 동일한 워크플로우를 다시 실행할 때 활용할 수 있는 `resume` 기능, 그리고 더 이상 필요 없는 작업 디렉터리를 정리하는 `nextflow clean` 명령어에 대해 알아봅니다.

### 3.1. 출력 결과 폴더에 저장하기

앞서 배운 것처럼, 파이프라인의 출력 파일은 여러 단계의 하위 작업 디렉터리 안에 저장됩니다. 이는 Nextflow가 해당 디렉터리를 완전히 제어하기 위한 설계이며, 사용자가 직접 그 내부를 다루는 것은 권장되지 않습니다.

그러나 이로 인해 우리가 필요한 출력 결과를 확인하거나 추출하는 과정이 다소 번거로울 수 있습니다.

다행히도 Nextflow는 이 문제를 더 편리하게 관리할 수 있는 방법을 제공합니다. 바로 프로세스 단위에서 동작하는 publishDir 지시어입니다.이 지시어는 Nextflow에게 해당 프로세스의 출력 결과를 지정된 출력 디렉터리에 저장하라고 지시합니다. 기본적으로 출력 파일은 `work` 디렉터리로부터 심볼릭 링크 형태로 출력 디렉터리에 연결됩니다.
이 기능을 사용하면 work 디렉터리의 복잡한 구조를 탐색하지 않고도 필요한 출력 파일에 쉽게 접근할 수 있습니다.

#### 3.1.1. `sayHello` 프로세스에 `publishDir` 지시문 추가하기

`hello-world.nf` 파일에 아래와 같이 코드를 추가합니다:

=== "변경 후"

    ```groovy title="hello-world.nf" linenums="6" hl_lines="3"
    process sayHello {

        publishDir 'results', mode: 'copy'

        output:
            path 'output.txt'
    ```

=== "변경 전"

    ```groovy title="hello-world.nf" linenums="6"
    process sayHello {

        output:
            path 'output.txt'
    ```

#### 3.1.2. 워크플로우 다시 실행하기

이제 수정한 워크플로우를 다시 실행해 봅니다:

```bash
nextflow run hello-world.nf
```

실행 로그는 이전과 비슷하게 나타납니다.

```console title="Output" linenums="1"
 N E X T F L O W   ~  version 25.04.3

Launching `hello-world.nf` [jovial_mayer] DSL2 - revision: 35bd3425e5

executor >  local (1)
[62/49a1f8] sayHello | 1 of 1 ✔
```

이번에는 Nextflow가 results/라는 새 디렉터리를 생성했습니다.
output.txt 파일은 이 디렉터리 안에 위치합니다.
이 파일의 내용을 확인해 보면 work 하위 디렉터리에 있는 출력 결과와 일치함을 알 수 있습니다.
이와 같은 방식으로 작업 디렉터리 외부에 결과 파일을 편리하게 게시할 수 있습니다.

보관 기간이 짧은 대용량 파일을 처리할 때는, `publishDir` 지시어를 사용하여 파일을 복사하는 대신 심볼릭 링크를 생성하도록 설정하는 것이 더 효율적일 수 있습니다.
그러나 정리 작업의 일환으로 work 디렉터리를 삭제하면 해당 파일에 접근할 수 없게 되므로, 중요한 파일은 삭제 전에 반드시 실제 복사본을 확보해 두시기 바랍니다.

!!! note

    [Nextflow 공식 문서](https://www.nextflow.io/docs/latest/workflow.html#publishing-outputs)에서는 워크플로우 전체 출력에 대한 새로운 선언 방식도 소개하고 있습니다.
    이 기능이 도입되면, 완료된 파이프라인에서는 프로세스 수준에서 `publishDir`를 사용하는 것이 점차 불필요해질 것으로 예상됩니다.
    다만, 파이프라인 개발 과정에서는 여전히 publishDir 지시어가 매우 유용하게 사용될 것으로 보입니다.

### 3.2. `-resume` 옵션으로 워크플로우 다시 실행하기

 워크플로우를 다시 실행할 때, 이미 성공적으로 완료된 단계는 다시 실행하지 않고 건너뛰고 싶을 때가 있습니다.

 Nextflow의 `-resume` 옵션을 사용하면, 이전 실행에서 동일한 코드, 설정, 입력값으로 이미 완료된 프로세스는 자동으로 건너뜁니다.
 즉, 마지막 실행 이후에 새로 추가하거나 수정한 프로세스, 혹은 입력값이 변경된 부분만 다시 실행됩니다.

 이 기능의 주요 장점은 다음과 같습니다:

 - 파이프라인을 개발 중일 때, 수정한 부분만 빠르게 테스트할 수 있습니다.
 - 운영 환경에서 오류가 발생해도, 문제를 수정한 뒤 중단된 지점부터 이어서 실행할 수 있어 시간과 자원을 절약할 수 있습니다.

 사용법은 매우 간단합니다. 명령어에 `-resume` 옵션을 추가하세요:

 ```bash
 nextflow run hello-world.nf -resume
 ```

실행 결과는 아래와 비슷하게 나타납니다.

```console title="Output" linenums="1"
 N E X T F L O W   ~  version 25.04.3

Launching `hello-world.nf` [golden_cantor] DSL2 - revision: 35bd3425e5

[62/49a1f8] sayHello | 1 of 1, cached: 1 ✔
```

프로세스 상태 줄에(5번째 줄) `cached:`가 추가된 것을 확인할 수 있습니다. 이는 Nextflow가 이미 해당 작업을 완료했음을 인식하고, 이전 실행 결과를 그대로 재사용했다는 의미입니다.

또한 work 하위 디렉터리의 해시값도 이전 실행과 동일하게 유지됩니다. Nextflow가 "이 작업은 이미 저기서 했으니 다시 할 필요 없어!"라고 알려주는 셈입니다.

!!! note

    `-resume` 옵션으로 파이프라인을 재실행할 때, 이미 성공적으로 실행된 프로세스가 `publishDir`에 기록한 파일은 덮어쓰지 않습니다.

### 3.3. 오래된 work 디렉터리 정리하기

파이프라인을 여러 번 실행하다 보면 work 하위에 많은 디렉터리가 쌓이게 됩니다. 디렉터리 이름이 무작위 해시값이기 때문에, 어떤 것이 오래된 실행 결과인지 구분하기 어렵습니다.

Nextflow의 `clean` 서브커맨드를 사용하면, 더 이상 필요 없는 이전 실행 결과를 손쉽게 삭제할 수 있습니다. [공식 문서](https://www.nextflow.io/docs/latest/reference/cli.html#clean)에서 다양한 옵션을 확인할 수 있습니다.

아래는 특정 실행(run name) 이전의 모든 work 디렉터리를 삭제하는 예시입니다. run name은 실행 로그의 `Launching (...)` 줄에 대괄호로 표시된 두 단어 조합입니다.

먼저, `-n` 옵션으로 실제 삭제 전 어떤 디렉터리가 삭제될지 미리 확인합니다:

```bash
nextflow clean -before golden_cantor -n
```

예상되는 출력 예시:

```console title="Output"
Would remove /workspaces/training/hello-nextflow/work/a3/7be2fad5e71e5f49998f795677fd68
```

만약 아무런 출력이 없다면, 올바른 run name을 입력하지 않았거나 삭제할 대상이 없는 경우입니다.

출력 결과가 예상대로라면, 실제 삭제를 진행할 때는 `-f` 옵션을 사용합니다:

```bash
nextflow clean -before golden_cantor -f
```

실제 삭제가 완료되면 아래와 같은 출력이 나타납니다:

```console title="Output"
Removed /workspaces/training/hello-nextflow/work/a3/7be2fad5e71e5f49998f795677fd68
```

!!! Warning

    과거 실행의 work 디렉터리를 삭제하면 Nextflow의 캐시가 사라지고, 해당 디렉터리에 저장된 출력 파일도 함께 삭제됩니다.
    즉, 이후 resume 기능을 사용할 수 없게 됩니다.

    중요한 출력 파일이나 앞으로 활용할 결과는 반드시 직접 저장해 두어야 합니다! 만약 publishDir 지시문을 사용하는 경우, 반드시 copy 모드를 사용하고 symlink 모드는 피하세요.

### 요약

이제 결과 파일을 지정한 폴더에 저장하는 방법, 이미 실행한 단계를 반복하지 않고 파이프라인을 재실행하는 방법, 그리고 `nextflow clean` 명령어로 오래된 work 디렉터리를 정리하는 방법을 알게 되었습니다.

### 다음 단계는?

명령줄 파라미터로 입력값을 전달하고, 기본값을 설정하는 방법을 배워봅시다.

---

## 4. Use a variable input passed on the command line

In its current state, our workflow uses a greeting hardcoded into the process command.
We want to add some flexibility by using an input variable, so that we can more easily change the greeting at runtime.

### 4.1. Modify the workflow to take and use a variable input

This requires us to make three changes to our script:

1. Tell the process to expect a variable input by adding an `input:` block
2. Edit the process to use the input
3. Set up a command-line parameter and provide its value as an input to the process call

Let's make these changes one at a time.

#### 4.1.1. Add an input block to the process definition

First we need to adapt the process definition to accept an input called `greeting`.

In the process block, make the following code change:

=== "After"

    ```groovy title="hello-world.nf" linenums="6" hl_lines="5 6"
    process sayHello {

        publishDir 'results', mode: 'copy'

        input:
            val greeting

        output:
            path 'output.txt'
    ```

=== "Before"

    ```groovy title="hello-world.nf" linenums="6"
    process sayHello {

        publishDir 'results', mode: 'copy'

        output:
            path 'output.txt'
    ```

The `greeting` variable is prefixed by `val` to tell Nextflow it's a value (not a path).

#### 4.1.2. Edit the process command to use the input variable

Now we swap the original hardcoded value for the value of the input variable we expect to receive.

In the process block, make the following code change:

=== "After"

    ```groovy title="hello-channels.nf" linenums="16" hl_lines="3"
    script:
    """
    echo '$greeting' > output.txt
    """
    ```

=== "Before"

    ```groovy title="hello-channels.nf" linenums="16"
    script:
    """
    echo 'Hello World!' > output.txt
    """
    ```

Make sure to prepend the `$` symbol to tell Nextflow this is a variable name that needs to be replaced with the actual value (=interpolated).

#### 4.1.3. Set up a CLI parameter and provide it as input to the process call

Now we need to actually set up a way to provide an input value to the `sayHello()` process call.

We could simply hardcode it directly by writing `sayHello('Hello World!')`.
However, when we're doing real work with our workflow, we're often going to want to be able to control its inputs from the command line.

Good news: Nextflow has a built-in workflow parameter system called `params`, which makes it easy to declare and use CLI parameters. The general syntax is to declare `params.<parameter_name>` to tell Nextflow to expect a `--<parameter_name>` parameter on the command line.

Here, we want to create a parameter called `--greeting`, so we need to declare `params.greeting` somewhere in the workflow.
In principle we can write it anywhere; but since we're going to want to give it to the `sayHello()` process call, we can plug it in there directly by writing `sayHello(params.greeting)`.

!!! note

    The parameter name (at the workflow level) does not have to match the input variable name (at the process level).
    We're just using the same word because that's what makes sense and keeps the code readable.

In the workflow block, make the following code change:

=== "After"

    ```groovy title="hello-world.nf" linenums="24" hl_lines="2"
    // emit a greeting
    sayHello(params.greeting)
    ```

=== "Before"

    ```groovy title="hello-world.nf" linenums="24"
    // emit a greeting
    sayHello()
    ```

This tells Nextflow to run the `sayHello` process on the value provided through the `--greeting` parameter.

#### 4.1.4. Run the workflow command again

Let's run it!

```bash
nextflow run hello-world.nf --greeting 'Bonjour le monde!'
```

If you made all three edits correctly, you should get another successful execution:

```console title="Output" linenums="1"
 N E X T F L O W   ~  version 25.04.3

Launching `hello-world.nf` [elated_lavoisier] DSL2 - revision: 7c031b42ea

executor >  local (1)
[4b/654319] sayHello | 1 of 1 ✔
```

Be sure to open up the output file to check that you now have the new version of the greeting.

```console title="results/output.txt" linenums="1"
Bonjour le monde!
```

Voilà!

!!! tip

    You can readily distinguish Nextflow-level parameters from pipeline-level parameters.

    - Parameters that apply to a pipeline always take a double hyphen (`--`).
    - Parameters that modify a Nextflow setting, _e.g._ the `-resume` feature we used earlier, take a single hyphen (`-`).

### 4.2. Use default values for command line parameters

In many cases, it makes sense to supply a default value for a given parameter so that you don't have to specify it for every run.

#### 4.2.1. Set a default value for the CLI parameter

Let's give the `greeting` parameter with a default value by declaring it before the workflow definition.

```groovy title="hello-world.nf" linenums="22"
/*
 * Pipeline parameters
 */
params.greeting = 'Holà mundo!'
```

!!! tip

    You can put the parameter declaration inside the workflow block if you prefer. Whatever you choose, try to group similar things in the same place so you don't end up with declarations all over the place.

#### 4.2.2. Run the workflow again without specifying the parameter

Now that you have a default value set, you can run the workflow again without having to specify a value in the command line.

```bash
nextflow run hello-world.nf
```

The console output should look the same.

```console title="Output" linenums="1"
 N E X T F L O W   ~  version 25.04.3

Launching `hello-world.nf` [determined_edison] DSL2 - revision: 3539118582

executor >  local (1)
[72/394147] sayHello | 1 of 1 ✔
```

Check the output in the results directory:

```console title="results/output.txt" linenums="1"
Holà mundo!
```

Nextflow used the default value of the greeting parameter to create the output.

#### 4.2.3. Run the workflow again with the parameter to override the default value

If you provide the parameter on the command line, the CLI value will override the default value.

Try it out:

```bash
nextflow run hello-world.nf --greeting 'Konnichiwa!'
```

The console output should look the same.

```console title="Output" linenums="1"
 N E X T F L O W   ~  version 25.04.3

Launching `hello-world.nf` [elegant_faraday] DSL2 - revision: 3539118582

executor >  local (1)
[6f/a12a91] sayHello | 1 of 1 ✔
```

Now you will have the corresponding new output in your results directory.

```console title="results/output.txt" linenums="1"
Konnichiwa!
```

!!! note

    In Nextflow, there are multiple places where you can specify values for parameters.
    If the same parameter is set to different values in multiple places, Nexflow will determine what value to use based on the order of precedence that is described [here](https://www.nextflow.io/docs/latest/config.html).

### Takeaway

You know how to use a simple variable input provided at runtime via a command-line parameter, as well as set up, use and override default values.

More generally, you know how to interpret a simple Nextflow workflow, manage its execution, and retrieve outputs.

### What's next?

Take a little break, you've earned it!
When you're ready, move on to Part 2 to learn how to use channels to feed inputs into your workflow, which will allow you to take advantage of Nextflow's built-in dataflow parallelism and other powerful features.
