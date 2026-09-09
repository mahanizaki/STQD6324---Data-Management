## Project Information:
- **Course**: STQD6324 Data Management
- **Student Name**: Mahani binti Mohamad Zaki  
- **Lecturer**: Dr. Bernard Lee Kok Bang
- **Email**: bernardlkb@ukm.edu.my 

## 1. Overview of the Project
This project focuses on building and evaluating machine learning classification models using the Iris dataset within the Apache Spark (PySpark) environment.

The main objective is to classify iris flowers into three species:
- Setosa  
- Versicolor  
- Virginica  
This classification is based on their physical characteristics.

The project implements a complete data pipeline including:
- Data loading  
- Data preprocessing  
- Feature engineering  
- Model training  
- Hyperparameter tuning  
- Model evaluation  

Three classification models are developed and compared:
- Logistic Regression  
- Decision Tree  
- Random Forest  

---

## 2. Description of Dataset and Methodology

### 2.1 Dataset Description
The dataset used is the Iris dataset, which contains:
- 150 observations  
- 4 numerical features:
  - Sepal length  
  - Sepal width  
  - Petal length  
  - Petal width  
- 1 categorical target variable:
  - Species (Setosa, Versicolor, Virginica)

This dataset is balanced (50 samples per class) and suitable for multi-class classification.

---

### 2.2 Methodology

#### Step 1: Environment Setup
- Configure PySpark and Java environment  
- Create Spark session for distributed data processing

#### Step 2: Data Loading
- Load dataset from CSV file into Spark DataFrame  
- Schema inferred automatically  

#### Step 3: Data Preprocessing
- Label encoding using `StringIndexer`  
- Feature engineering using `VectorAssembler`  
- Check class distribution  

#### Step 4: Train-Test Split
Dataset split into:
- 80% training data  
- 20% testing data  

#### Step 5: Model Development
Models used:
- Logistic Regression  
- Decision Tree  
- Random Forest  

All models use:
- Hyperparameter tuning  
- 5-fold cross-validation  

#### Step 6: Model Evaluation
Models were evaluated using:
- Accuracy  
- Precision (weighted)
- Recall (weighted)
- F1-score  

---

## 3. Summary of Results and Key Findings

### Model Performance

| Model                | Accuracy | Precision | Recall | F1-score |
|---------------------|----------|----------|--------|----------|
| Logistic Regression | 0.9655   | 0.9690   | 0.9655 | 0.9651   |
| Decision Tree       | 0.9310   | 0.9310   | 0.9310 | 0.9310   |
| Random Forest       | 0.9655   | 0.9690   | 0.9655 | 0.9651   |

### Key Findings
- Best-performing models:
  - Logistic Regression and Random Forest achieved the highest and identical
- Decision Tree performance:
  - Slightly lower accuracy, indicating it may overfit or be less stable.
- Dataset impact:
  - The balanced and simple nature of the Iris dataset contributes to high model performance.
- Model insight:
  - Logistic Regression works well due to linear separability of data
  - Random Forest improves robustness through ensemble learning
  - Decision Tree is simpler but less accurate

---

## 4. Instructions to Reproduce the Analysis
Follow these steps to reproduce the project:

### Step 1: Install Required Tools
- Install:
  - Python (≥ 3.x)
  - Apache Spark
  - Java (JDK 11)
- Install Python libraries
```bash
pip install pyspark pandas
```

### Step 2: Set Environment Variables
```python
import os

os.environ["PYSPARK_PYTHON"] = "python"
os.environ["PYSPARK_DRIVER_PYTHON"] = "python"
os.environ["JAVA_HOME"] = "path_to_your_java"
```

### Step 3: Create Spark Session
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .master("local[*]") \
    .appName("IrisFix") \
    .config("spark.driver.bindAddress", "127.0.0.1") \
    .getOrCreate()
```

### Step 4: Load Dataset
```python
iris = spark.read.csv("iris.csv", header=True, inferSchema=True)
iris.show(5)
```

### Step 5: Data Preprocessing
```python
from pyspark.ml.feature import StringIndexer, VectorAssembler

# Label encoding
indexer = StringIndexer(inputCol="species", outputCol="label")
iris = indexer.fit(iris).transform(iris)

# Feature engineering
assembler = VectorAssembler(
    inputCols=["sepal_length", "sepal_width", "petal_length", "petal_width"],
    outputCol="features"
)

iris = assembler.transform(iris)

# Check class distribution
iris.groupBy("label").count().show()
```

### Step 6: Train-Test Split
```python
train_data, test_data = iris.randomSplit([0.8, 0.2], seed=123)
```

### Step 7: Model Training
- Train Logistic Regression, Decision Tree and Random Forest
- Use CrossValidator with parameter grids

### Step 8: Model Evaluation
Evaluate model performance using classification metrics

### Step 9: Compare Model Performance
- Compare Accuracy, Precision, Recall, F1-score  
- Identify the best-performing model  

---

### Final Step
Run the entire notebook to reproduce the full workflow and results.
