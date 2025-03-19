# IMF-API-Dataflow
This repository describes the procedure to retrieve and collect data from International Monetary Fund API portal. This repo contains two python scripts. First script is an explorer of the data series. Users can change the input (expnse, Trade, revenue, etc.) and find the dataseries related to that. Explorer will also provide the codelists and dimensions of the data series. 

Second file uses one of the existing method (CompactData) to collect all data from the IMF API. 

# File 1. IMF Dataflow Explorer File (imf_dataflow_explorer.py)
This Python script fetches and explores dataflows from the International Monetary Fund (IMF) using the SDMX REST API. It searches for data series based on a keyword, retrieves their dimensions, and fetches the corresponding codelists for each dimension.

## Features
- Searches for available IMF dataflows using a keyword.
- Lists matching dataflows along with their IDs.
- Retrieves dimensions for each dataflow.
- Fetches codelists associated with each dimension.

## Prerequisites
Ensure you have Python installed along with the required library:
```bash
pip install requests
```

## How to Use
1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/imf-dataflow-explorer.git
   cd imf-dataflow-explorer
   ```
2. Run the script:
   ```bash
   python imf_dataflow_explorer.py
   ```
3. The script will prompt outputs for dataflows, dimensions, and codelists.

## Script Breakdown
### Step 1: Fetch Available Dataflows
- Connects to the IMF SDMX API.
- Retrieves all available dataflows.
- Searches for dataflows matching a specified keyword.

### Step 2: Retrieve Dimensions for Matching Dataflows
- Extracts the list of dimensions for each matching dataflow.
- Prints dimension names and corresponding codelist IDs.

### Step 3: Fetch Codelists for Each Dimension
- Retrieves and displays codelists containing valid codes and descriptions.

## Example Output
```plaintext
Found series - Name: Government Finance Statistics (GFS), Expense, ID: GFSE

Dimensions for series 'Government Finance Statistics (GFS), Expense':
  Dimension 1: REF_AREA (Codelist ID: CL_AREA_GFSE)
  Dimension 2: REF_SECTOR (Codelist ID: CL_SECTOR_GFSE)

Codelists for series 'Government Finance Statistics (GFS), Expense':
  Codelist ID: CL_AREA_GFSE
    Code: USA, Description: United States
    Code: IND, Description: India
```

## Customization
Modify the `search_term` variable in the script to change the keyword for searching dataflows:
```python
search_term = 'expense'  # Change to any keyword according to your requirement
```

# File 2: IMF API Access usign CompactData for a Dataflow (Retrieve all the dimensions) 
## Features
- Queries IMF's CompactData API for government finance statistics.
- Retrieves data based on user-specified parameters.
- Converts the response into a structured pandas DataFrame.
- Supports batch processing of multiple countries, sectors, and classifications.
- Implements rate limiting to handle API request constraints.
- Saves progress to avoid redundant API calls.


## How to Use
1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/imf-compactdata-fetcher.git
   cd imf-compactdata-fetcher
   ```
2. Modify parameters in the script as needed:
   ```python
   start_year = 2000  # Set start year
   end_year = 2024  # Set end year
   data_folder = "data"  # Folder to save results
   ```
3. Run the script:
   ```bash
   python imf_compactdata_fetcher.py
   ```
4. The script will fetch the data and save CSV files for each country.

## Script Breakdown
### Step 1: Define Query Parameters
- Set the start and end years.
- Use a dictionary (`data_dict`) containing country codes, sector codes, unit measures, and classification indicators.
- Data dictionary will vary according to the dataflow. 
- In order to construct the dataflow, please use the imf_dataflow_explorer.ipynb file.
- Check the example we have to construct the data dictionary in this file. 
### Step 2: Fetch Data in Batches
- Iterates over all country-sector-unit-classification combinations.
- Fetches data using the CompactData API.
- Handles rate limits by pausing after every 10 requests.

### Step 3: Process and Store Data
- Extracts metadata and observations from API responses.
- Saves country-wise data as CSV files.
- Keeps track of the last processed classification to resume efficiently.
- Maintains a master tracking file logging saved datasets.

## Example Output
```plaintext
  Country Code Country Name Sector Code Sector Name Unit Code Unit Name Classification Code Classification Name Year Attribute Value
0          IN        India      S1311B    Central Govt    XDC   Local Currency  W0_S1_G21      Public Expenses  2000 OBS_VALUE  12345.67
1          IN        India      S1311B    Central Govt    XDC   Local Currency  W0_S1_G21      Public Expenses  2001 OBS_VALUE  13000.89
```

## Customization
Modify `data_dict` to include desired countries, sectors, and indicators to extract different datasets.

## Contributions
Feel free to fork, improve, and submit pull requests!









