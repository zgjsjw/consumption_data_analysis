# pandas-
纪录学习pandas的一些小东西，还涉及seaborn\matplot画图

import pandas as pd
import numpy as np
import os
import matplotlib.pyplot as plt
import seaborn as sns

data_in = './data/online_retail.xlsx'
data_out = './output/result.csv'

def show_datainfo(data_file):
    print('***************')
    print(data_file.head())

def clean_data(datafile):
    adatafile = datafile.dropna()
    print(datafile.shape)
    print(adatafile.shape)
    bdatadile = adatafile.drop_duplicates()
    print(bdatadile.shape)
    bdatadile.to_csv(data_out,index=False,encoding='utf-8')
    return bdatadile

def show_pic(datafile):
    customer_per_country = datafile['Country'].value_counts()
    customer_per_country_df = \
        customer_per_country[customer_per_country.index != 'United Kingdom'].to_frame().T
    #print(customer_per_country)
    #print(customer_per_country_df)
    #customer_per_country
    sns.barplot(customer_per_country_df)
    plt.xticks(rotation=90)
    plt.xlabel('Country')
    plt.ylabel('#Customers')
    plt.tight_layout()
    plt.show()

def main():
    read_data = pd.read_excel(data_in)
    #show_datainfo(read_data)
    tem_data = clean_data(read_data)
    show_pic(tem_data)
    print(os.getcwd())
    #print('{}'.format('1'))

if __name__ == '__main__':
    main()
