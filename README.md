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

### Principles

Material design は UX としての階層化、意味付け、フォーカスを作るための、例えば、タイポグラフィ、グリッド、スペース、スケール、色、および画像のような印刷ベースの design 要素から導かれます。Material design は視覚的要素、構造グリッド、および間隔の繰り返しによるプラットフォームや画面サイズを跨がる一貫性を担保するためにベースライングリッドや構造化テンプレートのような印刷デザインの分野からツールを採用しています。これらのレイアウトは、スケーラブルなアプリケーションを作成するプロセスを簡素化し、任意の画面サイズに適合するように拡張します。

#### How paper works

Material design においては紙の物理的特性は、画面に変換されます。アプリケーションの背景は、用紙の平らな、不透明な風合いに似ています。

アプリケーションの振る舞いはリサイズされたり、チャップルされたり、複数シートが一緒になったりする紙の能力に似ています。ステイタスバー、システムバーのようなアプリケーションの外にある要素は別な扱いとします。それらはアプリ配下のコンテンツとは別のもので、紙の物理的特性を有していません。

Material の詳細な情報については、Material Properties を参照してください。

##### Seams

全体共通のエッジを共有する二枚の紙はシームと呼ばれます。縫い目によって繋がっている間、それらは一緒に移動します。

![Seams in two sheets of material](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7RVhqalJxN01Fb0U/layout_principles_papercraft_paper1.png)

##### Steps

