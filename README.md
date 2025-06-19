# Plotings-for-Attendance

import pandas as pd

# === Load attendance using correct header row ===
attendance_df = pd.read_excel("Physics.xlsx", header=1)
student_list_df = pd.read_excel("SPS LIST_25.xlsx")

# === Fix attendance column names manually ===
attendance_df.columns = ["STUDENT ID", "FULL NAME", "CLASSES HELD", "ATTENDED", "ATTENDANCE %"]

# === Normalize column names in student list ===
student_list_df.columns = student_list_df.columns.str.upper().str.strip()

# === Clean and normalize Student ID values ===
attendance_df["STUDENT ID"] = attendance_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()
student_list_df["STUDENT ID"] = student_list_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()

# === Merge only matching students ===
merged_df = pd.merge(student_list_df, attendance_df, on="STUDENT ID", how="inner")

# === Create full name from FIRST + LAST ===
merged_df["FULL NAME"] = merged_df["FIRST NAME"].str.upper().str.strip() + " " + merged_df["LAST NAME"].str.upper().str.strip()

# === Final output ===
final_df = merged_df[["FULL NAME", "STUDENT ID", "ATTENDANCE %"]]
final_df.to_excel("Filtered_Physics_Attendance.xlsx", index=False)

print("✅ Attendance exported successfully to 'Filtered_Physics_Attendance.xlsx'")
from google.colab import files
files.download('Filtered_Physics_Attendance.xlsx')





import pandas as pd

# === Load attendance using correct header row ===
attendance_df = pd.read_excel("ACCOUNTING SUMMARY.xlsx", header=1)
student_list_df = pd.read_excel("SPS LIST_25.xlsx")

# === Fix attendance column names manually ===
attendance_df.columns = ["STUDENT ID", "FULL NAME", "CLASSES HELD", "ATTENDED", "ATTENDANCE %"]

# === Normalize column names in student list ===
student_list_df.columns = student_list_df.columns.str.upper().str.strip()

# === Clean and normalize Student ID values ===
attendance_df["STUDENT ID"] = attendance_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()
student_list_df["STUDENT ID"] = student_list_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()

# === Merge only matching students ===
merged_df = pd.merge(student_list_df, attendance_df, on="STUDENT ID", how="inner")

# === Create full name from FIRST + LAST ===
merged_df["FULL NAME"] = merged_df["FIRST NAME"].str.upper().str.strip() + " " + merged_df["LAST NAME"].str.upper().str.strip()

# === Final output ===
final_df = merged_df[["FULL NAME", "STUDENT ID", "ATTENDANCE %"]]
final_df.to_excel("Filtered_ACCOUNTING_Attendance.xlsx", index=False)

print("✅ Attendance exported successfully to 'Filtered_ACCOUNTING_Attendance.xlsx'")
from google.colab import files
files.download('Filtered_ACCOUNTING_Attendance.xlsx')



[23]
0s
import pandas as pd

# === Load attendance using correct header row ===
attendance_df = pd.read_excel("BUSINESS STUDIES.xlsx", header=1)
student_list_df = pd.read_excel("SPS LIST_25.xlsx")

# === Fix attendance column names manually ===
attendance_df.columns = ["STUDENT ID", "FULL NAME", "CLASSES HELD", "ATTENDED", "ATTENDANCE %"]

# === Normalize column names in student list ===
student_list_df.columns = student_list_df.columns.str.upper().str.strip()

# === Clean and normalize Student ID values ===
attendance_df["STUDENT ID"] = attendance_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()
student_list_df["STUDENT ID"] = student_list_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()

# === Merge only matching students ===
merged_df = pd.merge(student_list_df, attendance_df, on="STUDENT ID", how="inner")

# === Create full name from FIRST + LAST ===
merged_df["FULL NAME"] = merged_df["FIRST NAME"].str.upper().str.strip() + " " + merged_df["LAST NAME"].str.upper().str.strip()

# === Final output ===
final_df = merged_df[["FULL NAME", "STUDENT ID", "ATTENDANCE %"]]
final_df.to_excel("Filtered_BUSINESS_Attendance.xlsx", index=False)

