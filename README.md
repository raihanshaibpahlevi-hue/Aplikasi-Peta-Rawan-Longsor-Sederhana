# Library imports
import streamlit as st
import rasterio
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# Tittle 
st.title("Aplikasi Peta Rawan Longsor Sederhana")

st.write("Upload file DEM (.tif) dan Data Curah Hujan (CSV atau TIFF)")

# Upload DEM
dem_file = st.file_uploader("Upload DEM (TIFF)", type=["tif", "tiff"])

# Upload Rainfall
rain_file = st.file_uploader("Upload Curah Hujan (CSV atau TIFF)", type=["csv", "tif", "tiff"])

if dem_file and rain_file:
    st.success("File berhasil diupload!")

    # ========== BACA DEM ==========
    with rasterio.open(dem_file) as dem_src:
        dem = dem_src.read(1).astype(float)

    # Hitung slope sederhana
    # (selisih elevasi antar piksel)
    gy, gx = np.gradient(dem)
    slope = np.sqrt(gx**2 + gy**2)

    # Normalisasi slope
    slope_norm = (slope - slope.min()) / (slope.max() - slope.min())

    # ========== BACA CURAH HUJAN ==========
    if rain_file.name.endswith(".csv"):
        rain_df = pd.read_csv(rain_file)
        # Ambil nilai rata-rata curah hujan (sederhana)
        rainfall_value = rain_df.iloc[:, 1].mean()
        # Buat raster curah hujan sebagai array dengan nilai rata-rata
        rainfall = np.full(dem.shape, rainfall_value)

    else:
        with rasterio.open(rain_file) as rain_src:
            rainfall = rain_src.read(1).astype(float)

    # Normalisasi curah hujan
    rain_norm = (rainfall - rainfall.min()) / (rainfall.max() - rainfall.min())

    # ========== HITUNG RISIKO ==========
    risk_map = slope_norm + rain_norm

    # Normalisasi risiko
    risk_map_norm = (risk_map - risk_map.min()) / (risk_map.max() - risk_map.min())

    # ========== TAMPILKAN HEATMAP ==========
    st.subheader("Peta Heatmap Kawasan Longsor")

    fig, ax = plt.subplots(figsize=(8, 6))
    heat = ax.imshow(risk_map_norm, cmap="hot")   # heatmap
    plt.colorbar(heat, ax=ax)
    st.pyplot(fig)
