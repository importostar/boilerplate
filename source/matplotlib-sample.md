---
title: matplotlib sample
date: 2020-05-07
---
Example Python program matplotlib-sample.py

## Modules

* from matplotlib import pyplot as plt

## Code

Python example

    from matplotlib import pyplot as plt
    
    # see http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.plot
    
    # 画像サイズ指定. 
    plt.figure(figsize=(25, 8))
    
    # 凡例などにTeX表記を使用. 
    plt.rc('text', usetex=True)
    
    # 
    plt.plot(x, y, "r-", label=r"$a_1$", lw=4)
    plt.plot(x, y, "g-", label=r"$a_2$", lw=4)
    
    # 10色作成
    colors = cm.jet(np.linspace(0,1,10))
    plt.plot(xx, a1, "--", color=colors[i], label=str(i+11))
    
    # x軸, y軸のラベル. 
    plt.xlabel("time", fontsize=30)
    plt.ylabel("gyarion radii", fontsize=30)
    
    # 軸のフォント. 
    ax = plt.gca()
    for i in ax.get_xticklabels():
        i.set_fontsize(20)
    for j in ax.get_yticklabels():
        j.set_fontsize(20)
    
    # テキスト. 座標(60, .025)にテキストを表示.
    plt.text(60, .025, r'$\mu=100,\ \sigma=15$')
    
    # タイトル
    plt.title('Histogram of IQ')
    
    # 横軸を(40, 160), 縦軸を(0, 0.03). 
    plt.axis([40, 160, 0, 0.03])
    
    # 凡例.
    plt.legend(loc='lower right', fontsize=25, ncol=3, bbox_to_anchor=(1.1, 1.05))
    
    # グリッド
    plt.grid(True)
    
    # 矢印.
    plt.annotate('local max', xy=(2, 1), xytext=(3, 1.5),
                arrowprops=dict(facecolor='black', shrink=0.05),
                )
    
    # 保存.
    plt.savefig("hoge.png")
    
    # 閉じる. 
    plt.close()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
