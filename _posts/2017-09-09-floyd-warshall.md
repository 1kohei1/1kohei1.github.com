---
layout: post
title: "ワーシャルフロイドの最小の初期値"
description: ""
category: 
tags: [競プロ]
image: "/assets/floyd-warshall/wa-1.png"
---
{% include JB/setup %}
今日は[ABC-73](http://abc073.contest.atcoder.jp/)でした。D問題を勘違いして解けませんでした。
その後解いたのですが、ワーシャルフロイドの最小の初期値はいくつだろうと考えたので、その考察です。

最初は距離の最大値+1だと思ったのですが、それではWAでした。
![floyd warshall WA 1]({{ site.url }}/assets/floyd-warshall/wa-1.png)

次に、距離の最大値を2倍して1を足したらいけるんじゃないかと試すもWAです。
![floyd warshall WA 2]({{ site.url }}/assets/floyd-warshall/wa-2.png)

よくよく考えてみると、距離の最大値×2+1でも、それを上回る距離で行ける点がみつかります。例えば距離の最大値が100の場合、
![floyd warshall AC]({{ site.url }}/assets/floyd-warshall/too-low-initial-value.png)
上のケースでは正しくAからCの距離が200にアップデートされます。ですが、下のケースでは201の方が距離の合計より小さいため、201でAからCへ行けることになります。初期値が小さすぎて、正しく距離が計算されてなかったのがWAの原因でした。

これを踏まえて最小初期値を考えます。ある点Aから点Bへ行くのに、最大N-1の道を経由することになるので、最小の初期値は`距離の最大値×(N-1)+1`だとわかります。

![floyd warshall AC]({{ site.url }}/assets/floyd-warshall/ac.png)

こんなことしなくても、単純に`Integer.MAX_VALUE / 2`を初期値に設定すれば解けますが、気になったので考えてみました。