print("✅ Attendance exported successfully to 'Filtered_BUSINESS_Attendance.xlsx'")
from google.colab import files
files.download('Filtered_BUSINESS_Attendance.xlsx')



[24]
0s
import pandas as pd

# === Load attendance using correct header row ===
attendance_df = pd.read_excel("Biology.xlsx", header=1)
student_list_df = pd.read_excel("SPS LIST_25.xlsx")

# === Fix attendance column names manually ===
attendance_df.columns = ["STUDENT ID", "FULL NAME", "CLASSES HELD", "ATTENDED", "ATTENDANCE %"]

# === Normalize column names in student list ===



[25]
0s
import pandas as pd

# === Load attendance using correct header row ===
attendance_df = pd.read_excel("CRS.xlsx", header=1)
student_list_df = pd.read_excel("SPS LIST_25.xlsx")

# === Fix attendance column names manually ===
attendance_df.columns = ["STUDENT ID", "FULL NAME", "CLASSES HELD", "ATTENDED", "ATTENDANCE %"]

# === Normalize column names in student list ===
student_list_df.columns = student_list_df.columns.str.upper().str.strip()

# === Clean and normalize Student ID values ===
attendance_df["STUDENT ID"] = attendance_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()
student_list_df["STUDENT ID"] = student_list_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()

# === Merge only matching students ===
merged_df = pd.merge(student_list_df, attendance_df, on="STUDENT ID", how="inner")

# === Create full name from FIRST + LAST ===
merged_df["FULL NAME"] = merged_df["FIRST NAME"].str.upper().str.strip() + " " + merged_df["LAST NAME"].str.upper().str.strip()

# === Final output ===
final_df = merged_df[["FULL NAME", "STUDENT ID", "ATTENDANCE %"]]
final_df.to_excel("Filtered_CRS_Attendance.xlsx", index=False)

print("✅ Attendance exported successfully to 'Filtered_CRS_Attendance.xlsx'")
from google.colab import files
files.download('Filtered_CRS_Attendance.xlsx')



[26]
0s
import pandas as pd

# === Load attendance using correct header row ===
attendance_df = pd.read_excel("Chemistry.xlsx", header=1)
student_list_df = pd.read_excel("SPS LIST_25.xlsx")

# === Fix attendance column names manually ===
attendance_df.columns = ["STUDENT ID", "FULL NAME", "CLASSES HELD", "ATTENDED", "ATTENDANCE %"]

# === Normalize column names in student list ===
student_list_df.columns = student_list_df.columns.str.upper().str.strip()

# === Clean and normalize Student ID values ===
attendance_df["STUDENT ID"] = attendance_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()
student_list_df["STUDENT ID"] = student_list_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()

# === Merge only matching students ===
merged_df = pd.merge(student_list_df, attendance_df, on="STUDENT ID", how="inner")

# === Create full name from FIRST + LAST ===
merged_df["FULL NAME"] = merged_df["FIRST NAME"].str.upper().str.strip() + " " + merged_df["LAST NAME"].str.upper().str.strip()

# === Final output ===
final_df = merged_df[["FULL NAME", "STUDENT ID", "ATTENDANCE %"]]
final_df.to_excel("Filtered_Chemistry_Attendance.xlsx", index=False)

print("✅ Attendance exported successfully to 'Filtered_Chemistry_Attendance.xlsx'")
from google.colab import files
files.download('Filtered_Chemistry_Attendance.xlsx')



[27]
0s
import pandas as pd

# === Load attendance using correct header row ===
attendance_df = pd.read_excel("ECONOMICS.xlsx", header=1)
student_list_df = pd.read_excel("SPS LIST_25.xlsx")

# === Fix attendance column names manually ===
attendance_df.columns = ["STUDENT ID", "FULL NAME", "CLASSES HELD", "ATTENDED", "ATTENDANCE %"]

# === Normalize column names in student list ===
student_list_df.columns = student_list_df.columns.str.upper().str.strip()

