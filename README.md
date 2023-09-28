# turtlebot3_config
TURTLEBOT3を無線ゲームパッドF710で運転するための設定ファイルです。

## 事前の準備
(https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/) を参照して、<br>
TURTLEBOT3にROS2(Foxy)をセットアップしてください。

## ダウンロード

```sh
$ cd ~
$ git clone https://github.com/ekasai6724/turtlebot3_config.git
```

## 設定ファイルのコピー

```sh
$ cd ~/turtlebot3_config
$ sudo cp teleop_linux-launch.py /opt/ros/foxy/share/teleop_twist_joy/launch/
$ sudo cp f710.config.yaml /opt/ros/foxy/share/teleop_twist_joy/config/
```

## F710のインストールと動作確認
[このページ](https://qiita.com/thun_build/items/6dd1ac4e0c11dcc0fa26)を参照してください。<br>
以下のようにROS2パッケージを追加インストールする必要があります。
```sh
$ sudo apt install ros-foxy-joy-linux
$ sudo apt install ros-foxy-joy-linux-dbgsym
```

## 起動コマンド
始めにTURTLEBOT3の共通処理部分を起動します。ロボットパラメータの設定が必要になる場合があります。<br>
詳細は(https://emanual.robotis.com/docs/en/platform/turtlebot3/bringup#bringup) を参照してください。
```sh
$ ros2 launch turtlebot3_bringup robot.launch.py
```

続いて別ターミナルウィンドウを起動し、以下のコマンドでゲームパッドによる手動操作を開始します。
```sh
$ ros2 launch teleop_twist_joy teleop_linux-launch.py
```
デバイスが`/dev/input/js0`以外で認識されている場合は、起動コマンドに以下のようにパラメータを追加してください。<br>
(`/dev/input/js2`の場合)
```sh
$ ros2 launch teleop_twist_joy teleop-launch_linux.py joy_dev:='/dev/input/js2'
```
