# M3 Project - Ironhack
By Pedro Consuegra Mateo

## Workflow

### Loading data

Después de cargar todas las tablas de datos de diamantes, las he unido en una de tal forma que tenga en un mismo DataFrame las diferentes propiedades de los diamantes.

### Feature Transform and Creation

#### Selected Features

Después de hacer un EDA y probar entrenar con diferentes features, concluyo con que las columnas que más afectan y que he elegido son **'depth', 'table', 'cut', 'color', 'clarity' y 'carat'**. 

El target es el precio 'price'.

#### New Features

Después de probar diferentes combinaciones con las medidas del diamante, he obtenido que **la división del carat entre el producto entre table y depth mejoraba notablemente las predicciones**. Esto puede ser a que la fórmula es parecida a una densidad del diamante.

He probado a combinar las medidas x y y z pero de ninguna forma parecía mejorar las predicciones. Por eso también he desechado las columnas.

### Encoding

Al principio he estado convirtiendo las variables categóricas cut, clarity y color a números con One Hot Encoding pero después he decidido usar un **label encoding** que me ha dado resultados mejores. Por tanto el encoding hecho finalmente ha sido con **label encoding**. 

### Scaling

**Robust** scaler ha sido el scaler que mejores resultados ha lanzado, aunque apenas variaba el RMSE usando MinMaxScaler o StandardScaler. 

## Best Model - XGBoost

Los modelos usados han sido:

- LinearRegression de Sklearn
- RandomForest de Sklearn
- SVR de Sklearn
- Ridge de Sklearn
- XGboost
- CatBoost

El modelo que mejores predicciones ha hecho ha sido XGBoost con unos hiperparámetros concretos, seguido muy de cerca por Randomforest.

Estos hiperparámetros son: max_depth=5, gamma=0, learning_rate=0.3,  n_estimators=200, min_child_weight= 3, colsample_bytree=0.9

Para obtenerlos he usado GridSearch haciendo varias pruebas para cada hiperparámetro con el fin de que no lleve mucho tiempo.


## Analysis

El proceso que he seguido ha sido primeramente obtener un workflow con los métodos más sencillos para conseguir unas predicciones. Una vez he conseguido hacer un feature selection - encoding - scaling - training - predicts he comenzado a variar cada apartado para ir mejorando progresivamente las predicciones.

Como feature nueva he combinado columnas numéricas que tienen que ver con las medidas y proporciones del diamante con el fin de encontrar relaciones entre ellas. Una buena combinación y que he incorporado ha sido dividir el carat entre el depth por el table. Las medidas de x y y z no funcionan por separado ni combinadas.

A la hora de elegir el modelo he probado con los modelos anteriormente mencionados con los hiperparámetros por defecto. Una vez que he visto que Randomforest y XGBoost son los mejores, he calculado valores óptimos con RandomizedSearchCV y GridSearchCV. El mejor ha sido XGBoost.

Usar label encoding en lugar de One Hot Encoding mejoró considerablemente las predicciones puesto que las variables categóricas definen qué diamante es mejor que otro.
