# do not public this file:

personal use only- not to be shared

# Question

Consider the following dataset that is to be clustered using the k-means algorithm with **k=3** and the **Farthest Centers heuristic** (the seven dataset elements are 1-dimensional, just numbers):

**2, 4, 6, 12, 14, 20, 22**

Let the randomly selected first center be **2**.

1. Which will be the **second** center using the Farthest Distance Heuristic?
    1. 2
2. Which will be the **third** center using the Farthest Distance Heuristic?
    1. 12 
    2. ( 12 and 14 have similar average Euclidean distance from 2 and 22. you could say that it’s randomly chosen based on that. I chose 12 because it’s also one that you would choose irregardless of point value by distance in the data set its self)
3. What are the three clusters for these initial centers? (List the points in each cluster).
    1. 2,4,6
    2. 12,14
    3. 20,22
4. Will the k-means algorithm terminate after this first iteration or will it continue? Answer in 1-2 sentences.
    1. there should be a first and second iteration. The first iteration used the initial values, than they are recalculated with the clusters centers being 4, 13, and 21 respective. Once these means have been evaluated, the algorithm ends, as the centers have finished converging to their attractors. 

# Question

Evaluation metrics
A classifier is a method to assign one of a few labels to a data instance. You are to evaluate the following classifier to distinguish between Setosa and Versicolor species:

"Any flower with Sepal.Length < 5 is Setosa, else it is Versicolor"

The test dataset is below:

Sepal.Length	Species
+ 4.4	Setosa
+ 4.6	Setosa
+ 4.8	Setosa
+ 4.9	Setosa
- 4.9	Versicolor 

**←——————→**
- 5.1	Setosa
- 5.2	Setosa
+ 5.3	Versicolor
+ 5.6	Versicolor
+ 5.8	Versicolor

---

For the given classifier, what is its:

1. Accuracy
    1. 7/10 (or 70%) 
2. Error rate
    1. 3/10 (or 30%)
3. Precision (of identifying Setosa)
    1. t ps/ truepos + false pos ⇒ 4/(4+1) ⇒  = 4/5
4. Recall (of identifying Setosa)
    1. true pos/ truepos+false neg ⇒  4/(4+2) = 4/6 ⇒ 2/3 
5. F1-score (of identifying Setosa)
    1. 2( (prec*recall) / (prec+recall) )
    2. 2 * (( (4/5) * (2/3) ) / ((4/5) + (2/3)))
    3. 0.72727272727……

# Question

Dynamic Time Warping

Compute the Dynamic Time Warping distance between the two time series:

- X = [0, 2, 4, 6]
- Y = [1, 4, 5, 6]

Let the cost function be cost(xi,yj )=(xi -yj)2

a) Show the cost matrix

$	1	4	5	6
0	1	16	25	36
2	1	4	9	16
4	9	0	1	4
6	25	4	1	0

b) Show the DTW matrix

1	17	42	78
2	5	14	30
11	2	3	7
36	6	3	3

c) The DTW distance between X and Y is: _____

3

d) What is an optimal alignment between the points in the two time series (i.e., x1 is matched to y?, x2 is matched to y?, ...)?

((0,1),(2,1),(4,4),(6,5)(,6,6))

# Question

Text analysis
Consider the following three short documents:

```
Document 1: warm summer breeze

Document 2: warm summer nights

Document 3: cool breeze

```

1. Show the Document-Term matrix weighted by normalized Term-frequency (Tf) for this dataset.
    1. 
        
        $	        doc1	doc2	doc3
        warm	1/3	        1/3	        0
        summer	1/3	        1/3 	        0
        breeze	1/3	        0	        1/2
        nights	0	        1/3	        0
        cool	        0	         0	        1/2
        
2. What is the inverse document frequency (idf) of each word?
    1. warm——- log(3/2) → 0.4054651
    2. summer—- log(3/2) → 0.4054651
    3. breeze—— log(3/2) → 0.4054651
    4. nights——- log(3/1) → 1.098612
    5. cool———- log(3/1) → 1.098612
3. Show the Document-Term matrix weighted by Tf-idf for this dataset.
    1. 
    
    $	        doc1	doc2	doc3
    warm	6/20	        6/20	       0
    summer	6/20	        6/20	        0
    breeze	6/20	        0	        6/19
    nights	0	        1/14	        0
    cool	        0	         0	        1/13
    
4. Which pair of documents is the most similar to each other? Why (show computations)?
    1. cos_sim()
    
    > cos_sim <- function(x, y) {sum(x*y)/sqrt(sum(x^2)*sum(y^2))}
    
    > doc1 = c(6/20,6/20,6/20,0,0)
    doc2 = c(6/20,6/20,0,1/14,0)
    doc3 = c(0,0,6/19,0,1/13)
    cos_sim(doc1,doc2)
    [1] 0.8051652
    cos_sim(doc1,doc3)
    [1] 0.5609479
    cos_sim(doc2,doc3)
    [1] 0
    >