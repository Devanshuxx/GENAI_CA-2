
# Medical Symptom Parser and Dictionary Enhancer

This repository contains a Python program that reads medical symptom data in various formats (CSV, TSV, JSON, XML), parses it into a dictionary, enhances the dictionary with new data, allows manual editing, and supports dictionary persistence for future reference.

## Features

- **Multi-format Data Support**: Reads data from CSV, TSV, JSON, and XML files.
- **Dictionary Creation and Enhancement**: Parses datasets to create a dictionary of symptoms and enhances it with additional data.
- **Missing Data Detection**: Identifies missing columns and tracks "Loss" of symptom information.
- **Manual Editing**: Allows users to manually edit the symptom dictionary for further customization.
- **Dictionary Persistence**: Saves the dictionary to a file and loads it for future runs.
- **File Export**: Exports the enhanced symptom dictionary for future use.

## Project Workflow

### STEP 1: Create a Symptom Dictionary

The program reads a dataset and creates a dictionary, indexed by `Patient_Id`, where the symptom values (e.g., `Fever_Mild`, `Cough_Low`, `Cold_High`) are stored. Missing data is tracked and recorded.

### STEP 2: Enhance the Symptom Dictionary

- Reads the dataset, identifies missing columns (referred to as "Loss"), and enhances the dictionary with new data.
- It reads the dataset multiple times, updating the dictionary with any new information.

### STEP 3: Attach Attributes and Ensure Zero Loss

- Additional attributes (e.g., `Patient_DOB`, `Patient_Age`) are attached to each patient in the dictionary.
- Ensures that the loss of attributes is zero, meaning no patient is missing any required data.

### STEP 4: Multi-format Data Handling, Editing, and Dictionary Persistence

- **Multi-format Support**: Reads data in CSV, TSV, JSON, or XML formats.
- **Dictionary Enhancement**: Continually enhances the dictionary with new data.
- **Dictionary Persistence**: Dumps the dictionary to a file and reloads it when needed.
- **Manual Editing**: Allows for manual editing of the dictionary, making it easy to reparse and adjust the data.

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/medical-symptom-parser.git
   cd medical-symptom-parser
   ```

2. Install the required Python dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Usage

### Step 1: Reading and Parsing the Data

You can load data in different formats (CSV, TSV, JSON, XML) and parse it into a dictionary of symptoms. The dictionary will be indexed by `Patient_Id` and will contain all the symptom information available.

Example:
```python
from main import read_data, create_symptom_dict

# Read data from a CSV file
file_path = 'data/symptoms.csv'
data = read_data(file_path, file_type='csv')

# Create the symptom dictionary
symptom_dict = create_symptom_dict(data)
```

### Step 2: Enhancing the Symptom Dictionary

As new datasets become available, you can enhance the dictionary by adding more data or correcting missing information.

Example:
```python
from main import enhance_symptom_dict

# Enhance the symptom dictionary with new data
new_data = read_data('data/new_symptoms.csv', file_type='csv')
symptom_dict = enhance_symptom_dict(new_data, symptom_dict)
```

### Step 3: Attaching Attributes and Ensuring Zero Loss

Additional attributes like `Patient_DOB` or `Patient_Age` can be added to each entry in the dictionary. You can also check that no attributes are missing (i.e., loss of attributes is zero).

```python
# Add attributes to dictionary
for patient_id in symptom_dict:
    symptom_dict[patient_id]['Patient_DOB'] = "1990-01-01"  # Example DOB
    symptom_dict[patient_id]['Patient_Age'] = 30  # Example Age
```

### Step 4: Manual Editing and Dictionary Persistence

You can manually edit the dictionary and save it for future reference using Python's `pickle` module.

Example of saving and loading the dictionary:
```python
import pickle

# Save the dictionary to a file
with open('symptom_dict.pkl', 'wb') as f:
    pickle.dump(symptom_dict, f)

# Load the dictionary from the file
with open('symptom_dict.pkl', 'rb') as f:
    symptom_dict = pickle.load(f)
```

You can also manually edit entries in the dictionary:
```python
# Example manual editing of the dictionary
symptom_dict[1]['Fever_Mild'] = 'Yes'  # Update a symptom for Patient 1
```

## Sample Data Formats

The program supports various input formats including CSV, TSV, JSON, and XML.

### CSV Example
```csv
Patient_Id,Fever_Mild,Cough_Low,Other_Symptoms
1,Yes,No,Fatigue
2,No,Yes,Headache
```

### JSON Example
```json
[
  {"Patient_Id": 1, "Fever_Mild": "Yes", "Cough_Low": "No", "Other_Symptoms": "Fatigue"},
  {"Patient_Id": 2, "Fever_Mild": "No", "Cough_Low": "Yes", "Other_Symptoms": "Headache"}
]
```

### XML Example
```xml
<Patients>
    <Patient>
        <Patient_Id>1</Patient_Id>
        <Fever_Mild>Yes</Fever_Mild>
        <Cough_Low>No</Cough_Low>
        <Other_Symptoms>Fatigue</Other_Symptoms>
    </Patient>
    <Patient>
        <Patient_Id>2</Patient_Id>
        <Fever_Mild>No</Fever_Mild>
        <Cough_Low>Yes</Cough_Low>
        <Other_Symptoms>Headache</Other_Symptoms>
    </Patient>
</Patients>
```
## Conclusion
The Medical Symptom Parser and Dictionary Enhancer provides a comprehensive framework for managing and enhancing medical symptom data. Its multi-format support, coupled with the ability to manually edit and enhance dictionaries, makes it an invaluable tool for researchers and practitioners alike. By tracking missing data and ensuring zero loss of attributes, it ensures that no patient information is overlooked.
