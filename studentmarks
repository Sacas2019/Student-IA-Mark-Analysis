import streamlit as st
import pandas as pd

st.set_page_config(page_title="Student Result Analysis", layout="wide")

st.title("📊 Student Result Analysis System")

uploaded_file = st.file_uploader(
    "Upload Student Excel File",
    type=["xlsx", "xls"]
)

if uploaded_file is not None:
    df = pd.read_excel(uploaded_file)

    st.success("File Uploaded Successfully!")

    st.subheader("Student Data")
    st.dataframe(df)

    # Enter your subject column names here
    subjects = ["Tamil", "English", "Maths", "Science", "Social"]

    df["Total"] = df[subjects].sum(axis=1)
    df["Percentage"] = df["Total"] / (len(subjects) * 100) * 100

    df["Rank"] = df["Percentage"].rank(
        ascending=False,
        method="min"
    ).astype(int)

    st.subheader("Student Result")

    st.dataframe(df)

    st.subheader("Top 3 Rank Holders")

    top3 = df.sort_values("Rank").head(3)

    st.table(
        top3[
            ["Roll No", "Student Name", "Total", "Percentage", "Rank"]
        ]
    )

    st.subheader("Subject-wise Average")

    st.bar_chart(df[subjects].mean())

    csv = df.to_csv(index=False).encode("utf-8")

    st.download_button(
        "Download Result",
        csv,
        file_name="Student_Result.csv",
        mime="text/csv"
    )
