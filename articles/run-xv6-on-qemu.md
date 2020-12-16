---
title: "xv6-riscv を QEMU で動かす"
emoji: "😊"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["xv6", "qemu", "risc-v"]
published: true
---

`RISC-V`エミュを作っていて最初のターゲットとして`xv6`の動作を目標にしてます。
`xv6`を試しに動かしてみたくて、`QEMU`が手っ取り早いかなって思ってやろうとしたんですが、日本語でまとまった手順がなかったのでメモがてら残しておきます。

📒 **[xv6サイト(英語) →](https://pdos.csail.mit.edu/6.828/2020/xv6.html)**
📕 **[RISC-Vサイト(英語) →](https://riscv.org/)**

# 環境

* masOS Catalina 10.15.7
* Homebrew 2.5.6
* QEMU emulator version 5.1.0
* xv6-riscv d4cecb269f2acc

# QEMU インストール

`Homebrew`でインストールします。

```
$ brew install qemu
```

下記コマンドでインストールが成功していることを確認する。

```
$ qemu-system-riscv64 --version
QEMU emulator version 5.1.0
Copyright (c) 2003-2020 Fabrice Bellard and the QEMU Project developers
```

# RISC-V 用のツールチェインのインストール

準備として下記ツール群をインストールする。

```
$ brew install python3 gawk gnu-sed gmp mpfr libmpc isl zlib expat
```

[riscv/riscv-gnu-toolchain](https://github.com/riscv/riscv-gnu-toolchain) をクローンしてビルドします。

```
$ git clone --recursive https://github.com/riscv/riscv-gnu-toolchain.git
$ cd riscv-gnu-toolchain
$ ./configure --prefix=/opt/riscv
$ make
```

詳細は [riscv/riscv-gnu-toolchain](https://github.com/riscv/riscv-gnu-toolchain) を参考してください。

# xv6-riscv を QEMU 向けにビルド

[mit-pdos/xv6-riscv](https://github.com/mit-pdos/xv6-riscv) をクローンしてきます。

```
$ git clone https://github.com/mit-pdos/xv6-riscv.git
$ cd xv6-riscv
$ make qemu
```

`make qemu` コマンドでビルドと `QEMU` の起動まで行うので、すぐに `xv6` が起動できます。

作業しながらメモしてましたが、手軽すぎてメモる必要もなかったかもしれません。
