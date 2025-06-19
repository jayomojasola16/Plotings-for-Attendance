# Plotings-for-Attendance
Attendance sheet

Untitled2.ipynb
Untitled2.ipynb_

[2]
0s
import pandas as pd

# === Step 1: Load Excel Files ===
# Update these file names if needed
attendance_df = pd.read_excel("Physics.xlsx")        # Full Physics attendance file
student_list_df = pd.read_excel("SPS LIST_25.xlsx")             # Students you're interested in

# === Step 2: Normalize Student ID column names and format ===
attendance_df.rename(columns=lambda x: x.strip().upper(), inplace=True)
student_list_df.rename(columns=lambda x: x.strip().upper(), inplace=True)

# Rename ID column to a common name
if "STUDENT ID" in student_list_df.columns:
    student_list_df.rename(columns={"STUDENT ID": "STUDENT_ID"}, inplace=True)

if "STUDENT ID" in attendance_df.columns:
    attendance_df.rename(columns={"STUDENT ID": "STUDENT_ID"}, inplace=True)

# Remove slashes or fix ID format if needed
student_list_df["STUDENT_ID"] = student_list_df["STUDENT_ID"].astype(str).str.replace("/", "").str.upper()
attendance_df["STUDENT_ID"] = attendance_df["STUDENT_ID"].astype(str).str.replace("/", "").str.upper()

# === Step 3: Merge to get attendance for only students in your list ===
filtered_df = pd.merge(student_list_df, attendance_df, on="STUDENT_ID", how="inner")

# Optional: clean up to just name + attendance
if "FIRST NAME" in filtered_df.columns and "LAST NAME" in filtered_df.columns:
    filtered_df["FULL NAME"] = (
        filtered_df["FIRST NAME"].astype(str).str.upper().str.strip() +
        " " +
        filtered_df["LAST NAME"].astype(str).str.upper().str.strip()
    )

# Select only key columns
columns_to_keep = ["FULL NAME", "STUDENT_ID", "ATTENDANCE %"] if "FULL NAME" in filtered_df.columns else ["STUDENT_ID", "ATTENDANCE %"]
final_df = filtered_df[columns_to_keep]

# === Step 4: Export to Excel ===
output_file = "Filtered_Physics_Attendance.xlsx"
final_df.to_excel(output_file, index=False)
print(f"\n✅ Done! Filtered attendance saved to: {output_file}")


Next steps:

[3]
0s
print("📄 Attendance columns:", attendance_df.columns.tolist())
print("📄 Student list columns:", student_list_df.columns.tolist())

📄 Attendance columns: ['UNNAMED: 0', 'UNNAMED: 1', 'UNNAMED: 2', 'UNNAMED: 3', 'UNNAMED: 4']
📄 Student list columns: ['FIRST NAME', 'LAST NAME', 'STUDENT_ID', 'PROGRAM']

[5]
0s
import pandas as pd

# === Step 1: Load Excel Files ===
attendance_df = pd.read_excel("Physics.xlsx")
student_list_df = pd.read_excel("SPS LIST_25.xlsx")

# === Step 2: Print columns to inspect them ===
print("📄 Attendance columns:", attendance_df.columns.tolist())
print("📄 Student list columns:", student_list_df.columns.tolist())

# === Step 3: Normalize column names ===
attendance_df.columns = attendance_df.columns.str.strip().str.upper()
student_list_df.columns = student_list_df.columns.str.strip().str.upper()

# Try to find the common ID column
attendance_id_col = next((col for col in attendance_df.columns if "ID" in col), None)
studentlist_id_col = next((col for col in student_list_df.columns if "ID" in col), None)

if not attendance_id_col or not studentlist_id_col:
    raise ValueError("❌ Could not find a 'Student ID' column in one of the files.")

# Rename to common key for merging
attendance_df.rename(columns={attendance_id_col: "STUDENT_ID"}, inplace=True)
student_list_df.rename(columns={studentlist_id_col: "STUDENT_ID"}, inplace=True)

# Clean ID format
attendance_df["STUDENT_ID"] = attendance_df["STUDENT_ID"].astype(str).str.replace("/", "").str.upper()
student_list_df["STUDENT_ID"] = student_list_df["STUDENT_ID"].astype(str).str.replace("/", "").str.upper()

# === Step 4: Merge and Filter ===
merged_df = pd.merge(student_list_df, attendance_df, on="STUDENT_ID", how="inner")

