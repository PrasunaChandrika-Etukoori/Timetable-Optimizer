# Timetable-Optimizer
A Streamlit app for optimizing timetables using Linear Programming (PuLP)
# 📅 Timetable Optimizer using Linear Programming (PuLP)

An interactive **Streamlit web app** that generates an optimized timetable using **Linear Programming** with PuLP.

## 🚀 Features
- Automatically creates conflict-free timetables
- Select custom courses and time slots
- Visualizes results with a heatmap
- Download the optimized schedule as a CSV file

## 🧠 How It Works
This app uses linear programming to assign courses to time slots so that:
- Each course appears exactly once.
- No two courses overlap.

## 🧰 Tech Stack
- Python
- Streamlit
- PuLP
- Pandas
- Matplotlib

## ▶️ Run Locally
```bash
git clone https://github.com/<your-username>/Timetable-Optimizer.git
cd Timetable-Optimizer
pip install -r requirements.txt
streamlit run app.py
