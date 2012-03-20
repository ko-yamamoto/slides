.. 20120317 documentation master file, created by
   sphinx-quickstart on Tue Mar  6 22:09:32 2012.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


//////////////////////////////////////////////////////
Scala/Akka Actor
//////////////////////////////////////////////////////


index
========================================

+ Scala?

+ Akka Actor?

+ Sample


.. s6:: effect slide



Scala
========================================

.. s6:: effect slide




Scala
========================================

+ JVM
+ Better Java
+ 関数型言語

.. s6:: effect slide


Scala
========================================

JVM 上で動作

* コンパイルすると class ファイルに
* Java の資産を利用可能
* ライブラリ


.. s6:: effect slide


Scala
========================================

Better Java

* Java のように書ける
* 便利な関数・文法


.. s6:: effect slide


Scala
========================================

関数型言語

* 「副作用なし」
* 「第1級関数」


.. s6:: effect slide


Scala
========================================

「副作用なし」

* val

   .. code-block:: scala

      val i = 1
      i = 2 // コンパイルエラー!!

* var

   .. code-block:: scala

      var i = 1
      i = 2 // コンパイル OK


.. s6:: effect slide



Scala
========================================

val と var

   .. code-block:: scala

      val = values
      var = variables

   -> val を推奨

* 副作用なし

.. s6:: effect slide



Scala
========================================

* sample

   .. code-block:: scala

      // Sample1.scala
      object Sample extends App {

        println("Hello World!!!")

      }

   run

   .. code-block:: bash

      $ scalac Sample1.scala
      $ scala Sample

   -> Hello World!!!



.. s6:: effect slide



Scala
========================================

* スクリプトとしても実行可能


   .. code-block:: scala

      // Sample2.scala
      println("Hello World!!!")

   run

   .. code-block:: bash

      $ scala Sample2.scala

   -> Hello World!!!



.. s6:: effect slide





Akka Actor
========================================

.. s6:: effect slide






Akka Actor
========================================

Akka - http://goo.gl/evYro

フレームワーク



* 分散処理
* 非同期処理


.. s6:: effect slide



Akka Actor
========================================

特徴

* 非同期 - Actor モデル


.. s6:: effect slide




Akka Actor
========================================

* Actor？ Thread？


.. s6:: effect slide




Akka Actor
========================================

Thread

.. s6:: effect slide


Akka Actor
========================================

Thread

* 共有データ・ロック

   .. image:: _img/mt.*
      :align: center


.. s6:: effect slide



Akka Actor
========================================

Thread

* 他のスレッドから変更される恐れ
* 失敗 - デッドロック
   

.. s6:: effect slide




Akka Actor
========================================

Actor


.. s6:: effect slide



Akka Actor
========================================

Actor モデル

* メッセージパッシング

   + メッセージ送信
   + メッセージ受信


.. s6:: effect slide



Akka Actor
========================================

Actor

* メッセージの送受信

* メッセージのキューイング

* メッセージ(の型)に応じた処理選択

.. s6:: effect slide



Akka Actor
========================================

Actor

* メッセージ送信

   .. image:: _img/1.*
      :align: center


.. s6:: effect slide


Akka Actor
========================================

Actor

* 処理

   .. image:: _img/2.*
      :align: center


.. s6:: effect slide



Akka Actor
========================================

Actor

* 結果をメッセージとして返却

   .. image:: _img/3.*
      :align: center


.. s6:: effect slide




Akka Actor
========================================

Actor

* データのやり取りはメッセージ
* 共有無し

   -> ロックなし


.. s6:: effect slide


Akka Actor
========================================

Actor

* 必要なもの

   + Actor(s) クラス
   + メッセージクラス


.. s6:: effect slide



Akka Actor
========================================

Actor

* Actorクラス

   + Main Actor
   + Worker Actor


.. s6:: effect slide


Akka Actor
========================================

Actor？

* あまり見かけない・・・

.. s6:: effect slide





Akka Actor
========================================

Actor？

* Thread 採用の言語が多い

* Java での実装難

-> Scala 標準 Actor


.. s6:: effect slide




Akka Actor
========================================

Scala Akka

* Actor モデルを標準化



