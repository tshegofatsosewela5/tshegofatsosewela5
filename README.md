import dash
from dash import dcc, html
from dash.dependencies import Input, Output, State
import plotly.express as px
import pandas as pd
# Sample Data
modules_data = pd.DataFrame({
    'Module': ['Module A', 'Module B', 'Module C', 'Module A', 'Module B', 'Module C'],
    'Risk Level': ['High', 'Medium', 'Low', 'High', 'Medium', 'Low'],
    'Pass Rate': [65, 75, 85, 70, 78, 88],
    'Avg Engagement': [40, 60, 80, 45, 62, 85]
})

# Initialize Dash app
app = dash.Dash(__name__)

# Options for dropdown
module_options = [{'label': mod, 'value': mod} for mod in modules_data['Module'].unique()]

# Layout of the dashboard
app.layout = html.Div([
    html.H1("Siyaphumelela University Module Performance Dashboard"),
    
    # University Emblem
    html.Div([
        html.Img(src="assets/SMU_logo.png", style={'height': '100px', 'width': 'auto'}),
        html.H3("Sefako Makgatho Health Sciences University")
    ], style={'textAlign': 'center'}),
    
    # Raw Data Entry Section
    html.Div([
        html.H2("Raw Data Input"),
        dcc.Textarea(
            id='raw-data-input',
            placeholder='Enter raw data here...',
            style={'width': '100%', 'height': 100},
        ),
        html.Button("Submit Data", id="submit-button", n_clicks=0)
    ], style={'margin-bottom': '20px'}),
    
    # Overview Section
    html.Div([
        html.H2("High-Risk Module Overview"),
        dcc.Graph(
            id='risk-level-bar',
            figure=px.bar(modules_data, x='Module', y='Pass Rate', color='Risk Level',
                          title="Pass Rate by Module Risk Level")
        )
    ]),
    
    # Engagement Metrics
    html.Div([
        html.H2("Student Engagement Metrics"),
        dcc.Graph(id='engagement-metrics'),
        dcc.Dropdown(
            id='module-dropdown',
            options=module_options,
            value='Module A'
        )
    ]),

    # Box and Whisker Plot Section
    html.Div([
        html.H2("Pass Rate Distribution Across Modules"),
        dcc.Graph(
            id='pass-rate-boxplot',
            figure=px.box(modules_data, x='Module', y='Pass Rate', color='Module',
                          title="Pass Rate Distribution by Module")
        )
    ]),

    # Interactive Module Tracking
    html.Div([
        html.H2("Module Tracking and Interventions"),
        dcc.Graph(id='module-tracking')
    ])
])

# Callbacks for interactivity
@app.callback(
    Output('engagement-metrics', 'figure'),
    [Input('module-dropdown', 'value')]
)
def update_engagement_chart(selected_module):
    filtered_data = modules_data[modules_data['Module'] == selected_module]
    fig = px.line(filtered_data, x='Module', y='Avg Engagement', title=f"Engagement Over Time for {selected_module}")
    return fig

@app.callback(
    Output('module-tracking', 'figure'),
    [Input('module-dropdown', 'value')]
)
def update_module_tracking(selected_module):
    filtered_data = modules_data[modules_data['Module'] == selected_module]
    fig = px.line(filtered_data, x='Module', y='Pass Rate', title=f"Pass Rate Trend for {selected_module}")
    return fig

# Optional: Callback for parsing raw data if needed
@app.callback(
    Output('risk-level-bar', 'figure'),
    [Input('submit-button', 'n_clicks')],
    [State('raw-data-input', 'value')]
)
def parse_and_update_data(n_clicks, raw_data):
    if n_clicks > 0 and raw_data:
        # Parse and update `modules_data` here as needed
        pass
    # Example figure to return
    return px.bar(modules_data, x='Module', y='Pass Rate', color='Risk Level')

# Run the Dash app
if __name__ == '__main__':
    app.run_server(debug=True)- 👋 Hi, I’m @tshegofatsosewela5
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
tshegofatsosewela5/tshegofatsosewela5 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
