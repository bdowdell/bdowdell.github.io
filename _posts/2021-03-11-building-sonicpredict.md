---
layout: post
title: "Building the SonicPredict API"
---

[SonicPredict](https://sonicpredict.com) is a Flask API that serves a fitted ML-model from which users can predict sonic well logs. The project began in March 2020 when I participated in the Society of Petrophysicists & Well Log Analysts (SPWLA) Petrophysical Data-Driven Analysis (PDDA) Special Interest Group's first machine learning contest. The objective of the contest was to build a machine learning model that given a set of input well logs could predict P- and S-Sonic well logs. The contest scoring was based upon minizming root mean squared error (RMSE) between predicted and real P- and S-Sonic well logs from a blind well not previously seen by the model. I will write more about my experience participating in the contest and the model I created in a separate post, but for now I want to write about the actual SonicPredict API.

### what, why, how, & where?

I previously learned Flask to translate PySeisTuned<sup>2.0</sup> from a PyQT5 GUI application into a web app. Flask is a really awesome Python framework (technically *micro*-framework) for building web applications. I chose to build using Flask because I like its extensible nature, meaning that as a developer you choose what features, or plug-ins, to use. Additionally, because Flask is a micro-framework, it doesn't come with all the bells and whistles installed as a default like Django does, so you only install what you need. For instance, if a project doesn't require a database (such as SonicPredict or PySeisTuned<sup>2.0</sup>), then you don't need to install any database-related Flask plug-ins.

So now that the **what** is established, I need to tell you **why** I built the SonicPredict API. Sure, I don't expect for my sonic log prediction model to be used in any meanginful way (and really it shouldn't be<sup>1</sup>), but I don't think any data science or machine learning project is complete until it is deployed in a manner in which end-users (the consumer) can use it. A very common way of serving pre-trained machine learning models is by creating a hosted API. An *application programming interface*, or API, basically is a software intermediary that enables one piece of software to request something from another piece of software. API's are typically accessed using specific urls designed to receive a request, do something with that request, and then return something back to who made the request. I created SonicPredict's API so that I could practice building a deployed machine learning model which is served using an API.

**How** does it work? SonicPredict's API receives well log data in the form of a json string, converts the string to a pandas dataframe, passes the data into the pre-trained model and the predictions are sent back as a json string. In other words, SonicPredict's API allows users to predict sonic curves using my pre-trained model without having to download and load it themselves everytime they want to make predictions. Instead, a user simply needs to send an HTTP request to *https://sonicpredict.com/api/get_predictions* (the **where**) from their IDE or Jupyter notebook, and then the SonicPredict API serves the user predicted sonic logs output from the pre-trained model. Putting this in terms of HTTP, a user makes a `POST` request to the API when sending the jsonified data. The API responds to the `POST` request by sending back a `200` response and the predicted logs meaning that the request was successful, or a `500` response meaning that something went wrong.

### learnings

#### when and where to load the model using Flask application factory & blueprints

