# 🧊 Classification of First-Year Ice (FYI) and Multi-Year Ice (MYI) & Snow Depth Estimation Using Passive Microwave Data

This project classifies Arctic sea ice into **First-Year Ice (FYI)** and **Multi-Year Ice (MYI)** and estimates **5-day averaged snow depth** using passive microwave satellite data. It leverages emissivity differences at microwave frequencies to distinguish ice types and visualizes snow depth over a defined Arctic region.

## 📡 Data Source

- **Dataset**: [NSIDC AE_SI12 v3](https://nsidc.org/data/au_si12/versions/1)
- **Format**: HDF-EOS5 (.he5)
- **Grid**: Northern Hemisphere Polar Stereographic, 12.5 km resolution
- **Fields Used**:
  - `SI_12km_NH_18H_ASC` and `SI_12km_NH_23H_ASC`: Brightness temperatures at 18 GHz and 23 GHz (horizontal polarization)
  - `SI_12km_NH_SNOWDEPTH_5DAY`: 5-day averaged snow depth over sea ice (in cm)
  - `lat`, `lon`: Geographic coordinates

## 🌍 Area of Interest

- Latitude: **70°N to 85°N**
- Longitude: **-10°E to 50°E**  
This region covers parts of the **central Arctic Ocean**.

## 🧠 Project Logic

This project is based on the principle that **different types of sea ice exhibit distinct microwave emission characteristics**, which can be detected by satellite sensors. Here's the logic broken down:

### 1. **Microwave Emissivity Behavior**
- **First-Year Ice (FYI)** has a smoother and wetter surface compared to MYI.
- **Multi-Year Ice (MYI)** has undergone multiple melt-freeze cycles, making it rougher and more emissive.
- As a result, FYI and MYI reflect and emit microwaves differently, especially at different frequencies.
---
### 2. **Using Emissivity Variability Difference (EVD)**
- We use **brightness temperature** values at two frequencies: **18 GHz** and **23 GHz**.
- The difference in brightness temperature (EVD) highlights the emissivity contrast between ice types:

---
- **Classification Rule**:
- If `0 ≤ EVD ≤ 100` → likely **FYI**.
- Otherwise → likely **MYI**.
- This rule is derived from observed patterns in microwave remote sensing literature.

### 3. **Snow Depth Estimation**
- Snow depth data from passive microwave sensors is available as a separate variable in the dataset.
- This is visualized directly to understand snow accumulation patterns over the classified sea ice.

By combining emissivity-based classification and snow depth mapping, this project provides a compact yet powerful view into the cryospheric conditions in the Arctic region using only satellite microwave data.

---

## 🧪 Methodology

### 1. **Preprocessing**
- Load HDF-EOS5 data using `h5py`.
- Extract latitude, longitude, and brightness temperature fields.
- Apply a mask to crop the Arctic region of interest.

### 2. **Sea Ice Classification**
- Compute **Emissivity Variability Difference (EVD)**:  
  `EVD = BT_18GHz - BT_23GHz`
- Classification Rule:
  - **FYI (First-Year Ice)**: `0 ≤ EVD ≤ 100`
  - **MYI (Multi-Year Ice)**: Otherwise
- Output: Classified map of ice types.---

### 3. **Snow Depth Estimation**
- Use `SI_12km_NH_SNOWDEPTH_5DAY` field.
- Convert fill values to NaNs.
- Plot snow depth as a 2D heatmap.

---

## 📊 Visualizations

- Brightness temperature maps (18GHz, 23GHz)
- EVD histogram
- Sea ice classification map
- 5-day averaged snow depth

---

## 🧰 Tools & Libraries

- Python 3
- `h5py`, `numpy`, `matplotlib`

---

## ✅ Results

- Successfully distinguished MYI and FYI using EVD thresholds.
- Generated visual maps of snow depth and ice type over the Arctic.
- Data-driven insight into seasonal ice patterns using passive microwave signatures.

---

## 🔖 Credits

- Data provided by **NASA NSIDC DAAC**
- Visualization and analysis by **[@gauravsinghiitb]**  

