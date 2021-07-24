# ANIFFT

[アニメのキャプチャにFFTをかけて、大まかな画質を推定する](https://github.com/yuuki76/NIBINA)プロジェクトに利用するコード。

Autofft.sh:FFTWが利用可能でImageMagickが利用できる必要がある。  
Autofft.py:現在開発中。クロスプラットフォームにしようと努力してる

## 基本的な仕組み

1920x1080の画像を入力として受け取ります。その画像に黒帯をつけて1920x1920に変形した後、`convert -fft`によって得られるhogehoge-0.png(magnitude値)をコントラストを最大化した後、log1000000で見やすい形に補正します。

コントラストの最大化をした後logをかけるとおそらく内部的に桁落ちが生じることを利用して見やすくしていましたが、代わりにコントラストと明るさを調整することでその機能を実装しました(fixedfft)

アニメ制作における解像度の推定に関する具体的方法は上リンク先を参照。

### ToDo

- Autofft.pyをAutofft.shと全く同じ動作をするように書き換える

- ~~引数の指定がhogehoge.pngではなくhogehogeになっている状況をどうにかする~~

- 入力サイズを1920x1080に限定する仕様をどうにかする

- ~~全処理をG'MICで実装する~~

### 作成されるファイルの解説

- -temp.miff  
  1920x1920にした後FFTをかけた生ファイル。magnitudeとphaseが含まれたImagemagick用中間ファイルの形で出力。

- -L6-FFT-c.png  
  以前の方法で見やすくしたmagnitude。(廃止)

- -rawfft.png  
  単にlogを取っただけのFFT。ほぼデバッグ用。

- -fixedfft.png  
  コントラストと明るさを調節したもの。これがメイン。
