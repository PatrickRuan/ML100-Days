# Part 1 Feature Engineering in ML100-Days
機器學習百日馬拉松：
第二部分 特徵工程 共 14天 (Day 17 ~ Day 30

Day 17: 什麼是特徵，什麼是特徵工程?
	
	我們藉由一些資料去推到目標的結果呈現，比如我們有房子的坪數、樓層、地點、區域等資料，這些資料類別可以影響我們關注的房價，那麼這些資料類別坪數、樓層、地點、區域等就是特徵，我們關注的房價就是目標。
	我們試圖整理挑選轉換組合特徵來影響我們的預測精確度，這過程就是特徵工程。未來的 14天就是要做這些處理。
	
	今天的作業練習有三個重點: 
	1.) 到https://www.kaggle.com/c/titanic 抓取房價預測的資料，當作未來14天的練習用。同時要留意資料要放在程式的上一層目錄下的 part02\ 下，如此一來，當我們用 pd.read_csv('..\part02\balabla.csv') 才能讀得到。
	2.) 判斷出哪一個欄位是目標，通常是看清楚題目來判斷，偷懶取巧的方式是，比對 training data 與 testing data 之間少了哪一個欄位作判斷。(why?)
	3.) 底下的 code 算是很典型作法，請思考，為什麼需要把 train data 與 test data 作 concat!
		train_Y = df_train['Survived']
		ids = df_test['PassengerId']
		df_train = df_train.drop(['PassengerId', 'Survived'] , axis=1)
		df_test = df_test.drop(['PassengerId'] , axis=1)
		df = pd.concat([df_train,df_test])
		df.head()
	衍生練習: 
		1. to read house_train.csv.gz and house_test.csv.gz from ../part02/ (done)
		2. to concat train and test data, you know how to handle them before you concat these 2 datasets (done)
		3. to check features, to check the amount of features in dataset (done)
		4. to check data type first, to filter out object features, then to label encode them in a very simple way.
		5. to minmax scale all features.
		6. to submit to Kaggle


Day 18: 特徵的類型

	特徵基本兩類數值型與類別型，其實我們從 Day 1 ~ Day 16 學過了 EDA，基本上是不陌生這兩個類別。這裡還會請大家嚐試了解還有一些小類別，比如說二元型別，秩序型別與時間型別，我們慢慢地都會練習到，
	
	今天的作業是 
	1.) 重複 Day 17作業 1.) 的工作，但是今天是把 kaggle 的經典題目  titanic 搬到 ..\part02\ 底下
	2.) 如同 Day 17 作業 3.) 整理 train data, test data 甚至 label(Y), 3.) 利用 df.dtypes 觀察 類別與每一個類別的數量(我最愛用的是 df.dtypes.value_counts()  也請思考最後要加上 .reset_index() 的原因。  4.) 對數值型資料作基本運算，比如 mean()，max() 等。 


Day 19: 數值型特徵 補缺失值與標準化:  
	在 EDA Day 6 時我們暴力的觀看所有欄位的 boxplot 可以看到一些 outlier，其實就是看最遠的那幾個圈是不是很遠，遠離正常的盒線，很孤獨的。如果是要找缺失值，也不難，只要用  isnull()測試就可以。 
	這裡我們業也很快的作同樣的運作。(參考 Cupoy ML100 day 19 資料)
		可以填補統計值
		• 填補平均值(Mean) : 數值型欄欄位，偏態不明顯 
		• 填補中位數(Median) : 數值型欄欄位，偏態很明顯 
		• 填補眾數(Mode) : 類別型欄欄位 填補指定值 - 
		如果對欄位領域知識已有了了解可能有其他的補法
		• 補 0 : 空缺原本就有 0 的含意，如一些房產的問題的房間數 
		• 補不可能出現的數值 : 類別型欄欄位，但不適合⽤用眾數時 
		填補預測值 - 速度較慢但精確，從其他資料欄欄位學得填補知識 
		• 若填補範圍廣，且是重要特徵欄欄位時可⽤用本⽅方式 
		• 本⽅方式須提防overﬁtting : 可能退化成為其他特徵的組合。
	然後我們要來練習 EDA Day 7 中介紹的 MinMaxScaler與 StandardScaler  
	
	作業 
	1.) 比較不同值的補值結果來作 LogisticRegression，藉由cross_val_score觀看那個結果比較好。
	2.) 比較不同標準化方法來作 LogisticRegression，藉由cross_val_score觀看那個結果比較好。
	
		