# === Clean and normalize Student ID values ===
attendance_df["STUDENT ID"] = attendance_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()
student_list_df["STUDENT ID"] = student_list_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()

# === Merge only matching students ===
merged_df = pd.merge(student_list_df, attendance_df, on="STUDENT ID", how="inner")

# === Create full name from FIRST + LAST ===
merged_df["FULL NAME"] = merged_df["FIRST NAME"].str.upper().str.strip() + " " + merged_df["LAST NAME"].str.upper().str.strip()

# === Final output ===
final_df = merged_df[["FULL NAME", "STUDENT ID", "ATTENDANCE %"]]
final_df.to_excel("Filtered_ECONOMICS_Attendance.xlsx", index=False)

print("✅ Attendance exported successfully to 'Filtered_ECONOMICS_Attendance.xlsx'")
from google.colab import files
files.download('Filtered_ECONOMICS_Attendance.xlsx')



[28]
0s
import pandas as pd

# === Load attendance using correct header row ===
attendance_df = pd.read_excel("GOVERNMENT.xlsx", header=1)
student_list_df = pd.read_excel("SPS LIST_25.xlsx")

# === Fix attendance column names manually ===
attendance_df.columns = ["STUDENT ID", "FULL NAME", "CLASSES HELD", "ATTENDED", "ATTENDANCE %"]

# === Normalize column names in student list ===
student_list_df.columns = student_list_df.columns.str.upper().str.strip()

# === Clean and normalize Student ID values ===
attendance_df["STUDENT ID"] = attendance_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()
student_list_df["STUDENT ID"] = student_list_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()

# === Merge only matching students ===
merged_df = pd.merge(student_list_df, attendance_df, on="STUDENT ID", how="inner")

# === Create full name from FIRST + LAST ===
merged_df["FULL NAME"] = merged_df["FIRST NAME"].str.upper().str.strip() + " " + merged_df["LAST NAME"].str.upper().str.strip()

# === Final output ===
final_df = merged_df[["FULL NAME", "STUDENT ID", "ATTENDANCE %"]]
final_df.to_excel("Filtered_GOVERNMENT_Attendance.xlsx", index=False)

print("✅ Attendance exported successfully to 'Filtered_GOVERNMENT_Attendance.xlsx'")
from google.colab import files
files.download('Filtered_GOVERNMENT_Attendance.xlsx')



[29]
0s
import pandas as pd

# === Load attendance using correct header row ===
attendance_df = pd.read_excel("ISS.xlsx", header=1)
student_list_df = pd.read_excel("SPS LIST_25.xlsx")

# === Fix attendance column names manually ===
attendance_df.columns = ["STUDENT ID", "FULL NAME", "CLASSES HELD", "ATTENDED", "ATTENDANCE %"]

# === Normalize column names in student list ===
student_list_df.columns = student_list_df.columns.str.upper().str.strip()

# === Clean and normalize Student ID values ===
attendance_df["STUDENT ID"] = attendance_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()
student_list_df["STUDENT ID"] = student_list_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()

# === Merge only matching students ===
merged_df = pd.merge(student_list_df, attendance_df, on="STUDENT ID", how="inner")

# === Create full name from FIRST + LAST ===
merged_df["FULL NAME"] = merged_df["FIRST NAME"].str.upper().str.strip() + " " + merged_df["LAST NAME"].str.upper().str.strip()

# === Final output ===
final_df = merged_df[["FULL NAME", "STUDENT ID", "ATTENDANCE %"]]
final_df.to_excel("Filtered_ISS_Attendance.xlsx", index=False)

print("✅ Attendance exported successfully to 'Filtered_ISS_Attendance.xlsx'")
from google.colab import files
files.download('Filtered_ISS_Attendance.xlsx')



[30]
0s
import pandas as pd

# === Load attendance using correct header row ===
attendance_df = pd.read_excel("LITERATURE.xlsx", header=1)
student_list_df = pd.read_excel("SPS LIST_25.xlsx")

# === Fix attendance column names manually ===
attendance_df.columns = ["STUDENT ID", "FULL NAME", "CLASSES HELD", "ATTENDED", "ATTENDANCE %"]

