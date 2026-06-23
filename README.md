# 本要約センター — Webサイト用 書籍データフィード（公開）

認証不要でGETできる公開フィードです。本要約センターのパイプラインが**毎日 6:00 JST**に再生成し、
このリポジトリの `honyo_site_export.json` を更新します。

## 固定URL（認証不要・CORS不要・サーバー/ビルド時取得）
```
https://raw.githubusercontent.com/takaakisugiyama-ship-it/honyo-site-data/main/honyo_site_export.json
```
※ raw.githubusercontent.com はCDNキャッシュ（数分）あり。日次更新には十分。

## スキーマ（schema_version = 1）
```jsonc
{
  "generated_at": "ISO8601 UTC",
  "schema_version": 1,
  "count": 110,
  "affiliate_amazon_tag": "otona_radio-22",
  "books": [{
    "asin": "B0F2HGTDSV",          // 一意キー(ASIN or ISBN-10の混在)
    "slug": "b0f2hgtdsv",          // = asin.lower()
    "title_book": "科学的に証明されたすごい習慣大百科",
    "title_video": "【徹底解説】…",  // YouTube動画タイトル(装飾付き)
    "author": "堀田秀吾",           // best-effort・null有
    "publisher": null,             // フィードに無し(常にnull)
    "genre": "自己啓発",            // お金/経営/マネジメント/教養/自己啓発/健康
    "amazon_url": "https://www.amazon.co.jp/dp/<ASIN>?tag=otona_radio-22&linkCode=ll1",
    "amazon_cover_url": "https://images-na.ssl-images-amazon.com/images/P/<ASIN>.jpg",
    "rakuten_url": null,           // pinned_commentにある時のみ・大半null
    "cover_scan": null,            // 公開フィードでは未提供(amazon_cover_urlを使用)
    "summary_md": "▼ 書籍 …",      // YouTube概要欄の散文(Web掲載可・生OCR全文は非含)
    "chapters": [{"t":"0:00","title":"…"}],
    "videos": [                    // 1冊にlong/medium最大2本。1動画=1冊(多対多無し)
      {"format":"long","variant":"v5_emotion","video_id":"…","url":"…","privacy":"public","publish_at":null,"uploaded_at":"…"},
      {"format":"medium","variant":"v15_digest","video_id":"…","url":"…","privacy":"unlisted","publish_at":null,"uploaded_at":"…"}
    ],
    "has_raw": true,
    "raw_type": "ocr",
    "updated_at": "ISO8601 UTC"
  }]
}
```

## 注意
- 書影はこのフィードには含めず、各書の `amazon_cover_url`（公開Amazon画像）を使用してください。
- サイト掲出は原則 `videos[].privacy == "public"` のみ。
- 出版社 / ISBN-13 / 読了時間 / excerpt はフィードに無し（Web側で補完）。
- 文字コード=UTF-8、日付=ISO8601(UTC)。
