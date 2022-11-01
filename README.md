# Data-Transformation-with-Analytics
Script Rationalisation using Python

import warnings
warnings.filterwarnings('ignore')

import pandas as pd
import numpy as np
from fuzzywuzzy import process, fuzz
df = pd.read_csv(r'C:\Users\HimanshiDua\Documents\DWM\abc2.csv')
df

df.loc[:,'Script Question_copy'] = df['Script Question']

compare = pd.MultiIndex.from_product([df['Script Question'],
                                      df['Script Question_copy']]).to_series()

def metrics(tup):
    return pd.Series([fuzz.ratio(*tup),
                      fuzz.token_sort_ratio(*tup)],
                     ['ratio', 'token'])

ratio=compare.apply(metrics)
ratio.reset_index(inplace=True)
ratio

ratio=ratio.rename(columns={'level_0': 'Input Question','level_1':'Output Result'})
ratio

ratio=ratio.sort_values(['Input Question','ratio'],ascending=[False,False])
ratio
df.loc[:,'Script Question_copy'] = df['Script Question']

compare = pd.MultiIndex.from_product([df['Script Question'],
                                      df['Script Question_copy']]).to_series()

def metrics(tup):
    return pd.Series([fuzz.ratio(*tup),
                      fuzz.token_set_ratio(*tup)],
                     ['ratio', 'token'])

ratio=compare.apply(metrics)
ratio.reset_index(inplace=True)
ratio

df.loc[:,'Script Question_copy'] = df['Script Question']

compare = pd.MultiIndex.from_product([df['Script Question'],
                                      df['Script Question_copy']]).to_series()

def metrics(tup):
    return pd.Series([fuzz.ratio(*tup),
                      fuzz.partial_ratio(*tup)],
                     ['ratio', 'token'])

ratio=compare.apply(metrics)
ratio.reset_index(inplace=True)
ratio
