# [WINDOWS] Windowsバッチ・コマンドで，大量のPDFを一括で結合・分割し，各ページ数を調べて一定サイズにまとめよう （pdftkをコマンドプロンプトやWSHから使う方法）

<https://language-and-engineering.hatenablog.jp/entry/20150113/PdftkOnWindowsBatch>

Windows上で，PDFファイルの結合・分割・ページ情報の取得などの処理を
自動化できるCUIのフリーソフト，「pdftk」の使い方。

コマンドラインの無料ツールなので，バッチ処理に組み入れて，大量のPDFを一括処理することも簡単。

## 目次

- （１） pdftkの導入
- （２） pdftkの基本的な使い方
  - （２−１） コマンドラインでのPDFの結合
  - （２−２） コマンドラインでのPDFの分割
  - （２−３） コマンドラインでPDFのページ数を取得する
  - （２−４） pdftk以外の類似ツール
- （３） 大量のPDFを一括で結合するバッチ
- （４） 大量のPDFを一括で「１００ページごと」に分割するバッチ
- 結論と補足

## （１）pdftkの導入

まず，pdftkのインストール。

下記のページにアクセス。

[PDFtk - The PDF Toolkit](https://www.pdflabs.com/tools/pdftk-the-pdf-toolkit/)

少し下にスクロールして，「Download pdftk free」という緑色のリンクをクリック。

`pdftk_free-2.02-win-setup.exe`のダウンロードが開始し，完了する。

このインストーラを実行。

ライセンスに同意し，インストールが完了。

PATHに自動的に追加される。

コマンドプロンプトを開いて，`pdftk` と打ち込んで，下記のように表示されれば導入成功。

```text
SYNOPSIS
       pdftk <input PDF files | - | PROMPT>
            [ input_pw <input PDF owner passwords | PROMPT> ]
            [ <operation> <operation arguments> ]
            [ output <output filename | - | PROMPT> ]
            [ encrypt_40bit | encrypt_128bit ]
            [ allow <permissions> ]
            [ owner_pw <owner password | PROMPT> ]
            [ user_pw <user password | PROMPT> ]
            [ flatten ] [ need_appearances ]
            [ compress | uncompress ]
            [ keep_first_id | keep_final_id ] [ drop_xfa ] [ drop_xmp ]
            [ verbose ] [ dont_ask | do_ask ]
       Where:
            <operation> may be empty, or:
            [ cat | shuffle | burst | rotate |
              generate_fdf | fill_form |
              background | multibackground |
              stamp | multistamp |
              dump_data | dump_data_utf8 |
              dump_data_fields | dump_data_fields_utf8 |
              dump_data_annots |
              update_info | update_info_utf8 |
              attach_files | unpack_files ]

       For Complete Help: pdftk --help
```

↑目次へ戻る

## （２）pdftkの基本的な使い方

pdftkコマンドを，Windows上で実際に使ってみよう。

### （２−１）コマンドラインでのPDFの結合

下記のように，結合したい複数のPDFファイル名と，結合後のファイル名を指定すればよい。

```bat
pdftk 元ファイル1.pdf 元ファイル2.pdf cat output 結合後のファイル名.pdf
```

とても簡単。

元ファイルの個数は，３個以上に増やしてもよい。

その場合，指定した順番どおりにPDFが結合される。

コマンドプロンプトで複数のファイルを指定するのが面倒ならば， `*.pdf` という記法も使える。

### （２−２）コマンドラインでのPDFの分割

分割は下記の書式で可能。

```bat
pdftk 元ファイル名.pdf cat 開始ページ-終了ページ output 出力ファイル名.pdf
```

参考：

[pdftk \[作業中\]](http://pdftk.nnn2.com/?p=1)

> DFファイルを分割する場合の書式は以下のとおり。 `pdftk 対象のPDFファイル cat ページ範囲 output 出力先のPDFファイル` 　
>
> 例えば、sample.pdfというPDFファイルから2ページ目を取り出して2.pdfというファイルを作成するなら、以下のコマンドを実行する。 `$ pdftk sample.pdf cat 2 output 2.pdf`

あらくさな日々をつれづれと : UbuntuでのPDFの結合、分割の方法
`http://blog.livedoor.jp/arakusa/archi...`

> `"pdftk 編集するpdf名 cat 編集するpdf部分 output 作成するpdf名"`
>
> ってな感じになっています だから他にも3ページ目と５ページ目が欲しい場合は `""pdftk keion.pdf cat 3 5 output keion3.pdf""` という感じで作ることができます
>
> 応用次第では 1から4ページと6ページのpdfを作りたければ `"pdftk keion.pdf cat 1-4 6 output keion4.pdf"`

ページ数を指定せずに，１ページごとにバラバラに分割したい場合は，`burst`オプションを使う。

PDFをコマンドラインから編集できるPDFtk使い方メモ - Programming Log
`http://nwpct1.hatenablog.com/entry/20...`

> ページ分割(burst) 入力ファイルをページ毎に分割して新しいPDFファイルを指定。 `$ pdftk input.pdf burst`

↑目次へ戻る

### （２−３）コマンドラインでPDFのページ数を取得する

pdftkには，PDFの情報を一括表示する`dump_data`コマンドがある。

```bat
pdftk 調べたいファイル名.pdf dump_data
```

このオプションをつけると，様々な情報がいっぺんに出てくる。

ページ数の情報だけを抜き出すには，`findstr`コマンドをパイプで使えばよい。

```bat
pdftk 非平衡統計力学.pdf dump_data | findstr NumberOfPages
```

```text
↓
NumberOfPages: 152
```

これでPDFのページ数がわかる。

pdftkでページ数を取得するサンプル：

RubyでPDFのページ数を数える | 坂本blog
`http://sakamotoken.sit.ac.jp/blog/201...`

> pdftkコマンドは`dump_data`オプションで様々なメタデータを表示してくれます。この中に `NumberOfPages: 10` というのがあるので，これを得る。

pdfのページ数を取得したいphp、javascript、コマンド(L...
`http://detail.chiebukuro.yahoo.co.jp/...`

> pdftkでは、pdfが置いてあるディレクトリ上で下記のようにコマンドを打ってみました `$ pdftk hoge dump_data`

### （２−４）pdftk以外の類似ツール

もし，何らかの理由でpdftkが動かなかったら，類似のCUIツールがいくつかある。

Imagickを使う方法：

[PHPのImagickでPDFを読み込んでPNGに変えるときの注意点 | 自転車で通勤しましょ♪ブログ](http://319ring.net/blog/archives/2218)

```php
$page_count = $imagick-＞getimagescene(); // ページ数を取得
```

XPDFのpdfinfo.exeを使う方法もある。

天地有情 XPDFパッケージの使い方
`http://konoyonohana.blog.fc2.com/blog...`

> XPDFパッケージはPDFを表示するプログラムですが、Windows版では以下のツールのみ入手可能です． `pdfimages.exe` -PDFから画像を抽出する(画像データーがあれば) `pdffonts.exe` -PDFのフォント情報を表示 `pdfinfo.exe` -PDFの作成者情報などを表示

pdfのページ数を取得したい - johnsonshu - 博客园
`http://www.cnblogs.com/johnsonshu/arc...`

> 以下のようにすればページ数のみ取得できます。 `＃ pdfinfo xxx.pdf 2＞/dev/null | gawk '/Pages/ {print $2}'`

[AS Hole（AppleScriptの穴） By Piyomaru Software » pdfinfoを使ってPDFのページ数をかぞえる » Blog Archive](http://piyocast.com/as/archives/437)

> フリーで配布されている「xpdf-tools」をインストールすると利用できるようになる「pdfinfo」というツールを呼び出し、指定のPDFのページ数を取得するAppleScriptです。リンク先のxpdf-tools（Universal Binary）はMac OS X標準のインストーラーが提供されているため、インストールもきわめて容易に行えます。

iTextSharpを使う方法：

[\[PowerShell\]iTextSharpを使ってPDFファイルのページ数を取得する | 初心者備忘録](http://www.ka-net.org/blog/?p=2317)

> PowerShellでiTextSharpを使ってPDFファイルのページ数を取得してみます

## （３）大量のPDFを一括で結合するバッチ

pdftkを呼び出して，カレントフォルダ以下の全サブフォルダを再帰的に検査し，
各フォルダ内の全PDFを結合するバッチ。

WSH/JSriptで記述。

**一括結合.bat**

```javascript
@if(0)==(0) ECHO OFF

cscript.exe //nologo //E:JScript "%~f0" "%~dp0" >out.log
@pause

GOTO :EOF
@end

/*
	カレント以下の全サブフォルダで，
	フォルダ内のPDFを結合するバッチ

	※PDF結合にはpdftkを使用。事前に導入のこと
*/



// ------------- ライブラリ関数 -------------


function log(s){ WScript.Echo(s); }

//
function err(s){ WScript.StdErr.WriteLine(s); log(s); }
	// リダイレクトされずにコンソールにも表示される

// ベンチ用
function tic(){
	tic.startTime = new Date().getTime();
}
function tac(){
	var ms = new Date().getTime() - tic.startTime;
	tac.time_span = ms / 1000;
}



// 配列のイテレータ
Array.prototype.each = function( func ){
	for( var i = 0; i < this.length; i ++ ){
		func.call( this, this[i], i );
	}
	return this; // チェインを継続
};

// map
Array.prototype.map = function( func ){
	var _arr = [];
	this.each(function( item, ind ){
		_arr.push( func.call( _arr, item, ind ) );
	});
	return _arr;
};


// コマンド実行結果を行ごとに配列として取得
// http://language-and-engineering.hatenablog.jp/entry/20081225/1230198688
function exec_cmd( str_cmd, params ){
	var current_dir    = ( params ) ? params.current_dir : null;
	var wait_while_net = ( params ) ? params.wait_while_net : null;

	var ws = WScript.CreateObject("WScript.Shell");

	// 必要ならカレントフォルダをセット
	if( current_dir ){
		ws.CurrentDirectory = params.current_dir;
	}
		//err( "カレントフォルダ：" + ws.CurrentDirectory + ", コマンド：" + str_cmd );

	// コマンド実行
	var proc = ws.Exec( "cmd /c " + str_cmd );

	// もしメール送信など通信系のコマンドであれば，終了まで待つ
	if( wait_while_net ){
		while( proc.Status == 0 ){
			WScript.Sleep(100);
		}
		// http://language-and-engineering.hatenablog.jp/entry/20100913/p1
	}

	// 出力を取得
	var str_out = proc.StdOut.ReadAll();

	// 末尾の空行を削除
	var arr = str_out.split("\r\n");
	arr.pop();

	return arr;
}



// ------------- メイン処理 -------------


// 結合で出力されたPDFの数
var joined_pdf_count = 0;

// 時間計測開始
tic();

// すべてのサブフォルダを列挙
var dirs = exec_cmd( "dir /a:D /s /b" );
dirs.each(function(dir_path){
		// log(dir_path);

	// 結合すべきPDFがここに存在するか？

	// ファイル名の特徴で判断
	// /O:Dは日時順でのソート
	var target_files = exec_cmd( 'dir /b /O:D *.pdf | findstr "^[a-z]*[0-9]*_[0-9]*\.pdf$"',{
		current_dir : dir_path
	});

	// 結合すべきPDFがあれば
	if( target_files.length > 0 ){
			//log("PDFあり：" + dir_path);
			//log(target_files.join("\n"));

		// 結合後のファイル名を決定
		// フォルダ名が本の名前であるとする
		var dir_name = dir_path.split("\\").pop();
		var output_pdf_name = dir_name + ".pdf";

		// これらのPDFを結合するコマンド
		var join_command = "pdftk "
			+ target_files.map(function(file_name){
				// ファイル名は引用符でくくっておく
				return '"' + file_name + '"';
			}).join(" ")
			+ ' cat output "..\\' // 一つ上のフォルダに保存
			+ output_pdf_name
			+ '"'
		;
			log(join_command);

		// 結合コマンドを実行
		exec_cmd( join_command, {
			current_dir : dir_path
		});
		joined_pdf_count ++;
			err("PDF結合が完了：" + output_pdf_name);

		// このフォルダは中身ごと削除

		// しかし安全のために，一項目ずつ実行。
		target_files.each(function(item){
			var file_del_command = 'del /q "' + item + '"';
				//err( "結合前のファイルを削除：" + file_del_command );
			exec_cmd( file_del_command, {
				current_dir : dir_path
			});
		})

		// フォルダ削除
		// /s /qオプションをつけない
		var del_dir_command = 'rd "' + dir_name + '"';
			err( "結合の完了したフォルダを削除：" + del_dir_command );
		exec_cmd(del_dir_command, {
			current_dir : dir_path + "\\..\\"
		})
			err("削除成功");

	}
});

tac();

err("全処理が完了しました。");
err("経過時間：" + tac.time_span + "秒");
err("結合で生成されたPDFの数：" + joined_pdf_count );
```

実行結果の出力はこんな感じ：

```text
pdftk "CCF20140817_0000.pdf" "CCF20140817_0001.pdf" "CCF20140817_0002.pdf" "CCF20140817_0003.pdf" "CCF20140817_0004.pdf" "CCF20140817_0005.pdf" "CCF20140817_0006.pdf" "CCF20140817_0007.pdf" "CCF20140817_0008.pdf" "CCF20140817_0009.pdf" "CCF20140817_0010.pdf" "CCF20140817_0011.pdf" "CCF20140817_0012.pdf" "CCF20140817_0013.pdf" cat output "..\Javaデザインパターン入門_マルチスレッド編.pdf"
PDF結合が完了：Javaデザインパターン入門_マルチスレッド編.pdf
結合の完了したフォルダを削除：rd "Javaデザインパターン入門_マルチスレッド編"
削除成功
pdftk "CCF20141021_0000.pdf" "CCF20141021_0001.pdf" "CCF20141021_0002.pdf" "CCF20141021_0003.pdf" "CCF20141021_0004.pdf" cat output "..\ソースコードリーディングJavaの設計と実装.pdf"
PDF結合が完了：ソースコードリーディングJavaの設計と実装.pdf
結合の完了したフォルダを削除：rd "ソースコードリーディングJavaの設計と実装"
削除成功
pdftk "CCF20140910_0000.pdf" "CCF20140910_0001.pdf" "CCF20140910_0002.pdf" "CCF20140910_0003.pdf" "CCF20140910_0004.pdf" "CCF20140910_0005.pdf" cat output "..\さらば失敗プロジェクト.pdf"
PDF結合が完了：さらば失敗プロジェクト.pdf
結合の完了したフォルダを削除：rd "さらば失敗プロジェクト"
削除成功
pdftk "CCF20141022_0000.pdf" "CCF20141022_0001.pdf" "CCF20141022_0002.pdf" "CCF20141022_0003.pdf" "CCF20141022_0004.pdf" "CCF20141022_0005.pdf" "CCF20141022_0006.pdf" "CCF20141022_0007.pdf" cat output "..\達人プログラマー.pdf"
PDF結合が完了：達人プログラマー.pdf
結合の完了したフォルダを削除：rd "達人プログラマー"
削除成功
pdftk "CCF20140817_0000.pdf" "CCF20140817_0001.pdf" "CCF20140817_0002.pdf" "CCF20140817_0003.pdf" "CCF20140817_0004.pdf" "CCF20140817_0005.pdf" "CCF20140817_0006.pdf" "CCF20140817_0007.pdf" "CCF20140817_0008.pdf" "CCF20140817_0009.pdf" "CCF20140817_0010.pdf" "CCF20140817_0011.pdf" cat output "..\HTML5Webアプリケーション作成入門.pdf"
PDF結合が完了：HTML5Webアプリケーション作成入門.pdf
結合の完了したフォルダを削除：rd "HTML5Webアプリケーション作成入門"
削除成功

・・・・

全処理が完了しました。
経過時間：2654.177秒
結合で生成されたPDFの数：399
```

４０分で４００個のPDFを生成している。

１分で１０個のPDFを結合結果として生成しているので，まあ速度は速いほう。

↑目次へ戻る

## （４）大量のPDFを一括で「１００ページごと」に分割するバッチ

pdftkを呼び出して，カレントフォルダ以下の全サブフォルダを再帰的に検査し，
各フォルダ内の全PDFのページ数を調べ，１００ページ単位で分割するバッチ。

「１００ページ単位で分割」というロジックの部分に，PDFの総ページ数を調べる処理が含まれている。

WSH/JSriptで記述。

**一括分割.bat**

```javascript
@if(0)==(0) ECHO OFF

cscript.exe //nologo //E:JScript "%~f0" "%~dp0" >out.log
@pause

GOTO :EOF
@end

/*
	カレント以下の全サブフォルダで，
	フォルダ内のPDFを適切なサイズに分割するバッチ

	※PDF分割にはpdftkを使用。事前に導入のこと
*/


// 何ページ単位に分割するか？
var pdf_page_max = 100;
	// 50だと300ページの本でもファイル数が多くなりすぎるため


// ------------- ライブラリ関数 -------------


function log(s){ WScript.Echo(s); }

//
function err(s){ WScript.StdErr.WriteLine(s); log(s); }
	// リダイレクトされずにコンソールにも表示される

// ベンチ用
function tic(){
	tic.startTime = new Date().getTime();
}
function tac(){
	var ms = new Date().getTime() - tic.startTime;
	tac.time_span = ms / 1000;
}
function how_many_seconds(){ // 計測時間が何秒だったかを返す
	return tac.time_span;
}


// 配列のイテレータ
Array.prototype.each = function( func ){
	for( var i = 0; i < this.length; i ++ ){
		func.call( this, this[i], i );
	}
	return this; // チェインを継続
};

// map
Array.prototype.map = function( func ){
	var _arr = [];
	this.each(function( item, ind ){
		_arr.push( func.call( _arr, item, ind ) );
	});
	return _arr;
};


// コマンド実行結果を行ごとに配列として取得
// http://language-and-engineering.hatenablog.jp/entry/20081225/1230198688
function exec_cmd( str_cmd, params ){

	// コマンドを実行したいカレントフォルダのパス
	var current_dir    = ( params ) ? params.current_dir : null;

	// 通信コマンドが終了するまで待つかどうか
	var wait_while_net = ( params ) ? params.wait_while_net : false;

	// 出力行から一行抜き出すための正規表現
	var get_one_output_re = ( params ) ? params.get_one_output_as : null;

	// 出力行から抜き出した一行をキャプチャするための文字列
	var capture_output_str = ( params ) ? params.capture_output_as : null;

	// コマンドを実際には実行しないデバッグモード
	var just_debug_mode = ( params ) ? params.just_debug : false;


	var ws = WScript.CreateObject("WScript.Shell");

	// 必要ならカレントフォルダをセット
	if( current_dir ){
		ws.CurrentDirectory = params.current_dir;
	}

	// もしデバッグモードなら，ここで終了
	if( just_debug_mode ){
		err( "カレントフォルダ：" + ws.CurrentDirectory + ", コマンド：" + str_cmd );
		err( "デバッグモードのため，コマンドは実行しません。" );

		return;
	}

	err( "実行します：カレントフォルダ：" + ws.CurrentDirectory + ", コマンド：" + str_cmd );

	// コマンド実行
		var proc = ws.Exec( "cmd /c " + str_cmd );

	// もしメール送信など通信系のコマンドであれば，終了まで待つ
	if( wait_while_net ){
		while( proc.Status == 0 ){
			WScript.Sleep(100);
		}
		// http://language-and-engineering.hatenablog.jp/entry/20100913/p1
	}

	// 出力を取得
	var str_out = proc.StdOut.ReadAll();

	// 出力の末尾の空行を削除
	var output_arr = str_out.split("\r\n");
	output_arr.pop();

	// 出力から一行だけ取り出す？
	if( get_one_output_re ){
		log("出力から一行取り出します。");
		var match_result = null;

		// 行ごとに検査
		output_arr.each(function(line){
			var m = line.match( get_one_output_re );

			// 初回マッチについて
			if( m && ( ! match_result ) ){
				// マッチ結果からキャプチャした文字列を保管
				match_result = line.replace(
					get_one_output_re,
					capture_output_str
				);
					err("マッチ結果を発見：" + match_result);
			}
		});

		// 全行を検査し終わってもマッチしていなかったらNG
		if( ! match_result ){
			throw("出力のどの行もマッチしませんでした。");
		}

		// マッチ結果を返す
		return match_result;
	}

	// 通常は出力の配列をそのまま返す
	return output_arr;
}


// 2桁に0埋め
function dig2( n ){
	if( n < 10 ){
		return "0" + n;
	}else{
		return "" + n;
	}
}



// ------------- メイン処理 -------------


// 分割の対象となったPDFの数
var divide_target_pdf_count = 0;

// 時間計測開始
tic();

// すべてのサブフォルダを列挙
var dirs = exec_cmd( "dir /a:D /s /b" );
dirs.each(function(dir_path){
		log(dir_path);

	// 分割すべきPDFがここに存在するか？
	var target_files = exec_cmd( 'dir /b *.pdf', {
		current_dir : dir_path
	});
		log(target_files.join("\n"));

	// 各PDFについて
	target_files.each(function( orig_pdf_name ){

		// ページ数を調べる

		// PDFTKでPDF情報をダンプする
		var get_page_command = 'pdftk "'
			+ orig_pdf_name
			+ '" dump_data'
		;

		// ページ数調査の実行
		var total_page_num = exec_cmd( get_page_command, {
			current_dir : dir_path,
			get_one_output_as : /^NumberOfPages: (\d+)$/,
			capture_output_as : "$1"
		});
			// 出力行の例
			// NumberOfPages: 192
		total_page_num = parseInt(total_page_num, 10);
			err("ページ数：" + total_page_num + ", " + orig_pdf_name);

		// 分割すべきページ量か？
		if( total_page_num <= pdf_page_max ){
			err("分割の必要なし");
			return; // 分割不要時
		}

		err( "分割の開始" );
		divide_target_pdf_count ++;

		// 分割用の名前を決定
		var pdf_name_main = orig_pdf_name.replace(/\.pdf$/, "");

		// 格納用のフォルダ作成
		var mkdir_command = 'mkdir "'
			+ pdf_name_main
			+ '"'
		;
		exec_cmd( mkdir_command, {
			current_dir : dir_path,
			just_debug : false
		});

		// PDFを分割
		var continue_flag = true;
		var divide_cnt = 1;
		while( continue_flag ){
			// 抽出の開始ページ
			var start_page = ( divide_cnt - 1 ) * pdf_page_max + 1;
			if( start_page > total_page_num ){
				err("最後のページまで抽出完了");
				continue_flag = false;
				break;
			}

			// 抽出の終了ページ
			var end_page = ( divide_cnt ) * pdf_page_max;
			if( end_page > total_page_num ){
				end_page = total_page_num;
			}

			// 抽出後のPDF名
			var new_pdf_name = pdf_name_main
				+ "_div" // 分割後のファイル名だとわかるようにしておく
				+ dig2( divide_cnt ) // 番号を0埋めして付与
				+ ".pdf"
			;
				err("分割後のファイル名：" + new_pdf_name);

			// 分割（というか抽出）コマンド
			var divide_command = 'pdftk "'
				+ orig_pdf_name
				+ '" cat '
				+ start_page
				+ "-"
				+ end_page
				+ ' output "'
				+ pdf_name_main // フォルダ内に出力する
				+ '\\'
				+ new_pdf_name
				+ '"'
			;
			exec_cmd( divide_command, {
				current_dir : dir_path,
				just_debug : false
			});

			divide_cnt ++;
		}

		// 分割前のPDFファイルも，消さずに残しておく。
		// 500冊で20GBぐらいだが，
		// Googleドライブは1TBオプションを使っていて容量に余裕があるし，
		// 外付けHDDを圧迫する分量でもないため。
		// また，まとめて１冊で取り扱いたい時もあるから。

		err("処理完了：" + orig_pdf_name );
	});
	err("このフォルダ内の処理完了：" + dir_path);
});

tac();

err("全処理が完了しました。");
err("経過時間：" + how_many_seconds() + "秒");
err("分割の対象となったPDFの総数：" + divide_target_pdf_count );
```

実行結果：

```text
実行します：カレントフォルダ：E:\book\01_開発・IT\_Java, コマンド：pdftk "Java_dezainpata-n_nyuumon_maruchisureddo_hen.pdf" dump_data
出力から一行取り出します。
マッチ結果を発見：704
ページ数：704, Java_dezainpata-n_nyuumon_maruchisureddo_hen.pdf
分割の開始
実行します：カレントフォルダ：E:\book\01_開発・IT\_Java, コマンド：mkdir "Java_dezainpata-n_nyuumon_maruchisureddo_hen"
分割後のファイル名：Java_dezainpata-n_nyuumon_maruchisureddo_hen_div01.pdf
実行します：カレントフォルダ：E:\book\01_開発・IT\_Java, コマンド：pdftk "Java_dezainpata-n_nyuumon_maruchisureddo_hen.pdf" cat 1-100 output "Java_dezainpata-n_nyuumon_maruchisureddo_hen\Java_dezainpata-n_nyuumon_maruchisureddo_hen_div01.pdf"
分割後のファイル名：Java_dezainpata-n_nyuumon_maruchisureddo_hen_div02.pdf
実行します：カレントフォルダ：E:\book\01_開発・IT\_Java, コマンド：pdftk "Java_dezainpata-n_nyuumon_maruchisureddo_hen.pdf" cat 101-200 output "Java_dezainpata-n_nyuumon_maruchisureddo_hen\Java_dezainpata-n_nyuumon_maruchisureddo_hen_div02.pdf"
分割後のファイル名：Java_dezainpata-n_nyuumon_maruchisureddo_hen_div03.pdf
実行します：カレントフォルダ：E:\book\01_開発・IT\_Java, コマンド：pdftk "Java_dezainpata-n_nyuumon_maruchisureddo_hen.pdf" cat 201-300 output "Java_dezainpata-n_nyuumon_maruchisureddo_hen\Java_dezainpata-n_nyuumon_maruchisureddo_hen_div03.pdf"
分割後のファイル名：Java_dezainpata-n_nyuumon_maruchisureddo_hen_div04.pdf
実行します：カレントフォルダ：E:\book\01_開発・IT\_Java, コマンド：pdftk "Java_dezainpata-n_nyuumon_maruchisureddo_hen.pdf" cat 301-400 output "Java_dezainpata-n_nyuumon_maruchisureddo_hen\Java_dezainpata-n_nyuumon_maruchisureddo_hen_div04.pdf"
分割後のファイル名：Java_dezainpata-n_nyuumon_maruchisureddo_hen_div05.pdf
実行します：カレントフォルダ：E:\book\01_開発・IT\_Java, コマンド：pdftk "Java_dezainpata-n_nyuumon_maruchisureddo_hen.pdf" cat 401-500 output "Java_dezainpata-n_nyuumon_maruchisureddo_hen\Java_dezainpata-n_nyuumon_maruchisureddo_hen_div05.pdf"
分割後のファイル名：Java_dezainpata-n_nyuumon_maruchisureddo_hen_div06.pdf
実行します：カレントフォルダ：E:\book\01_開発・IT\_Java, コマンド：pdftk "Java_dezainpata-n_nyuumon_maruchisureddo_hen.pdf" cat 501-600 output "Java_dezainpata-n_nyuumon_maruchisureddo_hen\Java_dezainpata-n_nyuumon_maruchisureddo_hen_div06.pdf"
分割後のファイル名：Java_dezainpata-n_nyuumon_maruchisureddo_hen_div07.pdf
実行します：カレントフォルダ：E:\book\01_開発・IT\_Java, コマンド：pdftk "Java_dezainpata-n_nyuumon_maruchisureddo_hen.pdf" cat 601-700 output "Java_dezainpata-n_nyuumon_maruchisureddo_hen\Java_dezainpata-n_nyuumon_maruchisureddo_hen_div07.pdf"
分割後のファイル名：Java_dezainpata-n_nyuumon_maruchisureddo_hen_div08.pdf
実行します：カレントフォルダ：E:\book\01_開発・IT\_Java, コマンド：pdftk "Java_dezainpata-n_nyuumon_maruchisureddo_hen.pdf" cat 701-704 output "Java_dezainpata-n_nyuumon_maruchisureddo_hen\Java_dezainpata-n_nyuumon_maruchisureddo_hen_div08.pdf"
最後のページまで抽出完了
処理完了：Java_dezainpata-n_nyuumon_maruchisureddo_hen.pdf

・・・

全処理が完了しました。
経過時間：5824.602秒
分割の対象となったPDFの総数：803
```

１００分で８００個のPDFを分割対象として処理している。

↑目次へ戻る

## 結論と補足

PDFの一括処理が必要になるのはどうしてか。

それは，今はやりの「電子書籍の自炊」のためだったりする。

自分で，ドキュメントスキャナを使って作成したPDFは

- １冊の本がマチマチのページ数に分かれている
- ファイル名も本の名前ではない

なので，まずはスキャン結果を１冊の本に対応する１個のPDFファイルとしてまとめるために，結合処理が必要。

それが今回述べたpdftkによる一括結合バッチだ。

PDFの結合と同時に，ファイル名として本の名前を日本語でリネームしてもいる。

また，それらのPDFファイルを全てクラウド上に保管するわけだが，
Googleドライブ上では，ファイル名が日本語ではなく，
半角英数字のファイル名であったほうがよい。

なので，下記エントリのように kakasiを使って，ファイル名を日本語から半角英数字に変換している。

Windowsで「kakasi」のコマンドを使い，日本語文章を単語に分解，ローマ字変換する方法 （kakasiで形態素解析するWindowsバッチのサンプルコード）
`http://language-and-engineering.hatenablog.jp/entry/20150109/KakasiOnWindowsU...`

こうしておけば，クラウド上のデータをiOS端末で開いた時に，
iBooksやGoodReaderなどのリーダーアプリに「送る」で転送・管理することができる。

また，古いiPadを電子書籍リーダーとして使う場合，PDFのサイズが大きいと開けない。

iPad1だと，５０MBや１００MBぐらいのPDFになると，Googleドライブ上で開いた瞬間にアプリが落ちる。

いつまでも開くことができないのだ。

なので，PDFのファイルサイズを調整して，
メモリの少ない低スペック端末でもPDFを開けるようにする必要がある。

それが，今回述べたpdftkによるPDF分割処理だ。

電子書籍の自炊について，ツールや方法の参考：

- [自炊に役立つドキュメントスキャナ「ADS-2000」の長所・短所まとめ](http://computer-technology.hateblo.jp/entry/20140810/p1)
- [自炊に役立つカールのディスクカッター「DC-210N」。大型の裁断機より軽くてコンパクト](http://computer-technology.hateblo.jp/entry/20140810/p2)
- [お風呂でタブレットで読書には，普通のiPadと防水ケースの組み合わせがベスト](http://computer-technology.hateblo.jp/entry/20140817/p3)

まとめると，大量のPDFに対して下記の操作をバッチで行なえる。

- 一括で結合
- 一括で日本語にリネーム
- 一括で半角英数字にリネーム
- 一括で１００ページごとに分割

これを全て無料ツールだけで実行できるのだ。

こういう手法を整備しておけば，個人の本棚もきれいさっぱり。

業務のペーパレス化・ドキュメント整備もはかどる。

Windowsバッチを使って，快適な自炊ライフを。

関連する記事：

- [バッチで，画像を生成・加工・一括処理しよう　（WSH/JScriptでImageMagickを呼び出す方法）](http://language-and-engineering.hatenablog.jp/entry/20111019/p1)
- [バッチで，Word文書の内容を読み取ろう　（WSH/JScriptでWordファイルを操作する方法）](http://language-and-engineering.hatenablog.jp/entry/20101105/p1)
- Excel VBAで，フォルダ内の画像ファイルを一括でシートに取り込み，サムネイルのアルバムを自動生成 `http://language-and-engineering.hatenablog.jp/entry/20131109/GenerateImageThu...`
- [UTF8Nの複数テキストを，一斉に置換するバッチ （JScriptでUTF8Nのファイルを読み書き）](http://language-and-engineering.hatenablog.jp/entry/20090723/p1)
- [WSHバッチで，OpenOffice.org Calcを自動操作する方法 （表計算のブックを，COM経由で新規作成・読み書き・保存）](http://language-and-engineering.hatenablog.jp/entry/20141227/OOoCalcByWSHJScript)
