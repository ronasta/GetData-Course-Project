GetData-Course-Project
======================

The project description is given in **documentation/instructions.pdf**  

**UCI_HAR.txt** is the submitted result data set. It's CodeBook is the file
**UCI_HAR_CodeBook.md** (generated by `knitr` from **UCI_HAR_CodeBook.Rmd**)


### Documentation of run_analysis.R

#### getting the data

The "UCI HAR Dataset" is downloaded and extracted into the `downloaded_data` directory. This step is executed only if the dataset has not already been downloaded. To force the execution, remove the directory.

#### prepare for X_data column extracting and labeling

* **notes:**  
    This prepares for steps 2 and 3 of the *documentation/instructions.pdf*.  
    The idea is to select only desired columns and attach meaningful column names
    **while reading in** the feature vectors from the X_... files. There is a discussion 
    in the forum about [what mean() and std() to use](https://class.coursera.org/getdata-016/forum/thread?thread_id=50#post-110). I therefore choose to include only features **ending** with 
    *mean()-[XYZ]* or *std()-[XYZ]*.   

Create the table `features` from the code-book *"features.txt"*. Attach a column
*"class"*, specifying for each feature "NULL" for not wanted columns or "numeric" 
for columns with feature labels **ending with *mean()* or *std()***.

#### define function read_data(type)

Following the DRY principle ("Don't Repeat Yourself"), a function is defined to read in the *test* and *train* data. It performs the following steps:  

- define the directory and filenames according to the `type` parameter (*test* or *train*)
- read and join the X_, Y_ and Subject_ files into the `DT` data table.  
  For reading the X_ files, use the `features` table (see above) to select and name columns.
- return the data table `DT`

#### read and merge the test and train datasets

- `TEST <- read_data("test")`
- `TRAIN <- read_data("train")`
- merge these two into data table `DATA`

#### calculate the averages and write the file to be submitted



