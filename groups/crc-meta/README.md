# crc-meta
## plan

7/20
1. 校對明儒下週要介紹的DeepMicrobes投影片
2. 乃恩目前打算用 [KMCP](https://academic.oup.com/bioinformatics/article/39/1/btac845/6965021) 來做reads classification，但目前在[github](https://github.com/shenwei356/kmcp)沒找到pre-trained model weight，可能要重頭train一個model
3. 原本打算用MetaPhlan來與kraken做出來的結果比較，但有[文獻](https://www.nature.com/articles/s41592-021-01141-3)說他們兩個output的東西其實不一樣，一個是sequence abundance 一個是 cell(?) abundance，可能轉為嘗試kraken下游分析differential species的軟體

7/27

明儒：
1. train model時會遇到使用超過helix 10% system memory的問題（待確定）
2. 要把所有reference genome合併cat到一個檔會跳error，改用 `find . -name "*.fa" | xargs -i cat {} allfiles.fa` 已可解決

乃恩：
1. KMCP沒有提供pretrained model，先想辦法用github repo的test資料試訓練一個model
2. 需要用的工具已經下載完畢且可以使用
3. 目前正在下載dataset

青勁：
1. [Pathonoia](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-023-05144-z), [Recentrifuge](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1006967)，看起來算是kraken的改良版（？），能分辨找出的species哪些是False Positive，[DiTASiC](https://academic.oup.com/bioinformatics/article/33/14/i124/3953953?login=false)還多了自己提出的differential方法
2. Recentrifuge [github](https://github.com/khyox/recentrifuge/wiki/Running-recentrifuge-for-Kraken)看起來是可以直接吃kraken/bracken output檔，然後吐出比較乾淨的結果，可能把之前的結果過一遍Recentrifuge再重畫火山圖，看differential species有沒有被文獻支持QQ


8/3

明儒：
1. 正在用tmux把所有下載的reference genome合併到一個檔
2. 確定模型輸出要分幾類（九萬多（？））

乃恩：
1. 使用作者給的測資沒有重現同樣的結果
2. 嘗試檢查database是否有誤

青勁：
1. Recentrifuge試跑kraken的結果沒辦法直接接到bracken，有點悲劇
2. 看了Steven Salzberg打臉（？）之前在nature上的[文章](https://www.nature.com/articles/s41586-020-2095-1)，主要討論兩個[問題](https://www.biorxiv.org/content/10.1101/2023.07.28.550993v1.full.pdf)
- GRCh37/38 不夠完整，會有大量的人類序列被分配給微生物，建議改用CHM13，各種微生物的read counts會少非～～～常多
- Voom-SNM這個normalization方法有非常嚴重的偷看答案嫌疑

