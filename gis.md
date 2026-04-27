# 🔥 Urban Growth Detection 

## 📌 Idea
Track how a city expanded over time using satellite images.

## 🧠 Tools
- **Google Earth Engine (GEE)** → get satellite images (Sentinel-2)  
- **Machine Learning (ML)** → classify land (urban, vegetation, water)  
- **ArcMap** → visualize maps & detect change  

## ⚙️ Workflow
1. Use GEE to collect images (e.g., 2015 vs 2025).  
2. Train a classifier (Random Forest).  
3. Detect change: vegetation → urban.  
4. Export results to ArcMap for map styling.  

## 📊 Output
- Urban growth heatmap  
- Change statistics (% growth)  

## 💡 Why it’s can be considered
- Easy dataset (available in GEE)  
- Very visual (prof loves this)  
- Direct real-world impact  
