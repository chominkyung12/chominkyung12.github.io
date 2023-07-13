---
layout: post
title:  "Introduce how to use Stream lit and deploy apps!"
---

# what is Streamlit?

Streamlit is a python library which is used for data visualization with ease.

Streamlit has various functions to show a data information like histogram or data_table, slide_box etc.


# Streamlit fucntion examples
first, import streamlit as st
st.write(): is like with print() in python 
ex) when I use st.write('Hello world') --> it can show the line: Hello world in homepage screen.
ex) when decribing data frame. 
st.title(): homepage title. input tiltle you want in the blank.
ex) st.title('Uber pickups in NYC')
st.text(): short sentence for your homepage's action. for example, short sentence for data loading.
st.subheader(): make subheader.

# data load

DATA_URL = ('https://s3-us-west-2.amazonaws.com/' 'streamlit-demo-data/uber-raw-data-sep14.csv.gz')
- it can be anything

def load_data(nrows):
    data = pd.read_csv(DATA_URL, nrows=nrows)
    lowercase = lambda x: str(x).lower()
    data.rename(lowercase, axis='columns', inplace=True)
    data[DATE_COLUMN] = pd.to_datetime(data[DATE_COLUMN]) # pd.to_datetime: 09/01/2023 --> 2023-09-01: fixed for datatime format 
    return data

- Create a text element and let the reader know the data is loading.
data_load_state = st.text('Loading data...')
- Load 10,000 rows of data into the dataframe.
data = load_data(10000)
-  Notify the reader that the data was successfully loaded.
data_load_state.text("Done! (using st.cache_data)")

# Make checkbox 

if st.checkbox('Show raw data'):
    st.subheader('Raw data')
    st.write(data)

if checkbox is true --> it show the data frame.

# histogram

hist_values = np.histogram(
    data[DATE_COLUMN].dt.hour, bins=24, range=(0,24))[0]

st.bar_chart(hist_values)



