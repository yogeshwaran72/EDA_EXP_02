**Ex 2 Netflix Shows & Movies**

# NAME : YOGESHWARAN A
# REG NO : 212223040249

**Aim**

To analyze Netflix dataset and compare movies vs TV shows, top producing countries, and release year trends.

**Procedure / Algorithm**

  1)Load dataset (netflix_titles.csv).
  2)Count movies vs TV shows.
  3)Group by country → top contributors.
  4)Create pivot table (release year vs type).
  5)Visualize with bar & line charts.

**Program**
```
import pandas as pd
df = pd.read_csv(r'https://raw.githubusercontent.com/allenkong221/netflix-titles-dataset/main/netflix_titles.csv')
df.head()
 print("Shape:", df.shape)
 print("Columns:", df.columns, "\n")
 print("Type counts:\n", df['type'].value_counts(), "\n")
df.groupby('type')['type'].count()
df.pivot_table(
    index='country', 
    columns='type', 
    values='title', 
    aggfunc='count', 
    fill_value=0
)
top_directors = df['director'].value_counts().head(5)
print("Top 5 Directors:\n", top_directors, "\n")
df['date_added'] = pd.to_datetime(df['date_added'])
df['year_added'] = df['date_added'].dt.year
df['month_added'] = df['date_added'].dt.month
trend = df.groupby(['year_added', 'type']).size().unstack(fill_value=0)
print("Yearly Trend by Type:\n", trend.head(), "\n")
df_genre = (df[['show_id','listed_in']] .dropna().assign(listed_in=df['listed_in'].str.split(', ')).explode('listed_in'))
df_expanded = df.merge(df_genre, on='show_id', how='left')
print("Columns after merge:\n", df_expanded.columns)
print("\nExpanded Genre Sample:\n", df_expanded[['title','listed_in_y']].head())
top_genres = df_expanded['listed_in_y'].value_counts().head(5)
print("\nTop 5 Genres:\n", top_genres, "\n")

```
**Ouptut**
<img width="1919" height="1094" alt="Screenshot 2025-09-10 085646" src="https://github.com/user-attachments/assets/a89737b8-ea20-4ab9-a202-ddf8faaf25e5" />
<img width="1919" height="1034" alt="Screenshot 2025-09-10 085711" src="https://github.com/user-attachments/assets/d241e22b-18a5-4965-b27d-45d787ab5762" />
<img width="1918" height="1085" alt="Screenshot 2025-09-10 085736" src="https://github.com/user-attachments/assets/4f36a988-e771-4e24-b164-677abaf62557" />
<img width="1919" height="1094" alt="Screenshot 2025-09-10 085752" src="https://github.com/user-attachments/assets/c245ec08-941a-4e1d-bf1f-1f842138d23c" />

**Result**
Helps Netflix in content planning & investments.
