import plotly.graph_objects as go

# Função para aplicar estilo moderno a gráfico de barras
def styled_bar_chart(df, x_col, y_col, title, height=600):
    fig = go.Figure(
        go.Bar(
            x=df[x_col],
            y=df[y_col],
            orientation='h',
            text=df[x_col],
            textposition='auto',
            marker=dict(color='rgba(58, 71, 80, 0.6)', line=dict(color='rgba(58, 71, 80, 1.0)', width=1.5))
        )
    )
    fig.update_layout(
        title=title,
        xaxis_title='Quantidade',
        yaxis_title='',
        template='plotly_white',
        height=height,
        font=dict(family='Arial', size=14),
        margin=dict(l=120, r=40, t=60, b=40),
    )
    return fig

# Redesenhar os 3 primeiros gráficos de barra
fig1_moderno = styled_bar_chart(top_clinicas.sort_values(by='Registros'), 'Registros', 'Clínica', 'Clínicas com Maior Número de Registros')
fig2_moderno = styled_bar_chart(top_pendencias_sim.sort_values(by='Pendências SIM'), 'Pendências SIM', 'Clínica', 'Top 10 Clínicas com Pendência = SIM')
fig3_moderno = styled_bar_chart(top_pendencias_nao_sim.sort_values(by='Registros sem Pendência SIM'), 'Registros sem Pendência SIM', 'Clínica', 'Top 10 Clínicas sem Pendência = SIM')

# Redesenhar o gráfico 4 com visual moderno
fig4_moderno = go.Figure(
    go.Bar(
        x=estado_cidade_summary_sorted['Qtd Clínicas'],
        y=estado_cidade_summary_sorted['Estado-Cidade'],
        orientation='h',
        text=estado_cidade_summary_sorted['Qtd Clínicas'],
        textposition='auto',
        hovertext=estado_cidade_summary_sorted['Clínicas (nomes)'],
        marker=dict(color='rgba(36, 123, 160, 0.6)', line=dict(color='rgba(36, 123, 160, 1.0)', width=1.5))
    )
)

fig4_moderno.update_layout(
    title='Quantidade de Clínicas por Estado e Cidade',
    xaxis_title='Qtd de Clínicas',
    yaxis_title='',
    template='plotly_white',
    height=900,
    font=dict(family='Arial', size=14),
    margin=dict(l=150, r=40, t=60, b=40),
)

# Salvar os gráficos modernos em HTML
html_moderno_path = "/mnt/data/graficos_modernos_planilha1.html"
with open(html_moderno_path, 'w') as f:
    f.write(plot(fig1_moderno, include_plotlyjs='cdn', output_type='div'))
    f.write(plot(fig2_moderno, include_plotlyjs='cdn', output_type='div'))
    f.write(plot(fig3_moderno, include_plotlyjs='cdn', output_type='div'))
    f.write(plot(fig4_moderno, include_plotlyjs='cdn', output_type='div'))

html_moderno_path
