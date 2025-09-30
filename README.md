index.htmlをブラウザで実行するとテストできます。


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
