# Material Design memo

## Introduction

この文書は以下ドキュメントの要約控えの下書きとなります。

- [Material design](https://www.google.com/design/spec/material-design/introduction.html)

また、当座は以下の項目について確認の方向です。

- What is material?
- Layout
- Components
- Patterns
- Usability

画像など、どうするかあまり考えていません。

## What is material?

### Environment

#### 3D world

material 環境は全ての物体が X, Y, Z 方向への広がりを持つ 3D 空間です。Z 軸は viewer 方向に正の Z 軸が展開する形でディスプレイ平面に整列されます。それぞれの material のシートは Z 軸に沿った一つの位置と標準的な 1dp の厚みを持ちます。

Web においては Z 軸はレイヤリングのために使われ、視点のために使われません。3D の世界は Y 軸の操作によってエミュレートされます。

#### Light and shadow

material 環境の中では、仮想のライトがシーンを照らします。周囲の光があらゆる角度からのソフトシャドウを作成する間、キーライトが、方向を示す影を作ります。

material 環境での影は、これら二つの光源により作られます。アプリ開発において、影は光 Z 軸に沿った光源が様々な位置の material のシートで遮断されたときに発生します。Web においては、影は、y軸を操作することのみによって描画されます。次に示す例は、6dpの高さのカードです。

- 光源による影
- 周囲の光による影
- 光源および周囲の光による影

### Material properties

Material には、固有の不変な特性や固有の振る舞いがあります。これらの特性を理解することは、material design のビジョンに沿った一貫性のある方法で material を操作するのに役立ちます。

#### Physical properties

##### Material は、様々な X および Y 寸法（単位は dp）と均一な厚さ（1dp）を持ちます。

- Do. 高さと幅は変更できる
- Don't. Material は常に 1dp の厚さ

##### Material は影を作ります。

影は、material の要素間の相対的な高さ（Z 位置）から自然に生じます。

- Do. 影は、material の要素間の相対的な高さを示しています。
- Don't. 影は、色によって影響されることはありません。

##### コンテンツは独立して、material として振る舞うことができますが、それは material の境界内に限定されます。

- Do. コンテンツの振る舞いは、material の挙動と無関係でかまわない。

##### Material は固体です。

入力イベントが、material を通過することはできません。

- Do. 入力イベントは、前景の材料に影響を与えます。
- Don't. 入力イベントは、material を通過することはできません。

##### 複数の material の要素が同時に空間内の同じポイントを占有することはできません。

- Do. Material の要素を分離するために elevation を使用することは、複数の material エレメントが同時に空間内の同じ位置を占めることを防止する1つの方法です。
- Don't. 複数の material の要素が同時に空間内の同じポイントを占有することはできません。

##### Material は、他の material を通過することはできません。

例えば、ある material のシートは elevation が変更されるときに、別の material のシートを通過することはできません。

- Don't. Material は他の material を通過できない

#### Transforming material

##### Material は形を変えることができます。

##### Material は自身の持つ面に沿って拡大、収縮ができます。

##### Material は曲げたりたたんだりできません。

##### 複数の Material のシートが、単一の material のシートになるために一緒に参加することができます。

##### 分割した material は修復できます。たとえば、あなたは材料のシートから材料の一部を切り離すしたとすると、それらの material のシートは、再び一つのシートになることができます。

#### Movement of material

##### Material は、自然に生成されるか、または環境の中の任意の場所で破壊することができます。

##### Material は任意の軸に沿って動かすことができます。

##### Z 軸の動作は、典型的な material を伴うユーザ interaction の結果となります。

### Elevation and shadows

Material design におけるオブジェクトは、現実世界の中のオブジェクトに似た性質を持っています。現実世界では、オブジェクトを積んだり接着したりできますが、お互いを通過することはできません。オブジェクトは影を作り、光を反射します。

これらの特性は、ユーザーにはおなじみで、アプリ全体に一貫して適用することができる空間モデルを形成します。この空間モデルを支えているのが高さと影の概念です。

#### Elevation (Android)

Elevation は、Z 軸に沿った 2 つの表面の間の相対的な深さ、または距離です。

##### Specificaations:

- Elevation は、一般的に、density-independent pixels（dp）として、x、y軸と同じ単位で測定されます。Material の要素が厚みを（すべての material が 1dp の厚さ）を持つため、elevation は、他の先頭にある面からの距離で測定されます。
- 子オブジェクトの elevation は、親オブジェクトの elevation を基準にしています。

##### Resting elevation

##### Component elevations:

##### Responsive elevation and dynamic elevation offsets

##### Avoiding elevation interference

##### Component elevation comparisons

#### Shadows

#### Object relationships

## Layout

> Under Construction

## Components

> Under Construction

## Patterns

> Under Construction

## Usability

> Under Construction
