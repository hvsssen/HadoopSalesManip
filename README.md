# HadoopSalesManip

A Hadoop MapReduce project for analyzing sales data using Docker containers.

## Project Structure

This repository contains Hadoop MapReduce jobs for processing and analyzing sales transactions data.

### enit_tp1_wordcount Folder

The `enit_tp1_wordcount` folder contains the complete MapReduce implementation for sales analysis. You can find this folder in the repository:[(https://github.com/hvsssen/MapreducesforHadoop)]

## Prerequisites

- Docker and Docker Compose installed
- Java Development Kit (JDK) 8 or higher
- Apache Maven
- Hadoop Docker containers running (namenode, datanode, etc.)

## Execution Steps

Follow these steps to build and execute the MapReduce jobs:

### 1. Navigate to the project directory
```bash
cd .\enit_tp1_wordcount\
```

### 2. Build the project (after adding or changing Java code)
```bash
mvn clean package
```
This command will:
- Clean any previous builds
- Compile the Java source code
- Package the application into a JAR file located in the `target/` directory

### 3. Copy the JAR file to the Hadoop namenode container
```bash
docker cp enit_tp1_wordcount/target/Wordcount2-0.jar namenode:/Wordcount2-0.jar
```

### 4. Execute the MapReduce job
```bash
docker exec -it namenode hadoop jar /Wordcount2-0.jar tn.enit.tp1.StoreSalesJob input output_store_sales
```
This command runs the StoreSalesJob with:
- Input directory: `input`
- Output directory: `output_store_sales`

### 5. View the results
```bash
docker exec -it namenode hadoop fs -cat /user/root/output_payment2/part-r-00000
```
This displays the output results from the MapReduce job.

## Available Jobs

- **StoreSalesJob**: Analyzes store sales data and generates aggregated reports

## Input Data

Ensure your input data is placed in the HDFS `input` directory before running the jobs.

## Output

Results are stored in the specified output directory in HDFS. Each job creates part files (e.g., `part-r-00000`) containing the processed results.

## Development Workflow

1. Make changes to the Java code in `enit_tp1_wordcount/src/`
2. Build the project using Maven: `mvn clean package`
3. Copy the new JAR to the namenode container
4. Execute the updated job
5. Review the results

## Notes

- Make sure your Hadoop cluster is running before executing these commands
- The output directory must not exist before running a job (Hadoop will create it)
- If you need to rerun a job, delete the output directory first using:
  ```bash
  docker exec -it namenode hadoop fs -rm -r output_store_sales
  ```

## License

This project is for educational purposes.
