# SparkStreamingPlayground

A learning playground for Apache Spark batch and streaming data processing, featuring word count examples with comprehensive test suites.

## 📋 Overview

This repository contains Jupyter notebooks and utilities for exploring PySpark batch and streaming capabilities. The project demonstrates:

- **Batch Processing**: Traditional batch word count implementation
- **Streaming Processing**: Real-time streaming word count using Spark Structured Streaming
- **Test-Driven Development**: Comprehensive test suites for both batch and streaming workflows
- **Reusable Utilities**: Shared libraries for configuration, logging, and testing

## 📁 Project Structure

```
SparkStreamingPlayground/
├── 01-batch-word-count.ipynb              # Batch word count implementation
├── 02-word-count-test-suite.ipynb         # Test suite for batch word count
├── 03-streaming-word-count.ipynb          # Streaming word count implementation
├── 04-streaming-word-count-test-suite.ipynb  # Test suite for streaming word count
├── 05-invoice-stream-processing.ipynb     # Invoice stream processing (WIP)
├── lib/                                   # Shared utilities
│   ├── utils.py                          # Spark configuration and data utilities
│   ├── test_utils.py                     # Unit testing utilities
│   └── logging_config.py                 # Logging configuration
├── datasets/                              # Sample datasets
│   ├── text/                             # Text files for word count
│   └── invoices/                         # Invoice data (future use)
└── data/                                  # Runtime data directory
```

## 🚀 Features

### Batch Word Count (`01-batch-word-count.ipynb`)
- Reads text files using Spark batch API
- Performs text cleaning (lowercase, trim, filtering)
- Counts word frequencies
- Saves results to Delta table

**Key Methods:**
- `getRawData()`: Load text files with custom line separator
- `getQualityData()`: Clean and filter words
- `getWordCounts()`: Aggregate word counts
- `writeWordCounts()`: Persist results

### Streaming Word Count (`03-streaming-word-count.ipynb`)
- Reads text files using Spark Structured Streaming
- Same data quality transformations as batch
- Writes to Delta table with checkpointing
- Supports trigger-once execution for testing

**Key Differences from Batch:**
- Uses `readStream` instead of `read`
- Uses `writeStream` with checkpoint location
- Returns streaming query for monitoring

### Test Suites
Both batch and streaming implementations include comprehensive test suites that:
- Clean up previous test data and tables
- Ingest test data iteratively
- Validate results with assertions
- Support multiple test iterations

### Utility Libraries

#### `lib/utils.py`
- `load_spark_configs()`: Load Spark configuration from file
- `load_survey_df()`: Load CSV data with schema inference
- `count_by_country()`: Example aggregation function

#### `lib/test_utils.py`
- `UtilsTest`: Unit test class with PySpark session setup
- Test data loading and transformation functions

#### `lib/logging_config.py`
- `setup_logging()`: Configure file and console logging
- `get_logger()`: Get configured logger instance

## 🛠️ Technologies

- **Apache Spark**: Distributed data processing
- **PySpark**: Python API for Spark
- **Spark Structured Streaming**: Real-time stream processing
- **Delta Lake**: ACID transactions and versioning
- **Python 3.13.5**: Programming language
- **Jupyter Notebooks**: Interactive development

## 📊 Data Flow

### Batch Processing
```
Text Files → Read → Split Words → Clean → Count → Write to Delta Table
```

### Streaming Processing
```
Text Files → ReadStream → Split Words → Clean → Count → WriteStream (with Checkpointing) → Delta Table
```

## 🧪 Running Tests

### Batch Word Count Test
```python
wc_test_suite = WordCountTestSuite(spark)
wc_test_suite.runTests()
```

### Streaming Word Count Test
```python
wc_test_suite = StreamingWordCountTestSuite(spark)
wc_test_suite.runTests()
```

## 📝 Notes

- Designed for Databricks environment (uses `dbutils`)
- Configurable base directory: `/Volumes/workspace/default/spark_streaming`
- Checkpoint location for streaming: `{base_dir}/checkpoint/word_count`
- Test assertions validate words starting with 's'

