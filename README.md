# csc172-data-cleaning-mocorro
CSC172 first assignment
# Data Cleaning with AI Support

## Student Information
- Name: CYRAMAE P. MOCORRO
- Course Year: BSCS 4
- Date: 2025-09-27

## Dataset
- Source: [Kaggle/UCI link]
- Name: TITANIC

## Issues found
- Missing values: age 177
                  cabin 687
                  embarked 2
- Duplicates: 0
- Inconsistencies: ...

## Cleaning steps
1. Missing values: 0
2. Duplicates: 0
3. Inconsistencies: 561
4. Outliers: 0

## AI prompts used
- Prompt 1: "generetae a cleaning code for the dataset given"
- Generated code: # ...existing code...

        # 4. Handle Missing Values (auto for all columns)
        for col in df.columns:
            if df[col].dtype == 'O':  # Object/string columns
                df[col] = df[col].fillna(df[col].mode()[0])
            else:  # Numeric columns
                df[col] = df[col].fillna(df[col].median())

        # 5. Remove Duplicates
        df = df.drop_duplicates()

        # 6. Standardize Formats (auto for all string columns)
        for col in df.select_dtypes(include='object').columns:
            df[col] = df[col].str.strip().str.lower()

        # 7. Outlier Detection & Treatment (auto for all numeric columns)
        for col in df.select_dtypes(include=np.number).columns:
            Q1 = df[col].quantile(0.25)
            Q3 = df[col].quantile(0.75)
            IQR = Q3 - Q1
            df = df[~((df[col] < (Q1 - 1.5 * IQR)) | (df[col] > (Q3 + 1.5 * IQR)))]

        # 8. Save Cleaned Dataset
        df.to_csv("../data/cleaned_dataset.csv", index=False)
        # ...existing code...
    
    - Prompt 2: "how to display missing values, duplicates, inconsistencies, outliers"
    - Generated code:# ...existing code...

            import matplotlib.pyplot as plt
            import seaborn as sns

            # Display missing values
            print("Missing values per column:")
            print(df.isnull().sum())
            plt.figure(figsize=(10, 6))
            sns.heatmap(df.isnull(), cbar=False, cmap='viridis')
            plt.title('Missing Values Heatmap')
            plt.show()

            # Display duplicates
            print("Number of duplicate rows:", df.duplicated().sum())
            if df.duplicated().sum() > 0:
                print("Sample duplicate rows:")
                print(df[df.duplicated()].head())

            # Display inconsistencies (example: inconsistent casing/whitespace in object columns)
            for col in df.select_dtypes(include='object').columns:
                unique_vals = df[col].unique()
                print(f"Unique values in '{col}':", unique_vals[:10])  # Show first 10 unique values

            # Display outliers (boxplots for numeric columns)
            for col in df.select_dtypes(include=np.number).columns:
                plt.figure(figsize=(6, 2))
                sns.boxplot(x=df[col])
                plt.title(f'Boxplot of {col}')
                plt.show()
            # ...existing code...
## Results
- Rows before: 891
- Rows after: 561

Video: link
