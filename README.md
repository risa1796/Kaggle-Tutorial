# Kaggle-Tutorial
https://www.kaggle.com/learn

## My lessons learned 
- ๐ How to handle missing values 
    - You can delete the columns with missing values (not so recommended due to information decrease)
    - Fill nan values with ex) mean value -> You can use SimpleImputer

    ```ruby
    
    from sklearn.impute import SimpleImputer

    # Fill in the lines below: imputation
    myinputer = SimpleImputer() # Your code here
    imputed_X_train = pd.DataFrame(myinputer.fit_transform(X_train))
    imputed_X_valid = pd.DataFrame(myinputer.transform(X_valid))

    # Fill in the lines below: imputation removed column names; put them back
    imputed_X_train.columns = X_train.columns
    imputed_X_valid.columns = X_valid.columns
    
    ```
    
    ์ฌ๊ธฐ์ Simplmputer strategy์ ๋ํดํธ ๊ฐ์ ํ๊ท ๊ฐ (mean) ์ด๊ณ , ์๋ฅผ ๋ค์ด ์ค์๊ฐ(median)์ผ๋ก ๋ณ๊ฒฝํ๊ณ  ์ถ๋ค๋ฉด SimpleImputer(strategy = median) ์ผ๋ก ํ๋ผ๋ฏธํฐ ๋ณ๊ฒฝ
    ์ด๋ ๊ฒ splitting ํ์ ์ ์ฉํ  ๊ฒฝ์ฐ, ํ์คํธ ๋ฐ์ดํฐ์์๋ ํ์คํธ ์ ์ ๋์ผํ ์ ์ฒ๋ฆฌ๋ฅผ ํด์ค์ผํ๋ค. 
    
    ```ruby
    
    final_X_test = pd.DataFrame(final_imputer.transform(X_test))
    preds_test = model.predict(final_X_test)
    
    ```
    
- ๐ How to handle Categorical values
     - OrdinalEncoder 
     - One-Hot Encoding 
     
     ์ด๋์ ๋ ๋ญํน์ด ๊ฐ๋ฅํ ๊ฒฝ์ฐ์๋ Ordinal feature ๋ก ๋ฐ๊ฟ์ฃผ๋ ๊ฒ๋ ์ข๊ณ  ๊ทธ๊ฒ ์๋๋ผ๋ฉด One-Hot Encoding ์ธ๋ฐ, ์ด๊ฑธ ์ฐ๊ฒ ๋๋ฉด ์ปฌ๋ผ ์๊ฐ ๋๋ฌด ๋ง์์ง๋ ๊ฒฝ์ฐ๊ฐ ์๊ธธ ์ ์๋ค. ๋๋ฌด ๋ง์ ์ปฌ๋ผ์ด ์๊ฒจ๋ ๋ชจ๋ธ ํ์ต์ด ์ ์๋  ์ ์๋ค๋ ์  ์ฐธ๊ณ ! 
     
     ```ruby
     
     from sklearn.preprocessing import OrdinalEncoder

    # Make copy to avoid changing original data 
    label_X_train = X_train.copy()
    label_X_valid = X_valid.copy()

    # Apply ordinal encoder to each column with categorical data
    ordinal_encoder = OrdinalEncoder()
    label_X_train[object_cols] = ordinal_encoder.fit_transform(X_train[object_cols])
    label_X_valid[object_cols] = ordinal_encoder.transform(X_valid[object_cols])

    print("MAE from Approach 2 (Ordinal Encoding):") 
    print(score_dataset(label_X_train, label_X_valid, y_train, y_valid))

    ```
