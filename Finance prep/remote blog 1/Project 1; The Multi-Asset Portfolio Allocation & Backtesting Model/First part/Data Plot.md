![[Normalized_ETF_Growth.png]]
## Code
```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# 1. Load the raw dataset as text to prevent header misalignments
file_path = 'Project_1.csv'
df_raw = pd.read_csv(file_path, header=None, dtype=str)

# 2. Dynamically locate the 'Date' header row and column index
date_row_idx = None
date_col_idx = None

for r in range(min(10, len(df_raw))):
    for c in range(df_raw.shape[1]):
        val = str(df_raw.iloc[r, c]).strip()
        if val.lower() == 'date':
            date_row_idx = r
            date_col_idx = c
            break
    if date_row_idx is not None:
        break

# Fallback positions if the text 'Date' is omitted
if date_row_idx is None:
    date_row_idx = 2
    date_col_idx = 1

data_start_row = date_row_idx + 1

# 3. Flexible Date Parsing (prevents empty DataFrame / NaT conversion errors)
dates = pd.to_datetime(df_raw.iloc[data_start_row:, date_col_idx], format='mixed', errors='coerce')

# Secondary fallback if automatic inference returns empty rows
if dates.isna().all():
    dates = pd.to_datetime(df_raw.iloc[data_start_row:, date_col_idx], dayfirst=True, errors='coerce')

# 4. Extract ETF Tickers and Closing Prices
tickers = ['AHIFX', 'VEU', 'VNQ', 'VOO']
plot_df = pd.DataFrame({'Date': dates})

for idx, ticker in enumerate(tickers):
    col_idx = date_col_idx + 1 + idx
    plot_df[ticker] = pd.to_numeric(df_raw.iloc[data_start_row:, col_idx], errors='coerce')

# Remove rows without valid dates
plot_df.dropna(subset=['Date'], inplace=True)

# Safeguard check before indexing
if plot_df.empty:
    raise ValueError("DataFrame is empty. Could not parse dates from column index.")

plot_df.set_index('Date', inplace=True)

# 5. Normalize all ETFs to start from the exact same baseline (100)
normalized_df = (plot_df / plot_df.iloc[0]) * 100

# 6. Plot static graph matching the darkgrid style
sns.set_theme(style="darkgrid")
fig, ax = plt.subplots(figsize=(10, 6))

for ticker in normalized_df.columns:
    ax.plot(normalized_df.index, normalized_df[ticker], label=ticker)

ax.set_title('Normalized ETF Growth Comparison (Base = 100)', fontsize=16)
ax.set_xlabel('Date', fontsize=14)
ax.set_ylabel('Normalized Value (Base = 100)', fontsize=14)
ax.legend(loc='upper left', fontsize=12)

plt.tight_layout()

# Save figure to file
plt.savefig('Normalized_ETF_Growth.png', dpi=300)
plt.show()
```