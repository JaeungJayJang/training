---
title: Hello Nextflow
hide:
  - toc
---

# Hello Nextflow

안녕하세요! 이제 Nextflow를 사용하여 재현 가능하고 확장 가능한 과학 워크플로우를 작성하는 여정에 들어섰습니다.

빅데이터의 부상으로 인해, 대용량 데이터를 다양한 환경에서 쉽게 실행하고 결과를 재현할 수 있는 방식으로 분석하고 실험하는 것이 점점 더 중요해지고 있습니다. 병렬화와 분산 컴퓨팅은 이러한 과제를 해결하는 가장 효과적인 방법이지만, 계산 과학자들이 일반적으로 사용하는 도구들은 이러한 기술을 충분히 지원하지 않거나, 계산 과학자의 실제 요구에 잘 부합하지 않는 경우가 많습니다. Nextflow는 이러한 문제를 해결하기 위해 특별히 만들어졌습니다.

이번 교육은 Nextflow의 개념과 사용법을 익힐 수 있도록 구성된 실습 중심 워크숍 시리즈로 이루어져 있습니다.
시작해볼까요? 아래의 "Open in GitHub Codespaces" 버튼을 클릭하여(별도의 탭에서 여는 것을 권장) 교육 환경을 실행한 후, 로딩되는 동안 이 페이지를 계속 읽어주세요.

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/nextflow-io/training?quickstart=1&ref=master)

<h2>
  <div style="float:right;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/videoseries?si=9bz6-59u_0XFmHB0&amp;list=PLPZ8WHdZGxmXiHf8B26oB_fTfoKQdhlik" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
  </div>

동영상 따라하기

</h2>

Hello Nextflow 교육은 각 장마다 상단에 동영상이 포함되어 있습니다.

[Nextflow YouTube 채널의 전체 재생목록](https://www.youtube.com/playlist?list=PLPZ8WHdZGxmXiHf8B26oB_fTfoKQdhlik)에서도 확인하실 수 있습니다.

<!-- Clearfix for float -->
<div style="content: ''; clear: both; display: table;"></div>

## 학습 목표

이 워크숍에서는 파이프라인 구축을 위한 기본 개념을 학습합니다.

이 워크숍을 마치면 다음과 같은 역량을 갖추게 됩니다:

- 간단한 다단계 워크플로우를 만들 수 있을 정도로 Nextflow의 핵심 구성요소를 이해하고 활용할 수 있습니다.
- 오퍼레이터(operators), 채널 팩토리(channel factories) 등 다음 단계 개념을 설명할 수 있습니다.
- Nextflow 워크플로우를 로컬에서 실행할 수 있습니다.
- Nextflow가 생성한 출력(결과) 및 로그 파일을 찾고 해석할 수 있습니다.
- 기본적인 문제를 해결할 수 있습니다.

## 대상자 및 요구되는 배경 지식

이 워크숍은 Nextflow를 처음 접하는 분들을 위한 것입니다.
명령어 줄(command line) 사용과 일반적인 파일 형식에 대한 기본적인 이해가 있다고 가정하고 진행됩니다.

**사전 준비 사항**

- GitHub 계정 또는 [여기](../envsetup/02_local)에서 설명한 로컬 설치
- 명령어 줄 사용 경험 및 간단한 스크립트 작성 경험
