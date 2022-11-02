**Проект "Рекомендация тарифов оператора сотовой связи"**

**Project 'Mobile tariff recommendation'**

На основе данных о поведении клиентов мобильного оператора было проведено машинное обучение. Цель: построение модели для задачи классификации, которая **выберет подходящий клиенту тариф**. В ходе выполнения проекта были построены модели DecisionTree, RandomForest и LogisticRegression, которые показали следующие результаты:

|model|accuracy|
|----|----|
|DecisionTree|0.80|
|RandomForest|0.82|
|LogisticRegression|0.73|

Лучшей моделью была признана модель случайного леса как имеющая наибольшую долю правильных ответов. Модель была проверена на тестовой выборке, показатель доли правильных ответов на которой оказался немного ниже 82 %. 

Модель была проверена на адекватность: в ходе проверки был вычислен accuracy для таргета, целиком состоящего из нулей - доминирующего класса. Accuracy оказался значительно ниже того, который мы получили на тестовой выборке: 69 против 82. Это говорит о том, что модель случайного леса, проверенная на тестовой выборке, адекватна.