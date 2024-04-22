# DentalDataHarvester 🦷🌐

## Table of Contents 📑
- [About The Project](#about-the-project-)
- [Getting Started](#getting-started-)
- [Usage](#usage-)
- [Notebooks](#notebooks-)
- [Disclaimer](#disclaimer-)
- [Contributing](#contributing-)
- [License](#license-)
- [Contact](#contact-)
- [Acknowledgements](#acknowledgements-)

## About The Project 📖
The **DentalDataHarvester** is a powerful suite designed for extracting high-quality dentistry-related data from large web datasets. This project specifically taps into the vast FineWeb dataset on Huggingface, specializing in fields such as implant dentistry, periodontics, digital dentistry, and more.

### Built With
- Python 🐍
- HuggingFace Datasets 🤗
- Datatrove Library 🗄️
- Jupyter Notebooks 📓

## Getting Started 🚀
Follow these steps to get your development environment running.

### Prerequisites
First, ensure you have the following installed:
- Python 3.6 or later
- pip package manager

### Installation
1. Clone the repo:
   ```sh
   git clone https://github.com/Tuminha/DentalDataHarvester.git
   ```
2. Install the required packages:
   ```sh
   pip install -r requirements.txt
   ```

## Usage 🛠️
The **DentalDataHarvester** project is designed to facilitate the exploration and processing of dental data for academic and research purposes. Below is a detailed example of how to use the project, incorporating a data processing pipeline that filters dental data for research purposes. This example draws from the workflows established in the `dentistry_dataset.ipynb` and `technical_dental_database.ipynb` notebooks.

```python
from datatrove.pipeline.readers import ParquetReader
from datatrove.pipeline.filters import LambdaFilter
from datatrove.pipeline.writers import JsonlWriter
from datatrove.executor import LocalPipelineExecutor
import os
import logging

# Function to check if any of the keywords are present in the document text
def is_dentistry_related(document):
    dentistry_keywords = [
        # Keywords array...
    ]
    try:
        text = document.text.lower()
    except AttributeError as e:
        logging.error(f"Error accessing document text: {e}")
        return False
    return any(keyword in text for keyword in dentistry_keywords)

# Set the output path to your preferred location and create a folder for the output
output_path = "path/to/your/output/folder"

# Ensure the output directory exists
os.makedirs(output_path, exist_ok=True)

# Define the data processing pipeline
pipeline = [
    ParquetReader("hf://datasets/HuggingFaceFW/fineweb/data", limit=1000),
    LambdaFilter(is_dentistry_related),
    JsonlWriter(output_path)
]

# Execute the pipeline
pipeline_executor = LocalPipelineExecutor(pipeline=pipeline, tasks=10)
pipeline_executor.run()
```



### Example 1: Reading and Filtering Dental Data
This example demonstrates how to read dental data from the FineWeb dataset, filter it based on dentistry-related keywords, and write the filtered data to a JSONL file for further analysis.

## Notebooks 📓
Our repository includes detailed Jupyter notebooks that provide walkthroughs and data processing scripts essential for leveraging the DentalDataHarvester effectively:

- **dentistry_dataset.ipynb**: A comprehensive guide to accessing and processing dental data from the FineWeb dataset.
- **technical_dental_database.ipynb**: Advanced techniques for analyzing and extracting insights from dental data.

> **Note**: Descriptions and code examples within these notebooks will be further enriched upon their review.

## Disclaimer ⚠️
The FineWeb dataset is utilized under the premise of research and educational purposes only. Please be aware that this dataset may be subject to copyright claims and could potentially be removed in the future.

## Contributing 🤝
We warmly welcome contributions to the DentalDataHarvester project. Whether you're looking to improve features, fix bugs, or enhance documentation, your input is invaluable. Join us in making this tool more robust and versatile!

## License 📄
DentalDataHarvester is made available under the MIT License. For more details, please refer to the LICENSE file in our repository.

## Contact 📬
For any queries or suggestions, feel free to reach out to the project maintainer:

- **Twitter**: [@Francisco T. Barbosa](https://twitter.com/FranciscoTBarbosa)
- **LinkedIn**: [Francisco Teixeira Barbosa](https://www.linkedin.com/in/franciscoteixeirabarbosa)
- **Email**: [cisco@periospot.com](mailto:cisco@periospot.com)

## Acknowledgements 🎉
This project is possible thanks to the tools and data provided by:

- [Hugging Face](https://huggingface.co/)
- Datatrove Library (Link to be added)
- [Jupyter Project](https://jupyter.org/)
