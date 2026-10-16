# rtk-sample

rtk の hook を入れた Claude Code に、落ちたテストを直させる実験用の教材リポジトリです。

Pallets の [click](https://github.com/pallets/click)（commit `2247b35`）を元にした教材です。ライセンスは click と同じ BSD-3-Clause で、`LICENSE.txt` をそのまま残しています。実装に手を加えて、テストが落ちる状態にしてあります。

## 前提

- Python 3.10 以上と pytest
- rtk 1.0.1
- Claude Code

## 手順

1. clone して依存を入れます。

   ```bash
   git clone https://github.com/zun-tools/rtk-sample.git
   cd rtk-sample
   python -m venv .venv && . .venv/bin/activate
   pip install pytest -e .
   ```

2. `pytest` で落ちるのを見ます。

   ```bash
   python -m pytest tests
   ```

3. 同じテストを `rtk pytest` で走らせ、出力を並べて見比べます。

   ```bash
   rtk pytest tests
   ```

4. Claude Code に hook を入れます。

   ```bash
   rtk init -g
   ```

5. このディレクトリで Claude Code を起動し、次の依頼文をそのまま頼みます。

   ```
   このリポジトリのテストが落ちています。原因を見つけて実装側を直してください（テストファイルは変更しないこと）。最後に python -m pytest tests を実行して全件通ることを確かめてください。
   ```

6. 終わったら `rtk gain` で、rtk が通した出力のサイズを確かめます。

   ```bash
   rtk gain
   ```

## 注意

- 手順 5 のあとは実装ファイルが書き換わります。もう一度試すときは `git checkout .` で戻してください。
- 出力量の変化は環境や回ごとにぶれます。`rtk gain` の数字は、あなたの環境での実測として読んでください。