# === Normalize column names in student list ===
student_list_df.columns = student_list_df.columns.str.upper().str.strip()

# === Clean and normalize Student ID values ===
attendance_df["STUDENT ID"] = attendance_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()
student_list_df["STUDENT ID"] = student_list_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()

# === Merge only matching students ===
merged_df = pd.merge(student_list_df, attendance_df, on="STUDENT ID", how="inner")

# === Create full name from FIRST + LAST ===
merged_df["FULL NAME"] = merged_df["FIRST NAME"].str.upper().str.strip() + " " + merged_df["LAST NAME"].str.upper().str.strip()

# === Final output ===
final_df = merged_df[["FULL NAME", "STUDENT ID", "ATTENDANCE %"]]
final_df.to_excel("Filtered_LITERATURE_Attendance.xlsx", index=False)

print("✅ Attendance exported successfully to 'Filtered_LITERATURE_Attendance.xlsx'")
from google.colab import files
files.download('Filtered_LITERATURE_Attendance.xlsx')



[31]
0s
import pandas as pd

# === Load attendance using correct header row ===
attendance_df = pd.read_excel("Mathematics.xlsx", header=1)
student_list_df = pd.read_excel("SPS LIST_25.xlsx")

# === Fix attendance column names manually ===
attendance_df.columns = ["STUDENT ID", "FULL NAME", "CLASSES HELD", "ATTENDED", "ATTENDANCE %"]

# === Normalize column names in student list ===
student_list_df.columns = student_list_df.columns.str.upper().str.strip()

# === Clean and normalize Student ID values ===
attendance_df["STUDENT ID"] = attendance_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()
student_list_df["STUDENT ID"] = student_list_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()

# === Merge only matching students ===
merged_df = pd.merge(student_list_df, attendance_df, on="STUDENT ID", how="inner")

# === Create full name from FIRST + LAST ===
merged_df["FULL NAME"] = merged_df["FIRST NAME"].str.upper().str.strip() + " " + merged_df["LAST NAME"].str.upper().str.strip()

# === Final output ===
final_df = merged_df[["FULL NAME", "STUDENT ID", "ATTENDANCE %"]]
final_df.to_excel("Filtered_Mathematics_Attendance.xlsx", index=False)

print("✅ Attendance exported successfully to 'Filtered_Mathematics_Attendance.xlsx'")
from google.colab import files
files.download('Filtered_Mathematics_Attendance.xlsx')



[32]
7s
import pandas as pd
import matplotlib.pyplot as plt

# Load the filtered attendance file
df = pd.read_excel("Filtered_Mathematics_Attendance.xlsx")  # Update filename if needed

# Make sure columns are clean
df.columns = df.columns.str.upper().str.strip()

# Sort by attendance %
df_sorted = df.sort_values("ATTENDANCE %", ascending=False)

# Plot
plt.figure(figsize=(12, 6))
plt.barh(df_sorted["FULL NAME"], df_sorted["ATTENDANCE %"], color="skyblue")
plt.xlabel("Attendance Percentage")
plt.title("Mathematics Attendance Performance")
plt.tight_layout()
plt.gca().invert_yaxis()  # Show top performers at the top
plt.show()



[33]
3s
import pandas as pd
import matplotlib.pyplot as plt

# Load the Excel file
df = pd.read_excel("Filtered_Mathematics_Attendance.xlsx")

# Normalize column headers
df.columns = df.columns.str.upper().str.strip()

# Sort by attendance percentage
df_sorted = df.sort_values("ATTENDANCE %", ascending=False)

# Plot
plt.figure(figsize=(12, 6))
bars = plt.barh(df_sorted["FULL NAME"], df_sorted["ATTENDANCE %"], color="skyblue", label="Attendance Percentage")

# Add legend
plt.legend(loc="lower right", frameon=True)

# Add axis labels and title
plt.xlabel("Attendance Percentage")
plt.title("Mathematics Attendance Performance")

# Invert y-axis so highest % is on top
plt.gca().invert_yaxis()

