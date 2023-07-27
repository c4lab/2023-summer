# crc-meta
## plan

7/20
1. 校對明儒下週要介紹的DeepMicrobes投影片
2. 乃恩目前打算用 [KMCP](https://academic.oup.com/bioinformatics/article/39/1/btac845/6965021) 來做reads classification，但目前在[github](https://github.com/shenwei356/kmcp)沒找到pre-trained model weight，可能要重頭train一個model
3. 原本打算用MetaPhlan來與kraken做出來的結果比較，但有[文獻](https://www.nature.com/articles/s41592-021-01141-3)說他們兩個output的東西其實不一樣，一個是sequence abundance 一個是 cell(?) abundance，可能轉為嘗試kraken下游分析differential species的軟體

7/27
明儒：
1. train model時會遇到使用超過10% memory的問題（待確定）
2. 要把所有reference genome合併cat到一個檔會跳error

乃恩：
1. KMCP沒有提供pretrained model，先想辦法用github repo的test資料試訓練一個model

青勁：
1. [Pathonoia](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-023-05144-z), [Recentrifuge](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1006967)，看起來算是kraken的改良版（？），能分辨找出的species哪些是False Positive，[DiTASiC](https://academic.oup.com/bioinformatics/article/33/14/i124/3953953?login=false)還多了自己提出的differential方法
2. Recentrifuge [github](https://github.com/khyox/recentrifuge/wiki/Running-recentrifuge-for-Kraken)看起來是可以直接吃kraken/bracken output檔，然後吐出比較乾淨的結果，可能把之前的結果過一遍Recentrifuge再重畫火山圖，看differential species有沒有被文獻支持QQ
