## **Introduction to project:**  

### Reading CSV file:  
There are different ways to read data. Depending on your work environment you can read it from local drive or from google drive (if you upload data to your drive).  

**1. Reading from local drive.**  
All you need to do is to know path to the file, and then you can use pandas function as in example below.  
```python
import pandas as pd
path = r"C:\Users\Example_path\Example_data.csv"
DF = pd.read_csv(path)
```
**2. Reading from google drive.**  
If you have enough space on google drive you can upload your dataset and then connect google drive to colab. To do so you need to exacute the following commands.  
```python
from google.colab import drive
drive.mount('/content/drive')
```
Now you can access your csv file. Let's say that it was uploaded to folder "Project". Then you access it by executing the following.  
```python
import pandas as pd
DF = pd.read_csv("/content/drive/MyDrive/Project/Example_data.csv") # The '/content/drive/MyDrive/' part will be the same in most ways.
```
### Data analysis
*To be added soon*

### Shuffle and split data   
We can use build in sklearn function to easily split into test and train sets. If we execute it twice, function will split set into train, test and validation. I have also added "fraction" parameter, so we can easily use only some percentage of data (see in function below).  
Load the function:  
```python
def shuffle_and_split_dataframe(dataframe, train_ratio=0.70, validation_ratio=0.15, test_ratio=0.15, fraction=1.0):
    from sklearn.model_selection import train_test_split
    """Shuffles and splits a DataFrame into train, validation, and test sets.

    Args:
    dataframe: The DataFrame to be shuffled and split.
    train_ratio: The proportion of the DataFrame to include in the train set.
    validation_ratio: The proportion of the DataFrame to include in the validation set.
    test_ratio: The proportion of the DataFrame to include in the test set.
    fraction: The fraction of dataset that will be used, by default 1.0 (100%)

    Returns:
    A tuple of three DataFrames, representing the train, validation, and test sets.
    """

    # Shuffle the DataFrame.
    dataframe = dataframe.sample(frac=fraction)

    train_set, test_set = train_test_split(dataframe, test_size=(1 - train_ratio))
    validation_set, test_set = train_test_split(test_set, test_size = test_ratio/(test_ratio + validation_ratio) ) 
    
    # Return the train, validation, and test sets.
    return train_set, validation_set, test_set
```
And then just execute it
```python
train_set, validation_set, test_set = shuffle_and_split_dataframe(DF)
```