# Layout formatting
plt.tight_layout()
plt.show()



[34]
5s
import pandas as pd
import matplotlib.pyplot as plt

# Load the Excel file
df = pd.read_excel("Filtered_Physics_Attendance.xlsx")

# Normalize column headers
df.columns = df.columns.str.upper().str.strip()

# Sort by attendance percentage
df_sorted = df.sort_values("ATTENDANCE %", ascending=False)

# Plot
plt.figure(figsize=(12, 6))
bars = plt.barh(df_sorted["FULL NAME"], df_sorted["ATTENDANCE %"], color="skyblue", label="Attendance Percentage")

# Add legend
plt.legend(loc="lower right", frameon=True)

# Add axis labels and title
plt.xlabel("Attendance Percentage")
plt.title("Physics Attendance Performance")

# Invert y-axis so highest % is on top
plt.gca().invert_yaxis()

# Layout formatting
plt.tight_layout()
plt.show()



[35]
2s
import pandas as pd
import matplotlib.pyplot as plt

# Load the Excel file
df = pd.read_excel("Filtered_Mathematics_Attendance.xlsx")

# Normalize column headers
df.columns = df.columns.str.upper().str.strip()

# Sort by attendance %
df_sorted = df.sort_values("ATTENDANCE %", ascending=False)

# Set up the plot
plt.figure(figsize=(14, 6))

# Plot vertical bars
bars = plt.bar(df_sorted["FULL NAME"], df_sorted["ATTENDANCE %"], color="skyblue", label="Attendance Percentage")

# Add labels and title
plt.ylabel("Attendance Percentage")
plt.title("Mathematics Attendance Performance")
plt.xticks(rotation=45, ha="right")  # Rotate x labels for readability

# Add legend
plt.legend(loc="upper right", frameon=True)

# Tight layout for cleaner spacing
plt.tight_layout()
plt.show()



[36]
4s
import pandas as pd
import matplotlib.pyplot as plt

# Load the Excel file
df = pd.read_excel("Filtered_ACCOUNTING_Attendance.xlsx")

# Normalize column headers
df.columns = df.columns.str.upper().str.strip()

# Sort by attendance %
df_sorted = df.sort_values("ATTENDANCE %", ascending=False)

# Set up the plot
plt.figure(figsize=(14, 6))

# Plot vertical bars
bars = plt.bar(df_sorted["FULL NAME"], df_sorted["ATTENDANCE %"], color="skyblue", label="Attendance Percentage")

# Add labels and title
plt.ylabel("Attendance Percentage")
plt.title("ACCOUNTING Attendance Performance")
plt.xticks(rotation=45, ha="right")  # Rotate x labels for readability

# Add legend
plt.legend(loc="upper right", frameon=True)

# Tight layout for cleaner spacing
plt.tight_layout()
plt.show()



[37]
3s
import pandas as pd
import matplotlib.pyplot as plt

# Load the Excel file
df = pd.read_excel("Filtered_Biology_Attendance.xlsx")

# Normalize column headers
df.columns = df.columns.str.upper().str.strip()

# Sort by attendance %
df_sorted = df.sort_values("ATTENDANCE %", ascending=False)

# Set up the plot
plt.figure(figsize=(14, 6))

# Plot vertical bars
bars = plt.bar(df_sorted["FULL NAME"], df_sorted["ATTENDANCE %"], color="skyblue", label="Attendance Percentage")

# Add labels and title
plt.ylabel("Attendance Percentage")
plt.title("Biology Attendance Performance")
plt.xticks(rotation=45, ha="right")  # Rotate x labels for readability

# Add legend
plt.legend(loc="upper right", frameon=True)

# Tight layout for cleaner spacing
plt.tight_layout()
plt.show()



[38]
4s
import pandas as pd
import matplotlib.pyplot as plt

# Load the Excel file
df = pd.read_excel("Filtered_CRS_Attendance.xlsx")

# Normalize column headers
df.columns = df.columns.str.upper().str.strip()

# Sort by attendance %
df_sorted = df.sort_values("ATTENDANCE %", ascending=False)

