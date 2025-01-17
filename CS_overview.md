[TOC]



## 序章

### 抽象化

あるものの外面的な性質と内面的な構造との詳細とを区別することを意味している．つまり抽象化によって複雑な装置の内部構造のｐ詳細は無視して，1つの理解可能な単位として使用できる．



## 1. データストレージ

### ビットとその格納

#### ゲートとフリップフロップ

**ゲート**

ブール演算の入力値が与えられたときに，出力を生じる装置のこと．

**フリップフロップ**

0か1の出力を生じる回路．他の回路からのパルスが値を変化させるまでその値を維持する．

フリップフロップは現代のコンピュータで1ビットを格納する手段の一つである．**大規模集積回路(VLSI)**にはフリップフロップが利用されている．



### メインメモリ

#### メモリ構成

コンピュータのメインメモリ中のここのセルを識別するために，各セルには**アドレス**と呼ばれる一意な名前が割り当てられている．これによって識別だけでなく順序づけることもできる．



コンピュータのメインメモリを構成するにはビットを実際に保持する回路+**メモリセルにデータを書き込む回路**と**メモリセルからデータを読み取る回路**が必要になる．

コンピュータのメインメモリは1つずつアドレスの付いたセルとして構成されるので要求に応じてセルを個別にアクセスできる．任意の順序でセルにアクセスできることを反映してコンピュータのメインメモリは**ランダムアクセスメモリ(RAM)**と呼ばれる．



**動的メモリ**

すぐに散逸してしまうような微笑な電荷によってビットを格納しており，1秒間に何回も電荷を繰り返して供給する回路が必要なコンピュータメモリを，この揮発性を表して**動的メモリ**と呼ぶ．



### マスストレージ

#### ファイルの格納と取り出し

マスストレージシステムに格納される情報は**ファイル**と呼ばれる大きな単位へと概念的にグループ化されている．マスストレージの都合によりこれらのファイルが小規模な複数バイト単位で格納されて取り出される．たとえば磁気ディスク上に格納されるファイルは固定的に前もって決められたサイズのセクタごとに扱わなければならない．記憶装置の物理的な性質に合わせたデータのブロックのことを**物理レコード**という．



表現される情報によって決定される自然な分割のデータブロックのことを**論理レコード**という．例としては，企業の従業員に関する情報を持つファイルはそれぞれが一人に従業員情報からなる複数のユニットから構成されるといったようなもの．

論理レコードはさらに，**フィールド**と呼ばれるより小さなユニットから構成される．たとえば従業員についての情報をもつ論理レコードは，名前，住所，従業員識別番号から構成される．ファイル中の論理レコードは，レコード中の特定のフィールドで一意に識別されるようになっている．



### ビットパターンとして情報を格納する

#### 画像を表現する

画像を表現する1つの方法は画像**ピクセル**と呼ばれる点のあつまりを解釈するもの．

**ビットマップ**

各ピクセルの状態を符号化することで，画像全体を符号化された集合で表すもの．



### 整数を格納する

#### 2の補数表現

**2の補数**表現はもっとも一般的な体系．最左端のビットは**符号ビット**である．



#### エクセス記法

最初に使用するビットパターンの長さを決定する．その上でその長さで可能なすべてのビットパターンを2進数で数え上げる順序で書き出す．**最左端のビットが1でそれ以外のビットは0になるようなものを0**としてそれに先行するパターンを-1,-2...として書き出していく．エクセス記法と2の補数記法では符号ビットが異なる．



### 小数を格納する

#### 浮動小数点

1バイトの領域を用いた例で**01101011**について考える．最左端のビットを符号ビットとする．残りの7ビットを2つのフィールドに分ける．**指数フィールド**と**仮数フィールド**である．

符号ビットに続く3ビットを指数フィールド，残りの4ビットを仮数フィールドとする．最初に仮数を取り出して左端に小数点を置く．

 ex.

**.1011**

次に指数フィールドを取り出して，それを3ビット**エクセス方式**によって格納された整数であると解釈する．指数フィールドは110であるので**正**の2を表していることになる．これは解の小数点を**右**に2ビット移動することを表している．結果として次を得る．

Ex.

**10.11**

よって符号ビットと合わせて，

$2 \frac{3}{4}$

となる．

**浮動小数点の正規形**

浮動小数点での表記において一意に定めるもの．仮数フィールドの左端が1となるようにする．これによって同じ値が複数の表現となる可能性がなくなる．



#### 打ち切り誤差

値$2\frac{5}{8}$を1バイトシステムに格納しようとするときに生じる問題がある．$2\frac{5}{8}$を2進数で書き表すと，10.101となる．しかしこれを仮数フィールドにいれようとしても場所が足りない．(最右端の1が失われてしまう．)これを**打ち切り誤差**あるいは**丸め誤差**と呼ぶ．

つまり**丸め誤差**とは仮数フィールドの長さが十分でないために，格納されるべき値の一部が欠落してしまうことを指す．



### データ圧縮

**データ圧縮**

基本的な情報は保ったままでデータのサイズを縮小する技法．



#### 汎用データ圧縮技法

データ圧縮には**ロスなし**，**ロスあり**がある．

- **ランレングス符号化**

  圧縮データ要素の列を繰り返す要素と，それが列中で出現する回数を示す符号へと置き換えるプロセス．253個の1のあとに118個の0が続き，さらに87個に1が続くことを示すビットパターンは実際に458ビットすべてを列挙するよりも少ない領域に格納できる．

- **頻度依存符号化**

  表現するデータ項目のビットパターンの長さをその出現頻度に反比例させるシステム．このような符号化システムを**ハフマンコード**という．

- **相対符号化(差分符号化)**

  連続するデータ単位の差分を記録する方法．各単位は直前の単位との関係が符号化される．

- **辞書式符号化**

  辞書とは圧縮されるメッセージが構成される構築ブロックの集合のことをいい，メッセージそのものが辞書への一連の参照として符号化される．

  - **適合型辞書式符号化**

    符号化のプロセスで辞書を変更できる．

  - **LZW符号化**

    xyx xyx xyx xyx

    とすると，xを1, yを2, 空白を3とする．さらに空白が現れた時点でxyxが1単語であるとわかるのでxyxを4とおく．すると，与えられた文字列は

    121343434

    となる．



### 通信エラー

#### パリティビット

エラーを検出する単純な方法は操作されるビットパターンがすべて奇数個の1からなるならば正しいというように決めておくことである．これは**パリティビット**と呼ばれる追加の1ビットを既存の符号化システムの各パターンに加えることで容易に得られる．パリティビット込みで9ビットであるなら8ビットの情報を含みつつ，パリティビットで偶奇を調整できる．



## 2. コンピュータアーキテクチャ

#### CPU

データの演算を実行する回路を含む**算術論理ユニット**，マシンの実行を調整する回路を含む**制御ユニット**，CPUないで情報を一時的に格納するのに使用される**レジスタ**(データ格納用セル)を含む**レジスタユニット**である．

ビットパターンを転送するためにマシンのCPUとメインメモリは**バス**という転送路で接続されている．



**キャッシュメモリ**

CPUの内部にある高速メモリ．マシンが現在使用中のメインメモリの一部を複写しておく．

(CPU内部にある)レジスタとメインメモリの間で(バスを経由して)行われるデータ転送を，(CPU内部の)レジスタと(CPU内部の)キャッシュメモリの間で行うため高速にデータ転送が行われる．(メモリ通信による遅延がなくなるため．)



**プログラム内蔵方式**

コンピュータのプログラムをメインメモリに格納するアイデアのこと．



#### アーキテクチャと命令の関係

- **縮小命令セットコンピュータ(RISC)**

  最小限のマシン命令を実行するようにCPUを設計すればよいというもの．

  - 利点

    高速で効率的

- **複合命令セットコンピュータ(CISC)**

  複数の命令を使用することなく，1命令で複雑な命令を実行することができるようにハードを設計したもの．

  - 利点

    複雑さを増すソフトウェアに対応できる．
  
  - 欠点
  
    電力消費が多い．



#### 命令の種類

**データ転送命令**

データをある場所から他の場所へ移動する命令群から構成される．

- **I/O命令**

  CPUとメインメモリの外側にある装置との通信のための命令．



**算術・論理命令**

制御ユニットに算術論理ユニットでの動作を行わせるように伝える．



**制御命令**

