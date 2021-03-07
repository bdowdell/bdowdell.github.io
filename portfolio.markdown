---
layout: page
title: portfolio.
permalink: /portfolio/
---

<div class="grid-container">
	<div class="card">
		<div class="bg-img">
			<a href="https://sonicpredict.com" target="_blank">
				<img src="{{site.url}}/assets/img/residual_plot.png">
			</a>
		</div>
		<div class="content">
			<h4>SonicPredict</h4>
			<p>
				SonicPredict is a Flask API that serves a fitted ML-model from which users can predict sonic well logs. The fitted model comes from my entry to the 2020 SPWLA PDDASIG Machine Learning Contest and consists of an ensemble of XGBoost, PCR regression, & KNN regression.
			</p>
			<button>Readmore</button>
		</div>
	</div>
	<div class="card">
		<div class="bg-img">
			<a href="https://pyseistuned.com" target="_blank">
				<img src="{{site.url}}/assets/img/synthetic_wedge_model_extra.png">
			</a>
		</div>
		<div class="content">
			<h4>PySeisTuned<sup>2.0</sup></h4>
			<p>
				PySeisTuned<sup>2.0</sup> is a Flask web app that allows users to produce seismic tuning wedge forward models. The original version was builting using PyQT5 and was a desktop app. In order to make the tool widely accessible, I rebuilt it using Flask, HTML, & Bootstrap CSS to create a web app that removed the need to install and launch the program. Now a user can simply visit the site, input the model parameters and receive the output plots and tuning estimates.
			</p>
			<button>Readmore</button>
		</div>
	</div>
</div>