異なる Z 位置 (あるいは深さ）でオーバラップしている二つの紙のシートは step を形成します。これらは、互いに独立して移動します。

![Steps in two sheets of overlapping material](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7ck5NWGtlRHBCWVE/layout_principles_papercraft_paper2.png)

#### Floating action button

##### Floating action button

フローティングアクションボタンは、ツールバーとは別の円形のシートです。これは、単一の何かを行うアクションを表します。

step を作るコンテンツに関連するのであれば step に跨がることができる。

![Floating action buttons straddling steps](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7aGcyakNwSW1iR1U/layout_principles_papercraft_actions1.png)

両方のシートのコンテンツに関連している場合、フローティングアクションボタンは、seam を跨ぐことができます。

アクションのためのアンカーポイントを提供するために装飾的な seam を導入しないでください。

![Floating action buttons straddling seams](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7eVA3azhXVEFabUE/layout_principles_papercraft_actions2.png)

floating action button の詳細な情報は Floating Action Button の項目を確認のこと。

### Units and measurements

一部のユニットは、異なるコンテキストで異なる意味を持ちます。この章では、画素密度のようなデバイスに依存しないピクセル、スケーラブルなピクセルの利用だけでなく、概念を説明します。

#### Pixel density

インチあたりのピクセル数は「ピクセル密度」と呼ばれます。高密度スクリーンは低密度のそれよりも多くのインチあたりのピクセル数を持ちます。その結果、ボタンなどの UI 要素は低密度スクリーンでは物理的に大きく表示され、高密度スクリーンでは小さく表示されます。

dpi、または画面の解像度は、特定の画面における画素数を意味します。

dpi = ピクセルで表現される画面の幅（または高さ）/ インチで表現される画面の幅（または高さ）

![High-density screen](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7N3BFUFpveGxFWVE/layout_units_density1.png)

![Low-density screen](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7MjdKekwta00yVFE/layout_units_density2.png)

#### Density-independent pixels (dp)

「密度の独立性」は、密度の異なる画面上のUI要素の均一な表示を指します。

密度非依存ピクセル（発音は「dips」）は、任意の画面上において均一な大きさに拡大縮小する柔軟なユニットです。 Androidアプリケーションを開発する時、密度の異なる画面上に均一に要素を表示するために dp を使用します。

![pixels and dip](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7SE4yRmp3SWsweE0/layout_units_dp.png)

|Screen resolution|Screen width in pixels (dpi * width in inches)|Screen width in density-independent pixels|
|:----------|:----------|:----------|
|120 dpi|180 px|240 dp|
|160 dpi|240 px| |
|240 dpi|360 px| |

あなたは3つの画面を使用している場合、画面解像度を変更することで、広いすべての1.5インチは、画面の幅は、まだすべての彼らのために240dpとなります。

dp は、160 dpiの画面上の1つの物理 pixel に等しいです。 DPを計算するには：

dp = (ピクセルの幅 * 160）/ dpi

CSSを書くとき、DPまたはSPが記載されていてもピクセルを使用します。 dp は Android向けの開発でのみ使われる必要があります。

#### Scalable pixels (sp)

Android 開発において、スケーラブルなピクセル（sp）は dp と同様の機能を提供しますがフォントのためではありません。sp のデフォルト値は、dp のデフォルト値と同じです。

sp と dp の主な違いは、sp がユーザーのフォント設定を保存することです。アクセシビリティのための大きなテキストの設定を持っているユーザーについては、自分のテキストサイズの好みに合わせたフォントサイズが表示されます。

#### Designing layout for dp

画面用のレイアウトを設計する時には、dp での要素の大きさを計算します。

dp = (ピクセルの幅 * 160）/ dpi

例えば、320dpi における 32x32 px のアイコンは 16x16 dp と等しい。

#### Image scaling

画像は、これらの比率を使用して、別の画面解像度で同じに見えるようにスケーリングすることができます：

|Resolution|dpi|Pixel ratio|Image size (pixels)|
|:---------|:--|:----------|:------------------|
|xxxhdpi|640|4.0|400 x 400|
|xxhdpi|480|3.0|300 x 300|
|xhdpi|320|2.0|200 x 200|
|hdpi|240|1.5|150 x 150|
|mdpi|160|1.0|100 x 100|

### Metrics & keylines

#### Baseline grids

すべてのコンポーネントは 8 dp の正方形のベースライングリッドに揃えます。タイプは　4　dp のベースライングリッドに揃えます。ツールバーにある icongraphy は 4 dp の正方形のベースライングリッドに揃えます。これは、モバイル、タブレット、デスクトップに適用されます。

![Example of baseline grid](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsTnQzUDZiZF9KNm8/layout_metrics_baseline1.png)

![Example of baseline grid](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsbExOZTZCd0hUZ0E/layout_metrics_baseline2.png)

![Example of baseline grid](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsc0tpMGdyWDh2OUE/layout_metrics_baseline3.png)

![Example of baseline grid](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsZGo1cVg1TFFzQzA/layout_metrics_baseline4.png)

![Example of typography in a baseline grid](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsNzAtNkU0RW1vSVE/layout_metrics_baseline5.png)

詳細な情報は typography を見なさい。

#### Keylines and spacing

##### Mobile

モバイルレイアウトテンプレートは、多種多様な画面とどのように keyline と spacing が画面の端と要素に跨がって働くかという情報を含みます。下記のダウンロードファイルに含まれる画面のサンプルです。

##### List

- A two-column, left-aligned list with a 56 dp floating action button

![Layout](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsb3ZESndwbXc0ekE/layout_metrics_keyline_mobile1.png)

- Screen edge left and right margins: 16dp
- Content associated with an icon or avatar left margin: 72dp
- Horizontal margins on mobile: 16dp

![Keylines and margins](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQseWRUbzJuUnpkNHM/layout_metrics_keyline_mobile2.png)

+ Status bar: 24dp
+ Toolbar: 56dp
+ Subtitle: 48dp
+ List item: 72dp

![Vertical spacing](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsWFRSRjhiV2t2WEE/layout_metrics_keyline_mobile3.png)

##### List with subheadings

- A two-column list, subtitle, and right-aligned icons, with a 40dp floating action button

![Layout](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQscjNUb2lvZkpZSDA/layout_metrics_keyline_mobile4.png)

- Screen edge left and right margins: 16dp
- Content left margin from screen edge: 72dp

![Keylines and margins](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsMldpS1Bzc2R0NVk/layout_metrics_keyline_mobile5.png)

+ Status bar: 24dp
+ Toolbar: 56dp
+ Title and list items: 72dp
+ Subtitle: 48dp
+ Space between content areas: 8dp

![Vertical spacing](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsUXV2Z1gwVjdFS0E/layout_metrics_keyline_mobile6.png)

##### Detial view

- A detail card with a 56dp floating action button

![Layout](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsbnJKY25tRkltekk/layout_metrics_keyline_mobile7.png)

- Screen edge left and right margins: 16dp
- Content left margin from screen edge: 72dp
- Right-side icons align 32dp from the right edge to coordinate with the floating action button

![Keylines and margins](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsNVlYYkdnMktUVmc/layout_metrics_keyline_mobile8.png)

+ Status bar: 24dp
+ Toolbar: 56dp
+ Space between content areas: 8dp
+ List item: 72dp

![Vertical spacing](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsN0hFU2wxOHNNU3M/layout_metrics_keyline_mobile9.png)

##### Mixed content

- icons, avatars, and text align on the left. A floating action button, icons, and text align on the right.

![Layout](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsRjlfWGpLMkUzRVU/layout_metrics_keyline_mobile10.png)

- icons alignment from left and right edges: 16dp
- Content associated with an icon or avatar left margin: 72dp

![Keylines and margins](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsMHFJN3BXcjl2NmM/layout_metrics_keyline_mobile11.png)

+ Status bar: 24dp
+ List items: 56dp
+ Subtitles and list items: 48dp
+ Space between content areas: 8dp

![Vertical spacing](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsOXd1NndUQlkyTDg/layout_metrics_keyline_mobile12.png)

##### Navigation drawer

- A side navigation menu with icons, avatars, and text aligned on the left. Other icons align on the right.

![Layout](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsRjc5TmFyN3F5aVU/layout_metrics_keyline_mobile13.png)

- Screen edge left and right margins: 16dp
- Content associated with an icon or avatar left margins: 72dp
- Side nav width: The screen width minus the height of the action bar: Here, the width is 56dp from the right screen edge.

![Keylines and margins](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsOFlvYmdNb3ZyYVk/layout_metrics_keyline_mobile14.png)

+ Account menu and list items: 48dp
+ Space between content areas: 8dp
+ navigation right margin: 56dp

![Vertical spacing](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsWWRuZnU4NS05cEU/layout_metrics_keyline_mobile15.png)

##### Tablet

タブレットレイアウトテンプレートは14種類のスクリーンを備え、画面の端と要素間でどのように keylines and spacing が働くかを示しています。下記のダウンロードファイルに含まれる14の画面のサンプルです。

##### List with detail view

![Example of tablet layout](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsYU9pMWZmVHlJWTQ/layout_metrics_keyline_tablet1.png)

![Keylines and margins](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsQ09PVGVhZEF6VWs/layout_metrics_keyline_tablet2.png)

![Vertical spacing](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsc0tUUXZrS0tmc0E/layout_metrics_keyline_tablet3.png)

+ Status bar and space above list: 24dp
+ List item: 64dp
+ Space between content areas: 8dp
+ List item: 72dp

##### List with detail view

![Example of tablet layout](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsZ3NBRUhMS3Njc3M/layout_metrics_keyline_tablet4.png)

![Keylines and margins](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsd1R5dnZ5TWJ2X00/layout_metrics_keyline_tablet5.png)

- Screen edge left and right margins: 24dp
- Vertical center of icons distance from screen edge: 52dp
- Left margin distance to nav item text content: 104dp
- Content left margin from screen edge: 80dp

![Vertical spacing](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsaDZ3NHRNbmJ3QVU/layout_metrics_keyline_tablet6.png)

+ Status bar: 24dp
+ Toolbar and list item: 64dp
+ Space between content areas: 8dp
+ Subtitle, list item, and slider: 48dp
+ Title: 80dp

##### Desktop

デスクトップレイアウトテンプレートは、4つの異なる画面、四つの異なるウィンドウサイズとそれぞれが含まれており、窓や要素間でどのように keylines and spacing が働くかを示しています。ウィンドウサイズに基づいて、keylines and spacing ブロックは、タブレットと携帯の両方からグリッド·ルールを継承します。これが、ダウンロードで利用可能な画面のサンプルです。

![Desktop full screen](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7c2FiNEFVZHJQcFE/layout_metrics_keylines_desktop1.png)

![Resized windows](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7Y18xZHdTUXkwVzA/layout_metrics_keylines_desktop2.png)

#### Ratio keylines

特定のアスペクト比、または要素の幅と高さの割合（width:height として表記される）は、UI要素と、モバイル画面のサイズの両方に適用されます。次のキーラインの画像は、これらの推奨比率を示しています：

- 16:9
- 3:2
- 4:3
- 1:1
- 3:4
- 2:3

モバイル、タブレット、デスクトップに適用されます。

例えば：

- 1 : 1 のアスペクト比、要素が等しい高さと幅を有しています。
- 2 : 3 のアスペクト比、360dp 幅の画像（フルスクリーン）は 540 の高さを持つでしょう

あなたの要素の適切な幅や高さを測定するために、上記のアスペクト比のいずれかを使用なさい。

幅 = アスペクト比 * 高さ

高さ = 幅 / アスペクト比

(両方の式において、アスペクト比は分数として表されます。例えば、3:2 は 3/2 となり、16:9 は 16/9 となります。)

![Screen width](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7ZjBCVzdPOENpT28/layout_metrics_ratiokeylines1.png)

![Example of screen width on mobile](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsS1RKNFQtdy1sYkU/layout_metrics_ratiokeylines2.png)

![Element width](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7LTV1b3k5ekZHa1E/layout_metrics_ratiokeylines3.png)

![Example of element width on mobile](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsM203V05SR1ZyX28/layout_metrics_ratiokeylines4.png)

#### Incremental keylines

Incremental keylines は、アクションバーの高さと同じように増分を定義し、サイズやアプリ内の他の要素の位置を決定するために、その増分の倍数を使用しています。

Incremental keylines は、多くの場合デスクトップに、そしてしばしばタブレットに、まれにモバイルに適用されます。増分の数は、ウィンドウサイズによって異なります。

![The space allocated for a hero image has a vertical increment of 3x.](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsTnNBT2NEX1RQTzg/layout_metrics_incremental1.png)

![The example card width has a horizontal increment of 8x.](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsQUxUQWYyUE5NaWs/layout_metrics_incremental2.png)

![THe height of the example extended app bar is 2x the increment, and the width of the right panel is 5x the increment.](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsSElrWE5scnNaNkE/layout_metrics_incremental3.png)

![Increments can work across many elements in Material UI.](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQseGRLSnk0LWhlZ3M/layout_metrics_incremental4.png)

#### Touch target size

使用可能なアプリケーションであることを確実にするために、タッチターゲットは少なくとも48×48 dp でなければなりません。ほとんどの場合、タッチターゲット間の空間は、8 dp 以上であるべきです。

レイアウト内のアイコン（24dp）またはアバター（40dp）の spacing 時には、この点に注意してください。タッチターゲットがオーバーラップしないようにしてください。

平均して、48dp は（ある程度の変動を含む）は約9ミリメートルの物理的なサイズに変換されます。これは、タッチスクリーンオブジェクトの推奨ターゲットサイズ（7〜10ミリメートル）の範囲内で快適であり、ユーザーは確実かつ正確に自分の指でそれらをターゲットできるようになります。

あなたは、少なくとも 48dp より高く、また幅広くにあなたの要素を設計する場合、次の項目を確認することができます。

- あなたのターゲットは表示された画面の 7 ミリメートルの最小推奨ターゲットサイズよりも小さくなることはありません。
- UI 要素の targetability と全体的な情報密度の間の良い折衷点を strike します。

![Example](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7eEVhSW1nVjBrZnM/layout_metrics_touchtarget1.png)

- Above: The element is 48dp wide and the avatar is 40dp wide.
- Below: The element is 48dp wide and the icon is 24dp wide.

![Example of touch target](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsaU12eTNLSnBEcXc/layout_metrics_touchtarget2.png)

![Example](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7dlN4cEMwWm9Tc28/layout_metrics_touchtarget3.png)

- Touch target height: 48dp
- Button height: 36dp

![Example of touch targets and buttons](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsZjVQbVZ1MzN3RGs/layout_metrics_touchtarget4.png)

### Structure

#### UI regions

正しい動作と影を実現するための Z 空間における要素の配置については、Environment および Elevations and shadows 節を参照してください。

##### Mobile structure

この構造は、恒久的なアプリバーとフローティングアクションボタンが含まれています。オプションとなる下のバーは追加機能やアクションオーバーフローのために追加できます。サイドナビゲーションメニューは他の全ての要素の上に重なります。

![Mobile structure](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7T0hfM01sSmRyTG8/layout_structure_regions_mobile.png)

- Top left to right: Side nav, app bar/primary toolbar, content area (below the app bar/primary toolbar),  and right nav
- On the bottom: bottom bar

##### Tablet structure

この構造は、恒久的なアプリバーとフローティングアクションボタンを表示します。アプリバーはタブレットおよびモバイルの下のバーの要素を吸収します。オプションとなる下のバーは追加機能やアクション·オーバーフローのために追加できます。サイドナビゲーションは他の全ての構成要素をオーバレイします。右のナビゲーションメニューは一時的に、または永久的な表示のためにピン止めされた形でアクセスすることができます。

![Tablet structure](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7VmpjWnp5UDZEWEU/layout_structure_regions_tablet.png)

- Top left to right: Side nav, app bar/primary toolbar, content canvas (below the app bar/primary toolbar),  and right nav
- On the bottom: bottom bar

##### Desktop Structure

デスクトップ構造はフローティングアクションボタンを伴った恒久的なアプリバーが含まれます。アプリバーはタブレットやモバイルの下のバーの要素を吸収します。可能であればウィンドウコントロールはアプリバーに吸収されます。

サイドナビゲーションメニューは（アプリバーの下を含む）画面サイズの全高を取ることができ、一時的に、または永久的な表示のためにピン止めされた形でアクセスすることができます。サイドナビゲーションメニューだけでなく、コンテンツ·キャンバスは、タブ、パレット、またはセカンダリアクションのための、独自のセカンダリツールバーを持つことができます。

![Desktop structure](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7SnotM2RNN2FFMzQ/layout_structure_regions_desktop.png)

- Top left to right: App bar/primary toolbar
- Second row from left to right: Toolbar, secondary toolbar, and toolbar
- Third row from left to right: side nav, content canvas, and right nav On the bottom: floating action button

##### UI regions

プライマリとなる水平または垂直方向の仕切りを定義しなさい。

![Vertical divider](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7cGZWZmxBV1d1M2s/layout_structure_regions_guidance1.png)

![Horizontal divider](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7dnhDVHg4WTBrbnc/layout_structure_regions_guidance2.png)

L shapes を引き起こし得る非常に沢山の領域をインターフェースで切り分けることは避けなさい。その代わりに、二次領域を表現するために空白を使用しなさい。

![DO](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7RVg5NlRYc29XRTQ/layout_structure_regions_guidance3.png)

![Don't](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7NHNfYW03U28wYnM/layout_structure_regions_guidance4.png)

edge をまたぐことができるのはカードと FAB のみ。

![Card breaking an edge](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7RHJsbFhpanhPQXc/layout_structure_regions_guidance5.png)

![Floating action button breaking an edge](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7aTFlbjdxV2dwZVE/layout_structure_regions_guidance6.png)

具体的な振る舞いが必要とされるときまたは情報のグループ化が空白またはディバイダが提供できる何かよりもさらなる分離を必要とするなら、コンテンツを整理するためにカードを使いなさい。

![Cards](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7QzR3ZFdSS1VhSkk/layout_structure_regions_guidance7.png)

![Cards](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7ZXRFRzA3eGpQSG8/layout_structure_regions_guidance8.png)

#### Toolbars

Toolbar は、汎用性があり、多くの異なる方法で使用することができます。ここではいくつかの例を示します。

![Full-width, default height app bar](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7eW41S2JtRm9CSmc/layout_structure_toolbars1.png)

Full-width, default height app bar

![Full-width, extended height app bar](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7UnNtdkNxY05oelk/layout_structure_toolbars2.png)

Full-width, extended height app bar

![Column-width toolbars at multiple levels of hierarchy](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7eTQ0WmN0cUlHWGs/layout_structure_toolbars3.png)

Column-width toolbars at multiple levels of hierarchy

![Flexible toolbar and card toolbar](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7bW1TYXlMT0JxUWM/layout_structure_toolbars4.png)

Flexible toolbar and card toolbar

![Floating toolbar](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7M1VKVkhLLUxuTGs/layout_structure_toolbars5.png)

Floating toolbar

![Detached toolbar palette](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7aEJPTW1iV0EwQ0E/layout_structure_toolbars6.png)

Detached toolbar palette

![Bottom toolbar that launches to a shelf and clings to the top of the keyboard or other bottom](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7M2djcm1TSG1ZQVU/layout_structure_toolbars7.png)

Bottom toolbar that launches to a shelf and clings to the top of the keyboard or other bottom

![Bottom toolbaar shelf](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7R21ES09zcURiR0k/layout_structure_toolbars8.png)

Bottom toolbaar shelf

#### App bar

以前の Android のアクション·バーとして知られている app bar は、ブランディング、ナビゲーション、検索、およびアクションに使用される特別な種類のツールバーです。

app bar の左側にある nav icon は

- ナビゲーションドロワーを開くためのコントロール
- アプリの階層を上方に移動するため上向き矢印
- この画面からナビゲーションが要求されない時は略

とすることができます。

app bar のタイトルは、現在のページを表現し、アプリのタイトル、ページタイトル、またはページフィルタとすることができます。

app bar の右側にあるアイコンは、アプリに関連するアクションです。メニューアイコンは、2 次アクションとヘルプ、設定、およびフィードバックなどのメニュー項目を含むオーバーフローメニューを開きます。

![App bar structure](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7RTFrbmpoWjRrY00/layout_structure_appbar_structure1.png)

- On the left: Nav icon, title, and filter icon
- On the right: Action and menu icons

[!Lignt](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsU1FwTUx3cmRUNG8/layout_structure_appbar_structure2.png)

Light

![Dark](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsbGREMW9BdDdnSUk/layout_structure_appbar_structure3.png)

Dark

![Colored](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsZF9VZDhtQlF5RGM/layout_structure_appbar_structure4.png)

Colored

![Transparent](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsQnFjd0tiMmtsMU0/layout_structure_appbar_structure5.png)

Transparent

##### Title color

app bar では、すべてのアイコンは、同じ色でなければなりません。

増加した視覚的な階層が必要な場合は、タイトルはアイコンと異なる色を持つことができます。異なるタイトルの色は白と黒の標識の両方にとって十分なコントラストを伴う背景で最高に働きます。

![Single color (default)](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsbkxqbW9kQWgxZkk/layout_structure_appbar_structure6.png)

Single color (default)

![Distinct totle color](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQselRDRFlzNkI0SFE/layout_structure_appbar_structure7.png)

Distinct totle color

##### Metrics

既定の高さ:

- モバイル横: 48dp
- モバイル縦: 56dp
- タブレット/デスクトップ: 64dp

拡張された app bar では、高さは既定の高さに加えて、コンテンツの増分（複数可）に等しいです。

![default](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsLUFJUnFlRHVhUVU/layout_structure_appbar_metrics1.png)

![default](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQscTFBTHJJTm41TzQ/layout_structure_appbar_metrics2.png)

![Extended1](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsSDBhX3BwSURRc1U/layout_structure_appbar_metrics3.png)

![Extended1](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsREdycWl2SmxSTVE/layout_structure_appbar_metrics4.png)

![Extended2](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsTW1zb2x5WWg5cDA/layout_structure_appbar_metrics5.png)

![Extended2](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsY19yMzV5RHZyams/layout_structure_appbar_metrics6.png)

![default(tablet/desktop)](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsOFVmeDlPTU5LZ1E/layout_structure_appbar_metrics7.png)

![Extended1(tablet/desktop)](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsVm5pN2ZRWFZQV3c/layout_structure_appbar_metrics8.png)

![Extended2(tablet/desktop)](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsUXlEQkIyN0xETTg/layout_structure_appbar_metrics9.png)

##### Menus

メニューは app bar の拡張機能として動作するというよりはむしろ、app bar に常に重ねられている紙の一時的なシートです。

![Example of App bar](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsU094a25SRS1LXzQ/layout_structure_appbar_menu1.png)

Example of App bar

![Example of menu in App Bar](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsLUtFU1dySnRkbFE/layout_structure_appbar_menu2.png)

Example of menu in App Bar

![Example of menu in an App Bar](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsd0JpVzNpNzBuMjQ/layout_structure_appbar_menu3.png)

Example of menu in an App Bar

![Example of menu in an App Bar](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsWFh0S09Rb3VvYWc/layout_structure_appbar_menu4.png)

Example of menu in an App Bar

![Example of menu in an App Bar](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsX1BHTWxFbUdzMXc/layout_structure_appbar_menu5.png)

#### System bars

##### Status bar/window bar

Android では、ステータスバーには通知アイコンとシステムアイコンが含まれています。Chrome では、トップバーには最小化、フルスクリーン、および close というウィンドウコントロールが含まれています。 Chrome のアプリでは上部のバーは消えることができ、消えた後にウィンドウコントロールは app bar に格納されます。

基準:

- Android status bar height: 24dp
- Chrome window height: 32dp

![Android status bar](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsLUFLM2xkRElVM2s/layout_structure_system_status1.png)

Android status bar

![Chrome window bar](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7Tkh3MGZVVktoOTQ/layout_structure_system_status2.png)

Chrome window bar

![Android status bar on top of the app bar](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsUkFVNERQODRoakk/layout_structure_system_status3.png)

Android status bar on top of the app bar

![Chrome window baar on top of the app bar](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7OFZxQTM5SmxHQjA/layout_structure_system_status4.png)

Chrome window baar on top of the app bar

![Chrome window controls inside app bar](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7cHV2LWpmTnRUbm8/layout_structure_system_status5.png)

##### Dark status bar

デフォルトでは、ステータスまたはウィンドウバーの色は、app bar の色の暗い影となります。レイアウトの別の要素の色を使用するか、半透明であることもできます。

![Color is based on a sample taken from the content](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsdkwzWUZZNEdaUzg/layout_structure_system_color1.png)

Color is based on a sample taken from the content

![Translucent status bar, 20% Black #000000](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsLWE2REc4RnVuTWc/layout_structure_system_color2.png)

Translucent status bar, 20% Black #000000

![Dark status bar](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsN3pJUmlJeDJ5NHc/layout_structure_system_color3.png)

Dark status bar

![Status bar color in a darker tone of the app bar color](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsdHAwWDlJWm1Sdnc/layout_structure_system_color4.png)

Status bar color in a darker tone of the app bar color

##### Light status bar

暗いアイコン付きの明るいステータスバーは、明るいコンテンツとより調和し、暗いステータスバーの代わりに使用することができます。

![Light status bar color is based on sample taken from content](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B8v7jImPsDi-X0Z6NHdnSjdUYTA/layout_structure_system_color5.png)

Light status bar color is based on sample taken from content

![Translucent light status bar, 70% White #FFFFFF](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B8v7jImPsDi-RmR0RU9hc1MzWGc/layout_structure_system_color6.png)

Translucent light status bar, 70% White #FFFFFF

![Light status bar, default background fill is #E0E0E0](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B8v7jImPsDi-VlV3YjN5bk0xUGc/layout_structure_system_color7.png)

Light status bar, default background fill is #E0E0E0

![Light status bar in darker tone of a light app bar color](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B8v7jImPsDi-eUoyd3JIWHc2MEU/layout_structure_system_color8.png)

Light status bar in darker tone of a light app bar color

##### Android navigation bar

Androidのナビゲーションバーには、デバイスのナビゲーションコントロール: Back、Home、および Overview を収容します。また、Android 2.3 またはそれ以前のバージョン用に書かれたアプリケーションのためのメニューも表示されます。

- Height: 48dp

![Dark](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7RWpaeTZqTmlYOHc/layout_structure_system_android1.png)

Dark

![Light](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7QkxkZjVDYmtSYXc/layout_structure_system_android2.png)

Light

##### Color variants

ナビゲーションバーは、不透明、半透明、または透明にすることができます。

![Translucent](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7RzhjWURpTWVsRTA/layout_structure_system_android3.png)

Translucent

![Translucent over complex image](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7bl93YnVqdWE3NGM/layout_structure_system_android4.png)

Translucent over complex image

![Translucent](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7MzdRU2EtbHlaRlk/layout_structure_system_android5.png)

![Transparent over even-toned image](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7S2tTVjBjcUNEM00/layout_structure_system_android6.png)

##### Chrome OS shelf

shelf には、Chrome OS 上のアプリケーションランチャー、アプリケーションのアイコン、およびシステム設定を収容します。

- Height: 56dp

![Example of Chrome OS shelf](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7R3BySy1UQ2pDbGc/layout_structure_system_chrome.png)

Example of Chrome OS shelf

#### Side nav

存在する場合、side nav bar は常に表示するため固定またはオーバレイとしての一時的な配置のために浮動表示することができます。Side nav は、画面の左側または右側に配置することができます。

左 nav に表示されるコンテンツはナビゲーションまたはアイデンティティベースのものが理想とされます。右 nav のコンテンツはページのメインコンテンツのセカンダリな情報であるべきです。

Navigation drawer も参照してください。

![Mobile screen](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsbU5RX3BYcTJiOFk/layout_structure_sidenav1.png)

Mobile screen

![Side nav menu](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsSnJFcnlLNUJXb2s/layout_structure_sidenav2.png)

Side nav menu

##### Structure

side nav bar は常に表示するため固定またはオーバレイとしての一時的な配置のために浮動表示することができます。コンテンツキャンバスに重ねられたテンポラリな nav drawer に対して固定された nav panel は横側やコンテンツキャンバス下に位置します。

画面サイズは、パネルが固定またはオーバーレイされているかどうかで決定されます。十分なスペースがある場合、パネルが固定され、コンテンツがそれに応じて調整します。十分なスペースが確保できない場合、パネルはオーバーレイされる必要があります。

規定値

モバイル：

Width = 画面の幅 - 56dp

最大幅：320dp

左の nav を使用した場合、最大幅にのみ適用されます。右の nav を使用する場合は、パネルがスクリーンの幅全体をカバーすることができます。

デスクトップ：左パネルの最大幅は 400dp です。右ナビゲーションは、コンテンツに応じて変えることができます。

![Left nav on mobile](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B6Okdz75tqQsanRZMG5CaFRDWlE/layout_structure_sidenav_structure1.png)

Left nav on mobile

![Left nav on desktop](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7bXlOVlM1bGV2Q0k/layout_structure_sidenav_structure3.png)

Left nav on desktop

![Right nav on desktop](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0Bx4BSt6jniD7d2Z0QURUVk5hV2M/layout_structure_sidenav_structure4.png)

Right nav on desktop

#### Whiteframes

Whiteframes は surface、レイヤー、影に一貫したアプローチを使用してレイアウト構造の多様性を提供します。

whiteframes に関するダウンロードおよびその他の情報については、Resources を参照してください。

![Carded content that expands and collapses](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B08MbvYZK1iNVGJCUHZUcUtBSVE/layout-structure-whiteframe_bigtop_large_xhdpi.png)

Carded content that expands and collapses

![Overlayed content details with focused app bar on mobile](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B08MbvYZK1iNZ3ZWYkxacmJBZ1E/layout-structure-whiteframe_calendar_large_xhdpi.png)

Overlayed content details with focused app bar on mobile

![Overlapping content card with multiple toolbars and background image on mobile](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B08MbvYZK1iNbjdWb0JqRmpOZFk/layout-structure-whiteframe_contacts_large_xhdpi.png)

Overlapping content card with multiple toolbars and background image on mobile

![Extended app bar and right side nav](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B08MbvYZK1iNbjdWb0JqRmpOZFk/layout-structure-whiteframe_contacts_large_xhdpi.png)

Extended app bar and right side nav

![Left side nav and one-up stream on mobile](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B08MbvYZK1iNWFBhWmo1d1gyMlU/layout-structure-whiteframe_gallery_large_xhdpi.png)

Left side nav and one-up stream on mobile

![Source list](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B08MbvYZK1iNMU12c2xDS1QtZFk/layout-structure-whiteframe_mail_large_xhdpi.png)

Source list

![Full-screen background image with inset search field and carded search results](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B08MbvYZK1iNM2k4eGVaYjg0LVk/layout-structure-whiteframe_maps_large_xhdpi.png)

Full-screen background image with inset search field and carded search results

![Expandable footer drawer](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B08MbvYZK1iNT29PaWxfZ21iOW8/layout-structure-whiteframe_music_large_xhdpi.png)

### Adaptive UI

material design における responsive layout は全ての画面サイズに適応します。この adaptive UI ガイダンスはレイアウトを超えた一貫性を保証する柔軟なグリッド、どうやってコンテンツは異なる画面にリフローするかについてのブレイクポイントの詳細およびどのようにアプリケーションが小さいものから特大の画面にスケールできるかの説明を含みます。

#### Breakpoints

最適なユーザーエクスペリエンスのために、material ユーザーインターフェイスは、次のブレークポイントの幅のためにレイアウトを適応させる必要があります：480、600、840、960、1280、1440、および1600dp。

![screen width and breakpoints](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B8olV15J7abPSGFxemFiQVRtb1k/layout_adaptive_breakpoints_01.png)

##### 1. Summary and detail view content in layouts

- 600dpより下の幅におけるレイアウトは幅の広いコンテンツ階層の単一レベル（サマリーまたは内容の詳細内容のいずれかで、両方ではありません）で画面を埋めてもかまいません。
- 600dp以上の幅でのレイアウトはワイド画面の内容 2 段階（サマリーおよび詳細内容の両方）の階層を配置してもかまいません。

##### 2. Max screen width

1600dp 以上の幅でのレイアウトは、その最大幅までレイアウトを広げてもかまいません。この時点で、グリッドは、次のいずれかを実行することがあります。

- 増加マージンを伴う中央揃え
- 右マージンが成長しながら、左側は揃えられる
- 追加コンテンツが現れながら、成長し続けます

##### Breakpoint system

これらのブレークポイントは、異なる画面、デバイス、及び画面の向きの列と幅の仕様を示します。

一部の測定値では、値は、デバイスが回転しても同じになります。そのためいずれの方向における最小の幅が規定する値です。

 * デバイスの最小幅が <600 である場合 16dp

 ** Desktop breakpoints are 16dp below the listed values to accommodate variations in browser chrome.

|Breakpoint (dp)|Handset / Tablet Portrait|Handset / Tablet Landscape|Window|Columns|Gutter|
|:--------------|:------------------------|:-------------------------|:----:|:-----:|:----:|
|0|small handset||xsmall|4|16|
|360|medium handset||xsmall|4|16|
|400|large handset||xsmall|4|16|
|480|large handset|small handset|xsmall|4|16|
|600|small tablet|medium handset|small|8|16/24*|
|720|large tablet|large handset|small|8|16/24*|
|840|large tablet|large handset|small|12|16/24*|
|960||small tablet|small|12|24|
|1024**||large tablet|medium|12|24|
|1280**||large tablet|medium|12|24|
|1440**|||large|12|24|
|1600**|||large|12|24|
|1920**|||xlarge|12|24|

#### Grid

material design の adaptive UI は 12 カラムの grid layout に基づいています。デザインの様々な全体の柔軟性を可能である間、グリッドはレイアウト間の視覚的一貫性を生成します。グリッドの列の数は、ブレークポイントシステムに基づいて変化します。

This animation shows how surfaces and panels can align to influence the 12-column grid.

##### Margins and Gutters（余白と溝）

adaptive grid はカラムの幅より margin および gutter の幅の一貫性に焦点を当てています。material design の margin および column は 8dp 正方形の baseline grid に従います。margin と gutter は 8、16、24、または 40dp の幅を取り得ます

margin と gutter は等しい必要はありません。同じレイアウトにおいて 40dp の margin と 24dp の gutter を使うことは許容されます。

This animation shows interactions of the following margin and gutter width variations:

+ 8dp margins and gutters
+ 16dp margins and gutters
+ 24dp margins and gutters
+ 40dp margins and gutters
+ 40dp margins and 24dp gutters

##### Full-width vs centered

Full-width grid はレイアウトが変更する必要がある時に fluid カラムとブレークポイントを使います。

Centered grid は全てのカラム（プラス定義されている margin）がこれ以上画面に適応しない時に fixed カラムと reflow を使います。

動画

+ Full-width grids
+ Centerd grids

##### Panel Influence ont the Grid

Navigation patterns で定義されているように、side nav は、永久的、持続的、または一時的であってもよい。これらの動作は、side nav だけではなく任意のパネルに適用されます。

##### Permanent

permanent panel は、adaptive grid の外に存在します。パネルは定義されたブレークポイントで表示され（スクリーンがパネルを収容できる時）、コンテンツを絞ります。パネルの表示/非表示を行うコントロールはありません。

The effects of a permanent panel on the adaptive grid.

##### Side panel effects on the grid

このアニメーションは、2つのフェーズで行われます。

+ 永続的なサイドパネルが表示され、コンテンツとグリッドの両方を絞ります。パネルが表示された状態の間はコンテンツがアクセス可能です。パネルはトグル時に非表示になります。
+ 一時的なサイドパネルが表示され、オフスクリーングリッドコンテンツをプッシュします。外のパネル、パネル内のアイテムのいずれかをタッチすると、パネルが非表示になります。

The effects of a persistent panel on the adaptive grid.

##### Temporary Overlay

off-screen 時には temporary panel はグリッドやコンテンツには影響しません。表示されるよう切り替える時にはパネルやパネル内の項目以外の場所をタッチすることで、再び非表示にすることができます。

The effects of a temporary panel on the adaptive grid.

#### Surface behaviors

画面サイズの変更時には、UIは、以下の surface 固有の動作を使用して適応します。

##### Visibility

|Behavior|Definition|
|:-------|:---------|
|Permanent|画面スペースが利用可能である場合には、surface が常に表示されます。|
|Persistent|surface の可視性は visible と hidden で切り替えることができます。visible の時、画面上の他の要素との相互作用で可視性が変わることはありません。|
|Temporary|surface の可視性は visible と hidden で切り替えることができます。visible の時、画面上の他の要素との相互作用で surface が隠れるか最小かされます。|

##### Width

|Behavior|Definition|
|:-------|:---------|
|Fixed|要素の幅は、画面サイズが変更されても同じままです。|
|Fluid|要素の幅は、画面サイズの変更に応じて成長します。|
|Sticky|他の要素またはブレークポイントによる影響が生じるまで要素の幅は固定されています。|
|Squeeze|要素の幅はパネルが明らかにする|
|Push|要素の幅は同じままです。その位置はパネルが表示されて水平方向に変わり、画面の端に部分的に隠れても良い。|
|Overlay|パネルがコンテンツ上に表示されても、素子の幅と位置は同じまま。|

##### Descriptions

|Behavior|Definition|
|:-------|:---------|
|Above, Below|要素の y 位置。|
|Over, Under|要素の動作における z 位置。|
|In Front, Behind|要素の静的な z 位置。|
|Left, Right, Centered|要素の x 位置|
|Top, Bottom|要素の y 位置と画面端との相対位置。|
|Flat, Raised|要素の z 位置、およびその影。フラット要素には影がありません。|
|Inset, Full Bleed|画像または要素のパディング|
|Summary, Detail|コンテンツの概要、および要約の完全な展開|

#### Patterns

多くの画面スペースが利用可能であるように、次のパターンを適用することができます。

##### Reveal

隠された UI を明らかに

![Elements such as a side nav may become visible](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B8olV15J7abPUWt3NmVSbHFWdDQ/layout_adaptiveUI_patterns_01_reveal.png)

Elements such as a side nav may become visible

##### Transform

UI はあるフォーマットから他に変換できます

![Side navigation may transform into tabs](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B8olV15J7abPSmpTSzdyVXdKS2s/layout_adaptiveUI_patterns_02_transform.png)

##### Divide

以前積み重ねていた UI は新しい可能なスペースに分割しなさい

![Side navigation, summary content, and detail content divide within the same view as space is available](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B8olV15J7abPUElOU1A5Q05ac28/layout_adaptiveUI_patterns_03_divide.png)

Side navigation, summary content, and detail content divide within the same view as space is available

##### Reflow

可能なスペースに UI を reflow しなさい

![Elements may reflow from a single-column format to fill the content area in various combinations of side-by-side elements](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B8olV15J7abPT1VuQ0hCa2VOY1k/layout_adaptiveUI_patterns_04_reflow.png)

Elements may reflow from a single-column format to fill the content area in various combinations of side-by-side elements

##### Expand

さらにスペースを消費するよう UI を育てる

![Content cards may expand to take up more horizontal space](https://material-design.storage.googleapis.com/publish/material_v_4/material_ext_publish/0B8olV15J7abPQnJWNW94UTZlWmc/layout_adaptiveUI_patterns_05_expand.png)

## Components

> Under Construction

## Patterns

> Under Construction

## Usability

> Under Construction