データを操作するのではなく，プログラムの実行の流れを変える命令群．



#### マシン語について

マシン命令は，2つの部分から構成される．その2つとは**オペコード**フィールドと**オペランド**フィールドである．

**オペコード**

基本命令のいずれの命令かが表されている．

**オペランド**

どのレジスタが格納されるデータを持っていてデータを受け取るのがどのメモリセルであるかといった情報を含む．



#### プログラムの実行

CPU内には2つの専用レジスタ(**命令レジスタ**, **プログラムカウンタ**)がある．

**命令レジスタ**

実行される命令を保持する．

**プログラムカウンタ**

次に実行される命令のアドレスをもつことでマシンがプログラムのどこを実行しているかをわかるようにする．



#### マシンサイクル

CPUでのプログラムの実行のサイクルのこと．取出し，解読，実行を繰り返す．

- **取出し**

  メモリ(プログラムカウンタが指定)から次の命令を取り出してからプログラムカウンタを繰り上げる．

- **解読**

  **命令レジスタ**内のビットパターンを解読する．

- **実行**

  命令レジスタ内の命令が指定する動作を実行する．



### 他の装置との通信

#### コントローラ

コンピュータと他の装置との間の通信の中継機器．



#### コントローラの役割

**メモリマップドI/O**

コンピュータとコントローラの間のデータの受け渡しに，メインメモリとの通信に使用されているCPU命令を利用するもの．この場合，**コントローラは，特定のメモリアドレスへの参照に対応するように設計される**．メインメモリはそれらのアドレスへの参照は無視する．そうすることでコントローラに割り当てられたメモリアドレスにビットパターンを格納するように，CPUがバスにメッセージを送信すると，そのビットパターンはメインメモリではなくコントローラに格納される．同様にCPUがそのようなメモリアドレスからデータを読み込もうとすると，メモリではなく，コントローラからビットパターンが渡されることになる．



#### ダイレクトメモリアクセス(DMA)

CPUがバスを使用していないナノ秒単位の間隙でコントローラがメインメモリと直接通信を行なえる機能のことを言う．

- 問題点

  DMAの使用によってコンピュータもバス上で実行される通信が複雑化する．

  CPUとコントローラがバスのアクセスで競合することがコンピュータの性能を制約することを**フォン・ノイマン・ボトルネック**という．なぜならこれはCPUがバスを通してメモリから命令を取り出すという**フォン・ノイマン・アーキテクチャ**によるものだからである．



#### ハンドシェーキング

コンピュータの構成要素間でのデータ転送が一方通行であることはまずない．コンピュータと他の機器でのやりとりには**ハンドシェーキング**と呼ばれる二方向の対話が必要である．

**ステータスワード**

周辺機器が生成してコントローラに送るビットマップ．



#### パイプライン

マシンサイクル中のステップを重複させる技法のこと．ある命令を実行している間に，次の命令を取り出せる．



#### よく使用される通信経路

- **パラレル通信**

  - 利点

    複数の線上で同時に転送するためデータを高速に転送できる．

  - 欠点

    比較的複雑な通信経路が必要になる．

- **シリアル通信**

  - 利点

    単純なデータ経路で済む．

    

### 他のアーキテクチャ

#### マルチプロセッサマシン

パイプライン化とは**並列処理**の第1段階と捉えることができる．真の意味での並列処理には2つ以上のプロセシングユニットがあり，そのようなコンピュータを**マルチプロセッサマシン**と呼ぶ．

このようなマルチプロセッサを利用したアーキテクチャには**SISD**と異なるデータセットに異なる命令列を適用して実行する**MIMD**がある．



#### SIMD

マルチプロセッサアーキテクチャの1つでプロセッサを連結して同じ一連の命令を同期を取って実行させる方式．

- 利点

  データの大きなブロック内の類似の項目に同じ作業を適用しなければならないようなアプリケーションに有用．



#### 並列処理に対するもう一つのアプローチ

それぞれが独自にメモリとCPUをもつ小さなマシンの集合体として大きなコンピュータを構成する方法．



## 3. オペレーティングシステム

**オペレーティングシステム**

コンピュータ全体の動作を管理するソフトウェア．

**バッチ処理**

実行中ユーザの介入なしでジョブをひとつのまとまりとして実行できる．

**リアルタイム処理**

環境にある締切内で作業を完了させること．

##### 対話型処理

遠隔端末から対話式にユーザがプログラムを実行できるオペレーティングシステム．

### オペレーティングシステムの歴史

#### タイムシェアリング

複数のユーザに同時にサービスを提供できるようにオペレーティングシステムを設計すること．(複数のユーザが1台のコンピュータを共通して使用すること)

タイムシェアリングを実装する手段として**マルチプログラミング**が挙げられる．



**マルチプログラミング**

コンピュータの各実行時間は細かい間隔に分割されて，各ジョブの実行はその実行時間分だけに制限される．分割された時間の終わりで現在のジョブは別のジョブが次の間隔で実行できるように一時的に取り除かれる．このように細かく分割し実行，中断を繰り返すことで複数のジョブが同時に実行されているように見せかけることができる．

この技法は現在の**マルチタスキング**に応用されている．



#### マルチタスキング

一人のユーザが多くの作業を同時に行うこと．



プロセッサ自体の数も増えたため以下の問題についても考えなければならなくなった．

- **ロードバランシング**

  さまざまなプロセッサに作業を**動的**に振り分けて全てのプロセッサが効率的に使用されるようにすること．

- **スケーリング**

  プロセッサの数に合うように1つの作業を複数の部分作業に分割すること．



### オペレーティングシステムのアーキテクチャ

#### ソフトウェア

マシンのソフトウェアは2つに大別される．一つは**アプリケーションソフトウェア**でもう一つは**システムソフトウェア**である．

**アプリケーションソフトウェア**

マシンを利用して作業を行うためのプログラムから構成されるもの．

**システムソフトウェア**

システムソフトウェアはさらに2つに分けることができる．一方はオペレーティングシステムそのもので，もう一方は**ユーティリティソフトウェア**と呼ばれる．

- **ユーティリティソフトウェア**

  コンピュータの利用に必要な作業を実行するプログラムであるが，オペレーティングシステムに含まれないものがある．それは**オペレーティングシステムの機能を拡張するソフトウェアである．**



#### オペレーティングシステムの構成要素

**ユーザインタフェース**

ユーザと対話するオペレーティングシステムの部分．



- **カーネル**

  オペレーティングシステムの内部部分．コンピュータの稼働にとって最も基本的な機能を実行するためのソフトウェアが含まれる．以下のソフトウェアが含まれている．

  - **ファイルマネージャ**

    マスストレージに格納されているすべてのファイルの記録を保持している．

  - **デバイスドライバ**

    マシンに接続されている周辺装置の操作を実行するためにコントローラと通信する装置のこと．

    - 利点

      デバドラがあるとそれをインストールして特定の機器の作業を扱ってもらえる．

  - **メモリマネージャ**

    マシンがメモリを使用する際の調整を行う．マルチユーザやマルチタスクの環境ではコンピュータが一度に多くの要求に応えなければならないため用いられる．こういったシステムでは多くのプログラムやデータのブロックをメインメモリ中に同時に配置しなければならない．

    - **ページング**

      プログラムやデータブロックをメインメモリとデータブロックの間でやり取りすることで，実際にある以上のメモリがあるかのような状態を作り出す．

      要求されるメモリの総量がそのコンピュータで利用できる実際のメモリ領域を超えている場合に有効．

      例としてメインメモリに8GB必要だったところ実際には4GBしかなかったとする．この場合，実際より大きなメモリ領域があるかのように　見せるためにメモリマネージャは8GBのストレージ領域を磁気ディスク上に用意する．そこにメインメモリが8GBあったら格納されたであろうビットパターンを記録する．このデータは**ページ**と呼ばれる均一な大きさの単位に分割される．

      ページのやりとりによって生じるこの大きな架空のメモリのことを**仮想メモリ**という．

  - **スケジュール**

    後述．

  - **ディスパッチャ**

    後述．



### オペレーティングシステムの起動

オペレーティングシステムの起動は**ブーティング(ブートストラップ)**という手続きを通して達成される．

#### ブーティング

