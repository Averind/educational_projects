**Проект "Предсказание оттока клиентов банка"**

**Project 'Bank customers outflow'**

На основе данных о поведении клиентов банка (в т.ч. о расторжении договоров с банком) были обучены модели машинного обучения. Цель: построение модели для задачи классификации, которая **предскажет, уйдёт клиент из банка в ближайшее время или нет**. 

В ходе выполнения проекта были обучены модели DecisionTree, RandomForest и LogisticRegression.

Наилучшие результаты модели показали на увеличенной выборке:

|model|f1|roc-auc|
|----|----|----|
|DecisionTree|0.58|0.83|
|RandomForest|0.65|0.87|
|LogisticRegression|0.45|0.72|

Лучшей моделью была признана RandomForest, как имеющая наибольшие показатели F1-меры и ROC-AUC. Модель была проверена на тестовой выборке, значение F1-меры оказалось равным 0.59. 
