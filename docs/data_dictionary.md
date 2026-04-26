# Data Dictionary — `accident_data.csv`

This document defines every column in the dataset, its data type, possible values, and known data quality notes.

---

## File Overview

| Property | Value |
|----------|-------|
| File | `accident_data.csv` |
| Rows | 660,679 |
| Columns | 14 |
| Time Range | January 2019 – December 2022 |
| Geography | United Kingdom |
| Source | UK STATS19 Road Safety Data |

---

## Column Definitions

### `Index`
- **Type:** String
- **Description:** Unique identifier for each accident record
- **Format:** Alphanumeric code (e.g., `200701BS64157`)
- **Nulls:** 0

---

### `Accident_Severity`
- **Type:** Categorical (String)
- **Description:** Overall severity classification of the accident
- **Values:**

| Value | Count | Description |
|-------|-------|-------------|
| `Slight` | 563,801 | Minor injuries only |
| `Serious` | 88,217 | At least one person seriously injured |
| `Fatal` | 8,661 | At least one person killed |

- **Nulls:** 0

---

### `Accident Date`
- **Type:** Date String
- **Description:** Date on which the accident occurred
- **Format:** `DD-MM-YYYY` (e.g., `05-06-2019`)
- **Range:** 01-01-2019 to 31-12-2022
- **Nulls:** 0
- **Note:** Must be parsed with `dayfirst=True` in pandas or set to Date data type in Tableau

---

### `Latitude`
- **Type:** Float
- **Description:** GPS latitude coordinate of the accident location
- **Range:** Approximately 50.0 – 60.0 (UK bounds)
- **Nulls:** 25
- **Note:** Used for map plotting in Tableau alongside `Longitude`

---

### `Longitude`
- **Type:** Float
- **Description:** GPS longitude coordinate of the accident location
- **Range:** Approximately -8.0 – 2.0 (UK bounds)
- **Nulls:** 26
- **Note:** Used for map plotting in Tableau alongside `Latitude`

---

### `Light_Conditions`
- **Type:** Categorical (String)
- **Description:** Ambient lighting conditions at time of accident
- **Values:**

| Value | Count |
|-------|-------|
| `Daylight` | 484,880 |
| `Darkness - lights lit` | 129,335 |
| `Darkness - no lighting` | 37,437 |
| `Darkness - lighting unknown` | 6,484 |
| `Darkness - lights unlit` | 2,543 |

- **Nulls:** 0

---

### `District Area`
- **Type:** String
- **Description:** Name of the local authority district where the accident occurred
- **Top Districts:**

| District | Count |
|----------|-------|
| Birmingham | 13,491 |
| Leeds | 8,898 |
| Manchester | 6,720 |
| Bradford | 6,212 |
| Sheffield | 5,710 |
| Westminster | 5,706 |

- **Nulls:** 0

---

### `Number_of_Casualties`
- **Type:** Integer
- **Description:** Total number of people (of any severity) injured or killed in the accident
- **Range:** 1 – 68
- **Mean:** 1.36
- **Total across dataset:** 896,568
- **Nulls:** 0
- **Note:** This counts people, not vehicles. A single accident can produce multiple casualties.

---

### `Number_of_Vehicles`
- **Type:** Integer
- **Description:** Count of vehicles involved in the accident
- **Nulls:** 0

---

### `Road_Surface_Conditions`
- **Type:** Categorical (String)
- **Description:** State of the road surface at the time of accident
- **Values:**

| Value | Count |
|-------|-------|
| `Dry` | 447,821 |
| `Wet or damp` | 186,708 |
| `Frost or ice` | 18,517 |
| `Snow` | 5,890 |
| `Flood over 3cm. deep` | 1,017 |

- **Nulls:** 726

---

### `Road_Type`
- **Type:** Categorical (String)
- **Description:** Classification of the road on which the accident occurred
- **Values:**

| Value | Count |
|-------|-------|
| `Single carriageway` | 492,143 |
| `Dual carriageway` | 99,424 |
| `Roundabout` | 43,992 |
| `One way street` | 13,559 |
| `Slip road` | 7,041 |

- **Nulls:** 4,520

---

### `Urban_or_Rural_Area`
- **Type:** Categorical (String)
- **Description:** Whether the accident occurred in an urban or rural setting
- **Values:**

| Value | Count |
|-------|-------|
| `Urban` | 421,663 |
| `Rural` | 238,990 |
| `Unallocated` | 11 |

- **Nulls:** 15

---

### `Weather_Conditions`
- **Type:** Categorical (String)
- **Description:** Weather at the time of accident
- **Values:**

| Value | Count |
|-------|-------|
| `Fine no high winds` | 520,885 |
| `Raining no high winds` | 79,696 |
| `Other` | 17,150 |
| `Raining + high winds` | 9,615 |
| `Fine + high winds` | 8,554 |
| `Snowing no high winds` | 6,238 |
| `Fog or mist` | 3,528 |
| `Snowing + high winds` | 885 |

- **Nulls:** 14,128 (~2.1% of rows)

---

### `Vehicle_Type`
- **Type:** Categorical (String)
- **Description:** Primary vehicle type involved in the accident
- **Top Values:**

| Value | Count |
|-------|-------|
| `Car` | 497,992 |
| `Van / Goods 3.5 tonnes mgw or under` | 34,160 |
| `Bus or coach (17 or more pass seats)` | 25,878 |
| `Motorcycle over 500cc` | 25,657 |
| `Goods 7.5 tonnes mgw and over` | 17,307 |
| `Motorcycle 125cc and under` | 15,269 |
| `Taxi/Private hire car` | 13,294 |

- **Nulls:** 0

---

## Data Quality Summary

| Column | Null Count | % Missing | Recommendation |
|--------|-----------|-----------|----------------|
| `Weather_Conditions` | 14,128 | 2.14% | Impute as "Unknown" or exclude from weather analysis |
| `Road_Type` | 4,520 | 0.68% | Impute as "Unknown" or exclude from road type analysis |
| `Road_Surface_Conditions` | 726 | 0.11% | Safe to drop or impute |
| `Latitude` / `Longitude` | 25–26 | <0.01% | Drop from map view only; retain for other analysis |
| `Urban_or_Rural_Area` | 15 | <0.01% | Negligible — safe to drop |
