# My-Project-Data-Handling
data handling project - sales LM

Project name: my-project-data-handling

Project alias: LM for sales

The creation of a LM for sales transactions is to assist on answering questions related to the sales information, such as: 
"What was the total revenue in Australia?" 
"Which 10 products generated the most revenue?" 
"What was the revenue in November 2019?"

Because my dataset contains only transactions from 2019 and purchasing behaviour may vary substantially by month, a purely chronological split could introduce a seasonal distribution difference between training and testing. Therefore, I will use a stratified 70/15/15 train-development-test split. The split will preserve approximately similar distributions of important variables such as month, country, and product characteristics across all three sets. The test questions will be held out from training and used only for final evaluation. I do not want to predict future sales.

Where will the raw data be stored? In Google Cloud Storage in CSV format, preserving the original source.

Where will processed data be stored? In Google Cloud Storage and BigQuery. Processed tables will be stored as Parquet files, as it is efficient, compressed and columnar. Each file will have a version identifier and timestamp. 
What file formats should I use? 
Data	Format	Reason
Original/raw data	CSV	Preserves the original source
Processed analytical data	Parquet	Efficient, compressed, columnar
LLM training data	JSONL	Standard format for LLM
Model files	Safetensors	Safe and efficient model-weight format
Configuration	JSON	Easy to read and use

Do you need a database or object storage? Both, because they solve different problems. Google Cloud Storage will have a object storage and BigQuery will have a database.

How will different versions of the data be identified? By saving the files with version numbers and timestamps. I would also maintain a JSON metadata file containing the following information: dateset_version, created, source, rows, processing_version.

How will the system access the data? I will have two different access points: 
Google Colab accessing Cloud Storage accessing files from the bucket and LLM accessing BigQuery, as I do not want to load the 431,709 rows into the LLM, keeping the database as the source of truth and avoiding overfitting.
