# Kaggle-Tutorial
https://www.kaggle.com/learn

## My lessons learned 
- 📌 How to handle missing values 
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
    
    여기서 Simplmputer strategy의 디폴트 값은 평균값 (mean) 이고, 예를 들어 중앙값(median)으로 변경하고 싶다면 SimpleImputer(strategy = median) 으로 파라미터 변경
    이렇게 splitting 후에 적용할 경우, 테스트 데이터에서도 테스트 전에 동일한 전처리를 해줘야한다. 
    
    ```ruby
    
    final_X_test = pd.DataFrame(final_imputer.transform(X_test))
    preds_test = model.predict(final_X_test)
    
    ```
    
- 📌 How to handle Categorical values
     - OrdinalEncoder 
     - One-Hot Encoding 
     
     어느정도 랭킹이 가능한 경우에는 Ordinal feature 로 바꿔주는 것도 좋고 그게 아니라면 One-Hot Encoding 인데, 이걸 쓰게 되면 컬럼 수가 너무 많아지는 경우가 생길 수 있다. 너무 많은 컬럼이 생겨도 모델 학습이 잘 안될 수 있다는 점 참고! 
     
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