メインメモリは一般に揮発性．しかしそれではプログラムの情報が消えてしまう．そのためこのままではCPUにプログラムを渡せない．そこでメインメモリの一部は**ROM**で構成されておりそこに**ブートローダ**というプログラムが格納されており，マシンの起動時にこのコードが一番最初に実行される．ブートローダ中の命令に従ってCPUは特定の場所に格納されているオペレーティングシステムをメインメモリに持ってくる．

こうしたオペレーティングシステムを開始させるプロセス全体のことを**ブート**と呼ぶ．



**ファームウェア**

ファームウェアルーチンはオペレーティングシステムが機能する前にブートローダが入出力動作を実行するのに使用される．(ブートのエラーを伝えるためなどにに必要)



### マシンの動作を調整する

#### プロセスの概念

**プロセス**

オペレーティングシステムの制御下でプログラムを実行する動作．

**プロセス状態**

実行されているプログラムの実行中の位置のみならず，他のCPUレジスタや関連するメモリの値が含まれる．



#### プロセス管理

プロセスの実行を調整する作業はオペレーティングシステムのカーネル中の**スケジューラ**と**ディスパッチャ**によって扱われる．

**スケジューラ**

コンピュータ中に存在するプロセスの記録を保持するだけでなく新たに到着したプロセスを現在プロセスに加え，完了したプロセスを現在プロセスから削除する．

- **プロセステーブル**

  メインメモリ中に保持されている情報のブロック．

  プログラムの実行が要求されるたびにスケジューラはプロセステーブル中にそのプロセスのエントリを新たに生成する．エントリにはプロセスに割り付けられたメモリ領域，プロセスの優先順位，プロセスが準備完了か待機中かといった情報が含まれる．

**ディスパッチャ**

スケジュールされたプロセスの実行を管理する．タイムシェアリングシステムやマルチタスキングシステムではこの作業は**マルチプログラミング**によって達成される．

プロセスから他のプロセスへと変更する手続きは**プロセススイッチ**または**コンテキストスイッチ**と呼ばれる．



ディスパッチャがプロセスにタイムスライスを割り当てる度に，タイマー回路も起動してタイムスライスの終わりに**割込み**と呼ばれるシグナルを発生させる．CPU がそのシグナルを受け取るとまず現在のマシンサイクルを完了し現在プロセス中の位置を保存してから**割込みハンドラ**と呼ばれるプログラムを実行する．



### プロセス間の競合を調整する

#### セマフォ

実行可能フラグをセットする前に割り込みが発生すると2つのプロセスが同時に同じ機器にアクセスしようとする場合がある．これを防ぐには2つのアプローチがある．

一つは割り込み不能命令と割り込み可能命令を使用すること．

もう一つは**テストアンドセット**命令を用いる方法である．これはCPUに実行可能フラグの値を取り出し，受け取った値を調べてからフラグをセットするといった一連の動作を1つの命令で行う．1命令で行うのでCPUが割り込みを認識する前にフラグをセットできる．

このように適切にセットされたフラグのことを**セマフォ**という．

一度に一つのプロセスしか実行できない一連の命令の部分を**クリティカル領域**という．一度に一つのプロセスしかクリティカル領域を実行できないようにするのは**相互排除**として知られている．



#### デッドロック

**デッドロック**とは2つ以上のプロセスが他者に割り付けられた資源を待って処理が進められない状態をいう．

デッドロックは次の3条件が**揃った**場合に，発生する．

1. 共有不能な資源を巡って競合がある．
2. 資源は部分的に要求できる．つまりある資源を受け取ったプロセスは，後に追加の要求を出せる．
3. いったん資源を割り当てられたならば強制的に取り上げることはできない．

これらの解消法はそれぞれ以下のようになる．

1. 共有不能な資源を共有可能にする．プリンタへの接続を要求している多数のプロセスがある場合，その要求を承諾はするがプリンタのデバイスドライバにプロセスを接続せず，マスストレージに格納するデバイスドライバにプロセスを接続する．こうすることで各プロセスがプリンタにアクセスしているかのように印字を実行できる．プリンタが利用可能になるとオペレーティングシステムがマスストレージからデータをプリンタに送信する．

   このように複数のプリンタがあるかのように見せることができる．都合の良い時まで入力データを保持しておく技法を**スプーリング**という．

2. 各プロセスがすべて一度に要求しなければならないとすればよい．

3. デッドロックが発生したらそれを検出して強制的に割り当てた資源を取り上げる．オペレーティングシステムではこれはプロセステーブルが満杯になってデッドロックが発生した場合にプロセスの一部を削除してプロセステーブルに余裕を与え残りのプロセスが作業を続行できるようにする．



### オペレーティングシステムのセキュリティ

#### 外部からの攻撃

システム管理者は通常のユーザには禁止されている様々な保守作業を実行できる．システム管理者はコンピュータプロセス中のプロセスでの動作を監視し，故意または不注意による破壊的動作を検出することに努める．これを監視するために**監査ソフトウェア**と呼ばれる多くのユーティリティソフトウェアが開発されてきた．以下の攻撃を検知する．

**攻撃**

例として権限のない(パスワードを知らない)ユーザがコンピュータへのアクセスを行おうとする，度重なるログインの試み．



監査ソフトウェアが検出するものはこれだけでなく**スニッフィングソフトウェア**がある．

**スニッフィングソフトウェア**とはコンピュータシステムに潜んで正規のユーザの動作の記録を取り，不正なユーザにその記録を報告するものである．例としてはオペレーティングシステムのログイン手続きをシミュレートするプログラムがある．

対処法としてコンピュータ設備を持つ組織ではユーザが守らねばならない規則と責任をまとめたセキュリティポリシーを徹底する．



#### 内部からの攻撃

悪意のある権限を持ったユーザがコンピュータシステムのアクセスに成功した後には探索を行う．興味のある情報を探したり，破壊ソフトウェアを仕掛ける場所を発見したりする．

攻撃の例としては

- メモリマネージャを騙して割り付けられた範囲外のメインメモリセルにプロセスがアクセスできるようにする．

- ファイルマネージャを騙してアクセスが禁止されているファイルを取り出そうとする．

- プロセスが追加のメモリを欲した時に，オペレーティングシステムの承認なしにメモリの上限を含むレジスタの値を増やして，そのまま追加のメモリ領域を使用してしまう．

対処法としてマルチプログラミングシステム用のCPUは2つの**権限レベル**(特権モード，非特権モード)でのいずれかで動作するように設定されている．特権モードでは全てのマシン語を実行できるようになっている．特権モードでだけ実行できる命令を**特権命令**と呼ぶ．命令の典型的な例としては，メモリの限界を示すレジスタの内容の変更やCPUの現在の権限モードを変更する命令などが含まれる．

CPUが非特権モードにあるのに特権命令を実行しようとすると割り込みが発生する．この割り込みは，CPUを特権モードに変換して，オペレーティングシステム内の割り込みハンドラに制御を渡す．



## 4. ネットワークとインターネット

### ネットワークの基礎

#### 分散システム

**クラスタコンピューティング**

多くの独立したコンピュータが密接に結合して作業を進めることで大型コンピュータに匹敵する計算能力やサービスを提供する分散システム．

- 利点

  スパコンより安価．高い可用性(1台故障しても問題ない)．**負荷分散システム**としての役割．



**グリッドコンピューティング**

ゆるく結びついたマシンが大規模な作業を実行するシステム．家庭や職場にあるPCが自発的に空き時間に計算能力を提供することでグリッドを構築する．



**クラウドコンピューティング**

ネットワーク上で共用される極めて多くのコンピュータを顧客の要望に応じて割り当てる方式の分散システム．



#### プロトコル

**CSMA/CD**

メッセージを他のメッセージがバス上にないことを見計らって送信を開始する．他のマシンが同時に通信を始めたならば，どちらのマシンも衝突を検出してそれぞれランダムに選んだ休止時間を挟んで再度送信を試みること．

- 欠点

  - 全てのマシンがセントラルAPを通じて通信する無線スター型ネットワークとは相容れない．マシンが自分の送信と他のマシンの送信が衝突したことを検出できないため．

  - **隠れ端末問題**によるため．

    **隠れ端末問題**とはマシンそれぞれはセントラルAPと交信できるものの，異なるマシンからの信号は，障害物や距離などが原因で妨害されてしまうから．

    - 隠れ端末問題の対処法として無線ネットワークは**CSMA/CA**を採用している．**CSMA/CA**は衝突を検出するのではなく衝突を回避する方法を採用している．

      衝突回避の最も一般的なアプローチは送信する機会を待っているマシンを優先するという考えに基づく．あるマシンがメッセージを送信する必要になってその時，通信チャネルが空いていたとしてもすぐには送信せず，他のマシンが使用しないことを確認してから送信する．



