index.htmlをブラウザで実行するとテストできます。

##  ゴルフ統計Pro v2.0 — チェンジログ 2025/10/07

###  デザイン & UI

* アプリ全体のデザインを全面リニューアル
  より立体感のあるシャドウ、柔らかなグラデーション、滑らかなアニメーションを追加。
* コンテナやカードの角丸を拡大（20px → 24px）し、モダンで上質な見た目に。
* 見出しやラベルのフォントウェイトを強化し、可読性を改善。
* ボタンやカードにホバーアニメーションを追加、操作感を向上。
* 各タブやセクション間に余白を追加し、情報の見やすさを最適化。

###  機能改善

* **風向き設定**が新方式に対応し、より細分化（フォロー/アゲインスト/横風）された9段階で入力可能。
* **距離単位の自動切り替え**に対応：
  グリーン上ではメートル、それ以外はヤードを自動表示。
* **番手選択の動的更新**を強化：
  グリーンに切り替えた際、自動的に「PT（パター）」を選択。
* **アニメーション導入**：各コンポーネントに`slideIn`や`fadeIn`アニメーションを実装し、スムーズな画面遷移を実現。
* **スコア表・統計カードの強化**：
  FWキープ率、パーオン率、寄せワン率、サンドセーブ率などの表示が視覚的に改善。
* **グラフタブの改良**：
  Chart.jsの最新バージョンを活用し、スコア推移・分布・ヒートマップの描画を最適化。

###  SG分析（Strokes Gained）

* SG分析機能を再構築し、

  * 総合SG（Total / T2G）
  * カテゴリ別（OTT, APP, ARG, PUT）
  * 個人ベースライン比較
  * 番手別SG分析
    をわかりやすく整理。
* SGカードを専用カラー（紫系グラデーション）で統一し、識別性を強化。

###  その他の改善

* **設定モーダル**のデザイン刷新：クラブ管理やベースラインリセット操作を直感的に。
* **コード全体の構造整理**とセクション分割を実施。
  HTMLの可読性と保守性を向上。
* 軽微なバグ修正とアニメーション最適化。
* データの質を向上させるために「ラウンド終了」を削除。新しいラウンドを始める際にはリセットをしてください。
* リセットの際には生成済みの個人ベースラインは削除されないように。（設定から削除可能）
* 操作の簡略化に伴いアドバンスド、シンプルの切り替えを削除

---

このプロジェクトはゴルフ統計計算アプリのソースです。







以下はindex.htmlをアプリストアに公開する手順です。

Android（Google Play）
>>>
必要なもの
 Android Studio
 開発者登録（25USD 一度きり）

手順
 Android Studioで新規プロジェクトを作成
 「Empty Activity」でOK
 assets フォルダを作り、その中に index.htmlを置く
 MainActivity.java または MainActivity.kt で WebViewを使ってindex.htmlを読み込む

 class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        val webView = WebView(this)
        webView.settings.javaScriptEnabled = true
        webView.loadUrl("file:///android_asset/index.html")
        setContentView(webView)
    }
}

ビルドして APK または AAB を生成
Google Playは現在 AAB必須

iOS（App Store）
必要なもの
 Mac（Xcode必須）
 Apple Developer Program 登録（年間99USD）

手順
 xcodeで新規プロジェクトを作成（Appテンプレート）
 WKWebView を配置し、index.html を読み込むようにする

 import UIKit
import WebKit

class ViewController: UIViewController {
    override func viewDidLoad() {
        super.viewDidLoad()
        let webView = WKWebView(frame: self.view.frame)
        if let filePath = Bundle.main.path(forResource: "index", ofType: "html") {
            let url = URL(fileURLWithPath: filePath)
            webView.loadFileURL(url, allowingReadAccessTo: url.deletingLastPathComponent())
        }
        self.view.addSubview(webView)
    }
}
index.html（＋CSS, JS）をプロジェクトに追加
ビルド → 実機テスト → IPAファイルを生成
XcodeやTransporter経由でApp Store Connectへアップロード & 公開

Google Play Consoleからアップロード & 公開
