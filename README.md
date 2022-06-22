# AngleSharp
## C# でスクレイピングの実現

<img src= "https://user-images.githubusercontent.com/88915966/174937856-8ba8995e-0e6b-4d74-96e4-e989c7a2d1e8.jpg">

~~~
    class Process
    {
        public static string _str = "";
        public Process(string str, string site)
        {
            _str = str;
        }

        public async Task<System.Collections.Generic.IEnumerable<string>> searchByGoogle()
        {
            // セットアップ
            var config = Configuration.Default.WithDefaultLoader();
            var context = BrowsingContext.New(config);

            // 検索ページを開く
            await context.OpenAsync("https://www.google.co.jp/");

            // 指定したキーワードで、検索を行う
            await context.Active.QuerySelector<IHtmlFormElement>("form").SubmitAsync(new
            {
                q = _str,
            });

            // 検索結果のタイトル一覧を取得する
            var tags = context.Active.QuerySelectorAll("h3");
            var titles = tags.Select(m => m.TextContent);

            return titles;
        }
    }
~~~
