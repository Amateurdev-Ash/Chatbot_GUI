# Chatbot with GUI

This project implements a chatbot with a graphical user interface (GUI) built using Tkinter. The chatbot uses a machine learning model to understand user queries and provide relevant responses. It leverages natural language processing (NLP) techniques to process text and includes functionality to train the chatbot with new data, allowing users to expand its knowledge base.

## Table of Contents

*   [How it Works](#how-it-works)
*   [Code Structure](#code-structure)
    *   [ChatBot\_GUI.ipynb](#chatbot_guiipynb)
    *   [Training\_Chatbot.ipynb](#training_chatbotipynb)
    *   [Testing\_Chatbot.ipynb](#testing_chatbotipynb)
*   [Requirements](#requirements)
*   [Installation](#installation)
*   [Usage](#usage)
*   [Contributing](#contributing)

## How it Works

The chatbot's core functionality is divided into three main modules:

*   **Training:** `Training_Chatbot.ipynb` handles the training process. It uses a dataset of intents (`intents.json`) to train a neural network model. This model learns to classify user input into different intents and associate them with appropriate responses.

*   **Testing/Prediction:** `Testing_Chatbot.ipynb` is responsible for predicting the intent of a user's query. It uses the trained model to classify the input and determine the most probable intent.

*   **GUI:** `ChatBot_GUI.ipynb` creates the user interface using Tkinter. It provides a window where users can type messages and see the chatbot's responses. It also includes a "Train Bot" tab to add new training data interactively.

## Code Structure

### ChatBot\_GUI.ipynb

This file contains the code for the GUI using Tkinter. It defines the main application window, widgets (labels, entry fields, buttons, etc.), and their layout. It also handles user interactions, such as sending messages and training the bot. Key functions and classes include:

*   `ChatBot` class:
    *   Initializes the main window and sets up the GUI elements (labels, text widgets, entry fields, scrollbars, buttons).
    *   Manages communication between the GUI and the chatbot's backend (training and testing modules).
    *   `main_window()` method:  Creates the main GUI window, configures its properties (title, size, background), and adds tabs for "BotChat" and "Train Bot."
    *   `add_bot()` method:  Sets up the "BotChat" tab, including the chat display area, message input field, and send button.
    *   `add_train()` method: Creates the "Train Bot" tab with fields for adding new intents, patterns, and responses.

*   Event handling methods:
    *   `on_enter()` method:  Retrieves user input from the entry field, sends it to the `Testing` module for processing, and displays the response in the chat window.
    *   `on_train()` method: Collects new training data entered by the user in the "Train Bot" tab, updates the `intents.json` file, and re-trains the chatbot model.

*   Helper methods:
    *   `bot_response()` method: Takes a message and sender (e.g., "You" or "Bot") as input and displays the message in the chat window with appropriate formatting.
    *   `my_msg()` method:  Similar to `bot_response()`, but specifically handles displaying the user's messages in the chat window.

### Training\_Chatbot.ipynb

This file is responsible for training the chatbot's NLP model. It reads the intents from `intents.json`, preprocesses the text data (tokenization, lemmatization), and trains a neural network model. Key aspects include:

*   `Training` class:
    *   `\_\_init\_\_()` method:  Loads the intents data from `intents.json` and initializes the preprocessing steps.
    *   `process_data()` method:
        *   Extracts patterns and classes (tags) from the intents data.
        *   Tokenizes the patterns into individual words.
        *   Lemmatizes the words to their base forms (e.g., "running" to "run").
        *   Creates a vocabulary of unique words and classes.
    *   `train_data()` method:
        *   Converts text data into numerical vectors using `CountVectorizer`.
        *   Creates one-hot encoded vectors for both the input patterns and output classes.
        *   Generates training data by pairing input word vectors with corresponding output class vectors.
    *   `build()` method:
        *   Creates a sequential neural network model with dense layers and dropout for regularization.
        *   Compiles the model with an appropriate loss function, optimizer, and metrics.
        *   Trains the model on the prepared training data.
        *   Saves the trained model to `chatbot_model.keras`.
        *   Saves the vocabulary and classes data to `training_data` using `pickle`.

### Testing\_Chatbot.ipynb

This file handles the prediction and response generation of the chatbot. It loads the trained model and uses it to classify user queries. Key components include:

*   `Testing` class:
    *   `\_\_init\_\_()` method:
        *   Loads the trained model (`chatbot_model.keras`).
        *   Loads the vocabulary and classes data (`training_data`).
    *   `clean_up_sentence()` method:
        *   Tokenizes and lemmatizes the user's input sentence.
        *   Removes punctuation and special characters.
    *   `wordvector()` method:
        *   Transforms the preprocessed sentence into a numerical vector using the same `CountVectorizer` used during training.
    *   `classify()` method:
        *   Predicts the probability distribution over classes (intents) using the trained model.
        *   Filters out predictions with low probabilities (below a threshold).
        *   Returns the top predicted classes with their probabilities.
    *   `results()` method:
        *   Provides an additional layer for handling context (not fully implemented in the provided code).
    *   `response()` method:
        *   Based on the predicted class (intent), selects a random response from the corresponding intent in `intents.json`.
        *   Handles basic context management by checking for "set" and "filter" keys in the intents data.

## Requirements

*   Python 3.x
*   Tkinter
*   TensorFlow
*   NLTK
*   scikit-learn

## Installation

1.  Install the required libraries: `pip install tkinter tensorflow nltk scikit-learn`
2.  Download the `intents.json` file (if not already included).
3.  Run `Training_Chatbot.ipynb` to train the model (or use a pre-trained model).
4.  Run `ChatBot_GUI.ipynb` to launch the chatbot interface.

## Usage

1.  Type your message in the input field of the GUI.
2.  Press Enter or click the "Send" button.
3.  The chatbot will respond based on its training data.
4.  Use the "Train Bot" tab in the GUI to add new training data.

## Contributing

Contributions are welcome! Feel free to open issues or pull requests.
