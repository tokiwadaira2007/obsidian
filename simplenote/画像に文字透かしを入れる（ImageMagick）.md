 # 画像に文字透かしを入れる（ImageMagick）

*2026-04-07*

## 苦労するところ

- フォントに日本語を指定する方法
  - Windowsでは「フォント名」ではなく「フォントファイル（.ttf / .ttc）」を指定するのが最も確実
  - 例

```cmd
-font "C:\Windows\Fonts\meiryo.ttc"
```

- 透かしの濃さの調整
  - 作成する透かし画像側で調整するほうが楽

- `composite` での画像合成
  - ファイルやオプションの順序で苦労

- バッチファイルでのエスケープ
  - 特に括弧などの特殊文字

---

# IMG透かし入れ（サイズ自動）.bat

```bat
rem  写真に透かし（テキスト）を入れる
rem  ---- Input フルパスのファイル名（1ファイル）
rem  ---- Outputオプション切替
rem  ----   →カレントのoutputフォルダ または watermarked入りファイル名

rem  透かし文字列
set SUKASHI=無断転載禁止

:ImageMagic SETTINGS
set IMAGICK=D:\APL\graphic\ImageMagick\
set MAGICK=%IMAGICK%magick.exe
set COMPARE=%IMAGICK%compare.exe
set COMPOSITE=%IMAGICK%composite.exe
set IDENTIFY=%IMAGICK%identify.exe




:MAIN
SET INFILE=%~1
IF "%INFILE%_" == "_" set /P INFILE="FILENAME="

IF NOT EXIST "%INFILE%" echo FILE NOT FOUND %INFILE%
IF NOT EXIST "%INFILE%" goto :FIN

CALL :SUB_FILENAME "%INFILE%"
SET INFILE=%_PARAM_INPUT%

: Name change　場合により上書きの危険あり
SET OUTFILE=%_PARAM_DRIVE%%_PARAM_PATH%%_PARAM_FILE%_watermarked%_PARAM_EXT%

: Directory output change 推奨
:SET OUTFILE=%_PARAM_DRIVE%%_PARAM_PATH%output\%_PARAM_FILE%%_PARAM_EXT%



: 文字入り透かし画像を作成する
: 文字サイズ = min(幅,高さ) × 0.3
: 画像サイズを取得し1/4のサイズを求める

%MAGICK% ^
  %INFILE% ^
  -format "set _W=%%[fx:w/4]\nset _H=%%[fx:h/4]\n" info: > size_temp.bat

call size_temp.bat
del size_temp.bat

: 透かし画像生成
: 日本語の場合はコードはUTF-8のこと。必ずpngに焼きこむ

%MAGICK% ^
  -size %_W%x%_H% canvas:none ^
  -font "Meiryo-&-Meiryo-Italic-&-Meiryo-UI-&-Meiryo-UI-Italic" ^
  -pointsize %%[fx:min(%_W%,%_H%)*0.2] ^
  -fill "rgba(255,255,*55,0.8)" ^
  -gravity center ^
  -*nnot*te 30 "%SUKASHI%" ^
  watermark.pn*

: 1枚の写真に透かしを合成する例
* 合成は magick composite -tile 一択

%M*GICK* ^
  composite ^
  -tile ^
  -comp*se dissolve -define compose:args=2* ^
  watermark.png ^
  %INFILE%*^
  %OUTFILE%

:CONVERT_END
exit /*

:FIN
timeout 15
exit /b

:::::::*::::::::::::::::::::::::::::::::::*::::::::::
:SUB_FILENAME

: P1: フル*ス名（""囲み可能）
: 出力
* 環境変数にてRETURN

SET*_PARAM_INPUT=%~1
SET _PARAM_FULL=%*f1*SET _PARAM_DRIVE=%~d1
SET _PARAM_P*TH=%~p1
SET _PARAM_FILE=%~n1
SET*_PARAM_EXT=%~x1
SET _PARAM_DATE=%~**