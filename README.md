# XXDScorecard
scorecard developing utilities.

from XXDBinning import *
from sklearn.model_selection import train_test_split

df = pd.read_csv('data.csv')

train_df, test_df = train_test_split(df,test_size=0.3,random_state=100,stratify=df.flgGood)

#
nb = XXDNumberBin()

## 1. 数值型等频分箱

nb.pct_bin(train_df,'req_inc_ratio','flgGood',max_bin=10)

## 分箱结果
nb.get_bin_stats()

## WOE图

nb.plot_woe()

## 测试集转woe

nb.trans_to_woe(test_df['req_inc_ratio'])

## 2. 手动调整分箱

nb.manual_bin(train_df,'req_inc_ratio','flgGood',[20,30,40])

## 3. 自动单调分箱
nb.monotone_bin(train_df,'req_inc_ratio','flgGood',max_bin=3)



## 4. 字符型自动分箱

cb = XXDCharBin()
cb.pct_bin(train_df,'name','flgGood')
cb.plot_woe()
cb.get_bin_stats()

## 5. 字符型手动分箱

cb.manual_bin(train_df,'name','flgGood',[['yuqing','xuxiaodong'],['jack ma'],['yq','dd','xxd','qq']])

## 6. 测试集转woe

cb.trans_to_woe(test_df['name'])