.. s6:: effect slide



Akka Actor
========================================

+ import とメッセージの作成

   .. code-block:: scala

      import scala.actors.Actor
      import scala.actors.Actor._

      // メッセージ用クラス
      case object Msg


.. s6:: effect slide

Akka Actor
========================================

+ Actor の宣言

   .. code-block:: scala
    
      class SampleActor extends Actor {
        def act() {
          receive {
            // Msg クラス受信時の処理
            case Msg =>
              println("Ping!!")
          }
        }
      }


.. s6:: effect slide


Akka Actor
========================================

+ 実行

   .. code-block:: scala
    
    
      object Main extends App {
    
        val sampleActor = new SampleActor
        // Actor 開始
        sampleActor.start
        // メッセージ送信
        sampleActor ! Show
    
      }


.. s6:: effect slide


Akka Actor
========================================

Scala Akka

* シンプル
* 複雑なことは実装が必要

   + ルーティング
   + バランサー


.. s6:: effect slide




Akka Actor
========================================

-> **Akka**!!!


.. s6:: effect slide


Akka Actor
========================================

Akka::

   Build powerful concurrent &
   distributed applications
   more easily.


.. s6:: effect slide


Akka Actor
========================================

Akka Actor

* Java でも Actor モデル実装可能
* より簡単に記述可能
* 設定ファイルでの Actor 設定可能
* ロードバランサー・ルーティング
* 自己修復
* remote Actor


.. s6:: effect slide


Akka Actor
========================================

Akka Actor

* Java

   .. code-block:: java

      // Actor 宣言
      public class MasterActor
                   extends UntypedActor {
        @Override
        public void onReceive(Object msg) {
          if (msg instanceof Hoge) {
          .
          .
          .


.. s6:: effect slide


Akka Actor
========================================

Akka Actor

* Java

   .. code-block:: java

      // 開始
      ActorRef actor =
          system.actorOf(
              new Props(new UntypedActorFactory() {
                  public UntypedActor create() {
                      return new SampleActor();
                  }
      }), "actor");



.. s6:: effect slide



Akka Actor
========================================

Akka Actor

* 設定ファイル

   + ログレベル設定
   + ルータータイプ設定
   + Akka 用動作パラメータ変更
   + などなど

.. s6:: effect slide




Akka Actor
========================================

Akka Actor

* 設定ファイル::

   actor.deployment {
     // 名前設定
     /masterActor/router {
       // ルータータイプ設定
       router = round-robin
       // ルーターに登録する Actor の数
       nr-of-instances = 3
       .
       .

.. s6:: effect slide


Akka Actor
========================================

Akka Actor

* 設定ファイル::

   actor.deployment {
     /masterActor/router {
       // ルータータイプ設定
       router = smallest-mailbox
       // ルーターに登録する Actor の数を動的に数を変更
       resizer {
         lower-bound = 3
         upper-bound = 10
         .


.. s6:: effect slide



Akka Actor
========================================

Akka Actor

* Router

   + Routees として Actor を登録
   + Routees にメッセージを割り振る
   + 数種類のタイプ

.. s6:: effect slide




Akka Actor
========================================

Akka Actor

* Router のタイプ

   + round-robin
   + random
   + smallest-mailbox
   + scatter-gather
   + broadcast


.. s6:: effect slide


Akka Actor
========================================

Akka Actor

* Router のメッセージ

   + Normal Messages
   + Broadcast Messages
      -> 全ての Routees へ


.. s6:: effect slide


Akka Actor
========================================

Akka Actor

* Router の作成1

   .. code-block:: scala

      /sampleActor/router {
        router = round-robin
        nr-of-instances = 3
                   }

.. s6:: effect slide



Akka Actor
========================================

Akka Actor

* Router の作成2

   .. code-block:: scala

      ActorRef router =
        system.actorOf(
          new Props(ExampleActor.class)
             .withRouter(
                new FromConfig()),
                "router"
             );

.. s6:: effect slide


Akka Actor
========================================

Akka Actor

* Sample

.. s6:: effect slide


終わりに
========================================

* Scala で簡潔なコードを
* Akka で見通しの良い並列処理を

.. s6:: effect slide