### インターネット

#### インターネットアドレッシング

システムの各コンピュータに一意なアドレスを割り当てるインターネット全域にわたるアドレスシステムが必要になる．このようなアドレスを**IPアドレス**という．

**IPアドレス**

インターネット全域にわたるコンピュータの一意なアドレス．

ニーモニックアドレスは人間にとっては便利であるが，メッセージはIPアドレスによってインターネット中を転送されていく．人間のユーザがメッセージを送る際に，送り先としてニーモニックアドレスで指定したなら，インターネット中のソフトウェアがメッセージを送信する前にそのニーモニックアドレスをIPアドレスに変換しなければならない．この返還は多くのサーバの力を借りて実行される．これらのサーバは**ネームサーバ**とよばれ，クライアントに対してアドレス変換サービスを提供している．これらを全体で**ドメインネームシステム**と呼び，DNSを用いて変換を行うプロセスは，**DNS ルックアップ**と呼ばれる．



#### インターネットアプリケーション

**電子メール**

電子メールサービスを提供するために，ドメイン内の特定のマシンが**メールサーバ**としての役割を担う．

**SMTP**

メールサーバ間でメールを転送したり，ローカルマシンからメールサーバへ新しいメッセージを送信したりするときに使用されるプロトコル．SMTPはもともとASCIIのやりとりを想定して作られたのでASCIIにないデータを扱うために**MINE**が開発された．

**ファイル転送プロトコル(FTP)**

インターネット間でファイルを転送するクライアントサーバプロトコル．



### ワールドワイドウェブ





### インターネットプロトコル

#### インターネットソフトウェアの階層的アプローチ

OSI7階層みたいなもん(しかしこれは後発の概念)．**アプリケーション層**，**トランスポート層**，**ネットワーク層**，**リンク層**がある．

**アプリケーション層**はそれぞれの作業を遂行するのにインターネット通信を使用するクライアントとサーバのようなソフトウェアユニットから構成される．

**トランスポート層**はアプリケーション層から受け取ったメッセージがインターネット中で転送するのに適切な形式になるようにすること．

**ネットワーク層**はインターネット上のパケット経路に沿って，どの方向にパケットを送信するのかを決定する．ネットワーク層はルータの転送表を保持していてそれに基づいてパケットの転送先を決定する．

**リンク層**はパケットの転送に責任を負う．コンピュータが接続されているネットワークに特有の詳細を扱う必要がある．(CSMA/CDを選ぶかCSMA/CAを選ぶかとか)



#### TCP/IPプロトコルスイート

**TCPとUDPの違い**

1. TCPでは受信側のトランスポート層に，これからメッセージを送る旨のトランスポート層独自のメッセージを送信する．その上で，そのメッセージの受信確認の応答を待ってから，アプリケーション層のメッセージを送信する．このようにしているのでTCPに基づくトランスポート層ではメッセージ送信前に接続を確立していると言われる．

   UDPではこのようなことはせず，単に与えられたアドレスにメッセージを送信するだけである．

2. TCPとUDPのもう一つ相違点は，送信側と受信側のトランスポート層が肯定応答を通して協働し，パケット送信を確実にすること．UDPにはこれがない．

3. TCPには**フロー制御**と**輻輳制御**の両方を提供していることにある．

   **フロー制御**

   メッセージの送信元のトランスポート層がセグメントを送出する転送レートを下げることで，受信側のトランスポートそうが圧倒されて機能不全に陥るのを防ぐこと．

   **輻輳制御**

   メッセージの送信元のトランスポート層が転送レートを調整して送信側と受信側の間の混雑を緩和する．



IPはネットワーク層に割り当てられた作業を実装するためのインターネット標準となっている．この作業は**転送**と**経路制御**から構成される．

**転送**

インターネットを通じてパケットを中継すること．

- ポップカウンタ

  パケットがインターネット中を転送される回数の上限を定めている．IPネットワーク層がパケットを転送するごとにパケットのポップカウンタを1つ下げる．これにより，パケットが無限に回遊することを防ぐことができる．

**経路制御**

状況の変化に応じてネットワーク層の転送表を更新すること．



### ネットワークとインターネットにおけるセキュリティ

#### 攻撃の形式

**ウイルス**

マシン上にあるプログラムに潜り込むことで感染するソフトウェア．通常はコンピュータ中の他のプログラムに自分自身のコピーを転送する以外ほとんど何もしない．しかしながらデータや他のプログラムを破壊するものも他にはある．

**ワーム**

ネットワーク中で自分自身を転送する自律的なプログラムである．自分自身を爆発的に複製することでネットワークに高負荷をかける．

**トロイの木馬**

前もって決められた期日などにイベントが発生しそれによって生起されるまでじっとしている．電子メールなどの添付ファイルに入っていることがあり不用意にファイルを開いてはならない．

**スパイウェア(スニッフィングソフトウェア)**

寄生するコンピュータ上で行われていることを記録し攻撃者に報告する．

**フィッシング**

直接尋ねることで明示的に情報を得ようとする方法．正当な情報の要求であるかのように偽った電子メールを送りつけてくる．

**サービス拒否攻撃(DoS)**

多量のメッセージを送りつけてくることでコンピュータに高負荷をかける攻撃．



#### 保護と予防

**ファイアウォール**

ネットワーク中のある点を通過するデータにフィルタをかけるプログラム．

一定の送り先のアドレスへの送信メッセージを阻止したり問題があると判断された送信元からのメッセージの流入を阻止したりする役割がある．



### 暗号

**HTTPS**

金融などで利用されている．HTTPSの核心部分は**セキュアソケットレイヤ(SSL)**とよばれるプロトコルシステムにある．

**公開鍵暗号**

公開鍵暗号とは**鍵**と呼ばれる2つの値を使用する．鍵の一方は**公開鍵**でメッセージの暗号化に使用される．もう一方は**秘密鍵**でメッセージの復号に使用される．メッセージの受取人は正規のメッセージ送信者に公開鍵を渡す．この時，メッセージの受取人は秘密鍵を厳重に保護し，外部に漏れないようにする．

**公開鍵暗号の問題点**

本当に正しい送信者であるかどうかは担保してくれない．

解決する方法として**認証局**が挙げられる．

認証局の役割は**公開鍵とその配布者の正確なリストを保守すること**にある．認証局はサーバとして機能して，信頼できる公開鍵情報を**公開鍵証明書**として知られるパッケージとしてクライアントに提供する．

公開鍵暗号は**認証**にも利用される．認証とはメッセージの著者を確認することである．秘密鍵はその人物しか知り得ない．したがって秘密鍵の保持者はデジタル署名と呼ばれるビットパターンを生成できる．この署名をメッセージに添付することで送信者はメッセージが真正なものであると受信者に認められる．



## 5. アルゴリズム

### アルゴリズムの形式的定義

アルゴリズムとは，停止するプロセスを定義する曖昧さがなく実行可能なステップの順序集合である．



```整列済みリストに対する逐次探索
procedure Search(List, TargetValue)
if(list is empty)
	then
		(tell Search was failed)
	else
		(choose first element of List as TestEntry;
		while(TestValue > TestEntry and elements rest in List)
			do(choose next elements as TestEntry);
		if(TargetValue = TestEntry)
			then(Search was successed)
			else(Search was failed)
		)end if
```



**挿入法によるアルゴリズム**

```挿入法アルゴリズム
procedure Sort(List)
N ← 2;
while(Nの値がListの長さを越えない) do
	(ListのN番目の要素をピボット要素として選択する;
	ピボット要素を一時的な場所に移動し，リストに隙間を作る;
	while(隙間より上に名前がある，かつその名前がピボット要素より大きい)
		do(隙間より上の名前を隙間までずらし，その名前の上に隙間が来るようにする)
	ピボット要素をリストの隙間に移動する;
	N ← N + 1
```







## 6. プログラミング言語

高レベルの基本命令で表現されたプログラムをマシン言語のようなプログラムに翻訳する**トランスレータ**が必要になる．このような変換プログラムを**コンパイラ**と呼ぶようになった．

コンパイラとは異なる手段として**インタプリタ**と呼ばれるプログラムも出現した．将来の変換のために前もって変換しておくコンパイラとは異なり，命令を変換しながら実行する．



