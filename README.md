# README

## Graduate Admission Prediction

This project uses a linear regression model to predict the chances of admission for graduate school based on various features. The dataset used for this analysis is assumed to be in a file named `admissionData.csv`.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [Dataset Information](#dataset-information)
- [Data Preparation](#data-preparation)
- [Model Training and Evaluation](#model-training-and-evaluation)
- [Visualizations](#visualizations)
- [Dependencies](#dependencies)

## Installation

1. Clone the repository or download the `admissionData.csv` file.
2. Ensure you have Python installed (version 3.6 or higher).
3. Install the necessary packages using pip:
    ```bash
    pip install pandas numpy scikit-learn matplotlib seaborn
    ```

## Usage

1. Load the dataset by placing the `admissionData.csv` file in the same directory as your script.
2. Run the script to train the linear regression model and evaluate its performance.
3. View the visualizations generated by the script to understand the data and model performance better.

## Dataset Information

The dataset used in this project contains the following columns:
- `Serial No`: A unique identifier for each row.
- `GRE Score`: GRE scores (out of 340).
- `TOEFL Score`: TOEFL scores (out of 120).
- `University Rating`: University rating (out of 5).
- `SOP`: Statement of Purpose strength (out of 5).
- `LOR`: Letter of Recommendation strength (out of 5).
- `CGPA`: Undergraduate CGPA (out of 10).
- `Research`: Research experience (0 or 1).
- `Chance of Admit`: The probability of admission (ranging from 0 to 1).

## Data Preparation

1. Load the dataset:
    ```python
    admission = pd.read_csv('admissionData.csv')
    ```
2. Separate the target variable (`Chance of Admit`) and features. Drop the `Serial No` and `Chance of Admit` columns from the features:
    ```python
    y = admission['Chance of Admit ']
    X = admission.drop(['Serial No', 'Chance of Admit '], axis=1)
    ```
3. Handle missing values by removing rows with NaN:
    ```python
    mask = ~np.isnan(X).any(axis=1)
    X = X[mask]
    y = y[mask]
    ```

## Model Training and Evaluation

1. Split the data into training and testing sets (70% training, 30% testing):
    ```python
    X_train, X_test, y_train, y_test = train_test_split(X, y, train_size=0.7, random_state=2529)
    ```
2. Initialize and train the `LinearRegression` model:
    ```python
    model = LinearRegression()
    model.fit(X_train, y_train)
    ```
3. Make predictions on the test set and evaluate the model using Mean Absolute Error (MAE), Mean Absolute Percentage Error (MAPE), and Mean Squared Error (MSE):
    ```python
    y_pred = model.predict(X_test)

    mae = mean_absolute_error(y_test, y_pred)
    mape = mean_absolute_percentage_error(y_test, y_pred)
    mse = mean_squared_error(y_test, y_pred)

    print(f'Mean Absolute Error: {mae}')
    print(f'Mean Absolute Percentage Error: {mape}')
    print(f'Mean Squared Error: {mse}')
    ```

## Visualizations

1. Distribution of `Chance of Admit`:
    ```python
    plt.figure(figsize=(8, 6))
    sns.histplot(y, kde=True)
    plt.title('Distribution of Chance of Admit')
    plt.xlabel('Chance of Admit')
    plt.ylabel('Frequency')
    plt.show()
    ```
2. Correlation Matrix:
    ```python
    plt.figure(figsize=(10, 8))
    sns.heatmap(admission.corr(), annot=True, cmap='coolwarm', fmt='.2f')
    plt.title('Correlation Matrix')
    plt.show()
    ```
3. Pairplot:
    ```python
    sns.pairplot(admission.drop('Serial No', axis=1))
    plt.show()
    ```
4. Actual vs Predicted `Chance of Admit`:
    ```python
    plt.figure(figsize=(8, 6))
    plt.scatter(y_test, y_pred, alpha=0.5)
    plt.plot([0, 1], [0, 1], '--', color='red')
    plt.xlabel('Actual')
    plt.ylabel('Predicted')
    plt.title('Actual vs Predicted Chance of Admit')
    plt.show()
    ```
5. Residuals Distribution:
    ```python
    residuals = y_test - y_pred
    plt.figure(figsize=(8, 6))
    sns.histplot(residuals, kde=True)
    plt.title('Residuals Distribution')
    plt.xlabel('Residuals')
    plt.ylabel('Frequency')
    plt.show()
    ```

## Dependencies

- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn
