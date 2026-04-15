# 📊 Pandas Checklist: `[]` vs `.loc[]`

---

## 1. Use `df['col']` when...

- **Select one column**
```python
df['price']
```

- **Build a boolean mask / filter condition**
```python
over_10k = df['price'] > 10_000
ideal_cut = df['cut'] == 'Ideal'
```

- **Create or replace an entire column**
```python
df['price'] = df['price'].astype(float)
```

- **Perform simple column operations**
```python
avg_price = df['price'].mean()
```

---

## 2. Use `df[['col1', 'col2']]` when...

- **Select multiple columns**
```python
df[['price', 'carat']]
```

> **Note:**  
> - Single brackets → `Series`  
> - Double brackets → `DataFrame`

---

## 3. Use `df[mask]` when...

- **Filter rows only**
```python
over_10k = df['price'] > 10_000
df[over_10k]
```

- **Apply multiple conditions**
```python
carat_lt5 = df['carat'] < 5
ideal_cut = df['cut'] == 'Ideal'

df[carat_lt5 & ideal_cut]
```

> ⚠️ This is safe for filtering only.  
> Problems start when you **filter AND assign**.

---

## 4. Use `df.loc[...]` when...

- **Filter rows explicitly**
```python
df.loc[df['price'] > 10_000]
```

- **Filter rows AND select columns**
```python
df.loc[df['price'] > 10_000, 'cut']
df.loc[df['price'] > 10_000, ['cut', 'color', 'clarity']]
```

- **Modify / assign values to part of a DataFrame**
```python
df.loc[df['price'] > 10_000, 'price'] = 10_000
```

- **Update values conditionally**
```python
df.loc[df['cut'] == 'Ideal', 'premium_flag'] = True
```

- **Select rows and columns by label**
```python
df.loc[0:5, ['price', 'carat']]
```

> 🔑 **Big Rule:**  
> If you are **changing part of a DataFrame**, use `.loc[]`

---

## 5. Safe Rule of Thumb

- Use `[]` for:
  - Selecting columns
  - Building masks
  - Simple filtering

- Use `.loc[]` for:
  - Filtering + selecting columns
  - Conditional assignment
  - Modifying subsets of data

---

## 6. Common Good Patterns

```python
# Build masks
over_10k = df['price'] > 10_000
ideal_cut = df['cut'] == 'Ideal'

# Apply mask
expensive_ideal = df.loc[over_10k & ideal_cut]

# Replace entire column
df['price'] = df['price'].astype(float)

# Conditional assignment
df.loc[df['price'] > 10_000, 'price_bucket'] = 'High'
```

---

## 7. Common Bad Patterns

### ❌ Chained indexing
```python
df[df['price'] > 10_000]['price'] = 0
```

**Why it’s bad:**  
Ambiguous—may not modify the original DataFrame.

### ✅ Correct
```python
df.loc[df['price'] > 10_000, 'price'] = 0
```

---

### ❌ Assigning to a filtered DataFrame
```python
filtered = df[df['cut'] == 'Ideal']
filtered['price'] = filtered['price'] * 1.1
```

**Why it’s bad:**  
Can trigger `SettingWithCopyWarning`

### ✅ Correct
```python
df.loc[df['cut'] == 'Ideal', 'price'] = df.loc[df['cut'] == 'Ideal', 'price'] * 1.1
```

---

## 8. Quick Decision Guide

| Task | Syntax |
|------|--------|
| Select one column | `df['col']` |
| Select multiple columns | `df[['col1', 'col2']]` |
| Build a condition | `df['col'] > value` |
| Filter rows | `df[mask]` or `df.loc[mask]` |
| Filter rows + columns | `df.loc[mask, 'col']` |
| Modify subset | `df.loc[mask, 'col'] = value` |
| Replace entire column | `df['col'] = ...` |

---

## 9. Most Important Takeaway

> ✅ Use `[]` to **get data simply**  
> ✅ Use `.loc[]` to **target data precisely**, especially when modifying
