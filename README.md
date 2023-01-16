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
