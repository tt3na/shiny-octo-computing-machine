## Relay drive Circuit
リレードライブ回路図とRaspberry piのGPIOからリレーを制御するシェルスクリプト

### 回路について
トランジスタを使ったリレードライブ回路を使用  
GPIO18、+5V、GNDピンを使用します。  

<img alt="回路図" width="50%" src="schematic.png" />

* トランジスタは2SC1815を使用
  - hfeは200で計算してます。
  - Vbeは0.6Vで計算します。
* リレーは941H-2C-5Dを使用
  - コイル電圧5V、コイル抵抗167Ω
  - 逆起電力対策に必ずダイオードを接続します。
* ベース(GPIO)側の抵抗は6kΩ程度
  - 以下のように算出しました。
    - Ib = Ic / hfe ≒ 30.0 [mA] / 200 = 0.15 [mA]
    - ( 0.15 [mA] * 3 (オーバードライブ) = 0.45 [mA] )
    - (Vgpio - Vbe) / (Ib * 3) = (3.3 - 0.6) / 0.45 [mA] = 6000 (6kΩ)
* ベース・エミッタ間抵抗は10kΩ (大体これで問題ないかと)

### Usage
GPIOがHIGHになるとリレーの4番と8番、もしくは9番と13番端子が繋がります。
パソコンの電源の遠隔操作などに使えます。

### 注意事項
* AC100Vの制御には絶対に使用しないでください。
* この回路及びスクリプトを使用することによって生じる問題等の責任を一切負いません
