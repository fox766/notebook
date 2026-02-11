# Ethical AI & Data

Your Information -> AI calculated Recidivism Risk Score, which creates False Positive and False Negative in Black.(racial problem)

## Is AI BETTER THAN YOU?

### First:

- Compare the preformance of ordinary peple and AI while judging some cases based on some real records, without telling them races. 
- The overall accuracy of AI and people are exactly likely. Interestingly, though humans don't know about the colors of the person, they also create false positive(predict the black to create a crime again in the follwing 2 years while they don't) and false negative(predict the white not to create a crime again while they actually do), a little better than the softerware.

### Second:

- Telling them the races, other information is the same.
- Overall accuray are exactly the same. And the situation of false positive and false negative didn't change.

## NOT RACE-BLIND? AI = RANDOM INTERNET USER?

### How does AI predict?

Example: Classifier -- Linear Seperation.

![image-20241116215624469](../assets/cs61a/image-20241116215624469.png)

LDA(Linear Discriminant Analysis) -- use some objective function

1. minimize within-class variance

![image-20241116220220966](../assets/cs61a/image-20241116220220966.png)

2. maximize across-class variance

![image-20241116220244845](../assets/cs61a/image-20241116220244845.png)

3. decide the boundary

### MAKE A ClASSIFIER OURSELVES(问题复现)

![image-20241116220825219](../assets/cs61a/image-20241116220825219.png)

Create different classifiers based on one, two or more factors to achive the best overall accuracy.

**Findings:** While using the easiest model(LDA), based on only two factors Age and Prior Crimes, we can make a classifier as acurate as the software.

### ANSWER1: PRIOR CRIMES IS A PROXY FOR RACE

### ANSWER2: PREDICTION IS SIMPLE

people's thinking acts really like a classifier.

### SO WHAT? AUTHORITATIVE

