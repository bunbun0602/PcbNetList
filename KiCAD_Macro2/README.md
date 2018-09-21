# "Any2Kicad.py"について


## Ａ.概要
+ "Any2Kicad.py"は、KiCADv4の基板設計ソフトPcbnewで動作するマクロプログラムであり、回路CADのネットリスト（Calay / CR-5000(CCF) / DK-Σ /  MM-2 / Telesis / PADS / Intergraph / KiCAD）を入力し、Pcbnew用ネットリストを出力するソフトです。


## Ｂ.ファイル内容
1. "Any2Kicad.py"   ... 8種類のネットリストからKicad用ネットリストへ変換するソフト（マクロ）
2. "telesis.net"    ... サンプルTelesisネットリスト(Bsch3V 0.82.01の中に付属された
　　　　　　　　　　　サンプル回路：「LEDPORT.CE3」より生成）
3. "calay.net"      ... サンプルCalayネットリスト
4. "partlist.csv"   ... サンプル部品情報ファイル


## Ｃ.動作確認環境
+ KiCAD Ver4.07 on Windows7-64bit　/ Ubuntu14.04LTS-64bit  


## Ｄ.使用方法
1. 回路CADで、ネットリストを下記の形式に従ったファイル名で、ネットリストを作成する。  
    
     |ネットリスト形式  |ファイル名      |   
     |:-----------------|:---------------|                                          
     | Calay形式        | "calay.net"    |    
     | CR-5000(CCF)形式 | "ccf.net"      |  
     | DK-Σ形式         | "dks.net"      |  
     | MM-2形式         | "mm2.net"      |  
     | Telesis形式      | "telesis.net"  |  
     | PADS形式         | "pads.net"     |  
     | Intergraph形式   | "intergra.net" |  
     | KiCad形式        | "kicad.net"    |  
  
2. このファイルを、KiCadのこれから編集する基板設計フォルダーへ、コピーする。
3. Pcbnewを起動し、Pythonコンソールを選択実行する。　
4. コンソール内で、「pwd」を実行し、出てきたフォルダ（普通は"C:\Program Files\KiCad")へ、本ソフト**"Any2Kicad.py"と上のフォルダにある"PcbNetList.py"**をコピーする。
5. コンソール内で、「execfile("Any2Kicad.py")」と入力、実行する。
6. Pcbnew用ネットリスト（自動的に「プロジェクト名」+ ".net"に設定）ファイルが生成される。尚、生成されたファイルは、部品パッドが各部品最大ピン数のピンヘッダやQFPパッケージを自動的に割り当てられる。
7. そのネットリストをインポートします。　その後、部品パッドを変更すれば、基板設計できます。
8. 上記7までの方法は部品一品毎に変更なので部品が多いと面倒です。それで、部番と部品パッド情報をcsvファイルで用意できれば、それを使っても、KiCAD用ネットリストを作成できます。  
+部番と部品パッド情報のcsvファイル名"partlist.csv"として、添付サンプルを参考に、今編集している基板設計フォルダーで、作成してください。    
+この状態で、上記5と同じようにコンソール内で、「execfile("Any2Kicad.py")」と入力実行すると、プログラムは、自動的に"partlist.csv"を検出し、このファイルを使ってネットリストが生成されます。
9. ネットリストのインポート時にエラーが発生した場合や、回路図に変更があった場合は、Pcbnewの「ファイル」->「エキスポート」->「コンポーネントファイル(.cmp)」を選択し、今設計している基板のコンポーネントファイルを作成してください。　その後、上記5〜7と同様にPythonコンソールで「execfile("Any2Kicad.py")」と入力実行して、更新されたネットリストを作成後、それをインポートしてください。  

## Ｅ.その他 
1. 回路CADネットリストのピン番号に英文字を含んでいる時やピン番号が256超える場合は、インポート時エラーが発生します。この場合は、部品パッド変更後、上記「Ｄ.使用方法」項目9を実行すれば、エラーはなくなります。   
2. 他に生成されるファイル"NET.TXT"は、ネットリストが正しく認識されたかを確認する為のものです。  
3. Pcbnewで部品パッドを変更する方法は、部品選択後 -> "e"を押して「プロパティ」 -> 「フットプリントの変更」 -> 「フットプリントの表示」です。尚、部品定数は、「部番記号」:「最大ピン数」（例："C:2"）になっていますので、「フットプリントの変更」の「オプション」を使って、抵抗・コンデンサ等をまとめてパッド変換可能です。  
4. Pcbnew基板のコンポーネント(cmp)ファイルから部品パッド情報(csv)ファイルへ変換するマクロは、「Orcad2Kicad」プロジェクト内の「cmp2csv」で公開されています。

## Ｆ.参考にさせて頂いたサイト 
+ 「KiCad用のPythonスクリプト ～ ほぼ回路図の配置通りにフットプリントを予備配置する」
        <https://qiita.com/silvermoon/items/da4fcdba319f46570a60>


## Ｇ.変更履歴 
---
2018/09/22   (7th commit)
      
---