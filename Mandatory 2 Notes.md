
* [Pipeline for token classification](https://huggingface.co/docs/transformers/en/main_classes/pipelines#natural-language-processing:~:text=to%20the%20model.-,TokenClassificationPipeline,-class%20transformers.)


# Preprocessing

## Plan

1. **Preprocess and Index:** In DataSet's \_\_init\_\_: Store sentences as lists of word tokens for later retrieval. Index sentences by index
2. **Dynamic Handling:** (In DataSet's get function)
	* **Return:** X_toks, y_toks, range
    - **Word-Token Alignment:** Retrieve original word-level ranges to track what maps where
    - **Tokenize with BERT:** Tokenize using the BERT tokenizer.
    - **Label Adjustment:** Create a new list of NER labels, adjusting 'B-' and 'I-' tags for entities that might be split during tokenization.
4. **Prediction:** Use the model to make NER predictions on the tokenized data.
5. **Reconstruction:** Evaluate predictions against the original word-level NER labels, taking into account the stored original word boundaries.