# FlexUI

ロールアウトコントロールをフレキシブルに配置するためのフレームワーク。

## 特徴

* Qtライクな使用感。

* 24種類のロールアウトコントロールに対応。
  （`comboBox`と`timer`は非対応）

* `progressBar`や`spinner`等、通常はサイズ変更できないコントロールもサイズ変更可能。

## サンプル

* ウィジェット

  ![WidgetSample](Resource/WidgetSample.gif "WidgetSample")

* レイアウト

  ![LayoutSample](Resource/LayoutSample.gif "LayoutSample")

## 要件

* [imaoki/Standard](https://github.com/imaoki/Standard)

## 動作確認

`3ds Max 2022.3 Update`

## スクリプトの実行とスタートアップへの登録

01. `Standard\register.ms`を実行する。

02. `FlexUI\register.ms`を実行する。

## スタートアップから登録解除する

`unregister.ms`を実行する。

## 使い方

### ウィジェット

* ウィジェットは全種類が共通のプロパティとメソッドを持つ。

* 既定のサイズ、最小サイズ、およびリサイズの可/不可はロールアウトコントロールの特性に合わせて定数として定義されている。

```maxscript
(
  local widget = ::flexUI.CreateWidget Edt

  -- 全体の水平方向の位置合わせ
  widget.SetAlignmentH #Center

  -- 全体の垂直方向の位置合わせ
  widget.SetAlignmentV #Center

  -- キャプションと本体との余白ピクセル
  widget.SetCaptionMargin 3

  -- キャプションの表示位置
  widget.SetCaptionPosition #Left

  -- キャプションを含まない明示的な高さ
  widget.SetExplicitH undefined

  -- キャプションを含まない明示的な幅
  widget.SetExplicitW undefined

  -- 矩形を設定
  widget.SetRect (Box2 0 0 100 100)
)
```

### レイアウト

#### Gridレイアウト

* 仮想のグリッド上にアイテムを配置するレイアウト。

* グリッドの数は必要に応じて自動的に拡張される。

```maxscript
(
  -- レイアウトオプションは任意で指定する
  local layoutOptions = ::flexUI.CreateLayoutOptions()
  local gridLayout = ::flexUI.CreateGridLayout options:layoutOptions

  -- レイアウトを追加（開始行、開始列の順）
  gridLayout.AddLayout vBoxLayout 1 1

  -- ウィジェットを追加（開始行、開始列、専有する行数、専有する列数の順）
  gridLayout.AddWidget widget 2 3 rowSpan:1 columnSpan:3

  -- 行の最小高を設定（行、高さの順）
  gridLayout.SetRowMinimumHeight 1 10

  -- 行のストレッチ係数を設定（行、ストレッチ係数の順）
  gridLayout.SetRowStretch 2 2

  -- 列の最小幅を設定（列、幅の順）
  gridLayout.SetColumnMinimumWidth 2 10

  -- 列のストレッチ係数を設定（列、ストレッチ係数の順）
  gridLayout.SetColumnStretch 3 2

  -- 矩形を設定
  gridLayout.SetRect (Box2 0 0 100 100)
)
```

#### Groupレイアウト

* `GroupBoxControl`用のレイアウト。

```maxscript
(
  local groupBoxWidget = ::flexUI.CreateWidget Gbx
  local groupLayout = ::flexUI.CreateGroupLayout groupBoxWidget

  -- レイアウトまたはウィジェットを追加
  groupLayout.SetCell widget

  -- 矩形を設定
  groupLayout.SetRect (Box2 0 0 100 100)
)
```

#### HBoxレイアウト

* 水平方向にアイテムを配置するレイアウト。

```maxscript
(
  -- レイアウトオプションは任意で指定する
  local layoutOptions = ::flexUI.CreateLayoutOptions()
  local hBoxLayout = ::flexUI.CreateHBoxLayout options:layoutOptions

  -- レイアウトを追加（ストレッチ係数は既定の`1`）
  hBoxLayout.AddLayout groupLayout

  -- 固定スペースを追加
  hBoxLayout.AddSpace 10

  -- ストレッチを追加（ストレッチ係数`2`）
  hBoxLayout.AddStretch stretch:2

  -- ウィジェットを追加（ストレッチ係数`3`）
  hBoxLayout.AddWidget widget stretch:1

  -- 矩形を設定
  hBoxLayout.SetRect (Box2 0 0 100 100)
)
```

#### VBoxレイアウト

* 垂直方向にアイテムを配置するレイアウト。

* メソッドはHBoxレイアウトと共通。

```maxscript
(
  -- レイアウトオプションは任意で指定する
  local layoutOptions = ::flexUI.CreateLayoutOptions()
  local vBoxLayout = ::flexUI.CreateVBoxLayout options:layoutOptions

  -- 矩形を設定
  vBoxLayout.SetRect (Box2 0 0 100 100)
)
```

## グローバル変数

* 通常はグローバル変数`::flexUI`を通して操作する。

* 詳細は[`mxsdoc.FlexUI.ms`](https://imaoki.github.io/mxskb/mxsdoc/flexui-flexui.html)を参照。

## ウィジェットの種類

| ウィジェット                                                                                                                    | コントロール     | 幅   | 高   | 画像                                                                                                         |
| ------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ---- | ---- | ------------------------------------------------------------------------------------------------------------ |
| [`FlexAngleControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexanglecontrolwidget.html)               | `angle`          | 可変 | 可変 | ![FlexAngleControlWidget](Resource/FlexAngleControlWidget.png "FlexAngleControlWidget")                      |
| [`FlexBitmapControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexbitmapcontrolwidget.html)             | `bitmap`         | 可変 | 可変 | ![FlexBitmapControlWidget](Resource/FlexBitmapControlWidget.png "FlexBitmapControlWidget")                   |
| [`FlexButtonControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexbuttoncontrolwidget.html)             | `button`         | 可変 | 可変 | ![FlexButtonControlWidget](Resource/FlexButtonControlWidget.png "FlexButtonControlWidget")                   |
| [`FlexCheckBoxControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexcheckboxcontrolwidget.html)         | `checkBox`       | 固定 | 固定 | ![FlexCheckBoxControlWidget](Resource/FlexCheckBoxControlWidget.png "FlexCheckBoxControlWidget")             |
| [`FlexCheckButtonControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexcheckbuttoncontrolwidget.html)   | `checkButton`    | 可変 | 可変 | ![FlexCheckButtonControlWidget](Resource/FlexCheckButtonControlWidget.png "FlexCheckButtonControlWidget")    |
| [`FlexColorPickerControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexcolorpickercontrolwidget.html)   | `colorPicker`    | 可変 | 可変 | ![FlexColorPickerControlWidget](Resource/FlexColorPickerControlWidget.png "FlexColorPickerControlWidget")    |
| [`FlexComboBoxControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexcomboboxcontrolwidget.html)         | `dropDownList`   | 可変 | 固定 | ![FlexComboBoxControlWidget](Resource/FlexComboBoxControlWidget.png "FlexComboBoxControlWidget")             |
| [`FlexDotNetControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexdotnetcontrolwidget.html)             | `dotNetControl`  | 可変 | 可変 | ![FlexDotNetControlWidget](Resource/FlexDotNetControlWidget.png "FlexDotNetControlWidget")                   |
| [`FlexEditTextControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexedittextcontrolwidget.html)         | `editText`       | 可変 | 可変 | ![FlexEditTextControlWidget](Resource/FlexEditTextControlWidget.png "FlexEditTextControlWidget")             |
| [`FlexGroupBoxControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexgroupboxcontrolwidget.html)         | `groupBox`       | 可変 | 可変 | ![FlexGroupBoxControlWidget](Resource/FlexGroupBoxControlWidget.png "FlexGroupBoxControlWidget")             |
| [`FlexImgTagWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-fleximgtagwidget.html)                           | `imgTag`         | 可変 | 可変 | ![FlexImgTagWidget](Resource/FlexImgTagWidget.png "FlexImgTagWidget")                                        |
| [`FlexLabelControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexlabelcontrolwidget.html)               | `label`          | 固定 | 固定 | ![FlexLabelControlWidget](Resource/FlexLabelControlWidget.png "FlexLabelControlWidget")                      |
| [`FlexLinkControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexlinkcontrolwidget.html)                 | `hyperLink`      | 固定 | 固定 | ![FlexLinkControlWidget](Resource/FlexLinkControlWidget.png "FlexLinkControlWidget")                         |
| [`FlexListBoxControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexlistboxcontrolwidget.html)           | `listBox`        | 可変 | 可変 | ![FlexListBoxControlWidget](Resource/FlexListBoxControlWidget.png "FlexListBoxControlWidget")                |
| [`FlexMapButtonControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexmapbuttoncontrolwidget.html)       | `mapButton`      | 可変 | 可変 | ![FlexMapButtonControlWidget](Resource/FlexMapButtonControlWidget.png "FlexMapButtonControlWidget")          |
| [`FlexMaxCurveCtlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexmaxcurvectlwidget.html)                 | `curveControl`   | 固定 | 固定 | ![FlexMaxCurveCtlWidget](Resource/FlexMaxCurveCtlWidget.png "FlexMaxCurveCtlWidget")                         |
| [`FlexMtlButtonControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexmtlbuttoncontrolwidget.html)       | `materialButton` | 可変 | 可変 | ![FlexMtlButtonControlWidget](Resource/FlexMtlButtonControlWidget.png "FlexMtlButtonControlWidget")          |
| [`FlexMultiListBoxControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexmultilistboxcontrolwidget.html) | `multiListBox`   | 可変 | 可変 | ![FlexMultiListBoxControlWidget](Resource/FlexMultiListBoxControlWidget.png "FlexMultiListBoxControlWidget") |
| [`FlexPickerControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexpickercontrolwidget.html)             | `pickButton`     | 可変 | 可変 | ![FlexPickerControlWidget](Resource/FlexPickerControlWidget.png "FlexPickerControlWidget")                   |
| [`FlexProgressBarWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexprogressbarwidget.html)                 | `progressBar`    | 可変 | 可変 | ![FlexProgressBarWidget](Resource/FlexProgressBarWidget.png "FlexProgressBarWidget")                         |
| [`FlexRadioControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexradiocontrolwidget.html)               | `radioButtons`   | 可変 | 可変 | ![FlexRadioControlWidget](Resource/FlexRadioControlWidget.png "FlexRadioControlWidget")                      |
| [`FlexSliderControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexslidercontrolwidget.html)             | `slider`         | 可変 | 固定 | ![FlexSliderControlWidget](Resource/FlexSliderControlWidget.png "FlexSliderControlWidget")                   |
| [`FlexSpinnerControlWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexspinnercontrolwidget.html)           | `spinner`        | 可変 | 固定 | ![FlexSpinnerControlWidget](Resource/FlexSpinnerControlWidget.png "FlexSpinnerControlWidget")                |
| [`FlexSubRolloutWidgetStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-widget-flexsubrolloutwidget.html)                   | `subRollout`     | 可変 | 可変 | ![FlexSubRolloutWidget](Resource/FlexSubRolloutWidget.png "FlexSubRolloutWidget")                            |

### 制限

* `FlexComboBoxControlWidgetStruct`は`dropDownList`にのみ対応する。
  `comboBox`には非対応。

* `curveControl`のサイズ変更には非対応。

* `slider`の`orient`パラメータは`#Horizontal`にのみ対応。

## レイアウトの種類

| レイアウト                                                                                          | 説明                            | 画像                                                               |
| --------------------------------------------------------------------------------------------------- | ------------------------------- | ------------------------------------------------------------------ |
| [`FlexGridLayoutStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-layout-flexgridlayout.html)   | グリッドにアイテムを配置する    | ![FlexGridLayout](Resource/FlexGridLayout.png "FlexGridLayout")    |
| [`FlexGroupLayoutStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-layout-flexgrouplayout.html) | `GroupBoxControl`用のレイアウト | ![FlexGroupLayout](Resource/FlexGroupLayout.png "FlexGroupLayout") |
| [`FlexHBoxLayoutStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-layout-flexhboxlayout.html)   | 水平方向にアイテムを配置する    | ![FlexHBoxLayout](Resource/FlexHBoxLayout.png "FlexHBoxLayout")    |
| [`FlexVBoxLayoutStruct`](https://imaoki.github.io/mxskb/mxsdoc/flexui-layout-flexvboxlayout.html)   | 垂直方向にアイテムを配置する    | ![FlexVBoxLayout](Resource/FlexVBoxLayout.png "FlexVBoxLayout")    |

## レイアウトオプション

* レイアウト各部の余白を設定する。

* 詳細は[`mxsdoc.FlexLayoutOptions.ms`](https://imaoki.github.io/mxskb/mxsdoc/flexui-layout-flexlayoutoptions.html)を参照。

```maxscript
(
  local layoutOptions = ::flexUI.CreateLayoutOptions()

  -- セル間の水平方向の余白
  layoutOptions.SetMarginH 0

  -- セル間の垂直方向の余白
  layoutOptions.SetMarginV 0

  -- レイアウト外周の下側の余白
  layoutOptions.SetPaddingB 0

  -- レイアウト外周の左側の余白
  layoutOptions.SetPaddingL 0

  -- レイアウト外周の右側の余白
  layoutOptions.SetPaddingR 0

  -- レイアウト外周の上側の余白
  layoutOptions.SetPaddingT 0

  -- マージンの一括指定（水平、垂直の順）
  layoutOptions.SetMargin 0 0

  -- パディングの一括指定（上、右、下、左の順）
  layoutOptions.SetPadding 0 0 0 0
)
```

## ライセンス

[MIT License](https://github.com/imaoki/DocGenerator/blob/main/LICENSE)