### 歴史的展望

#### 初期世代

**第3世代のプログラミング言語**

低レベルのアセンブリ言語よりもソフトウェア開発を容易にするプログラミング言語の開発に取り組んだ結果生まれたもの．

それ以前の言語に比べて基本命令が**高レベル**であること，**マシン独立**である．



#### マシン独立

**マシン独立**

プログラミング言語において特定のマシンの性質に依存しないこと．



#### プログラミングパラダイム

- **手続き型パラダイム(命令型パラダイム)**

問題を解くアルゴリズムを発見した上でそのアルゴリズムを一連の命令列として表現するプログラミングプロセスとして採用すること．

- **宣言型パラダイム**

問題解決のアルゴリズムではなく解くべき問題の厳密な記述を開発すること．問題を解く汎用問題解決アルゴリズムを適用する．

これが**論理プログラミング**の出現へと結実した．

- **関数型パラダイム**

プログラムは入力を入力を受け取り出力を生じるもの．

- **オブジェクト指向パラダイム**



### 伝統的なプログラミング概念

#### 変数とデータ型

**変数**

高レベルプログラミング言語においてメインメモリ中の場所を数値アドレスではなく記述的な名前で参照できるもの．

**データ型**

データ項目がどのように符号化されているか，そのデータ上でどのような演算が実行されるかを含む．

**基本データ型**

整数型を表すintや文字を表すcharといったプログラミング言語に基本型として含まれるデータ型のこと．



#### データ構造

**データ構造とは**データの概念的な配置である．

**配列**

一次元のリストや高次元の表といった**同じ型**の要素のブロックのこと．

**構造体型**

異なる要素は異なる型を取ることができるデータ構造．



#### 制御文

**制御文**

プログラムの実行順序を変えるもの．

**構造化プログラミング**

言語の制御文を適切にしようとすることを組み込んだ設計方法論．



### 手続きユニット

#### 引数

手続き中の汎用の名前のことを**引数**と呼ぶ．

**仮引数**

手続き中で使われる引数．

**実引数**

手続きが適用された時に仮引数に厳密な意味を与える引数．

**値渡し**

実引数の複製を作成してそれを手続きに渡すもの．

呼び出し側のプログラム中のデータをずさんな設計の手続きによって誤って変更されてしまうことから保護する．

**参照渡し**

呼び出しプログラムユニット中の実引数のアドレスを手続きに伝えることで手続きが実引数に直接アクセスできるようにすること．

引数を参照渡しすることは呼び出し側の環境にあるデータを手続きが変更することを許している．



#### 関数

**イベント駆動型ソフトウェアシステム**

明示的な要求ではなく，イベントによって手続きが起動されるソフトウェアシステムのこと．



### 言語の実装

#### 翻訳プロセス

プログラムをある言語から他の言語へと変換するプロセスのことを**翻訳**という．元の形式は**ソースプログラム**であり，翻訳されたものは**オブジェクトプログラム**である．

翻訳のプロセスは**字句解析**，**構文解析**，**コード生成**から構成される．

字句解析はソースコードを読み，どの記号のグループが**トークン**を表しているかを識別し，それらのトークンを数値，単語，算術演算子へと分類する．

構文解析については**文法**(プログラミング言語の構文を定義する規則の集合)に基づいている．

コード生成については構文解析器が認識した文を実装するマシン言語の命令を構成するプロセスである．



### オブジェクト指向プログラミング

#### クラスとオブジェクト

**クラス**

複数のオブジェクトに共通する性質が記述されたテンプレートのこと．

**インスタンス(オブジェクト)**

あるクラスから構成されたオブジェクトのこと．



#### オブジェクト指向の用語

**コンストラクタ**

オブジェクトがクラスから構成されるときに自動的に実行されるメソッド．

**ポリモーフィズム**

オブジェクトごとにメッセージの解釈を違えること．

**情報隠蔽**

オブジェクトの内部的な性質へのアクセスを制限すること．



## 7. ソフトウェア工学

ソフトウェアのライフサイクルは開発のあと使用と保守を繰り返すもの．



### 伝統的な開発フェーズ

**要求分析->設計->実装->テスト**とされることが多い．



### ソフトウェア工学の方法論

- **ウォーターフォールモデル**

  設計を開始する前にシステムの要求仕様全体を完了しており同様に実装の前に設計も完了しているもの．

- **インクリメンタルモデル**

  ウォーターフォールモデルでは対応できない開発に対応．最初に機能の制限を加えた単純版をを構築して，これをテストし少しづつ機能を足してはテストしていく．

- **反復モデル**

  インクリメンタルモデルと類似している．インクリメンタルモデルがある版からある版へと拡張していくのに対し，反復モデルでは各版を詳細にしていく概念を含んでいる．

- **アジャイルメソッド**

  インクリメンタルに手早く実装をまとめて，要求仕様の変更にも手早く対応することを強調している．

  - **エクストリームプログラミング(XP)**

    共同体的な作業空間で1ダース未満のメンバーからなるチームによって開発される．要求，設計，実装，テストといったことを日々行い，インクリメンタルに開発される．



### モジュール性

一般的にソフトウェアは**モジュール**と呼ばれるそれぞれがソフトウェアの動作の一部を受け持つ管理可能な単位いに分割しなければならない．

#### モジュールによる実装

手続きに名前をつけて各呼び出しを図的に示したものに**構造チャート**がある．



#### 結合度

モジュール化されたシステムを設計する際の目標はモジュール間の独立性を最大化することである．モジュール間の結合度は複数の形式で出現する．

- **制御結合**

  手続き呼び出しのように，実行制御を1つのモジュールから他のモジュールに渡すときに発生する．

- **データ結合**

  モジュール間でのデータの共有度を示している．

データを引数として明示的に渡すのとは対照的に**大域データ**の形式でシステム中のモジュールで自動的に利用可能になるデータ項目がある．大域データの使用には注意を要する．



#### 凝集度

モジュール間の結合度を最小にするのと同じように，各モジュール内の結合度を最大化することも重要である．**凝集度**とはモジュールの内部要素の関連の強さを表している．

- **論理的凝集**

  凝集度の弱い形式．モジュール内の構成要素が論理的に類似の動作を行うという理由で，同じモジュールに配置された場合を指す．

- **機能的凝集**

  凝集度の強い形式．モジュール内の全ての要素が，ある1つの動作を実行することでまとまっている場合を指す．



#### 情報隠蔽

優れたモジュール化が施された設計の基礎となるのは，**情報隠蔽**の概念である．情報隠蔽とは，情報をソフトウェアシステムの特定の部分に制限することである．

情報隠蔽の要点は，モジュールの動作が他のモジュールに不必要に依存したり，不必要に影響を及ぼしたりしないようにするということ．

情報隠蔽のために，2つの目標がある．モジュールは他のモジュールがその内部情報にアクセスしなくてもいいように設計しなければならない．

- 設計目標

  結合度の最小化と凝集度の最大化．

- 実装目標

  局所変数の使用，カプセル化の適用，よく定義された制御構造．



#### コンポーネント

オブジェクトはより一般的な概念である**コンポーネント**の特殊な場合である．コンポーネントとは定義により，ソフトウェアの再利用可能なユニットのことである．

コンポーネントは計算資源の制約のあるスマートフォンシステムにおいて威力を発揮する．



### ツール

**データフロー図**

システム中をデータがどのように移動していくかを調べることでデータの形式が変更される時点やデータの経路が合併したり分割したりする自転が特定できる．

データフロー図は分析段階で提案システムの理解を得るためにも有用．



**データディクショナリ**

ソフトウェアシステム全体を通して出現するデータ項目についての情報を蓄える中心的な貯蔵庫の役割を果たす．

ソフトウェアシステムの利害関係者と，利害関係者の要求を要求仕様へと変換するソフトウェア技術者との間のコミュニケーションを改善すること．

システムに統一性を持たせること．



### 品質保証

#### ソフトウェアテスト

**パレートの原理**

ソフトウェア工学におけるパレートの原理とは集中した部分に努力を傾注することによって結果を急速に向上させることができるといったもの．

**基礎パステスト**

ソフトウェア中の命令が少なくとも1回は実行されるようにテストデータの集合を作成するものである．

