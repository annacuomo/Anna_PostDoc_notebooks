# Plotting

## show matrix

```Python
import matplotlib.pyplot as plt
plt.matshow(M)
```

## histogram

```Python
import matplotlib.pyplot as plt
plt.hist(y)
plt.show()
```

## scatter

```Python
import matplotlib.pyplot as plt
plt.scatter(x,y)
```

## barplot

https://www.geeksforgeeks.org/bar-plot-in-matplotlib/

## QQplot

```Python
import numpy as np
import matplotlib.pyplot as plt
expected_pvalues = np.random.uniform(low=0, high=1, size=len(observed_pvalues))
x = -np.log10(np.sort(expected_pvalues))
y = -np.log10(np.sort(observed_pvalues))
plt.scatter(x,y)
```

## Venn

```Python
# pip install matplotlib-venn
from matplotlib_venn import venn2, venn2_circles, venn2_unweighted
from matplotlib_venn import venn3, venn3_circles
from matplotlib import pyplot as plt
%matplotlib inline
venn2(subsets = (30, 10, 5), set_labels = ('Group A', 'Group B'))
```

Slightly more complex example for neuroseq paper (Studies overlap figure; [Fig. 3A](https://github.com/single-cell-genetics/singlecell_neuroseq_paper/blob/main/plotting_notebooks/Figure_3/Figure_3a.ipynb))

## rotate axes

```Python
plt.xticks(rotation=45, ha='right')
```

## save plot

```Python
plt.savefig("fig.pdf")
```
