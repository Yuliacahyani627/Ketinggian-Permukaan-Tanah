import streamlit as st
import sympy as sp
import numpy as np
import plotly.graph_objs as go

# Judul aplikasi
st.title("Aplikasi Turunan Parsial dan Permukaan Tanah 3D")

# Definisikan variabel simbolik
x, y = sp.symbols('x y')
f = 100 - 0.1*x**2 - 0.2*y**2

# Hitung turunan parsial
df_dx = sp.diff(f, x)
df_dy = sp.diff(f, y)

# Input titik evaluasi dari user
st.sidebar.header("Titik Evaluasi")
x0 = st.sidebar.number_input("x₀", value=10.0)
y0 = st.sidebar.number_input("y₀", value=5.0)

# Evaluasi nilai turunan dan fungsi pada titik
f_val = f.subs({x: x0, y: y0})
dfdx_val = df_dx.subs({x: x0, y: y0})
dfdy_val = df_dy.subs({x: x0, y: y0})

# Tampilkan hasil turunan dan fungsi
st.write("### Fungsi:")
st.latex(sp.latex(f))
st.write("### Turunan Parsial:")
st.latex(r"\frac{\partial f}{\partial x} = " + sp.latex(df_dx))
st.latex(r"\frac{\partial f}{\partial y} = " + sp.latex(df_dy))

st.write(f"**f({x0}, {y0}) = {f_val}**")
st.write(f"**∂f/∂x at ({x0}, {y0}) = {dfdx_val}**")
st.write(f"**∂f/∂y at ({x0}, {y0}) = {dfdy_val}**")

# Buat meshgrid untuk grafik
x_vals = np.linspace(x0 - 10, x0 + 10, 50)
y_vals = np.linspace(y0 - 10, y0 + 10, 50)
X, Y = np.meshgrid(x_vals, y_vals)
Z = 100 - 0.1*X**2 - 0.2*Y**2

# Bidang singgung di sekitar titik evaluasi
Z_tangent = f_val + float(dfdx_val)*(X - x0) + float(dfdy_val)*(Y - y0)

# Buat grafik 3D dengan Plotly
fig = go.Figure()

# Permukaan asli
fig.add_trace(go.Surface(x=X, y=Y, z=Z, colorscale='Viridis', opacity=0.7, name='Permukaan'))

# Bidang singgung
fig.add_trace(go.Surface(x=X, y=Y, z=Z_tangent, colorscale='Reds', opacity=0.5, showscale=False, name='Bidang Singgung'))

# Titik evaluasi
fig.add_trace(go.Scatter3d(x=[x0], y=[y0], z=[float(f_val)],
                           mode='markers', marker=dict(size=6, color='red'),
                           name='Titik Evaluasi'))

# Layout
fig.update_layout(title="Permukaan dan Bidang Singgung",
                  scene=dict(xaxis_title='x', yaxis_title='y', zaxis_title='f(x, y)'))

# Tampilkan grafik
st.plotly_chart(fig)
