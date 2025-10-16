import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt
from pulp import LpMaximize, LpProblem, LpVariable, lpSum, PULP_CBC_CMD

st.set_page_config(page_title="Timetable Optimizer", page_icon="📅", layout="centered")

st.title("📅 Optimized Timetable Scheduler")
st.markdown("### Build an optimized class timetable using Linear Programming (PuLP)")

courses = st.multiselect(
    "Select Courses:",
    ["Math", "Physics", "Chemistry", "Biology", "English"],
    default=["Math", "Physics", "Chemistry"],
)

time_slots = st.multiselect(
    "Select Available Time Slots:",
    ["9AM", "10AM", "11AM", "12PM", "1PM", "2PM"],
    default=["9AM", "10AM", "11AM", "12PM"],
)

if st.button("Generate Optimized Timetable"):
    if not courses or not time_slots:
        st.warning("Please select at least one course and one time slot.")
    else:
        # Define binary variables
        x = {(c, t): LpVariable(f"x_{c}_{t}", cat="Binary") for c in courses for t in time_slots}

        # Define LP problem
        prob = LpProblem("Timetable_Scheduler", LpMaximize)
        prob += lpSum(x[c, t] for c in courses for t in time_slots)

        # Constraints
        for c in courses:
            prob += lpSum(x[c, t] for t in time_slots) == 1
        for t in time_slots:
            prob += lpSum(x[c, t] for c in courses) <= 1

        # Solve
        prob.solve(PULP_CBC_CMD(msg=False))

        # Extract results
        schedule = [{"Course": c, "Time": t} for c in courses for t in time_slots if x[c, t].value() == 1]
        df = pd.DataFrame(schedule)

        st.subheader("✅ Optimized Timetable")
        st.dataframe(df)

        # Visualization
        st.subheader("📊 Course-Time Allocation Heatmap")
        pivot = pd.crosstab(df["Course"], df["Time"])
        fig, ax = plt.subplots()
        ax.imshow(pivot, cmap="YlGnBu", aspect="auto")
        ax.set_xticks(range(len(pivot.columns)))
        ax.set_xticklabels(pivot.columns)
        ax.set_yticks(range(len(pivot.index)))
        ax.set_yticklabels(pivot.index)
        plt.colorbar(plt.cm.ScalarMappable(cmap="YlGnBu"), ax=ax)
        st.pyplot(fig)

        # Download CSV
        csv = df.to_csv(index=False).encode("utf-8")
        st.download_button("💾 Download Timetable as CSV", csv, "optimized_timetable.csv", "text/csv")
