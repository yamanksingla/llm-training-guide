# llm-training-guide

Source: https://www.philschmid.de/deploy-gptj-sagemaker

In Transformers the models loaded with the from_pretrained method are following PyTorch's [recommended practice](https://pytorch.org/tutorials/beginner/saving_loading_models.html#save-load-state-dict-recommended), which takes around 1.97 seconds for BERT [REF](https://colab.research.google.com/drive/1-Y5f8PWS8ksoaf1A2qI94jq0GxF2pqQ6?usp=sharing). PyTorch offers an additional alternative way of saving and loading models using [torch.save(model, PATH) and torch.load(PATH)](https://pytorch.org/tutorials/beginner/saving_loading_models.html#save-load-entire-model).


Saving a model in this way will save the entire module using Python’s pickle module. The disadvantage of this approach is that the serialized data is bound to the specific classes and the exact directory structure used when the model is saved. This means that when we save a model with transformers==4.13.2 it could be potentially incompatible when trying to load with transformers==4.15.0. However, loading models this way reduces the loading time by ~12x, down to 0.166s for BERT.



As per Somesh, for effective instruction finetuning, the SFT dataset should include a few samples from the Pretraining corpus as well.
