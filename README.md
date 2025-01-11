# Retrieve Data Project

This project is a Python-based data retrieval and processing script implemented in a Jupyter Notebook. The primary focus is interacting with NASA’s DONKI (Space Weather Database Of Notifications, Knowledge, and Information) API to retrieve, process, and analyze data about coronal mass ejections (CMEs) and their linked events. The code extracts key information and structures it into a Pandas DataFrame for further analysis.

## Features
- Interacts with NASA’s DONKI API to retrieve CME data.
- Processes JSON responses into a Pandas DataFrame.
- Handles nested and complex JSON structures, including linked events.
- Applies robust error handling to manage malformed data.
- Supports filtering and transformation of data for enhanced usability.

---

## Prerequisites
Ensure the following are installed on your system:
- Python (>= 3.7)
- Jupyter Notebook or Jupyter Lab
- Required Python libraries:
  - `pandas`
  - `requests`
  - `python-dotenv`
  - `json`
  - `datetime`

---

## Installation
1. Clone the repository containing this project.
2. Navigate to the project directory.
3. Create a virtual environment (optional but recommended):
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
   ```
4. Install required dependencies:
   ```bash
   pip install -r requirements.txt
   ```
   If a `requirements.txt` file does not exist, install the libraries manually:
   ```bash
   pip install pandas requests python-dotenv
   ```

---

## Setup
1. Obtain an API key from [NASA's API Portal](https://api.nasa.gov/).
2. Create a `.env` file in the project directory and add your API key:
   ```env
   NASA_API_KEY=your_api_key_here
   ```

---

## Usage
### Running the Notebook
1. Open the Jupyter Notebook:
   ```bash
   jupyter notebook retrieve_data.ipynb
   ```
2. Execute each cell sequentially to:
   - Load required libraries and configurations.
   - Fetch CME data from NASA’s DONKI API.
   - Process and analyze the retrieved data.

### Key Sections
- **Environment Setup**:
  Loads necessary dependencies and sets up the NASA API key.
- **Data Retrieval**:
  Constructs the API endpoint URL and fetches data for a specified date range.
- **Data Processing**:
  Converts JSON data into a Pandas DataFrame, handles missing values, and expands nested structures like linked events.
- **Error Handling**:
  Includes `try`/`except` blocks for graceful handling of unexpected API responses or data inconsistencies.
- **Data Analysis**:
  Extracts key details such as `activityID` from linked events and creates additional DataFrame columns for better insights.

---

## Key Functions
### `extract_activityID_from_dict(event_dict)`
- **Purpose**: Extracts the `activityID` field from a linked event dictionary.
- **Parameters**: `event_dict` (dict) – A dictionary containing event details.
- **Returns**: The `activityID` if available, otherwise `None`.
- **Error Handling**: Logs an error if the input is not a dictionary.

### DataFrame Transformation
- Expands rows where `linkedEvents` contain multiple entries.
- Filters rows with missing or invalid `linkedEvents` data.
- Adds a new column `GST_ActivityID` to link events to their respective Geomagnetic Storms (GSTs).

---

## Example Output
After processing, the DataFrame contains:
- `activityID`: Unique identifier for the CME.
- `startTime`: Start time of the CME event.
- `linkedEvent`: Details about linked events.
- `GST_ActivityID`: Extracted `activityID` from the linked events.

Example:
```plaintext
     activityID           startTime      linkedEvent                            GST_ActivityID
0  CME-2023-001  2023-01-01T00:00:00Z  {'activityID': 'GST-2023-001'}         GST-2023-001
1  CME-2023-002  2023-01-02T00:00:00Z  {'activityID': 'SEP-2023-002'}         SEP-2023-002
```

---

## Error Handling
- Handles invalid API responses using `try`/`except` blocks.
- Manages unexpected data formats by checking data types and structure.
- Logs meaningful error messages for debugging.

---

## Known Issues
- Large date ranges might lead to API rate limits. Consider narrowing the range or adding delays between requests.
- The notebook assumes that the `linkedEvents` column contains dictionaries or lists of dictionaries. Unexpected types may cause errors.

---

## Future Enhancements
- Add support for handling pagination in the API response if the data exceeds the default limit.
- Enhance visualization of CME data using libraries like `matplotlib` or `seaborn`.
- Automate saving processed data to CSV or database formats for downstream analysis.

---

## Reference
Original self-sourced code vetted and debugged with ChatGPT.

