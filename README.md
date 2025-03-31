# Election-Bot-MA: SafeChat Instance for Massachusetts Election Domain


## 📋 Prerequisites
Before you begin, ensure you have the following installed:
- [Python](https://www.python.org/)
- [Anaconda](https://www.anaconda.com/download)


## 🚀 Getting Started
1. **Clone the repository**
   ```bash
   git clone https://github.com/vnagpal25/Election-Bot-MA.git
   cd Election-Bot-MA
   ```
2. **Create and activate a conda virtual environment**
   ```bash
   conda create --name safechat_venv python==3.8
   conda activate safechat_venv
   ```
3. **Install required packages**
   ```bash
   pip install -r requirements.txt
   ```
4. **Provide question answer pairs for your use case**

    * Create a new `data/input/<file-name>.csv` file with your desired question answer pairs or use the existing one. Your CSV should have a column called *Question* and another one called *Answer*. Optionally, if you would like for your chatbot to give traceable responses to your user, include columns *Timestamp* with [UNIX timestamps](https://www.unixtimestamp.com/) corresponding to the date of the response and *Source* with strings which may be URLs or names of the organization which procured the response.
    * Create a new `data/input/DNA.csv` that is a single column list of questions that you would like your chatbot to avoid answering. Ensure that the heading of this column is *Questions*
5. **Process your data and configure the chatbot using the RASA Open Source framework**

    * Extract the intent for user queries: `python code/extract_intent.py` By default, this will read `data/input/Chat.csv`, however, you can specify a different csv file in the `data/input` directory with the `-f` or `--file` argument:`python code/extract_intent.py -f Election_QA.csv` 
      * Saves to `data/input/Chat_intent.csv` 
    * Paraphrase all user queries: `python code/paraphraser.py`
      * Saves to `data/input/paraphrased.json`
    * Configure directory for RASA Open Source: `python code/configure_rasa.py`
      * Saves to `Chatbot` directory. Deletes existing `Chatbot` by default, so save in different location if you would like to save the configuration.
6. **Train and converse with your chatbot**

    * Navigate to chatbot directory: `cd Chatbot` 
    * Train chatbot: `rasa train`
    * Converse with trained chatbot: `rasa shell`
    * Optionally, if you would like your chatbot to handle some business-logic for some queries, you may utilize the [RASA Actions](https://rasa.com/docs/rasa/actions/)


## 📁 Project Structure
```
.
├── code/               # SafeChat logic for generating chatbot files
├── data/               # All provided and intermediate data files
├── doc/                # Documentation and design assets
└── Chatbot/            # Trained chatbot for
```
