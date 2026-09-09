## Project Information:
- **Course**: STQD6324 Data Management
- **Student Name**: Mahani binti Mohamad Zaki  
- **Lecturer**: Dr. Bernard Lee Kok Bang

---

## Project Overview
This project demonstrates data processing and analytics using **Apache Spark (PySpark)** integrated with **Apache Cassandra** in a **Docker-based environment**.

The workflow includes:
- Data loading and preprocessing
- Data transformation using Spark SQL
- Storing and retrieving data from Cassandra
- Data visualization using Matplotlib
  
---

## Technologies Used

| Tool | Purpose |
|------|--------|
| Python | Programming language |
| PySpark | Big data processing |
| Apache Cassandra | NoSQL database |
| Docker | Containerization |
| Jupyter Notebook | Development environment |
| Matplotlib | Data visualization |

---

## System Requirements

- Docker Desktop installed
- At least 8GB RAM recommended
- Python 
- Internet connection (for dataset downloaded)

---

## Setup Instructions (Reproducibility)

### 1. Start Required Docker Containers

After system reboot or initial setup, start all required services:

```bash
docker start namenode
docker start datanode
docker start cassandra
docker start jupyter
```

These containers are responsible for:
- `namenode` & `datanode` → HDFS storage  
- `cassandra` → NoSQL database  
- `jupyter` → Notebook interface  

Verify all containers are running:

```bash
docker ps
```

---
### 2. Access Jupyter Notebook

Open your web browser and navigate to:

```
http://localhost:8888
```

This will open the Jupyter Notebook interface.

---

### 3. Access Cassandra Database

To interact with Cassandra, run:

```bash
docker exec -it cassandra cqlsh
```

This opens the Cassandra shell (`cqlsh`) where you can:
- Create keyspaces
- Create tables
- Run queries

---

### 4. Initialize Spark Session

Inside the Jupyter Notebook, create a Spark session with Cassandra connection:

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("CassandraSpark") \
    .config("spark.cassandra.connection.host", "cassandra") \
    .getOrCreate()
```

This step connects Spark to Cassandra for data operations.

---

### 5. Install Required Libraries

If the required Python libraries are not available, install them:

```bash
pip install pyspark pandas matplotlib
```

These libraries are used for:
- `pyspark` → Data processing  
- `pandas` → Data manipulation  
- `matplotlib` → Visualization  

---

### 6. Load Dataset

Ensure the dataset is available:
- Place dataset files inside the project directory or `data/` folder  
- If not included, download from:
  ```
  https://grouplens.org/datasets/movielens/
  ```

---

### 7. Run the Notebook

Open the notebook file:

```
Assignment 2 STQD6324_P147234.ipynb
```

Then:
- Run all cells sequentially (top to bottom)
- Ensure no errors occur during execution  

---

### 8. Expected Output

After successful execution, the notebook will produce:
- Processed data using Spark  
- Data stored and retrieved from Cassandra  
- Visualizations such as bar charts  

---

## Important Notes

- Cassandra **must be running before Spark connects**
- Restart Docker containers after system reboot  
- Spark session may timeout if left idle too long  
- Ensure correct container names are used in commands  
- If connection fails, check Docker network and container status  

---

