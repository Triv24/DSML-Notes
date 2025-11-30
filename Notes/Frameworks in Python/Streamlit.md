# Streamlit - Frontend in Python :
- streamlit is a powerful frontend framework for building AI applications in python.
- It is a frontend library.

- installing streamlit from terminal :
```bash
!pip install -U streamlit
```
- the `-U` ensures that the **Upgraded** version of streamlit is installed.

```py
import streamlit as st
import pandas as pd
import numpy as np

## Title of the application :
st.title("This is Title")

## Display simple text :
st.write("Simple text")

## Displaying a dataframe :
df = pd.Dataframe(
    {
        'first column' : [1, 2, 3, 4, 5],
        'second column' : ['a', 'b', 'c', 'd', 'e']
    }
)

st.write("DataFrame :")
st.write(df)

## Displaying a line_chart :
chart_data = pd.Dataframe(
    np.random.randn(20,3),
    columns=['a','b','c']
)
st.line_chart(chart_data)

```

- In streamlit, the displayed dataframe can be :
    - expanded
    - downloaded (.csv format)

- In line_chart we can :
    - save as :
        - PNG
        - SVG
    - view source
    
### Widgets in streamlit :

```py
## text input
name = st.text_input("label of the input box")
if name :
    st.write(f"Hello! {name}")

## Sliders :
age = st.slider("Select your age :", 0, 100, 25)
# 0 is minimum value 
# 100 is maximum value
# 25 is default value, the slider is set to default value at first

## Selectbox :
options = ["India", "Australia", "America", "Japan", "Korea", "UAE"]

country = st.selectbox("Select your country : ", options)

## Upload files :

file = st.file_uploader("Please upload your file :", type=".pdf", accept_multiple_files = True)

```

## Practical implementation of an end-to-end app with the help of streamlit :

- We are going to solve a classification problem.

`!pip install scikit-learn`

**classification.py**
```py
from sklearn.datasets import load_iris
from sklearn.ensemble import RandomForestClassifier # Random Forest is one of the ML Algorithms

@st.cache_data
def load_data():
    iris = load_iris()
    df = pd.Dataframe(iris.data, columns = iris.feature_names)
    df['species'] = iris.target
    return df, iris.target_names

df, target_name = load_data()

model = RandomForestClassifier()

model.fit(df.iloc[:,:-1], df['species'])

...even more code

```
- this example just shows how an app in strealit works. 