# Optional: build full name if name columns exist
if "FIRST NAME" in merged_df.columns and "LAST NAME" in merged_df.columns:
    merged_df["FULL NAME"] = merged_df["FIRST NAME"].str.upper().str.strip() + " " + merged_df["LAST NAME"].str.upper().str.strip()

# Select columns
columns_to_export = ["FULL NAME", "STUDENT_ID", "ATTENDANCE %"] if "FULL NAME" in merged_df.columns else ["STUDENT_ID", "ATTENDANCE %"]
final_df = merged_df[columns_to_export]

# === Step 5: Save filtered results ===
output_file = "Filtered_Physics_Attendance.xlsx"
final_df.to_excel(output_file, index=False)

print(f"\n✅ Done! Filtered attendance saved to: {output_file}")


Next steps:

[7]
0s
import pandas as pd

attendance_df = pd.read_excel("Physics.xlsx")
student_list_df = pd.read_excel("SPS LIST_25.xlsx")

print("📄 Columns in Physics_Attendance.xlsx:")
print(attendance_df.columns.tolist())

print("\n📄 Columns in SPS LIST_25.xlsx:")
print(student_list_df.columns.tolist())

📄 Columns in Physics_Attendance.xlsx:
['Unnamed: 0', 'Unnamed: 1', 'Unnamed: 2', 'Unnamed: 3', 'Unnamed: 4']

📄 Columns in SPS LIST_25.xlsx:
['FIRST NAME', 'LAST NAME', 'STUDENT ID', 'PROGRAM']

[8]
0s
attendance_df = pd.read_excel("Physics.xlsx", header=1)
print(attendance_df.columns.tolist())

['Physics', 'Unnamed: 1', 'Unnamed: 2', 'Unnamed: 3', 'Unnamed: 4']

[10]
0s
for i in range(1, 5):
    df = pd.read_excel("Physics.xlsx", header=i)
    print(f"🔍 Header row {i}:")
    print(df.columns.tolist())
    print()

🔍 Header row 1:
['Physics', 'Unnamed: 1', 'Unnamed: 2', 'Unnamed: 3', 'Unnamed: 4']

🔍 Header row 2:
['Registration Number', 'Student Fullname', 'Classes Held', 'Attended', 'Attendance %']

🔍 Header row 3:
['JFS92/24/0090', 'WADA MUFTAHU MUHAMMAD', 123, 96, 78.05]

🔍 Header row 4:
['JFS92/24/0090', 'WADA MUFTAHU MUHAMMAD', 123, 95, 77.24]


[11]
0s
import pandas as pd

# === Step 1: Load the Physics attendance with correct header row ===
attendance_df = pd.read_excel("Physics.xlsx", header=1)
student_list_df = pd.read_excel("SPS LIST_25.xlsx")

# === Step 2: Normalize column names ===
attendance_df.columns = attendance_df.columns.str.upper().str.strip()
student_list_df.columns = student_list_df.columns.str.upper().str.strip()

# Rename for consistency
attendance_df.rename(columns={"REGISTRATION NUMBER": "STUDENT ID"}, inplace=True)

# === Step 3: Clean and match Student IDs ===
attendance_df["STUDENT ID"] = attendance_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()
student_list_df["STUDENT ID"] = student_list_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()

# === Step 4: Merge to keep only matching students ===
merged_df = pd.merge(student_list_df, attendance_df, on="STUDENT ID", how="inner")

# Optional: Create full name
merged_df["FULL NAME"] = merged_df["FIRST NAME"].str.upper().str.strip() + " " + merged_df["LAST NAME"].str.upper().str.strip()


Next steps:

[12]
0s
import pandas as pd

# Load both files
attendance_df = pd.read_excel("Physics.xlsx", header=1)
student_list_df = pd.read_excel("SPS LIST_25.xlsx")

# Show column names after normalization
attendance_df.columns = attendance_df.columns.str.upper().str.strip()
student_list_df.columns = student_list_df.columns.str.upper().str.strip()


📄 Attendance columns: ['PHYSICS', 'UNNAMED: 1', 'UNNAMED: 2', 'UNNAMED: 3', 'UNNAMED: 4']
📄 Student list columns: ['FIRST NAME', 'LAST NAME', 'STUDENT ID', 'PROGRAM']

[14]
0s
import pandas as pd

# === Step 1: Load attendance with correct header row ===
attendance_df = pd.read_excel("Physics.xlsx", header=1)
student_list_df = pd.read_excel("SPS LIST_25.xlsx")

# === Step 2: Clean up column names ===
attendance_df.columns = attendance_df.columns.str.upper().str.strip()
student_list_df.columns = student_list_df.columns.str.upper().str.strip()