# Set up the plot
plt.figure(figsize=(14, 6))

# Plot vertical bars
bars = plt.bar(df_sorted["FULL NAME"], df_sorted["ATTENDANCE %"], color="skyblue", label="Attendance Percentage")

# Add labels and title
plt.ylabel("Attendance Percentage")
plt.title("CRS Attendance Performance")
plt.xticks(rotation=45, ha="right")  # Rotate x labels for readability

# Add legend
plt.legend(loc="upper right", frameon=True)

# Tight layout for cleaner spacing
plt.tight_layout()
plt.show()



[40]
0s
import pandas as pd
import matplotlib.pyplot as plt

# Load the Excel file
df = pd.read_excel("Filtered_ECONOMICS_Attendance.xlsx")

# Normalize column headers
df.columns = df.columns.str.upper().str.strip()

# Sort by attendance %
df_sorted = df.sort_values("ATTENDANCE %", ascending=False)

# Set up the plot
plt.figure(figsize=(14, 6))

# Plot vertical bars
bars = plt.bar(df_sorted["FULL NAME"], df_sorted["ATTENDANCE %"], color="skyblue", label="Attendance Percentage")

# Add labels and title
plt.ylabel("Attendance Percentage")
plt.title(" ECONOMICS Attendance Performance")
plt.xticks(rotation=45, ha="right")  # Rotate x labels for readability

# Add legend
plt.legend(loc="upper right", frameon=True)

# Tight layout for cleaner spacing
plt.tight_layout()
plt.show()



[42]
1s
import pandas as pd
import matplotlib.pyplot as plt

# Load the Excel file
df = pd.read_excel("Filtered_ISS_Attendance.xlsx")

# Normalize column headers
df.columns = df.columns.str.upper().str.strip()

# Sort by attendance %
df_sorted = df.sort_values("ATTENDANCE %", ascending=False)

# Set up the plot
plt.figure(figsize=(14, 6))

# Plot vertical bars
bars = plt.bar(df_sorted["FULL NAME"], df_sorted["ATTENDANCE %"], color="skyblue", label="Attendance Percentage")

# Add labels and title
plt.ylabel("Attendance Percentage")
plt.title("ISS Attendance Performance")
plt.xticks(rotation=45, ha="right")  # Rotate x labels for readability

# Add legend
plt.legend(loc="upper right", frameon=True)

# Tight layout for cleaner spacing
plt.tight_layout()
plt.show()



[43]
2s
import pandas as pd
import matplotlib.pyplot as plt

# Load the Excel file
df = pd.read_excel("Filtered_LITERATURE_Attendance.xlsx")

# Normalize column headers
df.columns = df.columns.str.upper().str.strip()

# Sort by attendance %



[44]
1s
import pandas as pd
import matplotlib.pyplot as plt

# Load the Excel file
df = pd.read_excel("Filtered_Physics_Attendance.xlsx")

# Normalize column headers
df.columns = df.columns.str.upper().str.strip()

# Sort by attendance %



[45]
2s
import pandas as pd
import matplotlib.pyplot as plt

# Load the Excel file
df = pd.read_excel("Filtered_BUSINESS_Attendance.xlsx")

# Normalize column headers
df.columns = df.columns.str.upper().str.strip()

# Sort by attendance %
…plt.title("BUSINESS Attendance Performance")
plt.xticks(rotation=45, ha="right")  # Rotate x labels for readability

# Add legend
plt.legend(loc="upper right", frameon=True)

# Tight layout for cleaner spacing
plt.tight_layout()
plt.show()



[46]
3s
import pandas as pd
import matplotlib.pyplot as plt

# Load the Excel file
df = pd.read_excel("Filtered_Chemistry_Attendance.xlsx")

# Normalize column headers
df.columns = df.columns.str.upper().str.strip()

# Sort by attendance %



[47]
4s
import pandas as pd
import matplotlib.pyplot as plt

# Load the Excel file
df = pd.read_excel("Filtered_GOVERNMENT_Attendance.xlsx")

# Normalize column headers
df.columns = df.columns.str.upper().str.strip()

