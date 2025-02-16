# Global Interpreter Lock (GIL) とは？

Global Interpreter Lock（GIL） は、Python の CPython 実装 で使用される 排他ロック（mutex） のことです。

GIL の主な役割は 「同時に実行される Python スレッドが 1つだけになるように制御する」 ことです。
つまり、Python のマルチスレッド処理は「並列実行」ではなく「逐次実行」 になってしまいます。

## 1. GIL の仕組み

通常、CPU には複数のコア（マルチコア）があり、
「スレッド（Thread）」を使えば複数の処理を並行実行できる はずです。

しかし、CPython の GIL により、複数のスレッドを作成しても 1つのスレッドしか同時に実行されません。

```python
import threading

def worker():
    for _ in range(5):
        print("Working...")

thread1 = threading.Thread(target=worker)
thread2 = threading.Thread(target=worker)

thread1.start()
thread2.start()

thread1.join()
thread2.join()
```

🔹 期待する動作（GIL がなければ）
2つのスレッドが 完全に並列で動作 する → CPU 使用率が 200% になるはず（デュアルコアの場合）

🔹 実際の動作（GIL の影響）
スレッドは 1つずつしか実行されない → CPU 使用率は 最大でも 100%

## 2. なぜ Python は GIL を採用しているのか？

GIL は「Python のスレッドが同時に 1つしか動かない」という 制約 を生むため、
マルチコア CPU の性能を十分に活かせません。

それでも Python が GIL を採用している理由 は、主に以下の 2つです。

理由 ①: メモリ管理の簡略化

Python は 動的型付け（Dynamic Typing） であり、
内部では メモリ管理（Garbage Collection: GC） を行っています。

🔹 GIL を導入すると…
	•	Python オブジェクトのメモリ管理を簡単にする
	•	スレッドセーフなガベージコレクションを実装しやすくなる

もし GIL がなければ、各スレッドが 同じオブジェクトのメモリを同時に変更 する可能性があり、
メモリ管理の複雑さが大幅に増加 してしまいます。

理由 ②: シングルスレッドのパフォーマンスを向上

GIL を シングルスレッドのコード最適化 に活用することで、
シングルスレッドの Python コードの 実行速度を向上 できます。

例えば、Python のオブジェクト操作（リスト、辞書など）は スレッドセーフ にする必要がありますが、
GIL があることで ロック機構を減らし、スレッドの切り替えコストを最小化 できます。

## 3. GIL の影響と解決策

影響: マルチスレッドでの並列実行ができない

GIL のせいで Python のスレッドは実際には並列実行されない ため、
以下のような CPU 負荷の高い処理（CPU バウンド処理） は、マルチスレッド化しても高速化できません。

❌ GIL によって高速化できない例
	•	画像処理（OpenCV など）
	•	数値計算（行列演算、ニューラルネットワーク）
	•	データ圧縮（zip、gzip など）

✅ 解決策
	1.	マルチプロセス（multiprocessing）を使う
→ GIL の影響を受けない「プロセス（Process）」を活用
	2.	C 言語や Rust で処理を実装する
→ NumPy, TensorFlow などのライブラリは内部で C 言語を使って並列処理を実現
	3.	GIL がない Python 実装を使う
→ PyPy, Jython, IronPython などの GIL を持たない実装を検討

## 4. GIL を回避する方法: multiprocessing

Python には multiprocessing モジュールがあり、
これを使うことで GIL の影響を受けずに並列実行 できます。

```python
import multiprocessing

def worker():
    print("Processing...")

if __name__ == "__main__":
    process1 = multiprocessing.Process(target=worker)
    process2 = multiprocessing.Process(target=worker)

    process1.start()
    process2.start()

    process1.join()
    process2.join()
```

💡 threading.Thread の代わりに multiprocessing.Process を使うことで、
プロセス（Process）単位で並列実行 でき、GIL の制約を受けません！

|言語	| GIL の影響 | 並列処理のしやすさ |
|------|-----------|------------|
| Python (CPython)	| GIL あり	| ❌ マルチスレッドが遅い
| Elixir	| GIL なし	| ✅ 軽量プロセス (BEAM) により超並列
| Go	| GIL なし	| ✅ Goroutine による並列処理が簡単
| Java | GIL なし	| ✅ マルチスレッド（JVM）で並列可能
| C / C++ | GIL なし | ✅ 低レイヤでスレッド管理可能

* ✅ Elixir や Go は GIL の問題がなく、並行処理が簡単に書ける！
* ✅ Python は multiprocessing を使えば並列処理が可能！

## 5. まとめ

🔹 GIL（Global Interpreter Lock）とは？
	•	Python（CPython）では、スレッドが 1つずつしか実行されない
	•	マルチスレッドを使っても並列実行できず、CPU パワーを活かしにくい

🔹 なぜ GIL があるのか？
	1.	メモリ管理（Garbage Collection）を簡単にする
	2.	シングルスレッドの Python コードを最適化する

🔹 GIL の影響
	•	マルチスレッドは 並列実行できない
	•	CPU 負荷の高い処理（画像処理、機械学習など）には向かない
	•	Python での 並列処理には multiprocessing を使うべき

🔹 GIL を回避する方法
	1.	multiprocessing を使う（プロセス単位で並列化）
	2.	C / Rust で並列処理を書く（NumPy, TensorFlow など）
	3.	GIL を持たない言語（Elixir, Go）を使う

