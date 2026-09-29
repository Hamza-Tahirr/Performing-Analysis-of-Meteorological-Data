# Performing Analysis of Meteorological Data

A Jupyter notebook that prepares hourly weather records from 2006 to 2016 for analysis. It checks and fills missing values, converts the timestamps, builds daily and monthly averages and turns the dates into calendar features with fastai. This was my internship project at Suven Consultants & Technology Pvt. Ltd. (SCTPL).

## Background

Meteorological analyses help determine whether an event was unusual when compared to the historical record. Before that kind of comparison can be made, the raw observations have to be cleaned and put into a consistent time format, and that is the part this notebook covers.

## Dataset

`weatherHistory.csv` is included in the repository (about 13 MB). It contains 96,453 hourly observations from 1 January 2006 to 31 December 2016, with timestamps stored at a +01:00/+02:00 UTC offset.

Columns: `Formatted Date`, `Summary`, `Precip Type`, `Temperature (C)`, `Apparent Temperature (C)`, `Humidity`, `Wind Speed (km/h)`, `Wind Bearing (degrees)`, `Visibility (km)`, `Pressure (millibars)`, `Daily Summary`.

## What the notebook does

1. Loads the CSV and previews the first and last rows (96,453 rows, 11 columns).
2. Checks for missing values. Only `Precip Type` has gaps: 517 values, which is 0.0487% of the 1,060,983 cells. Rain is by far the most common type (85,224 rows against 10,712 for snow), so the gaps are filled with `rain` instead of dropping those hours.
3. Drops `Daily Summary`, since the hourly `Summary` column already describes the conditions.
4. Parses `Formatted Date` as UTC datetimes and sorts the data by time.
5. Resamples the numeric columns to daily means (4,019 rows) and monthly means (133 rows).
6. Uses fastai's `add_datepart` to split the timestamp into year, month, week, day, day of week, day of year, month/quarter/year start and end flags, and elapsed time. This brings the hourly table to 23 columns.

The notebook stops after this feature engineering step. It does not include charts or statistical tests yet.

## Tech stack

- Python 3 and Jupyter Notebook
- pandas and NumPy
- fastai (`add_datepart` from `fastai.tabular`)

## Project structure

```
.
├── Performing Analysis of Meteorological Data.ipynb   # the notebook
├── weatherHistory.csv                                 # hourly weather data
├── requirements.txt
└── LICENSE
```

## Setup and running

```bash
git clone https://github.com/Hamza-Tahirr/Performing-Analysis-of-Meteorological-Data.git
cd Performing-Analysis-of-Meteorological-Data

python -m venv venv
source venv/bin/activate        # on Windows: venv\Scripts\activate
pip install -r requirements.txt

jupyter notebook "Performing Analysis of Meteorological Data.ipynb"
```

fastai installs PyTorch as a dependency, so the first install can take a while. The notebook reads `weatherHistory.csv` with a relative path, so start Jupyter from the project folder. You don't need any API keys or environment variables.

## License

This project is released under the MIT License. See [LICENSE](LICENSE).
