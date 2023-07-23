# Legal-Document-Summarization
# Deep Learning Approach

The main objective of the project is to develop a system that can automatically summarize lengthy legal documents into concise and meaningful summaries. Our model is also capable of generating aspect based summaries. This will save time and effort for legal professionals and researchers who need to quickly grasp the key points of complex legal cases. This summarizer particularly aims to build a model that can perform well for Indian legal documents.

Structure of our directory:
 
    Root directory
    | - README.md
    | - dataset
        | - test-data
            | - judgement
                | - (contains set of files storing judgements)
            | - summary
                | - (contains set of files storing summaries of the (corresponding judgement - based on filename))
        | - train-data
            | - judgement
                | - (contains set of files storing judgements)
            | - summary
                | - (contains set of files storing judgements)
        | - csvdataset.zip
            1. This zip folder contains judge.csv and sum.csv where dataset is converted into csv file with one column as filename with which it was stored and the other with the corresponding judgement/summary
    | - analysis
        | - analysis.xlsx
            1. Excel file that stores various columns(filename, judgement, summary, freq of words, freq of nouns in judgement, etc)
        | - train_data_analysis.ipynb
            1. File that creates analysis.xlsx
            2. This also generates some most freq used words in the whole dataset after removing legal stopwords
            3. Also identifies various abbreviation used in our judegements thus helps in creating our abbreviation mapping.
    | - preprocessing.ipynb
        This file basically does all preprocessing in our judgements
        1. Deletes english-stopwords as well as legal-stopwords from our dataset
        2. Deletes various punctuation marks.
        3. converts each letter into it's lowercase.
        4. We tokenize each judgement and summary into sentences and removed those sentences whose len<50 as those sentences generally doesnt add any value to summary.
        5. We store all the list of sentences(each list denotes one judgement) into another list
        6. jgslist_latest.pickle store our final judgements(list of list of strings)
        7. sumlist_new.pickle store our final summaries(list of list of sentence)
        8. Then we store these files into 'intermediate' directory
    | - sentence_similarity_bert
        | - sentence_similarity_bert.ipynb
            1. This stores all the vector embeddings generated using bert in '..\intermediate'
            2. Also finds the score of each sentences using cosine similarity -> stores this scores(list of list of float) as pickle file in '..\intermediate' as scores_bert.pickle
    | - sentence_similarity_infer_glove
        | - sentence_similarity_inferglove.ipynb
            1. This stores all the vector embeddings generated using InferSent and GloVe model combined in '..\intermediate'
            2. By combining InferSent and GloVe model we mean concatenating vectors formed by both of these models, and thus in this way we get the benefit of both of these models.
            3. Also finds the score of each sentences using cosine similarity -> stores this scores(list of list of float) as pickle file in '..\intermediate' as scores_bert.pickle