パレートの原理と基礎パステストにはテストするソフトウェアの内部構造の知識が必要になる．したがってそれらは**グラスボックステスト**の範疇に入る．つまりソフトウェアをテストする技術者はソフトウェアの内部構造を知っていてテストを設計する際には，その知識を用いる．

それと対照的なのは**ブラックボックステスト**と呼ばれる範疇に入るもので，ソフトウェアの内部構造についての知識にテストが依存しない．

ブラックボックステストの好例は**境界値分析法**がある．ソフトウェアが同じように実行される同値類と呼ばれるデータの範囲を特定してその範囲の境界に近いデータでソフトウェアをテストするもの．同値類を同定することでテストケースの数を最小化する．

ブラックボックステストの範疇に入るもう1つの方法論に，**ベータテスト**がある．ベータテストでは製品の最終版を確立して市場にリリースする前にソフトウェアの予備版を潜在的なユーザの一部に配布して現実の状況でソフトウェアがどのように動作するかを学び取ろうとするもの．開発者が類似のテストを行うことは**アルファテスト**と呼ばれる．



### ドキュメンテーション

ソフトウェアのドキュメンテーションは3つの目的があり，それぞれ次のように分類される文書を作成する重要なトピックである．

- **ユーザドキュメンテーション**

  目的は，ソフトウェアの機能を説明してどのように使用するかを記述すること．

- **システムドキュメンテーション**

  ソフトウェアの内部構造を記述することであり，ソフトウェアライフサイクルの後半での保守作業に資するためのもの．

- **技術文書**

  ソフトウェアをどのようにインストールしてサービスするかを記述するもの．



## 8. データ抽象

### 基本データ構造

#### 配列

一次元のリストや行と列を持つ2次元の表，あるいはもっと高次元の表といった同じ型の要素のブロック．

#### 構造体

すべてのデータ項目が同じ型でなければならに配列とは対照的に，**構造体型**では，異なる要素は異なる型を取ることができる．ブロック中の項目は，**構成要素**と呼ばれる．Cにおける構造体内部の要素は**フィールド**と呼ばれる．



#### リスト，スタック，キュー

**リスト**とは一列に並べられた要素の集まり．リスト先頭の要素を**頭部(head)**と呼び，残りのリストの**尾部(tail)**と呼ぶ．

**スタック**とは，headでのみその要素を挿入したり削除したりすることのできるリストのことを言う．スタックの頭部のことを**トップ**，尾部のことを**ボトム**という．この構造から**後入れ先出し**の構造として知られている．

**キュー**

頭部からだけ要素を取り除けて新しい要素は尾部の後ろにだけ挿入できるリスト．**先入れ先出し**の構造になっている．



#### 木

一旦，分岐した組織は下部で合併することはない．2つの親を持たない．木中の各位置を**節点(node)**と呼ぶ．最上位の節点は，**根(node)**と呼ばれる．もう一方の端にある節点を**葉(leaf)**と呼ぶ．

直近の子孫を**子**，直近の祖先を**親(root)**と呼ぶ．各親節点が2より多くの子を持たない木を**二分木(binary tree)**と呼ぶ．木中のある任意の節点を取り出してその節点とその節点より下の節点は木構造になっておりそれを**部分木(subtree)**と呼ぶ．したがって各子節点はその子の親より下の部分木の根である．そのような部分木は親からの**枝(branch)**であるという．



#### 静的構造と動的構造

抽象データ構造を構成する際の重要な区別は，シミュレートする構造が静的か動的か．リストがずっと固定のサイズなのか，追加や削除が行われたりはしないか．



#### ポインタ

コンピュータのメインメモリのセルは数値アドレスによって識別されている．それらのアドレスはそれ自身を符号化してメモリセルの中に格納できる．**ポインタ**はそのような符号化されたアドレスを含むストレージ領域のことである．



### データ構造の実装

#### 配列と構造体の格納

**配列**

24時間のデータを扱う場合，24個の連続したメモリセルに一次元配列として割り当てる．

二次元配列において，

 |    行1     | |    行2     | |    行3     |

というように格納されていく場合を**行優先順**を使用するといい，列ごとに格納する場合を，**列優先順**を使用するという．



**構造体**

各構成要素が必要とするメモリセルの数が固定であるならば連続したセルのブロックの中に構造体を格納できる．



#### リストを格納する

リスト全体がメモリブロックの連続したメモリセルに順序よく格納されているような構成を**連続リスト**という．

リストの各ブロックの最後のセルを次のブロックへのポインタとすると，各ブロックはメモリの中に散在することになる．この連結システムを**連結リスト**と呼ぶ．連結リストの実現方法として，リストの頭部を持つ**ヘッドポインタ**，リストの最後であることを示すため**NILポインタ**を使用する．



#### スタックとキューを格納する

スタックに新しい要素を追加するためにはスタックポインタをスタックのトップの次の空間を指すように調整した上で，新しい要素をその場所に置く．スタックからポップするにはスタックポインタが指しているデータを読みだしてからスタックポインタが直前の要素を指すようにする．

キューの伝統的な実装法も同様である．**ヘッドポインタ**と**テールポインタ**を利用する．追加するときはテールポインタが後方に移動する．要素を取り出す時は，ヘッドポインタを後方に移動させる．しかしながらこの場合，エンキューとデキューを繰り返すとキューの領域がメモリ内部を移動する．そこで，循環キューを利用する．ブロックの最初と最後のセルを指定しておき，ヘッドポインタとテールポインタで指しておく．その指定したセルの範囲内で挿入と削除を行う．



#### 二分木を格納する

データを持つセル | 左の子へのポインタ | 右の子へのポインタ

連続リストで二分木を構成する場合もある．その場合は，

|    1     |         2 3         |       4 5 6 7       |
| :------: | :-----------------: | :-----------------: |
| 根の節点 | 木の第2レベルの節点 | 木の第3レベルの節点 |

というようにメモリセルを割り当てて行けば良い．



#### 動的なデータ構造に対する問題と解決法

- **ガベージコレクション**

  動的なデータ構造が成長したり収縮したりするにつれて，ストレージ領域も使用されたり解放されたりする．使われなくなったストレージ領域を将来の使用のために回収するプロセスのことを**ガベージプロセス**という．

- **メモリリーク**

  ガベージコレクションがストレージ領域の回収にした場合，利用できる領域が徐々に少なくなる．



#### 抽象データ型

演算の定義を含むデータ型のことを，**抽象データ型**という．



### クラスとオブジェクト

オブジェクト指向パラダイムでは作業を達成するために相互作用するオブジェクトと呼ばれる単位からシステムが構成される．オブジェクトはクラスとして知られるテンプレートにより記述される．



### マシン語におけるポインタ

**即値アドレッシング**

オペランドフィールドがデータを明示的に含んでいるもの．

**直接アドレッシング**

オペランドフィールドがデータのアドレスを含んでいるもの．

**間接アドレッシング**

オペランドフィールドはデータのアドレスのアドレスを含んでいるもの．



## 9. データベースシステム

### データベースの基礎

#### スキーマの役割

ユーザ毎にデータベース内の異なる情報にアクセスできるようにするために，データベースシステムはスキーマやサブスキーマを利用することが多い．

**スキーマ**とはデータベースの全体構造の記述であり，データベースソフトウェアがデータベースを保守するのに使用する．**サブスキーマ**とは特定のユーザにとって必要な部分だけの記述である．



#### データベース管理システム

ユーザインタフェースと実際のデータ操作を2つの層へとグループ化する．こうしてアプリケーションソフトウェアが直接データベースシステムを操作するわけではない．

アプリケーションソフトウェアが直接データベースを操作するわけではない．データベースの実際の変更を行うのは**データベース管理システム(DBMS)**である．

DBMSとアプリケーションソフトウェアを分離する利点の一つは，**抽象化ツールを構成して使用できること**．データベースがどのように格納されているかの詳細がDBMSの中に格納されているならば，アプリケーションソフトウェアの設計を大いに単純化できるため．

優れた設計のDBMSを利用することでアプリケーションソフトウェアはデータベースが1台のマシン上に格納されているのか，あるいは**分散データベース**としてネットワーク上の複数のマシン上に分散して格納されているのかを意識する必要がなくなる．

アプリケーションソフトウェアをDBMSから分離する2つ目の利点は**データベースへのアクセスを制御する手段が生まれる**というところにある．DBMSにデータベースの全てを委ねることによってさまざまなサブスキーマによって課せられる制限をDBMSが実装できる．DBMSは，全体のデータベーススキーマを内部的に使用しつつ，各ユーザのアプリケーションソフトウェアの実行をユーザのサブスキーマが記述する制限内に留められる．

