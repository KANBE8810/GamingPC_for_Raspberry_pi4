# GamingPC_for_Raspberry_pi4
ロボットシステム学の演習1で作成したデバイスドライバ
---
## 説明
講義内で作成したデバイスドライバを元に,コンデンサを用いて小さい冷却ファンを制御したり,LED3個を点滅させるデバイスドライバを作成しました.<br>
ゲーミングPC上でのようにLEDのを点滅させながら,冷却ファンを回転させます.

## 用意するもの
- Raspberry Pi 4 ModelB
- ミニブレッドボード
- LED × 3
- 市販されている冷却ファンが固定できるケース
- 市販されているラズベリーパイ用の冷却ファン
- コンデンサ PN 2222
- ジャンパケーブル(オスメス) × 9
- ジャンパケーブル(オスオス) × 2
- 抵抗 330Ω × 3
- 抵抗 10KΩ<br>
※個数が書いていない物はそれぞれ1つで大丈夫です.

## 回路図
![image](https://user-images.githubusercontent.com/50877609/100971898-256bbf80-357b-11eb-9c59-ed0034a285fe.png)<br>
全体画像<br>
![image](https://user-images.githubusercontent.com/50877609/101059979-3ac00880-35d2-11eb-88b9-1d196904395a.png)<br>
冷却ファンの拡大画像<br>

上記の用に回路を組みました.<br>
トランジスタのベースをGPIO25(緑ケーブル),LEDをそれぞれGPIO16(青ケーブル),GPIO23(黄ケーブル),GPIO26(灰ケーブル)に接続しています.<br>
その際,トランジスタのベースのところに10KΩの抵抗を,各LEDにはそれぞれ330Ωの抵抗を挟んでいます.<br>
わかりにくいですが,冷却ファンの回路は5.0Vピン(赤ケーブル)からエミッタに接続し,コレクタをGND(白ケーブル)に接続しています.
GNDに関しては他の場所でも大丈夫です.<br>
ピンの位置など詳しくは以下のリンクから確認してください.<br>
https://www.raspberrypi.org/documentation/usage/gpio/README.md

## ビルド
```sh
$ git clone https://github.com/KANBE8810/GamingPC_for_Raspberry_pi4
$ cd GamingPC_for_Raspberry_pi4/myled  
$ make
$ sudo insmod gaming.ko  
$ sudo chmod 666 /dev/gaming0  
```
## 実行結果
* ### fまたはFを入力した場合
  ```sh
  $ echo f > /dev/gaming0
  ```
  または
  ```sh
  $ echo F > /dev/gaming0
  ```
  `f`または`F`をデバイスファイルに入力すると,冷却ファンがか回転します.

* ### gまたはGを入力した場合
  ```sh
  $ echo g > /dev/gaming0
  ```
  または
  ```sh
  $ echo G > /dev/gaming0
  ```
  `g`または`G`をデバイスファイルに入力すると,3つのLEDを点滅させながら冷却ファンが回転します.<br>
  尚,このLEDは約1分後に消えます.
  また, `g`と`G`でLEDの点滅の仕方が違います.

* ### eまたはEを入力した場合
  ```sh
  $ echo e > /dev/gaming0
  ```
  または
  ```sh
  $ echo E > /dev/gaming0
  ```
  `e`または`E`をデバイスファイルに入力すると,冷却ファンの回転を停止します.

## デモ動画
https://www.youtube.com/watch?v=hODM32MakM8<br>
[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/hODM32MakM8/0.jpg)](http://www.youtube.com/watch?v=hODM32MakM8)<br>
画像をクリックしても見ることができます.