Building from my previous PySeisTuned<sup>2.0</sup> Flask web app experience, I created a bare-bones [Flask web app template repository](https://github.com/bdowdell/flask_template) on my GitHub which I can use as a starting point for new projects. This template: 
+ creates a basic Flask application factory using Flask Blueprints
+ defines basic routes, or views
+ includes a contact page Flask Form
+ includes template HTML pages for each view
+ has basic unit tests

Most of the simple examples for building a Flask API do not use Flask Blueprints and instead demonstrate a very basic single-file Flask app that contains all the code. However, the bare-bones template I created structures the app using Flask Blueprints and the Application Factory concept (more on that in a bit). For the single-file Flask app case, when and where to load the model is pretty obvious :point_down:

```python
from flask import Flask, request
import joblib
import pandas as pd

app = Flask(__name__)

@app.route('/api', methods=['POST'])
def predict():
	data = request.get_json()
	df = pd.read_json(data, orient='split')
	y_pred = model.predict(df)
	df_out = pd.DataFrame(data=y_pred, columns=['pred_DTC', 'pred_DTS'])
	return df_out.to_json(orient='split')


if __name__ == '__main__':
	model = joblib.load('model.joblib')
	app.run()
```

And that's it! It's very quick to create a basic Flask API. The model gets loaded at runtime just prior to running the Flask app.

While this application structure would certainly work for SonicPredict, my template uses blueprints and the application factory. Using blueprints allows me to factor the application in a more modular approach separating out web page views as 'main' and the actual API as 'api'. Additionally, I can register all routes associated with the 'api' Blueprint to have a url prefix of `/api`. While blueprints allow for more flexibility, especially with larger applications, they do result in a more complicated project structure (omitting objects not really necessary here) :point_down:

```bash
/home/user/flask_project
|--app/
|  |--api/
|  |   |models/
|  |   |  |--model.joblib
|  |   |--__init__.py
|  |   |--api_routes.py
|  |--main/
|  |   |--__init__.py
|  |   |--views.py
|  |--static/
|  |   |--css/
|  |   |--img/
|  |   |--js/
|  |--templates/
|  |   |--base.html
|  |   |--index.html
|  |   |--404.html
|  |--__init__.py
|--tests/
|--config.py
|--project.ppy
```

This structure creates an `app` module which contains both `main` and `api` submodules. The `app` module is imported into `project.py` which creates an instance of the application factory defined in `app/__init__.py`. The application factory is a function which creates the app, sets the configuration and registers any blueprints with the app.

However, this presents a slight question as to when and where to load a model pickle. I quickly discovered that if I attempted to load the model in `app/api/__init__.py` or `app/api/api_routes.py`, when I tried to make predictions against the model I would get a `500` response and an error that the model file did not exist. But I know the file exists because I can clearly see it is at `app/api/models/model.joblib`, so what's the issue?

Well, it turns out that by nature of how blueprints and the application factory works, by the time `model.joblib` is loaded, it's too late if done in either `app/api/__init__.py` or `app/api/api_routes.py`. Recall in the very simple Flask app above, the model is loaded at runtime just before the app is created, meaning it is in global scope. When using blueprints and the application factory, this state occurs in the `app` module `__init__.py` prior to defining the application factory :point_down:

```python
#/flask_project/app/__init__.py
from flask import Flask
from config import config
import joblib

# load the model here!
model = joblib.load('app/api/models/model.joblib')

# create the application factory
def create_app(config_name):
	app = Flask(__name__)
	app.config.from_object(config[config_name])

	# register the main blueprint
	from .main import main as main_blueprint
	app.register_blueprint(main_blueprint)

	# register the api blueprint
	from .api import api as api_blueprint
	app.register_blueprint(api_blueprint, url_prefix='/api')

	return app
```

Now, when the `app` module is imported by `project.py`, the pre-trained model is in the current app's global scope and available for making predictions! :raised_hands: It took me longer than I would have liked to come to this realization, but now it seems glaringly obvious. The model is then able to be used by the API as such :point_down:

```python
#flask_project/app/api/api_routes.py
from flask import request, jsonify
from . import api
from app import model  # now the model is available for use by the API predict route
import pandas as pd

@api.route('/predict', methods=['POST'])
def predict():
	data = request.get_json()
	df_in = pd.read_json(data, orient='split')
	y_pred = model.predict(df_in)
	df_out = pd.DataFrame(data=y_pred, columns=['pred_DTC', 'pred_DTS'])
	return df_out.to_json(orient='split')
```

Here, `model` is imported from `app` and used in the API's `predict` route. :heavy_check_mark:

You might be wondering why I have a `main` blueprint and an `api` blueprint. The `main` submodule of `app` acts as a traditional web app that has a home page, an about page, and an email contact page. The home page explains how to use the API while the about page gives more details about the competition and what I did. Given that this is still a relatively simple app, I could possibly have opted for the one-file flavor and placed the routes for `/`, `/about`, and `/contact` in addition to an `/api` route, but if the project ever grows larger, it will become unwieldy rather quickly.

#### model memory size versus model performance

Something else I learned in making SonicPredict is that in using [DigitalOcean's](https://www.digitalocean.com/) basic droplet for deploying the project, I have only 1 GB of RAM with which to work. As this is a simple project for my portfolio, I'd like to keep costs as minimal as possible, and DO's basic droplets are perfect for this. However, my model is actually an average ensemble of five different regression models, three of which are tree-based models. Specificaly, I used a Random Forest, Gradient Boosting Decision Trees, XGBoost, PCA-Regression, & KNN regression. The tree-based model pickles are rather large, with the random forest requiring 2.1GB, the Gradient Boosting DT requiring 43 MB, and the XGBoost requiring 20 M. I quickly realized that loading these models and using them was not going to be possible with only 1 GB of RAM on the droplet!

This led me to first experiment with using compression when I output the models using joblib. While this helped, the five models were still nearly 1 GB altogether. So, I decided to drop the Random Forest & Gradient Boosting DT models from the ensemble. This resulted in only slightly worse RMSE for the blind test (16.51 using only XGBoost, PCR, & KNN versus 16.31 using all five models). Something to keep in mind in the future is that there appears to be a tradeoff between model performance and model weight :muscle:, but the incremental improvement in performance may not be worth the weight savings! Said differently, the lighter model performs nearly as well as the full model, at least on the provided blind test data. 

### summary

In this post I first discussed what the SonicPredict API is, why I made it, how it works, and where a user can interact with it. My main motivation for the project was to close out a data-science & machine learning project by deploying a pre-trained model with an API powered by Flask. I then discussed several learnings I made along the way, including when and where to load a model when using Flask's application factory and blueprints for structuring an app, as well as some observations regarding model performance versus model memory size.

I'll write more about the actual competition and model in a future post.

Thanks for reading! :wave:

<hr />
<small>
	1. I say that the model shouldn't be used in a meaningful way not because I think it does a poor job of predicting P- and S-Sonic curves, but because I don't know how reliable the predicted curves would be for tasks such as well ties, fluid substitution, and AVO forward modeling. Furthermore, this model is built from a single well in the North Sea basin, and using it to predict sonic curves for wells outside of this basin may produce unexpected and potentially erroneous results. I think for this model to be generalized to different basins, additional training features such as depth below mudline and lithology may be needed. While I am quite happy with the model's current performance, I think it is best to treat it as an academic tool until further development is undertaken.
</small>