---
layout: manual
language: ko
github: https://github.com/defold/doc
toc: ["3D graphics","Defold resources","Collada support","Materials and textures","Rendering"]
title: Defold manual
---

# 3D graphics
Defold는 3D 엔진의 기능을 사용하고 있습니다. 2D 메터리얼을 사용하더라도 모든 렌더링은 3D로 처리되지만 화면에는 직교(orthographic)로 투영되어 2D 처럼 보이게 됩니다. 이 매뉴얼은 어떻게 3D 모델, 스켈레톤, 애니메이션을 게임에 불러오는지 설명합니다.

Defold는 3D 에셋이나 모델을 컬렉션에 포함해서 3D 컨텐츠를 완전하게 활용하는 것이 가능합니다. 3D 에셋만을 사용해서 완전한 3D 게임을 만들 수도 있고 2D 컨텐츠와 섞어서 개발 할 수도 있습니다.

## Defold resources

#### Model
모델 컴포넌트는 오브젝트 메쉬(mesh), 스켈레톤(skeleton), 애니메이션(animation)을 포함합니다. 다른 모든 시각적 컴포넌트들 처럼 메터리얼(material)과 엮어서 사용할 수 있습니다.

#### Animation Set
애니메이션 세트 파일은 애니메이션을 읽기 위해 **.dae** 파일의 목록을 포함하고 있습니다. 또한 애니메이션 세트에 **.animationset** 파일을 추가 할 수도 있으며, 이는 여러 모델들 사이의 부분 에니메이션 세트를 공유하는 경우 편리합니다.

[Model](/ko/manuals/model) 문서는 3D 에셋을 임포트하고 모델을 만드는 방법에 대해 설명합니다.

[Animation](/ko/manuals/animation) 문서는 3D 모델을 에니메이션 처리 하는 방법에 대해 설명합니다.

## Collada support
Defold의 3D 지원을 위해서는 모델, 스켈레톤, 애니메이션 데이터를 Collada 라는 포멧으로 저장하고 익스포트 해야 합니다. 이 포멧은 대부분 3D 모델링 소프트웨어에서 광범위하게 지원되고 있는  포멧입니다. 그러므로 마야, 3D맥스, 블렌더, 스케치업 등의 유명한 소프트웨어로 에셋을 생성하고 Defold로 결과 파일을 불러올 수 있게 해야 합니다.

> Defold는 현재 현재 베이크 애니메이션(baked animations)만 지원합니다. 애니메이션은 키프레임마다 각각의 애니메이션 본(animated bone)을 위한 메트릭스를 가져야 하며 위치, 회전, 스케일은 별도의 키로 가지지 말아야 합니다.

> 또한 애니메이션은 선형적으로 보간(linearly interpolated)됩니다. 고급 곡선 보간(curve interpolation)을 하려면 애니메이션을 익스포터(exporter)에서 미리 구워(prebake)야 합니다.

> Collada의 애니메이션 클립(Animation clip)은 지원하지 않습니다. 모델별로 다수의 애니메이션을 사용하기 위해서는 각각 별도의 **.dae** 파일로 익스포트 하고 Defold의 **.animationset** 파일로 합쳐야 합니다.

## Materials and textures
일반적으로 3D 소프트웨어에서는 오브젝트가 얼마나 빛나거나 투명하게 할지 혹은 오브젝트가 털이 휘날리는지 카메라를 어디에 배치할지 카메라 렌즈를 어떻게 할지 등의 고급 메터리얼 속성을 설정할 수 있습니다. 이 모든 정보는 3D 소프트웨어에서 익스포트하는 Collada **.dae** 파일에 저장되며 오프라인으로 오브젝트를 렌더링하는 데 유용합니다. Defold 같은 실시간 게임 엔진에서는 이렇게 많은 정보는 필요하지 않으므로 Defold는 에셋 파일을 읽을 때 이 정보들을 무시합니다. 게임의 요구사항에 따라 적절하고 효과적인 메터리얼을 선택 혹은 생성 해야 하며, 의도된 게임플레이로 동작하게끔 게임 카메라를 디자인하고 구현해야 합니다.

당신의 Defold 프로젝트는 렌더 스프라이트, 타일, 파티클, GUI노드에 사용되는 몇 가지 내장 메터리얼(built-in material)을 가지고 있습니다. 3D 모델을 위한 적합한 내장 메터리얼은 없으므로 직접 제작해야 합니다. 하지만 책 모델을 위해서 미리 만들어 놓은 "textured.material" 예제가 있습니다.

메터리얼이 작동되는 방법과, 질감이 입혀진 3D 모델로 작업하는 방법에 대해 자세히 알고 싶다면  [Material](/ko/manuals/material) 문서를 참고 바랍니다.

## Rendering
모델을 게임에 적용하기 위한 마지막 작업은 프로젝트의 **Render Script**를 변경하는 것입니다. 기본 렌더 스크립트는 2D 게임을 위해 맞춰져 있으며 3D 모델에는 동작하지 않습니다. 하지만 기본 렌더 스크립트를 복사해서 Lua 코드 몇 줄을 추가해서 3D 모델이 렌더링 되게 할 수 있습니다. 샘플 프로젝트의 경우 이미 이 렌더 스크립트가 셋팅되어 있습니다.

렌더 스크립트가 동작하는 방법을 자세히 알고 싶다면 [Rendering](/manuals/rendering) 문서를 참고 바랍니다.
