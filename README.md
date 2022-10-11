# M3 Project - Ironhack
By Pedro Consuegra Mateo

## Workflow

### Loading data

Después de cargar todas las tablas de datos de diamantes, las he unido en una de tal forma que tenga en un mismo DataFrame las diferentes propiedades de los diamantes.

### EDA Conclussions


Después de hacer un EDA se concluyó lo siguiente: 

 - City no influye apenas en el precio.
 - X Y y Z no influyen en el precio
 - Carat, Cut, Color y Clarity son las variables que más influyen en el precio.
 - Depth y Table influyen medianamente pero no tanto como las anteriores.

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

He utilizado un scaling manual logarítmico después de probar robust scaler, minmaxscaler y standard scaler. Esto mejoró las predicciones en el notebook local.

## Best Model - CatBoost

Los modelos usados han sido:

- LinearRegression de Sklearn
- RandomForest de Sklearn
- SVR de Sklearn
- Ridge de Sklearn
- XGboost
- CatBoost

El modelo que mejores predicciones ha hecho ha sido CatBoost con unos hiperparámetros concretos, seguido muy de cerca por XGBoost.

Para obtenerlos he usado GridSearch haciendo varias pruebas para cada hiperparámetro con el fin de que no lleve mucho tiempo.

Este modelo tiene como resultado 476 RMSE con todos los diamantes y 528 en Kaggle public.

El segundo modelo elegido tiene como resultado un RMSE de 514 y 528 en Kaggle.

Por tanto, tiene sentido elegir el que tiene error 476.


## Analysis

El proceso que he seguido ha sido primeramente obtener un workflow con los métodos más sencillos para conseguir unas predicciones. Una vez he conseguido hacer un feature selection - encoding - scaling - training - predicts he comenzado a variar cada apartado para ir mejorando progresivamente las predicciones.

Como feature nueva he combinado columnas numéricas que tienen que ver con las medidas y proporciones del diamante con el fin de encontrar relaciones entre ellas. Una buena combinación y que he incorporado ha sido dividir el carat entre el depth por el table. Las medidas de x y y z no funcionan por separado ni combinadas.

A la hora de elegir el modelo he probado con los modelos anteriormente mencionados con los hiperparámetros por defecto. Una vez que he visto que Randomforest y XGBoost son los mejores, he calculado valores óptimos con RandomizedSearchCV y GridSearchCV. El mejor ha sido XGBoost.

Usar label encoding en lugar de One Hot Encoding mejoró considerablemente las predicciones puesto que las variables categóricas definen qué diamante es mejor que otro.

Por último, el scaling con logaritmos parece dar mejor resultado en local aunque en kaggle no parece tener efecto. Este fue el último cambio que hice.
