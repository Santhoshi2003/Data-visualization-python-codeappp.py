# Data-visualization-python-codeappp.py
from flask import Flask, render_template, request
import plotly
import plotly.graph_objs as go
import json

app = Flask(_name_)

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/visualize', methods=['POST'])
def visualize():
    data = request.form.get('data')
    data_list = [int(x) for x in data.split(',')]
    x_values = list(range(1, len(data_list) + 1))
    y_values = data_list

    trace = go.Scatter(x=x_values, y=y_values, mode='lines+markers')
    data = [trace]
    layout = go.Layout(title='Dynamic Data Visualization', xaxis=dict(title='X'), yaxis=dict(title='Y'))

    graphJSON = json.dumps({'data': data, 'layout': layout}, cls=plotly.utils.PlotlyJSONEncoder)

    return render_template('visualization.html', graphJSON=graphJSON)

if _name_ == '_main_':
    app.run(debug=True)
