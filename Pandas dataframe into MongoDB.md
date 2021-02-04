# 將資料讀取至 DataFrame 後，做完前處理將 DataFrame 中的資料儲存至 MongoDB
ref: https://oranwind.org/python-pandas-ji-chu-jiao-xue-2/ 
-----------------------------------------------------------------------------------
-----------------------------------------------------------------------------------
# 需要先安裝 MongoDB
# 透過 pip install 安裝 pandas 及 pymongo lib
pip install pandas  
pip install pymongo  

import pandas as pd                # 引用套件並縮寫為 pd  
from pymongo import MongoClient

# 系統環境
Ubuntu 16.04
Python 2.7.8
-------------------------------------------------------------------------------
# step 1: data to dataframe #

def data_to_dataframe():

    groups = ["Movies", "Sports", "Coding", "Fishing", "Dancing", "cooking"]
    num = [46, 8, 12, 12, 6, 58]

    dict = {"groups": groups,
            "num": num
           }

    select_df = pd.DataFrame(dict)
    dataframe_to_mongo(select_df)

-----

# step 2: dataframe to mongo #

def dataframe_to_mongo(select_df):

    client = MongoClient()
    database = client["db_name"]            # SQL: Database Name
    collection = database["collection"]     # SQL: Table Name


    records = select_df.to_dict('records')  # 參數 record 代表把列轉成個別物件
    collection.insert_many(records)


def main():  
    data_to_dataframe()


if __name__ == "__main__":  
    main()
