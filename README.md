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

![3D space with x, y, and z axes](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7UXpQYWltVjNPWXc/whatismaterial_environment_3d.png)

Web においては Z 軸はレイヤリングのために使われ、視点のために使われません。3D の世界は Y 軸の操作によってエミュレートされます。

#### Light and shadow

material 環境の中では、仮想のライトがシーンを照らします。周囲の光があらゆる角度からのソフトシャドウを作成する間、キーライトが、方向を示す影を作ります。

material 環境での影は、これら二つの光源により作られます。アプリ開発において、影は光 Z 軸に沿った光源が様々な位置の material のシートで遮断されたときに発生します。Web においては、影は、y軸を操作することのみによって描画されます。次に示す例は、6dpの高さのカードです。

![光源による影](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsSFZUZ01GTk13T28/whatismaterial_environment_shadow1.png)
![周囲の光による影](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsdDhaaTMwMTFVLTA/whatismaterial_environment_shadow2.png)
![光源および周囲の光による影](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsNnVmbTNMUF9DR0U/whatismaterial_environment_shadow3.png)

### Material properties

Material には、固有の不変な特性や固有の振る舞いがあります。これらの特性を理解することは、material design のビジョンに沿った一貫性のある方法で material を操作するのに役立ちます。

#### Physical properties

##### Material は、様々な X および Y 寸法（単位は dp）と均一な厚さ（1dp）を持ちます。

- Do. 高さと幅は変更できる

![1dp thickness](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B8v7jImPsDi-aTBFT1FDVEstenM/whatismaterial_materialproperties_physicalproperties_thickness_01_yes.png)

- Don't. Material は常に 1dp の厚さ

![not 1dp](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B8v7jImPsDi-Sno0Qy1FY3UtaFk/whatismaterial_materialproperties_physicalproperties_thickness_02_no.png)

##### Material は影を作ります。

影は、material の要素間の相対的な高さ（Z 位置）から自然に生じます。

- Do. 影は、material の要素間の相対的な高さを示しています。

<!--
![Do](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsM01aOVkzWXFYb1k/inline%20whatismaterial-materialprop-physicalprop-PaperShadow_01_xhdpi_008.webm)
-->

- Don't. 影は、色によって影響されることはありません。

