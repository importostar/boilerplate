---
title: account info (1)
date: 2020-05-07
---
Example Python program account-info (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* import numpy as np
* import pandas as pd
* import multiprocessing
* import matplotlib.pyplot as plt
* from multiprocessing import Queue
* import web3
* # import matplotlib.mlab as mlab
* # import matplotlib.pyplot as plt

## Methods

* def get_account_nonce(file):
* def get_nonce(df):
* def write_nonce(count):

## Code

Python example

    import os
    import numpy as np
    import pandas as pd
    import multiprocessing
    import matplotlib.pyplot as plt
    from multiprocessing import Queue
    import web3
    
    # import matplotlib.mlab as mlab
    # import matplotlib.pyplot as plt
    
    
    def get_account_nonce(file):
        pdata = pd.read_csv('accounts.csv')
    
        infura = web3.Web3(web3.Web3.HTTPProvider('https://mainnet.infura.io/v3/6298c99dc1ee434aa64cf0c3c19e365f'))
    
        q = Queue()
    
        def get_nonce(df):
            for index, row in df.iterrows():
                addr = row[0]
                ether = row[1]
                nonce = infura.eth.getTransactionCount(addr, 'latest')
                q.put_nowait((addr, ether, nonce))
    
        def write_nonce(count):
            with open(file, 'a') as f:
                f.write('Account,Ether,Nonce\n')
                got = 0
                while got < count:
                    addr, ether, nonce = q.get()
                    f.write("{},{},{}\n".format(addr, ether, nonce))
                    got += 1
                print("get: {}, len: {}".format(got, len(pdata)))
    
        processes = []
    
        total = 10
        for i in range(total):
            step = len(pdata) // total
            start = i * step
            end = start + step if i < total - 1 else len(pdata)
            process = multiprocessing.Process(target=get_nonce, args=(pdata[start:end], ))
            processes.append(process)
            process.start()
    
        write_process = multiprocessing.Process(target=write_nonce, args=(len(pdata), ))
        processes.append(write_process)
        write_process.start()
    
        for process in processes:
            process.join()
    
        q.close()
    
    
    nonce_file = "nonce.csv"
    if not os.path.exists(nonce_file):
        get_account_nonce(nonce_file)
    
    pdata = pd.read_csv(nonce_file)
    
    
    top_accounts = pdata[pdata['Ether'] >= 200000].sort_values('Ether', ascending=False).reset_index(drop=True)
    top_accounts_len = len(top_accounts)
    print("The top {} accounts are\n {}".format(top_accounts_len, top_accounts))
    top_accounts.to_csv('top-{}.csv'.format(top_accounts_len), index_label='Index')
    print("The sum of top {} accounts balance are: {}, take in charge of {}".format(
        top_accounts_len, top_accounts.sum()['Ether'], top_accounts.sum()['Ether'] / pdata.sum()['Ether']
    ))
    maximum_account = pdata.max()
    
    
    plt.clf()
    plt.figure(figsize=(20, 10))
    plt.xlabel('Balance')
    plt.ylabel('Count')
    plt.tight_layout()
    
    the_next_account = top_accounts['Ether'].iloc[-1]
    plt_data = pdata[pdata['Ether'] < the_next_account]['Ether']
    bins = np.arange(0, the_next_account, 1000)
    
    plt.hist(plt_data, density=False, bins=bins, facecolor='green', alpha=0.85)
    
    plt.title('Account 54th..(total: {}/{})'.format(len(plt_data) - top_accounts_len, len(plt_data)))
    plt.grid(True)
    plt.savefig('genesis-summary.png', dpi=100)
    
    # clear the current figure
    plt.clf()
    plt_data = pdata[pdata['Ether'] < 25000]['Ether']
    bins = np.arange(0, 25000, 100)
    
    # normalize probability from
    # https://github.com/matplotlib/matplotlib/issues/10398/#issuecomment-366021979
    weights = np.ones(len(plt_data)) / len(plt_data)
    plt.hist(plt_data, bins=bins, density=False, weights=weights, facecolor='green', alpha=0.85)
    
    plt.title('Account ether balance <10000 (total: {})'.format(len(plt_data)))
    plt.xlabel('Balance')
    plt.ylabel('Percent')
    plt.axis([0, 25000, 0, 0.15])
    plt.grid(True)
    plt.savefig('genesis-0-25000.png', dpi=100)
    
    plt.clf()
    plt_data = pdata[pdata['Nonce'] < 1000]['Nonce']
    bins = np.arange(0, 1000, 50)
    
    # normalize probability from
    # https://github.com/matplotlib/matplotlib/issues/10398/#issuecomment-366021979
    weights = np.ones(len(plt_data)) / len(plt_data)
    plt.hist(plt_data, bins=bins, density=False, weights=weights, facecolor='green', alpha=0.85)
    
    plt.title('Account Nonce <1000 (total: {})'.format(len(plt_data)))
    plt.xlabel('Nonce')
    plt.ylabel('Percent')
    plt.axis([0, 1000, 0, 1])
    plt.grid(True)
    plt.savefig('nonce.png', dpi=100)
    
    
    plt.clf()
    plt_data = pdata[(pdata['Ether'] > 10000) & (pdata['Ether'] < 100000)]['Ether']
    bins = np.arange(10000, 100000, 1000)
    weights = np.ones(len(plt_data)) / len(plt_data)
    plt.hist(plt_data, bins=bins, density=False, weights=weights, facecolor='green', alpha=0.85)
    
    plt.title('Account ether balance 10000-100000 (total: {})'.format(len(plt_data)))
    plt.xlabel('Balance')
    plt.ylabel('Percent')
    plt.axis([10_000, 100_000, 0, 0.4])
    plt.grid(True)
    plt.savefig('genesis-10000-100000.png', dpi=100)
    
    
    plt.clf()
    plt_data = pdata[pdata['Ether'] > 100000]['Ether']
    bins = np.arange(100000, 1000000, 10000)
    weights = np.ones(len(plt_data)) / len(plt_data)
    plt.hist(plt_data, bins=bins, density=False, weights=weights, facecolor='green', alpha=0.85)
    
    plt.title('Account ether balance 10000-100000 (total: {})'.format(len(plt_data)))
    plt.xlabel('Balance')
    plt.ylabel('Percent')
    plt.axis([100_000, 1_000_000, 0, 0.4])
    plt.grid(True)
    plt.savefig('genesis-100000-1000000.png', dpi=100)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