ユーザインタフェースと実際のデータ操作を2つの層に分離するもう一つの理由は，**データの独立性**を達成するためである．

**データの独立性**

アプリケーションソフトウェアを変更することなくデータベースの構成を変更する性質のこと．



**分散データベース**

ネットワーク上の複数のマシン上に分散して格納されているデータベース．コンピュータが発展するにつれてネットワークシステムがデータベースを包含するようになったもの．検索の時間を短縮するために同一のデータをそれぞれが持つこともあるがこの場合，変更などの同期を取る必要がある．



#### データベースモデル

データベース管理システムはデータベースの内部構造を隠蔽してデータベースのユーザには情報が扱いやすい形式でデータベース中に格納されているかのように見せることを可能にしている．この概念的外観のことを**データベースモデル**という．



### 関係モデル

関係データベースモデルは**関係**と呼ばれる長方形の表の中に格納されているものとして描き出す．

関係中の行は**タプル**，関係の列は**属性**と言われる．



### オブジェクト指向データベース

**オブジェクト指向データベース**

関係を反映するよに連結されたオブジェクトから構成されるもの．

オブジェクト指向データベース中のオブジェクト間の連結は，通常DBMSにより管理される．すなわち，どのように連結が実装されているかをアプリケーションソフトウェアを書くプログラマは関心を持つ必要がない．

オブジェクト指向DBMSのもう一つの役割は，委託されたオブジェクトに恒久的な格納場所を提供することである．一見当たり前だが通常のオブジェクト指向の扱いとは異なる考え方である．一般にオブジェクト指向プログラムを実行するとオブジェクトは，プログラムの実行に伴って生成されてプログラムの終了と同時に破棄される．しかし生成されてデータベースに加えられたオブジェクトはそのオブジェクトを生成したプログラムの実行終了後も保存されなければならない．そのようなオブジェクトは，**永続的**であると言われる．



**オブジェクト指向アプローチが関係アプローチより優れていると考える人の主張**

- オブジェクト指向アプローチではソフトウェアシステム全体(アプリケーションソフトウェア，DBMS，データベースそのもの)を同じパラダイムで設計できるというもの．
- 関係データベース中に従業員の氏名を格納する問題を考えるとき，氏名全体を関係中の1つの属性として格納してしまうと姓だけによる問合せがうまくできない．しかしながら氏名を名，ミドルネーム，姓と個別の属性に分けて格納したとしても，属性の数をいくつにするかが問題になる(名前が4つの構造に分かれていることもあるため)．オブジェクト指向データベースでは，これらの問題は従業員の氏名を保持するオブジェクトの中に隠蔽できる．



### データベースの完全性を保つ

トランザクションのすべてのステップがログに記録された時点を**コミット時点**と呼ぶ．これは必要に迫られた時にトランザクションを再構成するために必要な情報が揃う時点のことである．

トランザクションがコミット時点に到達する前に問題が生じたときDBMSは，完了できずに中途半端に実行されているトランザクションの最中にいることがある．この場合，ログはトランザクションによって実際に実行された動作の**ロールバック**に使用される．

ロールバックにおいて，あるトランザクションがデータを更新はしたもののそのトランザクションで停止した．別のトランザクションがそのデータを使って処理を行おうとした．この時，ロールバックするのに，別のトランザクションもロールバックしなければならなくなる．これを**波及ロールバック**という．



#### ロック法

**不正確な合計問題**(1つのトランザクションがある銀行口座から他の口座へ送金している最中に別のトランザクションが銀行の預金残高の総計の計算を試みたときに発生)   や   **遺失更新問題**(一つのトランザクションが口座残高を読み取り，しかし新しい残高を計算し終えないうちにもう一つのトランザクションが現在の残高を読み取るとどちらのトランザクションも同じ初期残高に基づいて引き落としを行うことになってしまうこと)  に対処するために，DBMSは新しいトランザクションをそれ以前に生成されたトランザクションが完了するまで待ち行列にいれることで，トランザクションを一度に1つずつ実行して完了させるようにしている．

したがって，ほとんどの大規模データベース管理システムはプロセスの並行実行を調整するマルチプログラミングオペレーションシステムと同じようにしてトランザクション間のタイムシェアリングを管理するスケジューラを含んでいる．

これらのスケジューラには不正確な合計問題や遺失更新問題のような異常からシステムを守るために，**ロックプロトコル**が組み込まれている．

**ロックプロトコル**

現在あるトランザクションによって使用されているデータベース内の項目に印をつけるもの．2つの**共有ロック**と**排他ロック**が一般的．

トランザクションがデータ項目を変更しないのであれば，そのトランザクションは共有アクセスを要求する．つまり他のトランザクションにもそのデータを見ること許す．しかし，そのトランザクションが値を変更するのであれば排他的なアクセスを要求して，そのトランザクションだけがデータにアクセスできるように確保しなければならない．

2つのトランザクションが同じ2つのデータ項目に対して排他的アクセスをを要求してそれぞれ片方ずつの排他的アクセスを獲得してもう片方のアクセスを待つ状態になると，お互いの進行をブロックしてデッドロックに陥ってしまう．そのようなデッドロックを避けるために，データベース管理システムでは古いトランザクションに優先権を与えるものがある．このプロトコルを**負傷待機プロトコル**(古いトランザクションは新しいトランザクションを傷つけ，新しいトランザクションは古いトランザクションに譲って待つ)という．



### 伝統的ファイル構造

#### 順編成ファイル

始めから終わりまで情報が1つの長い列になっているかのように順番にアクセスされるファイルのことを**順編成ファイル**という．

- 利点

  ファイルのエントリが格納された順に処理されるデータを格納するには理想的である．

- 欠点

  ファイル中のレコードを不規則な順序で検索しなければならないような場合には効率が悪くなる．



#### 索引ファイル

求める論理レコードの場所を即座に特定する手段として，ファイルの索引を使用するシステムを**索引ファイル**と呼ぶ．

ファイルの索引は，ファイル中のキーとそのキーをもつレコードがどこに格納されているかを示すエントリのリストを含んでいる．

ファイルの索引は，通常索引されるファイルと同じマスストレージ装置上の別ファイルとして格納されている．索引はファイル中のレコードが必要になったときにアクセスが容易になるように通常ファイル中の処理が開始される前にメインメモリに転送される．



#### ハッシュファイル

ハッシュ法は時間のかかる索引の保守といったオーバーヘッドなしにアクセスを提供するもの．

ハッシュシステムはデータの格納空間を**バケット**と呼ばれる複数のセクションに分割する．各セクションは複数のレコードを保持できる．キーの値をバケット番号へと変換するアルゴリズムによってレコードをバケットへ配置する．

ハッシュ法は，マスストレージからデータを取り出す手段に使われるだけでなくメインメモリ中に格納されている大きなデータブロックから項目を取り出す手段としても使用される．

**ハッシュファイル**

**マスストレージ**中のストレージ構造にハッシュ法を適用したもの．

**ハッシュテーブル**

**メインメモリ**中のストレージ構造にハッシュ法を適用したもの．



### データマイニング

**データマイニング**はデータの集合にパターンを発見する技法から構成される．



**データウェアハウス**

静的なデータの集合のこと．



#### データマイニングの形式

- **クラス記述**

  与えられたデータ項目のグループを特徴付ける性質を特定すること．

- **クラス分類**

  2つのグループへ分割する性質を特定すること．

- **クラスタ分析**

  クラスを発見すること．グループ化を可能とするようなデータ項目の性質を発見する試み．

- **相関分析**

  データグループ間の連結を発見しようとすること．

- **外れ値分析**

  標準に当てはまらないデータエントリの特定を試みること．

- **時系列パターン分析**

  時間とともに変化する振る舞いのパターンの特定を試みること．

**データキューブ**

データを複数の視点から見ること．



## 11. 人工知能

### 知能とマシン

#### チューリングテスト

質問者と呼ばれる人間が実験対象が人間であるかマシンであるかを告げられずにタイプライタシステムを通じて対象と対話するものである．この環境で質問者がマシンを人間と区別できなければマシンは知的に振る舞ったと宣言される．



### 認識

#### 画像理解

**画像処理**

画像の特徴を識別するプロセス

