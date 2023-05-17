## Laptop-Price-Predictions
Dataset Details :
- Columns : `'Company', 'TypeName', 'Inches', 'ScreenResolution', 'Cpu', 'Ram', 'Memory', 'Gpu', 'OpSys', 'Weight', 'Price'`. 
- No Missing Values 


**Price Distribution :** Slightly Left skewed<br>
  <img width="300" alt="Screenshot 2023-05-17 at 12 25 11 PM" src="https://github.com/ayushs0911/Laptop-Price-Predictions/assets/122048067/ff11fc2e-c75c-463c-a106-1c36a2756440"><br>
Took log of the price distribution to make it more Gaussian. This can improve the assumptions of linear regression models that assume normally distributed errors.<br>
<img width="300" alt="Screenshot 2023-05-17 at 1 09 54 PM" src="https://github.com/ayushs0911/Laptop-Price-Predictions/assets/122048067/b6ee0b02-2138-49ac-b74a-9dc815626415">

## Data Preprocessing 
- `RAM` : Dropped "GB", and converted to `int`
- `Weight`: Dropped "Kg", and converted to `float32`
- `ScreenResolution` : Breakdown this in differents columns : `Touchscreen` `IPS` `X_res` `Y_res`
- `CPU` : Converted into 3 categories :  `i5, i7, other`
- Feature Engineering : Added `PPI` column i.e., Pixel Per Inches using `X_res` `Y_res` `Inches`
- `Memory` : Broke down this in 4 categories : `HDD`,`SSD`,`Hybrid`,`FlashStorage`
- `OpSys` : Clubbing Windows 10, windows 7, windows 7S --> `Windows` | club macOS, macOS x ---> `mac` | else return `others`.

## Relationship of price with various Variables
<img width="300" alt="Screenshot 2023-05-17 at 12 31 43 PM" src="https://github.com/ayushs0911/Laptop-Price-Predictions/assets/122048067/6abe5119-a896-423c-82c6-4232abac8a2f">
<img width="300" alt="Screenshot 2023-05-17 at 12 33 06 PM" src="https://github.com/ayushs0911/Laptop-Price-Predictions/assets/122048067/45ba8b02-ab6b-4282-bbe8-f5dafb089124">
<img width="300" alt="Screenshot 2023-05-17 at 12 34 09 PM" src="https://github.com/ayushs0911/Laptop-Price-Predictions/assets/122048067/3c700913-0e7b-4a0b-b0f4-ea09c25b9469">
<!-- <img width="300" alt="Screenshot 2023-05-17 at 12 34 25 PM" src="https://github.com/ayushs0911/Laptop-Price-Predictions/assets/122048067/9da756f0c2eb-423b-9841-e00c4c166c46"><br> -->
<img width="300" alt="Screenshot 2023-05-17 at 12 34 52 PM" src="https://github.com/ayushs0911/Laptop-Price-Predictions/assets/122048067/ec5a24ac-ea1f-4277-b229-06e35744dda7">
<img width="300" alt="Screenshot 2023-05-17 at 12 35 09 PM" src="https://github.com/ayushs0911/Laptop-Price-Predictions/assets/122048067/759e86e6-429b-410a-b3a1-cfa2719bf90b">
<img width="300" alt="Screenshot 2023-05-17 at 12 35 33 PM" src="https://github.com/ayushs0911/Laptop-Price-Predictions/assets/122048067/dd3883b9-e6ec-4f7d-9831-4b73c6f12853">
<img width="300" alt="Screenshot 2023-05-17 at 12 35 49 PM" src="https://github.com/ayushs0911/Laptop-Price-Predictions/assets/122048067/49527580-6d51-4b3f-abe1-6573b183d710">
<img width="300" alt="Screenshot 2023-05-17 at 12 45 00 PM" src="https://github.com/ayushs0911/Laptop-Price-Predictions/assets/122048067/c817896a-a49c-41c8-a3af-002d9928ef56">

## Models 
- `Linear Regression` : R2 score 0.8073277448418601 MAE 0.21017827976428896
- `Ridge Regression` : R2 score 0.8127331031311809 MAE 0.20926802242582968
- `Lasso Regression` : R2 score 0.8071857196899417 MAE 0.2111435071691317
- `Decision Tree` : R2 score 0.8279260753130654 MAE 0.1869543941221999
- `Random Forest` : R2 score 0.8851499847098487 MAE 0.15870252595141304 <br>
### Hyperparameter Tuning for Random Forest 
```
rf1 = RandomForestRegressor(n_estimators=100,
                              random_state=3,
                              max_samples=0.5,
                              max_features=0.75,
                              max_depth=15)

rf1.fit(X_train,y_train)
print(f'R2 score : {metrics.r2_score(y_test,rf1.predict(X_test))}')
```
## Comparing Predicted Values and True Values. 

<img width="606" alt="Screenshot 2023-05-17 at 1 03 25 PM" src="https://github.com/ayushs0911/Laptop-Price-Predictions/assets/122048067/91ae4650-5ded-404c-a91d-df44abb83124">
