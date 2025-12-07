
# Data Visualization Project

## Overview
This project demonstrates how raw numbers can be transformed into meaningful insights through data visualization.

## Contents
- sales_data.csv - 12 months sales data
- Data_Visualization_Project.ipynb - Complete analysis notebook
- Charts: Line, Bar, Pie, Heatmap
- Insights and business recommendations

## Tools Used
- Python
- Pandas
- Matplotlib
- Seaborn
- Google Colab / Jupyter Notebook

## Purpose
To showcase how data visualization helps understand patterns, trends, and insights effectively.



## Codes

            import pandas as pd

            from google.colab import files
            uploaded = files.upload()

            import pandas as pd
            import matplotlib.pyplot as plt
            import seaborn as sns
            import numpy as np
            %matplotlib inline
            plt.style.use('default')
            sns.set_palette("husl")
            plt.rcParams['figure.figsize'] = (12, 8)
            print("Libraries imported successfully!")


             df = pd.read_csv('sales_data.csv')
             print("Dataset Preview:")
             print(df.head())
             print("\nDataset Info:")
             print(df.info())
             print("\nDataset Description:")
             print(df.describe())            

             plt.figure(figsize=(10,6))
             plt.plot(df['Month'], df['Sales'], marker='o', linewidth=2.5, markersize=8, color='#2E86AB')
             plt.title('Monthly Sales Trend', fontsize=16, fontweight='bold')
             plt.xlabel('Month', fontsize=12)
             plt.ylabel('Sales (₹)', fontsize=12)
             plt.grid(True, alpha=0.3)
             plt.xticks(rotation=45)
             plt.tight_layout()
             plt.show()

             
             plt.figure(figsize=(12,6))
             bars = plt.bar(df['Month'], df['Sales'], color='skyblue', edgecolor='navy', alpha=0.8)
             plt.title('Sales by Month', fontsize=16, fontweight='bold')
             plt.xlabel('Month', fontsize=12)
             plt.ylabel('Sales (₹)', fontsize=12)
             plt.xticks(rotation=45)
             # Add value labels on bars
                      for bar, sales in zip(bars, df['Sales']):
                          plt.text(bar.get_x() + bar.get_width()/2, bar.get_height() + 200,
                                     f'₹{sales:,}', ha='center', va='bottom', fontsize=10)
                        plt.tight_layout()
                        plt.show()


              plt.figure(figsize=(10,10))
              plt.pie(df['Sales'], labels=df['Month'], autopct='%1.1f%%', startangle=90,
                      colors=sns.color_palette("Set3", 12), textprops={'fontsize': 11})
              plt.title('Sales Distribution by Month', fontsize=16, fontweight='bold', pad=20)
              plt.axis('equal')
              plt.tight_layout()
              plt.show()


              # Create numeric month column for correlation
              df_numeric = df.copy()
              df_numeric['Month_Num'] = range(1,13)
              corr_matrix = df_numeric[['Month_Num', 'Sales']].corr()

              plt.figure(figsize=(8,6))
              sns.heatmap(corr_matrix, annot=True, cmap='coolwarm', center=0,
                          square=True, linewidths=1, cbar_kws={"shrink": .8})
              plt.title('Correlation Heatmap: Month vs Sales', fontsize=14, fontweight='bold')
              plt.tight_layout()
              plt.show()
              print("Correlation between Month Number and Sales:", corr_matrix.iloc[0,1].round(3))