<!--
![Don't](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsRGhTci1mN2dWUW8/inline%20whatismaterial-materialprop-physicalprop-PaperShadow_02_xhdpi_008.webm)
-->

##### コンテンツは独立して、material として振る舞うことができますが、それは material の境界内に限定されます。

- Do. コンテンツの振る舞いは、material の挙動と無関係でかまわない。

<!--
![Do](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsaGVXTFRCVG1iU2M/whatismaterial-materialprop-physicalprop-InkDisplay_xhdpi_006.webm)
-->

##### Material は固体です。

入力イベントが、material を通過することはできません。

- Do. 入力イベントは、前景の材料に影響を与えます。

![Do](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7bDZac2JGV2RUNk0/whatismaterial_properties_physical3.png)

- Don't. 入力イベントは、material を通過することはできません。

![Don't](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7RVdsUWRKN2xlaGc/whatismaterial_properties_physical4.png)

##### 複数の material の要素が同時に空間内の同じポイントを占有することはできません。

- Do. Material の要素を分離するために elevation を使用することは、複数の material エレメントが同時に空間内の同じ位置を占めることを防止する1つの方法です。

![Do](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7aVhXV0EtZ29OSU0/whatismaterial_properties_physical5.png)

- Don't. 複数の material の要素が同時に空間内の同じポイントを占有することはできません。

![Don't](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7UFdUMnRKaW5PSXM/whatismaterial_properties_physical6.png)

##### Material は、他の material を通過することはできません。

例えば、ある material のシートは elevation が変更されるときに、別の material のシートを通過することはできません。

- Don't. Material は他の material を通過できない

<!--
![Don't](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsekRnTGVlVEQzNXc/whatismaterial_properties_physical_07_xhdpi_009.webm)
-->

#### Transforming material

##### Material は形を変えることができます。
<!--
![Material can change shape.](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsRjREbXNsZXBrTFU/whatismaterial-materialprop-transformingmaterial-PaperShape_xhdpi_005.webm)
-->
##### Material は自身の持つ面に沿って拡大、収縮ができます。
<!--
![Do](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsZWtfWjlEQ0RTcXc/whatismaterial-materialprop-transformingmaterial-PaperShapeLinear_xhdpi_005.webm)
-->
##### Material は曲げたりたたんだりできません。
<!--
![Don't](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsMXhFNUo2WmJrLWc/whatismaterial-materialprop-transformingmaterial-PaperBendFold_xhdpi_006.webm)
-->
##### 複数の Material のシートが、単一の material のシートになるために一緒に参加することができます。
<!--
![Multiple sheets of material can join toather to become a single sheet](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsRmdDaEl6aTVGREU/whatismaterial-materialprop-transformingmaterial-PaperHeal_xhdpi_004.webm)
-->
##### 分割した material は修復できます。たとえば、あなたは材料のシートから材料の一部を切り離すしたとすると、それらの material のシートは、再び一つのシートになることができます。
<!--
![Material can split and become whole again](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsQV9PS2Q0anFoZzg/whatismaterial-materialprop-transformingmaterial-PaperSplitHeal_xhdpi_005.webm)
-->
#### Movement of material

##### Material は、自然に生成されるか、または環境の中の任意の場所で破壊することができます。
<!--
![Material can be spontaneously generated or destroyed](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQseERpUzUxRVRtMGs/whatismaterial-materialprop-movementmaterial-PaperPointExpand_xhdpi_005.webm)
-->
##### Material は任意の軸に沿って動かすことができます。
<!--
![Material can move along various axes](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsWkhGeVpPNVdZbE0/whatismaterial-materialprop-movementmaterial-PaperMove_xhdpi_008.webm)
-->
##### Z 軸の動作は、典型的な material を伴うユーザ interaction の結果となります。
<!--
![Z-axes motion prompted by user interaction](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsYWJoQjFCYmdvU3c/whatismaterial-materialprop-movementmaterial-Material_Response_xhdpi_003.webm)
-->
### Elevation and shadows

Material design におけるオブジェクトは、現実世界の中のオブジェクトに似た性質を持っています。現実世界では、オブジェクトを積んだり接着したりできますが、お互いを通過することはできません。オブジェクトは影を作り、光を反射します。

これらの特性は、ユーザーにはおなじみで、アプリ全体に一貫して適用することができる空間モデルを形成します。この空間モデルを支えているのが高さと影の概念です。

#### Elevation (Android)

Elevation は、Z 軸に沿った 2 つの表面の間の相対的な深さ、または距離です。

##### Specificaations:

- Elevation は、一般的に、density-independent pixels（dp）として、x、y軸と同じ単位で測定されます。Material の要素が厚みを（すべての material が 1dp の厚さ）を持つため、elevation は、他の先頭にある面からの距離で測定されます。
- 子オブジェクトの elevation は、親オブジェクトの elevation を基準にしています。

![Multiple elevation measurements for two objects](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsTVdGcm1LX0dVeGM/whatismaterial_3d_elevation1.png)

##### Resting elevation

すべての material オブジェクトは、サイズに関係なく、静止時の elevation、または変更されないデフォルトの elevation を持ちます。オブジェクトが elevation を変更する場合には、できるだけ早くその resting elevation に戻す必要があります。

##### Component elevations:

- コンポーネントタイプの resting elevation はアプリ間で一貫しています（例えば、FABの elevation は、あるアプリでは 6dp で他のアプリで16dpで、ということにはなりません）。

- コンポーネントは、環境の深さに応じて、プラットフォーム間で異なる resting elevation を持つ事ができます（例えば、テレビは、モバイルやデスクトップよりも大きな深さを持ちます）。

##### Responsive elevation and dynamic elevation offsets

一部の component type は、それらがユーザ入力（例えば、通常、フォーカスがあたった、あるいは押された）、またはシステム·イベントに応答して elevation を変更する responsive elevation を持っている。これらの elevation の変化は一貫して、dynamic elevation offset を使って実装されます。

dynamic elevation offset はコンポーネントのデフォルト位置に関連してコンポーネントが動く方向のゴールとなる elevation になります。それらは elevation の変化がアクションや component type 全体で一貫していることを意味します。例えば、プレスで持ち上げられたすべてのコンポーネントは、それらのデフォルト位置に応じて同じ elevation の変化を持ちます。

入力イベントが完了またはキャンセルされると、コンポーネントはそのデフォルト位置に戻ります。

##### Avoiding elevation interference

responsive elevation を持つコンポーネントはそれらのデフォルト位置と dynamic elevation offset の間を動く他のコンポーネントと出会う事があります。material は他の material を通過することができないため、コンポーネントはコンポーネント単位でまたはアプリ全体のレイアウトを使ったいくつかの方法で他との干渉をさけます。

コンポーネントレベルでコンポーネントは干渉を引き起こす前に移動または削除されることが可能です。例えば、フローティングアクションボタン（FAB）が消えたり、ユーザーがカードをピックアップする前に画面をオフに移動したり、スナックバーが表示された場合には、移動することができます。

レイアウトレベルでは、干渉の機会を最小限にするようアプリのレイアウトを設計しなさい。例えばユーザがカードをピックアップする時に FAB が干渉しないようなカードの流れの一方の側への FAB の配置。

|Elevation (dp)|Component|
|:-------------|:--------|
|24            |Dialog|
|              |Picker|
|23||
|22||
|21||
|20||
|19||
|18||
|17||
|16 |Nav drawer|
|   |Right drawer|
|   |Bottom Sheet|
|15||
|14||
|13||
|12||Floating action button (FAB - pressed)|
|11||
|10||
|9  |Sub menu (+1dp for each sub menu)|
|8  |Menu|
|   |Card (picked up state)|
|   |Raised button (pressed state)|
|7||
|6  |Floating action button (FAB - resting elevation)|
|   |Snackbar|
|5||
|4  |App Bar|
|3  |Refresh indicator|
|   |Quick entry / Search bar (scrolled state)|
|2  |Card (resting elevation)|
|   |Raised button (resting elevation)|
|   |Quick entry / Search bar (resting elevation)|
|1  |Switch|

##### Component elevation comparisons

次の図は、さまざまなコンポーネントのデフォルト位置と dynamic elevation offset の比較です。

![Component elevation comparisons](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B8v7jImPsDi-aVd2NXFLaHBJLUE/whatismaterial_3d_elevation2.png)

この図では、コンポーネントのための elevation の幅とレイアウトのみが正確です。他の寸法とコンポーネントの全体的なレイアウトは、説明のためだけのものです。

![cards and FAB](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B8v7jImPsDi-cUtqZzE0REdJdnc/whatismaterial_3d_elevation3.png)

カードと FAB があるアプリレイアウトの例と Z 軸に沿ったコンポーネント elevation の断面図

![navigation drawer](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B8v7jImPsDi-eV81TDFrR2ZPU1E/whatismaterial_3d_elevation4.png)

ナビゲーションドロワーが開いた状態のアプリレイアウトの例と Z 軸に沿ったコンポーネント elevation の断面図


#### Shadows

影は、オブジェクトの深さと方向性についての重要な視覚的な手がかりを提供します。これらは、surface の間の分離の量を示す唯一の視覚的な手がかりです。オブジェクトの elevation は、その影の外観を決定します。

- Don't. 影がないと、フローティングアクションボタンは、背景の surface から分離されていないことになります。

![Don't](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsYUJ6a1luU1ZtUWs/whatismaterial_3d_elevation_shadow1.png)

- Don't. crisp 影は FAB とブルーシートが別々の要素であることを示します。しかし、それらの影はそれらが共に同じ elevation であるかのように似ています。

![Don't](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsTVNmT0l2YWEzc3c/whatismaterial_3d_elevation_shadow2.png)

- Do. より柔らかく、より大きな影が FAB が鮮明な影を持っているブルーシートより高い elevation であることを示しています。

![Do](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsRW1LMUtEODctY3M/whatismaterial_3d_elevation_shadow3.png)

運動においては影がオブジェクトの移動の方向について、および surface 間の距離が増えているか減っているかどうかなどの有益な手がかりを提供します。

- Don't. elevation を示す影なしでは、この正方形のサイズが増加しているのかその高さを増加しているかは不明です。

![Don't](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsRlUtdkk1c2xwUkU/whatismaterial_3d_elevation_shadow4.png)

- Do. 影は、オブジェクトの高さの増加に伴って柔らかく、大きくなり、標高が減少するとはっきりと小さくなります。

![Do](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsMlg5UmlWV2FnQ3M/whatismaterial_3d_elevation_shadow5.png)

- Do. このケースでは、影が変わらないことが、elevation を変えるのではなく、オブジェクトの形状を変更していることをユーザが理解するのに役立ちます。

![Do](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsY1hrcHlOdEJuU1k/whatismaterial_3d_elevation_shadow6.png)

##### Component reference shadows

以下のコンポーネントの影が正規の基準として使用されるべきです。

##### App bar

- 4dp

![App bar](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B-Ef4kCjUzkPZ1lQV2ZEeTAxMzg/whatismaterial_3d_elevation_component06.png)

##### Raised button

- デフォルト: 2dp
- 押された状態: 8dp

![PRESSED](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B-Ef4kCjUzkPSy1NQUtNdW5idXc/whatismaterial_3d_elevation_component02.png)

##### floating action button

- デフォルト: 6dp
- 押された状態: 12dp

![PRESSED](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B-Ef4kCjUzkPRFp6VHZ0UTc1V2M/whatismaterial_3d_elevation_component08.png)

##### Card

- デフォルト: 2dp
- ピックアップされた状態: 8dp

![PICKED-UP](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B-Ef4kCjUzkPb1Y5MjNXT2owMFE/whatismaterial_3d_elevation_component03.png)

##### メニュー、サブメニュー

- メニュー: 8dp
- サブメニュー: 9dp (サブメニュー毎で 1dp 増やす)

![menu](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B-Ef4kCjUzkPN0FNTXJ0eU5ybXM/whatismaterial_3d_elevation_component09.png)

##### ダイアログ

- 24dp

![dialog](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B-Ef4kCjUzkPbEVrM01tYlVwR28/whatismaterial_3d_elevation_component12.png)

##### Nav Drawer および Right drawer

- 16dp

![drawer](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B-Ef4kCjUzkPT2pNX0hoeWN5YzA/whatismaterial_3d_elevation_component10.png)

##### Bottom sheet

- 16dp

![bottom sheet](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B-Ef4kCjUzkPRXF4amhNZVFFcjQ/whatismaterial_3d_elevation_component11.png)

##### Refresh indicator

- 3dp

![refresh indicator](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B-Ef4kCjUzkPMWh1ZmwtTHlwMk0/whatismaterial_3d_elevation_component05.png)

##### Quick entry/Search bar

- デフォルト: 2dp
- スクロール状態: 3dp

![scrolled state](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B-Ef4kCjUzkPWXU3dHFBWG84eDg/whatismaterial_3d_elevation_component04.png)

##### Snackbar

- 6dp

![snackbar](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B-Ef4kCjUzkPeUFYaWwwM1N3d0E/whatismaterial_3d_elevation_component07.png)

##### switch

- 1dp

![switch off](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B-Ef4kCjUzkPc1E0T1BZZ2V2d2s/whatismaterial_3d_elevation_component01.png)

#### Object relationships

##### Object hierarchy

あなたがアプリの中でどのようにオブジェクトを編成するのかまたはオブジェクトを収集するのかは他との関連でそれらをどのように移動するかで決定します。オブジェクトは、互いに独立して動くことができるか、上位の階層のオブジェクトによる制約を受けます。

すべてのオブジェクトは親子関係の観点から説明される階層の一部です。これらの関係のそれぞれに「子」は、その「親」要素に従属する要素を指します。オブジェクトは、システムや他のオブジェクトのいずれかの子となることができます。

親子の使用:

- 個々のオブジェクトは単一の親を持つ
- 個々のオブジェクトはいくつでも子を持つ事ができる
- 子は、そのような位置、回転、スケール、elevation などを親からの変更可能なプロパティとして継承します。
- 兄弟は、同一階層のオブジェクトです。

<!--
![As the parent sheet scrolls, the raised button (its child) scrolls off screen with it](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsbHQ3X1ZoVXY3NjQ/WhatIsMaterial_ObjectsIn3DSpace_ObjectRelationships_01_RaisedChildButton_001.webm)
-->

##### Exceptions

このような主要なUI要素として、ルートを親として持つアイテムは、他のオブジェクトとは独立して移動します。例えば、フローティングアクションボタンは、コンテンツとスクロールしません。

他の要素としては以下:

- アプリの side nav drawer
- アクションバー
- ダイアログ

##### interaction

オブジェクトが他のオブジェクトと協調動作する方法はそれらが置かれる親子関係の中において決められます。

例えば:

- 子どもたちは、親からの最低限のz軸の間隔を持っています。他のオブジェクトは、親と子の間に挿入されません。
- スクロールカードコレクションにおいては、カードは、互いに兄弟であるので、それらすべては、タンデムで一緒に移動します。彼らは彼らの動きを制御するカードコレクションオブジェクトの子です。

##### Elevation

オブジェクトの elevation - z-space におけるそれらの位置 - を決めるにはあなたが表現したいコンテンツ階層とオブジェクトが他のオブジェクトから独立して移動する必要があるかどうかに依存します

<!--
![scrolling](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQscnNBNFlpaTIxNnM/WhatIsMaterial_ObjectsIn3DSpace_ObjectRelationships_02_FAB_001.webm)
-->

## Layout

> Under Construction

## Components

> Under Construction

## Patterns

> Under Construction

## Usability

> Under Construction
