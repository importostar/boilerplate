---
title: evaluations
date: 2020-05-07
---
Example Python program evaluations.py

## Modules

* import tensorflow as tf
* import numpy as np
* import sys
* from datetime import datetime
* import warnings
* from sklearn.cluster import KMeans
* from sklearn.metrics import normalized_mutual_info_score as NMI
* from sklearn.utils.linear_assignment_ import linear_assignment
* import matplotlib
* import matplotlib.pyplot as plt
* import matplotlib.cm as cm
* from sklearn.decomposition import PCA
* import matplotlib
* import matplotlib.pyplot as plt
* import matplotlib.cm as cm
* from MulticoreTSNE import MulticoreTSNE as TSNE

## Methods

* def eval_acc(e2e_in, enc, data, ground_truth, n_clusters, SEED=1234):
* def log(s, label='INFO'):
* def cluster_acc(Y_pred, Y):
* def plot_class_space_PCA2d(z, labels, out=None, distinct=False):
* def plot_class_space_tSNE(z, labels, out=None, distinct=False):
* def vis_2d_distributions(e2e_in, enc, data, ground_truth, flag='PCA'):

## Code

Python example

    import tensorflow as tf
    import numpy as np
    import sys
    from datetime import datetime
    
    # Suppress sklearn warnings
    
    import warnings
    warnings.filterwarnings("ignore", category=FutureWarning)
    
    ##############################################################################
    # Evaluation (Clustering accuracy)
    ##############################################################################
    
    
    def eval_acc(e2e_in, enc, data, ground_truth, n_clusters, SEED=1234):
        # Define pseudo model to get intermidiate layer output
        E2E_HIDDEN_OUT = tf.keras.models.Model(inputs=e2e_in.input,
                                               outputs=enc.output)
        # Get hidden layer value
        Z = E2E_HIDDEN_OUT.predict(data)
        from sklearn.cluster import KMeans
        from sklearn.metrics import normalized_mutual_info_score as NMI
    
        # Logging messages such as loss,loading,etc.
    
        def log(s, label='INFO'):
            sys.stdout.write(
                label + ' [' + str(datetime.now()) + '] ' + str(s) + '\n')
            sys.stdout.flush()
    
        # Unsupervised clustering accuracy from DEC
        # (https://arxiv.org/pdf/1511.06335.pdf)
    
        def cluster_acc(Y_pred, Y):
            from sklearn.utils.linear_assignment_ import linear_assignment
            assert Y_pred.size == Y.size
            D = max(Y_pred.max(), Y.max()) + 1
            w = np.zeros((D, D), dtype=np.int64)
            for i in xrange(Y_pred.size):
                w[Y_pred[i], Y[i]] += 1
            ind = linear_assignment(w.max() - w)
            return sum([w[i, j] for i, j in ind]) * 1.0 / Y_pred.size, w
    
        # KMeans model
        km = KMeans(n_clusters=n_clusters, n_init=10, n_jobs=-1,
                    random_state=SEED)
    
        pred = km.fit_predict(Z)
    
        log('--------------- {} {} ------------------------'.
            format('Clustering accuracy', cluster_acc(pred, ground_truth)[0]))
    
    
    ##############################################################################
    # Visualization (2D data distribution scatter)
    ##############################################################################
    
    
    # Plot 2d projection of latent represtations z, given their labels (PCA)
    
    
    def plot_class_space_PCA2d(z, labels, out=None, distinct=False):
        import matplotlib
        matplotlib.use('agg')
        import matplotlib.pyplot as plt
        import matplotlib.cm as cm
        from sklearn.decomposition import PCA
        # Transform to 2D using PCA
        z = PCA(n_components=2).fit_transform(z)
        fig = plt.figure()
        # Color selection
        if distinct:
            color = plt.get_cmap("viridis")
            color = color(np.linspace(0, 1, 10))
        else:
            color = cm.rainbow(np.linspace(0, 1, 10))
        # Scattering using different color for each label
        for l, c in zip(range(10), color):
            ix = np.where(labels == l)[0]
            plt.scatter(z[ix, 0], z[ix, 1], c=c, label=l, s=8, linewidth=0)
        plt.legend()
        # Save or show
        if out:
            fig.savefig(out + ".png")
        else:
            plt.show()
    
    
    # Plot 2d projection of latent represtations z, given their labels (t-SNE)
    
    
    def plot_class_space_tSNE(z, labels, out=None, distinct=False):
        import matplotlib
        matplotlib.use('agg')
        import matplotlib.pyplot as plt
        import matplotlib.cm as cm
        from MulticoreTSNE import MulticoreTSNE as TSNE
        z = TSNE(n_jobs=-1, n_components=2, verbose=1).fit_transform(z)
        fig = plt.figure()
        # Color selection
        if distinct:
            color = plt.get_cmap("viridis")
            color = color(np.linspace(0, 1, 10))
        else:
            color = cm.rainbow(np.linspace(0, 1, 10))
        # Scattering using different color for each label
        for l, c in zip(range(10), color):
            ix = np.where(labels == l)[0]
            plt.scatter(z[ix, 0], z[ix, 1], c=c, label=l, s=8, linewidth=0)
        plt.legend()
        # Save or show
        if out:
            fig.savefig(out + ".png")
        else:
            plt.show()
    
    def vis_2d_distributions(e2e_in, enc, data, ground_truth, flag='PCA'):
        # Define pseudo model to get intermidiate layer output
        E2E_HIDDEN_OUT = tf.keras.models.Model(inputs=e2e_in.input,
                                               outputs=enc.output)
        # Get hidden layer value
        Z = E2E_HIDDEN_OUT.predict(data)
        
        # Call plotting function
        if flag == 'PCA':
            plot_class_space_PCA2d(data, ground_truth, out='data_distribution')
            plot_class_space_PCA2d(Z, ground_truth, out='latent_representations_distribution')
        else:
            plot_class_space_tSNE(data, ground_truth, out='data_distribution')
            plot_class_space_tSNE(Z, ground_truth, out='latent_representations_distribution')
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
