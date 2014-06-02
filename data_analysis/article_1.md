# Loading Data and Cleaning It

From a fresh iPython Notebook, we'll load some required libraries and set some global options. As a reminder, all of the libraries we're using come included out-of-the-box with the freely available [Enthought Canopy Express](https://www.enthought.com/canopy-express/) Python environment.

### Loading Dependencies

In a new iPython Notebook:

```python
import pandas as pd          # our core data analysis toolkit
import pylab as pl           # our plotting library
from pandas import read_json # a function for reading data in JSON files

# This option shows our plots directly in iPython Notebooks
%matplotlib inline

# This option gives a more pleasing visual style to our plots
pd.set_option('display.mpl_style', 'default')

# The location of our playtest data file
filepath = "2014-05-13 makescape playtest.json"
```

### Loading and Sorting the Data

```python
def loadDataSortedByTimestamp(filepath):
    x = read_json(filepath)
    x = x.sort(columns='timestamp')
    x.index = range(0, len(x))
    return(x)

ms = loadDataSortedByTimestamp(filepath)
```

Now that our data is loaded with the variable `ms` (I chose it as an abbreviation of MakeScape), let's look at it and make sure it loaded properly and it makes sense.
