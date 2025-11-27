
1: Install Python
Windows:

Download Python from https://www.python.org/downloads/
Run the installer
Check "Add Python to PATH" during installation
Verify installation: Open Command Prompt and run python --version

macOS:

Download Python from https://www.python.org/downloads/
Run the .pkg installer
Verify installation: Open Terminal and run python3 --version

2: Install PyCharm

Download PyCharm Community Edition from https://www.jetbrains.com/pycharm/download/
Install using default settings
Launch PyCharm

3: Get the Project
Option A: Download ZIP

Click the green "Code" button on this repository
Select "Download ZIP"
Extract the ZIP file to your preferred location
In PyCharm: File → Open → Select the extracted BCPNN folder

Option B: Clone Repository

In PyCharm: File → New → Project from Version Control
Enter the repository URL
Click Clone

4: Configure Python Interpreter

Open the project in PyCharm
Go to File → Settings (Windows/Linux) or PyCharm → Preferences (macOS)
Navigate to Project: BCPNN → Python Interpreter
If no interpreter is shown:

Click the gear icon → Add Interpreter → Add Local Interpreter
Select "Virtualenv Environment"
Click OK
Click Apply and OK


5:
Create 3 empty CSV files:

Right-click project folder → New → File
Create: alpha.csv, beta.csv, gamma.csv


6:
Get FDA data:

Visit: https://fis.fda.gov/extensions/FPD-QDE-FAERS/FPD-QDE-FAERS.html
Download latest ASCII quarterly data(2025 Q3)
Extract and find DRUG25Q3.txt and REAC25Q3.txt files
Drag them into your PyCharm project folder

7:
Verify your Project Structure:
BCPNN/
├── bcpnn.py                 # Main execution file
├── bcpnn_parameters.py      # Parameter calculation functions
├── bcpnn_data.py           # Data processing module
├── alpha.csv               # Drug parameter output(empty for now)
├── beta.csv                # ADR parameter output(empty for now)
├── gamma.csv               # Drug-ADR pairs with signals(empty for now)
├── DRUG25Q3.txt            # FDA drug data (included)
└── REAC25Q3.txt            # FDA reaction data (included)


8: Running the Program

Method 1: Using Run Button

Open bcpnn.py
Click the green play button in the top-right corner

Method 2: Using Terminal
bashpython bcpnn.py
Or on macOS:
bashpython3 bcpnn.py

Usage
After running the program, you will see processing output:
1987571
26.34555697441101
Required Drug:


The numbers indicate:

Total records processed from FDA data
Calculated logarithmic parameter

Enter a drug name when prompted:
Required Drug: aspirin
Required ADR: bleeding
The program will output the signal strength for the drug-ADR pair.
Example Queries
Drug: ibuprofen, ADR: nausea
Drug: acetaminophen, ADR: liver damage
Drug: warfarin, ADR: bleeding
Drug: metformin, ADR: diarrhea

Output Files

After execution, three CSV files are filled:
alpha.csv

Contains drugs with calculated parameters
Columns: Drug name, frequency, statistical values

beta.csv

Contains adverse reactions with parameters
Columns: ADR name, frequency, statistical values

gamma.csv

Contains drug-ADR pairs with signal strength
Columns: Drug, ADR, IC (Information Component), signal classification

Understanding Results
Signal Classifications:

Strong Signal (IC > 2.0): High confidence association
Medium Signal (IC 0.5-2.0): Moderate confidence association
Weak Signal (IC 0-0.5): Low confidence association
No Signal: No significant association detected

The Information Component (IC) is the primary metric. Higher values indicate stronger associations.
Technical Details
Algorithm: Bayesian Confidence Propagation Neural Network (BCPNN)
Data Source: FDA Adverse Event Reporting System (FAERS), 2025 Q3
Dependencies: csv, collections, math (Python standard library)
Processing Time: 5-30 minutes depending on system specifications
