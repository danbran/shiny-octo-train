Title: code example 
Date: 2017-12-27 12:00 
Tags: thats, awesome 
Category: python 
Slug: code-example
Author: dan
Summary: code example with python and pandas


# code example


```python
import math
```

a textbox to explain the code


```python
def a_function(a,b):
    return math.sqrt(a) + b**2
```

show function output


```python
a_function(10,20)
```




    403.1622776601684



# pandas example


```python
import pandas as pd
```


```python
df = pd.DataFrame({'a':[35,63,21,58,84]})
df['b'] = df.a.cumsum()
df['b^2'] = df['b']**2
df['c'] = df['b^2'].map(lambda x: a_function(x,0))
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>b^2</th>
      <th>c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>35</td>
      <td>35</td>
      <td>1225</td>
      <td>35.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>63</td>
      <td>98</td>
      <td>9604</td>
      <td>98.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>21</td>
      <td>119</td>
      <td>14161</td>
      <td>119.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>58</td>
      <td>177</td>
      <td>31329</td>
      <td>177.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>84</td>
      <td>261</td>
      <td>68121</td>
      <td>261.0</td>
    </tr>
  </tbody>
</table>
</div>



## calculate the friction coefficient using pandas


```python
%matplotlib inline
import pandas as pd
import numpy as np
```


```python
def friction(Re):
    # laminar: Hagen-Poiseuille equation
    if Re < 2300:
        return 64/Re
    # turbulent: Blasius equation
    elif Re > 4000:
        return 0.3164*Re**(-0.25)
    else:
        return np.nan
```


```python
Re = np.linspace(1e03,1e04,21)
Re
```




    array([  1000.,   1450.,   1900.,   2350.,   2800.,   3250.,   3700.,
             4150.,   4600.,   5050.,   5500.,   5950.,   6400.,   6850.,
             7300.,   7750.,   8200.,   8650.,   9100.,   9550.,  10000.])




```python
df = pd.DataFrame(Re, columns=['Re'])
df['$\lambda$'] = df.Re.map(lambda x: friction(x))
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Re</th>
      <th>$\lambda$</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000.0</td>
      <td>0.064000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1450.0</td>
      <td>0.044138</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1900.0</td>
      <td>0.033684</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2350.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2800.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.set_index('Re').dropna().plot(marker='o',loglog=True)
```








```python
![png]({{ "/data/output_15_1.png" | https://github.com/danbran/danbran.github.io/blob/master/data/output_15_1.png }})
```
