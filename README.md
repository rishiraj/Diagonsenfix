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
## Steps <br />
The required steps for proper deployment of the repo are as follows <br />
1)make sure all requirements for mlflow and evidently library are met. <br />
2)Load the data in train.py script file <br />
3)Define column mapping  <br />
4)The logic to log the metrics <br />
5)Define the comparison window <br />
```
experiment_batches = [
    ('2011-02-01 00:00:00','2011-02-28 23:00:00'),
    ('2011-03-01 00:00:00','2011-03-31 23:00:00'),
    ('2011-04-01 00:00:00','2011-04-30 23:00:00'),
    ('2011-05-01 00:00:00','2011-05-31 23:00:00'),  
    ('2011-06-01 00:00:00','2011-06-30 23:00:00'), 
    ('2011-07-01 00:00:00','2011-07-31 23:00:00'), 
]

```
Also mention the reference dates for experiments <br />
```
reference_dates = ('2011-01-01 00:00:00','2011-01-28 23:00:00')
```
6)Run and log experiments in Mlflow <br />
7)view the results in mlflow webui <br />
## Exercise questions <br />
Q1) To initiate the training in heroku what commands need to be provided in Procfile to initiate the python script in this exercise <br .>
a)python main.py <br />
b)python train.py <br />
c)python ab.py <br />
d)None of these <br />

Answer b) <br />
Q2)To initiate mlflow within heroku which command is passed with the training parameter <br />
a)python main.py --host 0.0.0.0 --port ${PORT} <br />
b)python main.py & mlflow --host 0.0.0.0 <br />
c)web: python train.py & mlflow ui --host 0.0.0.0 --port ${PORT} <br />
d)None of these <br />
Answer c) <br /> update the answer in the procfile where it is mentioned ##inserthere## and save the file.
Q3)What additonal should be added inside requirements.txt file such that it is able to retrieve the mlflow ui <br />
a)mlflow ui <br />
b)ui <br />
c)mlflow <br />
d)None of these <br />
Answer c) update the same in the repo(github) inside requirements.txt file and save it. <br />
Q4)lets focus on train.py file,we are missing essential import for mlflow.What are these <br />
a)import mlflow <br />
b)import ui <br />
c)None of these <br />
Answer a) Add the same in the ##insert here## option in the import section and save the file <br />
Q5)in the train.py script file what is the way to get inside mlflow <br />
a) c = mlclient() <br />
b) client = MlflowClient() <br />
c)None of these <br />
Answer b) add the code within train.py file in the ##insertHere## where it is mentioned login inside mlflow client and save it. <br />
Q6)in the train.py script file what will be the code to start mlflow experiment <br />
a)mlflow.experiment <br />
b)mlflow.start <br />
c)mlflow.set_experiment('Experiment Name') <br />
d)None of these  <br />
Answer c) Update the code in the train.py script under set experiment section where it is mentioned ##inserthere## and save the file. <br />
##Solution <br />
The solution file is hosted in github [a link] (https://github.com/AbhiLegend/mlflowsolution) <br />
Login to heroku using the free account.Similarly as shown before create a new app.Deployment method would be github.Make sure the repo [a link] (https://github.com/AbhiLegend/mlflowsolution) is forked <br />
Search and add the forked repo.Uploading and hosting the files would take time.You will see the update link.Goto the link and you will see the mlflow ui. <br />
