# Rename Registration Number to match ID naming
attendance_df.rename(columns={"REGISTRATION NUMBER": "STUDENT ID"}, inplace=True)

# === Step 3: Format student IDs ===
attendance_df["STUDENT ID"] = attendance_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()
student_list_df["STUDENT ID"] = student_list_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()

# === Step 4: Merge and filter ===
merged_df = pd.merge(student_list_df, attendance_df, on="STUDENT ID", how="inner")

# Create full name column
merged_df["FULL NAME"] = merged_df["FIRST NAME"].str.upper().str.strip() + " " + merged_df["LAST NAME"].str.upper().str.strip()

# Select final columns
final_df = merged_df[["FULL NAME", "STUDENT ID", "ATTENDANCE %"]]

# === Step 5: Export to Excel ===
final_df.to_excel("Filtered_Physics_Attendance.xlsx", index=False)

print("✅ Filtered Physics attendance saved to 'Filtered_Physics_Attendance.xlsx'")


Next steps:

[16]
0s
import pandas as pd

# === Step 1: Load attendance from correct header row ===
attendance_df = pd.read_excel("Physics.xlsx", header=1)  # Header is row 2
student_list_df = pd.read_excel("SPS LIST_25.xlsx")

# === Step 2: Normalize column names ===
attendance_df.columns = attendance_df.columns.str.upper().str.strip()
student_list_df.columns = student_list_df.columns.str.upper().str.strip()

# === Step 3: Rename Registration Number to Student ID
if "REGISTRATION NUMBER" in attendance_df.columns:
    attendance_df.rename(columns={"REGISTRATION NUMBER": "STUDENT ID"}, inplace=True)

# === Step 4: Format Student ID columns
attendance_df["STUDENT ID"] = attendance_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()
student_list_df["STUDENT ID"] = student_list_df["STUDENT ID"].astype(str).str.replace("/", "").str.upper()

# === Step 5: Merge and filter only matching students ===
merged_df = pd.merge(student_list_df, attendance_df, on="STUDENT ID", how="inner")

# Create full name
merged_df["FULL NAME"] = merged_df["FIRST NAME"].str.upper().str.strip() + " " + merged_df["LAST NAME"].str.upper().str.strip()

# Final columns to export
final_df = merged_df[["FULL NAME", "STUDENT ID", "ATTENDANCE %"]]

# === Step 6: Save output ===
final_df.to_excel("Filtered_Physics_Attendance.xlsx", index=False)
print("✅ Filtered attendance saved to 'Filtered_Physics_Attendance.xlsx'")


Next steps:

[17]
0s
import pandas as pd

# Load both files
attendance_df = pd.read_excel("Physics.xlsx", header=1)
student_list_df = pd.read_excel("SPS LIST_25.xlsx")

# Clean up column names
attendance_df.columns = attendance_df.columns.str.upper().str.strip()
student_list_df.columns = student_list_df.columns.str.upper().str.strip()


📄 Attendance file columns:
['PHYSICS', 'UNNAMED: 1', 'UNNAMED: 2', 'UNNAMED: 3', 'UNNAMED: 4']

📄 SPS list columns:
['FIRST NAME', 'LAST NAME', 'STUDENT ID', 'PROGRAM']

📌 Sample attendance data:
               PHYSICS                    UNNAMED: 1    UNNAMED: 2 UNNAMED: 3  \
0  Registration Number              Student Fullname  Classes Held   Attended   
1        JFS92/24/0090         WADA MUFTAHU MUHAMMAD           123         96   
2        JFS92/24/0090         WADA MUFTAHU MUHAMMAD           123         95   
3        JFS92/24/0031  IDIAGHE SAMUEL ONYINYECHUKWU           123         94   
4        JFS92/24/0225            BELLO KHADIJA UMAR           123         94   

     UNNAMED: 4  
0  Attendance %  
1         78.05  
2         77.24  
3         76.42  
4         76.42  

📌 Sample student list data:
  FIRST NAME  LAST NAME   STUDENT ID PROGRAM
0     Joshua    Chijoke  JFS92240111     SPS
1       Paul    Terkula  JFS92240070     SPS
2      Elvis     Lawson  JFS92240227     SPS
3      Jason  Ken-Maobi  JFS92240230     SPS
4      David   Adedoyin  JFS92240019     SPS

[20]
0s
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



[21]
0s
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

# Sort by attendance %


Double-click (or enter) to edit

Colab paid products - Cancel contracts here
Analyze your files with code written by Gemini
..
Drop files to upload them to session storage.
Disk
70.21 GB available
ow()
