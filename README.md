# cadenceprobe

DVD本編の映像方式を自動判定し、適切なエンコード設定を提示するツール。

インターレース、プログレッシブ、テレシネを解析し、HandBrakeなどで必要となる映像処理とフレームレートを提示する。実際のエンコードは行わない。

## 環境

- macOS
- Python 3.12 / uv
- FFmpeg / ffprobe
- VapourSynth / BestSource / TIVTC

依存関係はプロジェクト専用環境で管理する。

## 使い方

DVDのタイトル一覧を取得する。

```sh
uv run cadenceprobe titles /path/to/dvd.iso
```

本編のタイトルと解析範囲を指定する。

```sh
uv run cadenceprobe analyze /path/to/dvd.iso \
  --title 3 --start 60 --end 5400 \
  --output reports/example
```

## 出力

- 映像方式：Soft Telecine / Hard Telecine / Progressive / Interlaced / Mixed / Unknown
- 入力・推奨出力フレームレート
- フィールド順序（TFF / BFF）
- 推奨処理（逆テレシネ・インターレース解除・無処理）
- HandBrake向けのフィルター設定、CFR / VFR
- 判定根拠と判定不能な範囲

詳細な仕様は [SPEC.md](SPEC.md) を参照。
