# Task-1-november-
Load the CSV file
file_path = input("Enter path to your CSV file: ")
df = pd.read_csv(file_path)
️  missing values
df.fillna("Unknown", inplace=True)
Removing duplicate records
df = df.drop_duplicates()
Clean and standardize column headers
df.columns = (
    df.columns
    .str.strip()
    .str.lower()
    .str.replace(' ', '_')
    .str.replace('[^0-9a-zA-Z_]', '', regex=True)
Convert inconsistencies
for col in df.select_dtypes(include=["object"]).columns:
    df[col] = df[col].astype(str).str.strip()
    Detect and clean JavaScript-style Sale Dates ===
def clean_js_date_column(df, column_name):
    try:
        df[column_name] = pd.to_datetime(df[column_name], errors="coerce")
        df[column_name] = df[column_name].dt.strftime("%d/%m/%Y %H:%M GMT")
        print(f"✅ Converted '{column_name}' to standardized date format.")
    except Exception as e:
        print(f"⚠️ Could not convert '{column_name}': {e}")
    return df
     Save cleaned dataset ===
output_file = "cleaned_dataset.csv"
df.to_csv(output_file, index=False)
data set used : https://www.kaggle.com/datasets/syedanwarafridi/vehicle-sales-data?resource=download
