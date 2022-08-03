# Diagonsenfix
## How to diagnose and fix problem in a production deployed code <br />
## The important points <br />
To see how the model works and find problems and fixing them there.Three things matter the most <br />
1.We need to plan for periodic training.We have to take care for optimal retraining strategy. <br />
2.Monitor for actual performance.We should keep an eye on how the production model is performing <br />
3.Analyse.Detailed visibility of the model helps us and guide for the model performance. <br />
## Summary <br />
In this section we will explore ways to diagnose problems in production deployed code and fix them. <br />
1.We will use evidently and mlflow library together. <br />
2.We will deploy ml models in heroku. <br />
First we will calculate data drift for the model. <br />
To diagnose and fix problems the ml training experiments that do data drift are tracked by mlflow tracking <br />
To fix the problems we we will explore the results using mflow ui. <br />
## Exercise: Data Drift/Mlflow <br />
in this exercise we will be using the bike sharing dataset.We will load the data first <br />
```
content = requests.get("https://archive.ics.uci.edu/ml/machine-learning-databases/00275/Bike-Sharing-Dataset.zip").content
with zipfile.ZipFile(io.BytesIO(content)) as arc:
    raw_data = pd.read_csv(arc.open("day.csv"), header=0, sep=',', parse_dates=['dteday'], index_col='dteday')
#observe data structure
raw_data.head()
```
The same is shown in the train.py file where we can see the data loading option <br />
## Environment setup <br />
Make sure we have a heroku account.Also we need active github account too. <br />
The github repo has the following files. <br />
1)requirements.txt <br />
2)train.py        <br />
3)Procfile(for heroku) <br />
4)runtime.txt <br />








