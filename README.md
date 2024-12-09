# ETL Data Engineering Project

This project demonstrates a complete ETL pipeline to process international trade data from multiple sources using both Python and Pentaho. The goal is to extract, clean, and transform the data into a star schema, which is then loaded into an Amazon Redshift data warehouse.

## Project Overview
- **Sources:**
  - PostgreSQL (Table: `trades`)
  - JSON File (`country-data.json`)
  - CSV File (`hs-codes.csv`)
- **Tools Used:**
  - Python (Pandas, Boto3, SQLAlchemy)
  - Pentaho Data Integration
  - Amazon Redshift
  - PostgreSQL
  - Docker 
  - Conda
- **Data Volume:** ~6 million records
- **ETL Phases:**
  1. **Extract:** Gather data from PostgreSQL, JSON, and CSV.
  2. **Transform:** Clean and reformat data for analysis.
  3. **Load:** Store cleaned data into Redshift via Amazon S3.


---

## Folder Structure
```plaintext
ETL-Data-Engineering-Project/
├── data/                       # Sample data files (JSON and CSV)
├── scripts/                    # Python scripts for ETL
│   └── template_etl_oec.ipynb  # Main ETL script
├── pentaho/                    # Pentaho workflows
│   └── transformations.ktr     # Transformation files
├── requirements.txt            # Python dependencies
├── screenshots/                # Visuals of the project
│   ├── pipeline-diagram.png    # ETL pipeline overview
│   ├── pentaho-workflow.png    # Pentaho workflow screenshot
│   └── star-schema.png         # Star schema design
└── README.md                   # Project documentation
```

---

## How to Reproduce

### 1. Clone the Repository

Clone this repository to your local machine using Git:

```bash
git clone git@github.com:Gabmax4/ETL-Data-Engineering-Project.git
```

### 2. Set Up the Environment
#### 2.1. Configure PostgreSQL with Docker
To set up the PostgreSQL database, it's recommended to use Docker to avoid installing PostgreSQL directly on your machine.

**Prerequisites:**

- Docker installed on your machine.
- Basic knowledge of Docker commands.

**Steps:**

##### 1. Create and Run the PostgreSQL Container:

**For WSL 2, Linux, or macOS:**

```bash
sudo docker run -d --name=postgres -p 5433:5432 -v postgres-volume:/var/lib/postgresql/data -e POSTGRES_PASSWORD=mysecretpass postgres
```

**For Windows:**

```bash
docker run -d --name=postgres -p 5433:5432 -v postgres-volume:/var/lib/postgresql/data -e POSTGRES_PASSWORD=mysecretpass postgres
```

**Explanation:**

- `--name=postgres`: Names the container "postgres".
- `-p 5433:5432`: Maps port 5433 on your machine to port 5432 in the container.
- `-v postgres-volume:/var/lib/postgresql/data`: Creates a Docker volume for persistent data storage.
- `-e POSTGRES_PASSWORD=mysecretpass`: Sets the PostgreSQL password to mysecretpass.

---

### Step 2: Configure DataSpell
1. Install [JetBrains DataSpell](https://www.jetbrains.com/dataspell/) and activate a free trial.
2. Create a Conda environment for the project:
```bash 
   conda create --name etl-project python=3.9
   conda activate etl-project
```
   
3. Open DataSpell and select the Conda environment created above.

#### **Connect to PostgreSQL**
1. Open the database tab in DataSpell.
2. Add a new connection with the following details:
   - **Name**: `local_postgres`
   - **Host**: `localhost`
   - **Port**: `5433`
   - **User**: `postgres`
   - **Password**: `mysecretpass`
3. Test the connection and accept any prompts to update drivers.

---

### Step 3: Load Initial Data
Download the SQL script [here](https://drive.google.com/file/d/19U7l0kp3mEh8SYYG6BjoDp0kVPYWDsqI/view) and execute it in DataSpell to populate the `trades` table.

---

### Step 4: Run the ETL Pipeline
1. Navigate to the `scripts/` folder and run the Python ETL script:
   python etl_pipeline.py
2. Verify the data in Redshift using your preferred SQL client.

---

### Key Visuals

1. **Pipeline Diagram:** [Pipeline Overview](screenshots/pipeline-diagram.png)
2. **Star Schema:** [Star Schema](screenshots/star-schema.png)
3. **Pentaho Workflow:** [Pentaho Workflow](screenshots/pentaho-workflow.png)

---

## Results
- Data successfully cleaned and transformed.
- Loaded into Amazon Redshift for querying and analytics.