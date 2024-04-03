# Document Layout Extracting and Parsing to extract entities

**Problem Statement**: Using NER on text extracted from a document through OCR does not take layout into consideration, which actually holds vital information 
to correctly detect entities. A process which combines the layout knowledge as well as OCR is promising in this aspect.

## In this Repo

- `layouttest.ipynb` contains the code to load, finetune, and generate inferences with LayoutLMV3 model
- `test/` contains the fintuned model


## Tools

### OCR
- Tesseract (Google, open source) : most robust open source OCR
- EasyOCR (open source) : sometimes faster than Tesseract

### Layout Detection
- LayoutLMV (Meta, open source): 

### End-to-end
- DocumentAI (Google, prop.) : prop. product for a variety of document pipelines like NER, question answering. 

### Other relevant tools
- pdfplumber (parsing scanned pdf to extract info about each character, graphic, table)


## LayoutLMV3

- Base model can be finetuned with 100-500 (1000 recommended) documents to get good results
- Fine tuning on FUNSD (Form Understanding in Noisy Scanned Documents) on Ryzen 5 3400G, 16 GB, RTX 4060 6GB:
    - ```{'train_runtime': 616.7343, 'train_samples_per_second': 3.243, 'train_steps_per_second': 1.621, 'train_loss': 0.32155079650878904, 'epoch': 13.33}```
    - ```{'eval_loss': 0.7001778483390808,'eval_precision': 0.8904968644476604,'eval_recall': 0.9170392449080974,'eval_f1': 0.90357317670093,'eval_accuracy': 0.849875193153453,'eval_runtime': 3.8124,'eval_samples_per_second': 13.115,'eval_steps_per_second': 6.557,'epoch': 13.33}```
- Custom data must have bounding boxes and labels. OCR not required, can be handled by the processor

