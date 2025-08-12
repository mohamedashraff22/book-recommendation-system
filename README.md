# Book Recommender

## Overview
The **Book Recommender** is a Python-based application designed to provide book recommendations using semantic similarity search. It utilizes a dataset of approximately 7,000 books with metadata, sourced from Kaggle, to suggest books based on user queries (e.g., "A book about history" or "A book to teach children about nature"). The project is implemented as a Jupyter Notebook (`Book_recommender.ipynb`) and employs NLP techniques with vector embeddings to match queries to book descriptions, offering recommendations via a Gradio interface.

<img width="1919" height="891" alt="image" src="https://github.com/user-attachments/assets/ff87e2a4-05c6-420a-bc20-c73dce20f125" />

<img width="1914" height="870" alt="image" src="https://github.com/user-attachments/assets/77b61572-f005-407d-a8a5-92a46fd906f2" />

## Features
- **Semantic Search**: Recommends books by comparing user queries to book descriptions using embeddings from the `sentence-transformers/all-MiniLM-L6-v2` model.
- **Dataset**: Uses the [7k-books-with-metadata](https://www.kaggle.com/datasets/dylanjcastillo/7k-books-with-metadata) dataset, including details like title, authors, average rating, number of pages, publication year, categories, and descriptions.
- **Data Exploration**: Includes visualizations for analysis, such as histograms, boxplots, and correlation matrices, embedded in the notebook.
- **Persistent Vector Database**: Stores book embeddings in a Chroma vector database (`chroma_db_books`) for efficient retrieval and reuse.
- **Interactive Interface**: Features a Gradio-based web interface for users to input queries and view recommendations in a tabular format.

## Prerequisites
To run this project, ensure you have the following:
- **Python**: Version 3.8 or higher.
- **Jupyter Notebook**: For running the `Book_recommender.ipynb` file.
- **Kaggle API Key**: A `kaggle.json` file with your Kaggle API credentials (downloadable from your Kaggle account settings).
- **Dependencies**: Install required Python libraries by running:
  ```bash
  pip install -r requirements.txt
  ```

## Installation
1. **Clone the Repository** (if applicable):
   ```bash
   git clone <repository-url>
   cd book-recommender
   ```

2. **Set Up Kaggle API**:
   - Upload your `kaggle.json` file to the project directory or follow the notebook instructions to upload it via Google Colab.
   - Configure the Kaggle API by running the commands in the notebook.

3. **Download the Dataset**:
   - Download the dataset from Kaggle using the notebook's Kaggle API commands.
   - Unzip the dataset as instructed in the notebook.

4. **Install Dependencies**:
   - Install the required Python libraries using the provided `requirements.txt`:
     ```bash
     pip install -r requirements.txt
     ```

## Usage
1. **Run the Jupyter Notebook**:
   - Open `Book_recommender.ipynb` in Jupyter Notebook or an equivalent environment.
   - Execute the cells to:
     - Load and clean the dataset (removing the `subtitle` column and rows with missing descriptions).
     - Create a tagged description file (`tagged_description.txt`) combining ISBN13 and book descriptions.
     - Build or load a Chroma vector database.
     - Launch the Gradio interface for interactive recommendations.
   - Follow the notebook's instructions to run each section.

2. **Interact with the Gradio Interface**:
   - Once the Gradio interface launches (via the notebook), enter a query in the text box (e.g., "A book about history").
   - View the recommended books in a table displaying title, authors, average rating, number of pages, publication year, categories, and description.

3. **Data Exploration** (Optional):
   - The notebook includes exploratory data analysis (EDA) with visualizations such as:
     - Histogram of average ratings.
     - Boxplot of page counts.
     - Bar plot of top genres.
     - Scatter plot of ratings vs. page counts.
     - Line plot of average ratings over publication years.
     - Correlation matrix of numeric features.
   - Run the relevant cells to view these visualizations.

## Project Structure
```
BOOK RECOMMENDATION SYSTEM/
├── chroma_db_books/        # Directory for persistent Chroma vector database
├── .gitignore              # Git ignore file
├── Book_recommender.ipynb  # Main Jupyter Notebook
├── LICENSE                 # License file
├── requirements.txt        # List of Python dependencies
└── tagged_description.txt  # Generated file with ISBN13 and descriptions
```

## How It Works
1. **Data Preparation**:
   - Loads the `books.csv` dataset using pandas.
   - Cleans the data by dropping the `subtitle` column and removing rows with missing descriptions.
   - Combines ISBN13 and descriptions into a `tagged_description` column, saved as a text file.

2. **Vector Database**:
   - Uses `langchain` to load the tagged descriptions and split them into documents.
   - Generates embeddings using the `sentence-transformers/all-MiniLM-L6-v2` model.
   - Stores embeddings in a Chroma vector database, persisted in the `chroma_db_books` directory.

3. **Recommendation System**:
   - The `retrieve_semantic_recommendations` function performs a similarity search on the vector database based on user queries.
   - Returns a pandas DataFrame with the top matching books (default: 10), including relevant metadata.

4. **Gradio Interface**:
   - Provides a web-based interface within the notebook for users to input queries and view recommendations.

## Example Queries
- "A book about history"
- "A book to teach children about nature"
- "A science fiction novel with strong female characters"
- "A mystery book set in the 19th century"

## Limitations
- The dataset is limited to ~7,000 books, potentially missing some genres or recent publications.
- Recommendation quality depends on the descriptiveness of book descriptions.
- The application runs locally or in a Colab environment; public hosting requires additional setup.
- The Chroma database is stored locally, requiring sufficient disk space.

## Future Improvements
- Expand the dataset with more books or additional metadata.
- Fine-tune the embedding model for better semantic matching.
- Add filters for recommendations (e.g., by genre or rating).
- Deploy the Gradio interface on a public server.
- Incorporate user feedback for dynamic recommendations.

## Contributing
Contributions are welcome! To contribute:
1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Make your changes and commit (`git commit -m "Add feature"`).
4. Push to the branch (`git push origin feature-branch`).
5. Open a pull request.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments
- Dataset: [7k-books-with-metadata](https://www.kaggle.com/datasets/dylanjcastillo/7k-books-with-metadata) by Dylan J. Castillo.
- Libraries: `pandas`, `langchain`, `sentence-transformers`, `gradio`, `chromadb`, and others.
