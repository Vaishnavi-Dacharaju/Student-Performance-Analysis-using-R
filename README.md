# Student-Performance-Analysis-using-R
A data analytics project using R to analyze student performance data, exploring the impact of socio-demographic factors, study habits, and behavioral attributes on academic outcomes through data preprocessing, visualization, and statistical analysis.
# Load necessary libraries
library(dplyr)
library(ggplot2)
install.packages("dplyr")
library(dplyr)
# Load the dataset
student_data <- read.csv("C:/Users/vaish/Downloads/student-por.csv")
# Show the structure of the dataset
str(student_data)
# Summary statistics
summary(student_data)
# Show the first few rows of the dataset
head(student_data)
# Histograms for numeric variables
hist(student_data$age)
hist(student_data$absences)
# Boxplot example
boxplot(student_data$G1, main="Boxplot of G1 Grades")
# Check for missing values
colSums(is.na(student_data))
# Normalize numeric variables (optional based on your analysis needs)
student_data$age <- scale(student_data$age)
student_data$absences <- scale(student_data$absences)
# Install and load necessary library
install.packages("arules")
library(arules)
# Convert to transactions format (example with dummy data)
trans <- as(head(student_data), "transactions")
# Find association rules
rules <- apriori(trans, parameter=list(support=0.1, confidence=0.5))
# Install and load necessary packages
install.packages("dplyr")
install.packages("arules")

library(dplyr)
library(arules)

# Load the dataset
student_data <- read.csv("C:/Users/vaish/Downloads/student-por.csv")

# Check for missing values (if needed)
colSums(is.na(student_data))

# Normalize numeric variables (if needed)
student_data$age <- scale(student_data$age)
student_data$absences <- scale(student_data$absences)

# Convert data to transactions
trans <- as(split(student_data, seq(nrow(student_data))), "transactions")

# Find association rules
rules <- apriori(trans, parameter=list(support=0.1, confidence=0.5))

# Show rules
inspect(rules)


# Convert data to transactions format
trans <- as(student_data, "transactions")

# Create a list of transactions
trans <- as(split(student_data, seq(nrow(student_data))), "transactions")

# Inspect the transactions (optional step to verify)
inspect(trans)

# Convert data to transactions format
trans <- as(as.matrix(student_data), "transactions")


# Install and load necessary library
install.packages("rpart")
library(rpart)

# Build decision tree
tree_model <- rpart(G3 ~ ., data=student_data, method="anova")

# Predict using the model
predictions <- predict(tree_model, newdata=student_data, type="response")

# Show confusion matrix (example of evaluation)
table(predictions, student_data$G3)

