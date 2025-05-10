# voicevox_song_prompt
voicevox songの歌作成プロンプト

# 参考資料
https://github.com/VOICEVOX/voicevox_engine

https://github.com/ts-klassen/abc_voicevox_song/tree/main

https://note.com/hachi_mori_/n/n21adf74558ce

# 説明

このプロンプトは作成したい歌のテーマを入力すると、AIがvoicevox song用の歌を作成してくれるプロンプトです。

BPM、タイトル、歌詞、楽譜（WEB版VOICEVOX歌唱合成仕様）、score.json（VOICEVOXソング・ハミングAPIのJSON形式）が出力されます。

# 推奨AI
Google Gemini 2.5 Flash または Gemini 2.5 Pro

## 出力例

### BPM

ここにBPM出力

### 曲のタイトル

ここに曲のタイトル出力

### 歌詞

ここに歌詞出力

### 楽譜（WEB版VOICEVOX歌唱合成仕様）

ここに楽譜出力

### score.json

ここに VOICEVOXソング・ハミングAPIのJSONを出力

# 使い方

# 1 プロンプトをGeminiの画面に張り付ける
[Voicevox_song_prompt.md](https://github.com/haru-works/voicevox_song_prompt/blob/main/Voicevox_song_prompt.md) をGeminiの画面のチャットに張り付ける

そうするとこんな感じでAIが質問を聞いてきます。

![image](https://github.com/user-attachments/assets/2cbcfdfc-930e-4f61-8f8a-ebfe4d967428)

# 2 歌のテーマを書く
AIに作ってもらいたい歌のテーマを色々を書いていきます。

![image](https://github.com/user-attachments/assets/ad38cdd4-27da-4b5b-98d9-dd5e2adcc6ec)

# 3 AIの結果が出力される
こんな感じで出力されます。

![image](https://github.com/user-attachments/assets/cbfe6732-f437-423c-b3a3-46e29607f70c)

# 4 WEB版VOICEVOX（歌唱）で作る場合
* https://www.voicevox.su-shiki.com/song にアクセスする
* 出力された **楽譜（WEB版VOICEVOX歌唱合成仕様）** の下の部分を **WEB版VOICEVOX（歌唱）** の **ひらがなで歌詞を入力**部分にコピペする
  
　この部分をコピぺ

  ![image](https://github.com/user-attachments/assets/0699ed92-5b5c-4832-93ae-d4e4ba792ca9)

* **楽譜を作成** ボタンを押す。メロディーが生成されます。
* **楽譜を合成** ボタンを押す。選択したキャラで歌が生成されます。

# 5 VOICEVOXエンジンのAPIで作る場合
* https://github.com/VOICEVOX/voicevox_engine の説明に沿って、ローカルにVOICEVOX ENGINEを構築する
* 出力された **score.json** をコピーして、ローカルPCの任意の場所に**score.json**の名前で保存する

この部分を**score.json**の名前で保存する

![image](https://github.com/user-attachments/assets/0a33e082-ed7e-493a-9127-84c27bb17a4a)

* VOICEVOX ENGINEのREADMEの**[HTTP リクエストで歌声合成するサンプルコード](https://github.com/VOICEVOX/voicevox_engine?tab=readme-ov-file#http-%E3%83%AA%E3%82%AF%E3%82%A8%E3%82%B9%E3%83%88%E3%81%A7%E6%AD%8C%E5%A3%B0%E5%90%88%E6%88%90%E3%81%99%E3%82%8B%E3%82%B5%E3%83%B3%E3%83%97%E3%83%AB%E3%82%B3%E3%83%BC%E3%83%89)**の説明に従って、保存したscore.jsonのパスを指定して、curlコマンドでquery.jsonを生成し、audio.wavを生成する

* query.json生成とaudio.wav生成のcurlコマンド
```
curl -s \
    -H "Content-Type: application/json" \
    -X POST \
    -d @score.json \
    "127.0.0.1:50021/sing_frame_audio_query?speaker=6000" \
    > query.json

curl -s \
    -H "Content-Type: application/json" \
    -X POST \
    -d @query.json \
    "127.0.0.1:50021/frame_synthesis?speaker=3001" \
    > audio.wav
```
