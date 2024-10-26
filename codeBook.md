# Code Book for Samsung Data Analysis Project

## Introduction
This code book describes the variables, data transformations, and the structure of the tidy dataset created from the Samsung Human Activity Recognition (HAR) dataset for this project. The goal is to prepare a dataset that is easy to analyze and provides an independent summary for each activity and each subject.

## Data Source
The dataset used for this project is the "Human Activity Recognition Using Smartphones Dataset" from the UCI Machine Learning Repository. It contains accelerometer and gyroscope measurements taken from Samsung Galaxy S smartphones, recording the activities of 30 participants.

## Steps in Data Preparation

1. **Download and Extract Data**: The dataset is downloaded and extracted into a folder named `UCI HAR Dataset`.
   
2. **Assign Data to Variables**:
   - `features`: List of all 561 features (variables) from `features.txt`.
   - `activities`: List of activities and their respective codes from `activity_labels.txt`.
   - `subject_test`: Identifiers for the test subjects (9 out of 30 participants).
   - `x_test`: Recorded feature values for test subjects.
   - `y_test`: Activity codes for the test set.
   - `subject_train`: Identifiers for the train subjects (21 out of 30 participants).
   - `x_train`: Recorded feature values for train subjects.
   - `y_train`: Activity codes for the train set.

3. **Merging Datasets**:
   - `X`: Combines `x_train` and `x_test` datasets using `rbind()` (10299 rows, 561 columns).
   - `Y`: Combines `y_train` and `y_test` datasets using `rbind()` (10299 rows, 1 column).
   - `Subject`: Combines `subject_train` and `subject_test` datasets using `rbind()` (10299 rows, 1 column).
   - `Merged_Data`: Combines `Subject`, `Y`, and `X` datasets using `cbind()` (10299 rows, 563 columns).

4. **Extracting Mean and Standard Deviation Measurements**:
   - `TidyData`: A subset of `Merged_Data` with columns for subject, activity code, and only the mean and standard deviation (std) measurements (10299 rows, 88 columns).

5. **Using Descriptive Activity Names**:
   - Replaces codes in the activity column of `TidyData` with descriptive activity names from the `activities` dataset.

6. **Labeling Data Set with Descriptive Variable Names**:
   - `code` column renamed to `activity`.
   - Abbreviations replaced to improve clarity:
     - `Acc` → `Accelerometer`
     - `Gyro` → `Gyroscope`
     - `BodyBody` → `Body`
     - `Mag` → `Magnitude`
     - `t` → `Time`
     - `f` → `Frequency`

7. **Creating a Summary Tidy Dataset**:
   - `FinalData`: Summarizes `TidyData` by calculating the mean of each variable for each activity and subject (180 rows, 88 columns).
   - Exported as `FinalData.txt`.

## Variables in FinalData

Each row in `FinalData` represents the mean values for each variable, grouped by subject and activity.

### Key Variables

1. **subject** (Integer): The identifier for each participant (values 1 to 30).
2. **activity** (Categorical): The name of the activity being performed:
   - WALKING
   - WALKING_UPSTAIRS
   - WALKING_DOWNSTAIRS
   - SITTING
   - STANDING
   - LAYING

### Feature Variables
The remaining 86 variables in `FinalData` represent mean values of measurements on the mean and standard deviation (std) for each feature. Examples include:

- **TimeBodyAccelerometer-mean()-X**: Mean of time-domain body accelerometer signal in the X direction.
- **TimeBodyAccelerometer-std()-Y**: Standard deviation of time-domain body accelerometer signal in the Y direction.
- **FrequencyBodyGyroscope-mean()-Z**: Mean of frequency-domain body gyroscope signal in the Z direction.
- **TimeBodyAccelerometerMagnitude-std()**: Standard deviation of the magnitude of time-domain body accelerometer signal.

For each variable:
- `Time` or `Frequency`: Indicates whether the measurement is in the time or frequency domain.
- `Body` or `Gravity`: Refers to signals derived from body or gravity movement.
- `Accelerometer` or `Gyroscope`: Indicates the source sensor.
- `Magnitude`: Refers to the Euclidean norm of the three-dimensional signals.
- `mean()` or `std()`: Indicates mean or standard deviation.

## Additional Notes
- All values are normalized between -1 and 1, making them unitless.
- Each row represents the mean measurement for each combination of subject and activity.