**画像分析**

それらの特徴が何を表しているかを見るプロセス



#### 画像処理のプロセス

- エッジ強調

  数理技法を適用して画像中の領域の境界を検出するプロセス

- 領域発見

  画像中に，明るさ，色，質感といった共通の性質を特定するプロセス

- 平滑化

  画像の傷を取り除くプロセス



#### 言語処理

自然言語の文の意味を解きほぐすには，複数レベルの分析が必要．

- **構文解析**

  主語などの特定がここで行われる．

- **意味解析**

  文の各単語の意味的役割を特定する作業を行う．

- **文脈解析**

  理解のプロセスに文脈が持ち込まれる．



自然言語処理のもう一つの研究分野は個々の文ではなく文書全体に関するものである．すなわち**情報抽出**と**情報検索**である．



**情報検索**

手元にあるトピックに関連するドキュメントを特定すること．

**情報抽出**

他のアプリケーションでも使用できるような形式で文書から情報を抽出する作業のことをいう．これは特定の質問に対する回答をみつける場合もあれば，あとで質問に答えられるように情報をある形式で記録しておくことを意味することもある．そのような形式**フレーム**として知られるものもあるがそれは特定のものが記録されるテンプレートである．

情報抽出器が情報を抽出するもう一つの形式は，**意味ネット**として知られるものである．

**意味ネット**

ポインタによってデータ項目の関連を示す大規模な連結データ構造である．



### 推論

#### プロダクションシステム

マシン中に推論能力を持たせることは研究課題となってきた．その研究成果に，共通の性質を持つ推論問題の大きなクラスが存在するということがある．この共通の性質を抽象化したものが，**プロダクションシステム**として知られるものである．**プロダクションシステム**は3つの構成要素からなる．

1. **状態の集合**

   **状態**とはアプリケーションの環境で発生する状況のこと．始まりの状態は，**出発状態**で，求める状態は**目標状態**と呼ばれる．

2. **プロダクションの集合**

   **プロダクション**とは1つの状態から別の状態に移動するためん，アプリケーションの環境で実行される操作のこと．各プロダクションには，前提状態が関連づけられている．

3. **制御システム**

   制御システムとは，出発状態から目標状態まで移動して問題を解決するための論理から構成される．制御システムを開発する際に重要なのは，**問題空間**の概念である．

   **問題空間**

   プロダクションシステム内のすべての状態，プロダクション，前提状態の集合のこと．問題空間は，**状態グラフ**の形で概念化されることが多い．



プロダクションシステムの例は，与えられた命題から新しい命題を形成する**推論規則**である．

今日，このような推論システムは，論理プログラミング言語によって実装されることが多いのだがこれは，**エキスパートシステム**の中核となっている．

**エキスパートシステム**

人間のエキスパート(専門家)が同じ状況に直面したときに使用する原因結果の推論をシミュレートするように設計されたソフトウェアパッケージのこと．



### その他の研究領域

#### 知識の表現と操作

よりよい知識抽出を開発する際のもう一つのアプローチは，知識抽出のプロセス内に様々な形式の推論を挿入することである．これは**メタ推論**(推論のための推論)と呼ばれるものとして結実している．メタ推論の1つの適用の例として**閉世界仮説**の適用がある．

**閉世界仮説**

元来，データベースを探索する文脈で使用されていたもので，利用可能な情報から明示的に導き出せない命題は偽であると仮定する考えた．



**フレーム問題**

変化する環境中で格納された知識をどのように最新に保つか．



#### 学習

どの程度人間が介入するかのレベル別によってコンピュータ学習を分類するアプローチがある．

第1のレベルは**模倣**による学習．作業のステップごとに人間が直接お手本となる動作をしてみせる方法でありコンピュータはその動作を記録するだけである．

第2レベルは**教師あり学習**である．教師あり学習では人間が一連の例を示して正しい反応を識別できるようにし，エージェントはそれらの例示を一般化することで，新しい場面に適用できるアルゴリズムを開発する．この一連の例示を**訓練セット**という．

第3のレベルは，**強化学習**である．強化学習でエージェントは判断のための一般的な規則を与えられる．そして自分で試行錯誤により成功と失敗を繰り返す．教師あり学習と対照的に強化学習では時間をかけて振る舞いを改善するため，自律的に行動できるようになっている．



#### 遺伝的アルゴリズム

計算量が大きすぎるような問題に変わって，多くの試行錯誤を含む進化的プロセスを通じて解が発見できることがある．この考え方が，**遺伝的アルゴリズム**の基礎である．

**遺伝的アルゴリズム**

端的に言うと，ランダムな振る舞いに再生産理論のシミュレーションと自然淘汰による進化プロセスを組み合わせて解を発見する手法のこと．

ランダムな試行の集合を生成することで問題解決を開始する．各試行は**染色体**と呼ばれ，染色体の構成要素は**遺伝子**と呼ばれる．集合から2つの染色体を取り出して子孫を生成することで新しい染色体の集合を生成する．親は集合から解を導くと思われる可能性がもっとも高くなるように確率的にしかしランダムに選択される．なお遺伝的アルゴリズムが最終的な最適解を出す保証はない．

プログラム開発に遺伝的アルゴリズムを適用したものが，**進化プログラミング**として知られるものである．その目標は，明示的に記述する代わりに進化させることでプログラムを記述しようというものである．



### 人工ニューラルネットワーク

**人工ニューラルネットワーク**

生物の神経ネットワークを模倣するコンピュータによる処理モデル．



人工ニューラルネットワーク中のニューロンは有効な入力が与えられた値を越えたかどうかによって1か0を出力として生じるようになっている．ニューロンに対するそれぞれの結合には**重み**が関連づけられている．



#### 連想記憶

現在の情報に関連や関係のある情報を検索するものを**連想記憶**という．



## 12. 計算の理論

数学における**関数**とは可能な入力値の集合と可能な出力値の集合の間に，各入力に1つの出力が割り当てられるように対応づけをおこなうことである．



**計算不能**

入力値に基づいて出力を決定的かつ段階的に求めることができないほど複雑な関数が存在しており，そのような関数の計算はあらゆるアルゴリズムシステムの能力を超えていること．

**計算可能**

翻って，入力値からアルゴリズムによって決定的に出力値を得られる関数のことをいう．



### チューリングマシン

**チューリングマシン**

読み書きヘッドによってテープ状の記号を読み取ったり書き込んだりできる制御ユニットから構成されるマシンのこと．



#### チャーチ＝チューリングの提唱

チューリングマシンは，後者関数として知られる関数を計算するのに使用できる．後者関数とは負ではない整数入力値nに，出力値n+1を割り当てるものである．マシンのテープ上に2進数で入力値を配置して，マシンが停止するまで実行し，停止したらテープから出力値を読み取ればよい．このようにしてチューリングマシンによって計算できる関数を，**チューリング計算可能**という．



### 万能プログラミング言語

万能プログラミング言語で解決できない問題は，その問題を解くアルゴリズムは存在しないことになる．



### 計算不能関数

#### 停止問題

**停止問題**とはあるプログラムが，ある特定の条件で開始して停止するか前もって予測しようとするもの．



#### 停止問題の解決不能性

そもそも停止問題を解くことはマシンの能力を超えたところに存在している．

停止関数が計算可能でないという結論を得たとき，停止問題への解は停止関数の計算可能性に依存しているため，停止問題を解くことはいかなるアルゴリズムシステムの能力をも超えている．このような問題を解決不能問題という．



### 問題の複雑さ

#### 多項式問題対非多項式問題

**多項式問題**

関数$f(n)$が多項式であるか，他の多項式より上に有界である場合，ある問題が$O(f(n))$に含まれる問題．

#### NP問題

**非決定性アルゴリズム**

意思決定をプログラムを実行する機構の創造性に委ねており，このような命令軍を非決定的であるといい，そのような命令を含むアルゴリズムのことを指す．

巡回セールスマン問題は非決定的解法は多項式時間で実行できるが，多項式時間で実行できる決定的な解法は見つかっていない．

**非決定的多項式問題，NP問題**

非決定性アルゴリズムによって多項式時間で解くことのできる問題のこと．

Pのすべての問題はNPでもある．



**NP完全問題**

この問題のうち一つでも多項式時間で解くことができるアルゴリズムが見つかったなら，そのアルゴリズムを拡張してNP中の他の全ての問題を解けるというもの．