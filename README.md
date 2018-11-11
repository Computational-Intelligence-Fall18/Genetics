
# Genetics
In this assignment, you will implement main parts of genetic algorithms. <br>
There is a lot of algorithms researchers use in each part and your are going to implement the famous ones. And of course there are some rare ideas to implement here(we have to grade your work by hard things)!
<br><br>

### Implementations
1. First of all, you should implement anything **only using numpy or built-in libraries**.
2. You should implement **just functions** to do the task for each module. This means, you have to assume some predefined code and you implementd your code with respect to that.
3. You can define subfunctions for simplifing your task.
3. We provided a **sample class of chromosome** with some attributes. You can imagine this class will be parsed as chromosome in your functions. 
4. In some of modules, **you need to change the class** to add some new attribute. To do so, you should **extend class and add new attributes** to your new implemented class.

### Grading
1. **Modules have weighted grades** so more work more points.
2. **Some modules are optional for some groups**.
3. **Groups are categorized based on theirs skills**. So more skills more tasks and different points for each tasks.
4. (optional) **Unit testing** has bonus points. If you use online CI tools like Travis CI or Azure Devops for testing, you will have more bonus points!!!

Note: If you want to use unit testing in your codes, please provide high quality tests. writing low quality tests is just wasting time (Go play GTA instead!)

### Documentation
1. For god's sake write something! maybe someday you have to use your own work(hopefully).
2. You have to provide documentation for all of function **arguments** and **return value** and of course a **simple explanation about your function** and a **numerical example** how would your function work.
3. You don't know how to write docs in python? ok go google it!

This <a href='https://realpython.com/documenting-python-code/'>tutorial</a> may help you to write better docs.

### Modules
1. For each section, we provided some modules.
2. Each **module will be a function** as described in <a href='#Implementaitons'>implementation</a> section.
3. There is a **little description** what is this module and some **links as reference**. You must read those links and implement modules based on algorithms provided in the reference. In some modules, we provided **a paper corresponding to module**. It is your task to **study paper and find out how to implement**. 

## Genetics
This assignment include these parts:
1. Initialization (Population and Chromosome)
2. Selection Methods
3. Crossover Methods
4. Mutation Methods

We will describe each section

## Initialization
In this step we talk about initializing chromosome and population.
So here is the contents:
1. Chromosome
2. Population

### Chromosome
Here we assume every problem can be encoded to chromosomes with a 1 dimensional vector genes.<br>
But the structure of this genes depends on the probelm. We assume most famous ones here so we have 3 type of gene vector:
1. A binary vector which 1 represent existance of gene and 0 represents non-existance.<br>
Numeric example: <br>
```python
genes = [0, 1, 0, 0, 0, 1, ... , 0]
print(chromosome.genes)
output: [0, 1, 0, 0, 0, 1, ... , 0]
```

2. A integer vector of vectors which each elemnt represent a vecotr of the batch of genes with same size. something like a flatten 2 dimensional matrix. <br>
```python
genes = [
    [1,2,3],
    [2,1,3],
    [3,2,1],
    [3,1,2]
        ]
chromosome.genes = genes.flatten()
print(chromosome.genes)
output: [1,2,3,2,1,3,3,2,1,3,1,2]
```

3. a integer vecotr of vectors like state 2, but each element has different size. So this is your duty to think about best encoding way of this.
```python
genes = [
    [1,2,3,4,5],
    [3,2,1],
    [2,3,1,4],
    [1]
        ]
chromosome.genes = genes.flatten()
print(chromosome.genes)
output: [1,2,3,4,5,3,2,1,2,3,1,4,1]
```
but as you, `lengths` is important. So we add another attribute to the `chromosome` class. <br>
```python
chromosome.lengths = [5,3,4,1]
```
So every time you want to apply any operation on these features, you have to do it with respect to `lengths`.<br>

**Note: These numbers are just for demonestration purposes and in real world example, they are data points (features).**

We provided a class represents a simple chromosome. You need to complete all function with respect to this class.


```python
import numpy as np
```


```python
class chromosome():
    def __init__(self, genes, id=None, fitness=-1, flatten= False, lengths=None):
        self.id = id
        self.genes = genes
        self.fitness = fitness
        
        # if you need more parameters for specific problem, extend this class
    def flatten_feaures():
        # in this function you should implement your logic to flatten features
        pass
    
    
    def describe(self):
        print('ID=#{}, fitenss={}, \ngenes=\n{}'.format(self.id, self.fitness, self.genes))
```


```python
c = chromosome(genes=np.array([1,2,3]),id=1,fitness = 125.2)
c.describe()

c2 = chromosome(genes = np.array([[1,2],[2,1]]).flatten(), id=2,
                fitness=140, flatten=True)
c2.describe()
```

    ID=#1, fitenss=125.2, 
    genes=
    [1 2 3]
    ID=#2, fitenss=140, 
    genes=
    [1 2 2 1]
    

### Population
Population is the chromosomes as friends and enemies. So all operators in mutation and crossover will be applied on these chromosomes based on nature selection idea and survival the fittest.<br><br>
Initialization can help to find global optima faster or even stuck in local optima. So it is an important part.<br>
There are some methods to initialize population and it's hyperparameters.<br>
**Hyperparameters** are:
1. **Population Size**
2. **Chromosome Genes**

The most famous one is random initialization.<br>

**Population** initialization:
1. **Pseudo Random**
2. **Quasi Random Sequence**
3. **Centroid Voronoi Tessellation**

#### Psuedo Random
This is the simplest method. Actually the `random` class in every programming language is a psuedo random number. And of course make a uniform random using this psuedo randoms.<br>
So in you implementation, you must use `numpy.random` to initialize population and chromosomes.<br>
Just do everything random! If you need more information, check <a href='#More-Reading'>more reading</a> section below.

#### Quasi Random Sequence
the initial population is often selected randomly using <a href='#Psuedo-Random'> pseudorandom</a> numbers. Usually, however, it is more important that the points are as **evenly distributed** as possible than that they imitate random points. In this paper, we study the use of quasi-random sequences in the initial population of a genetic algorithm. Sample points in a **quasi-random sequence are designed to have good distribution properties**.<br><br>
Use this <a href='https://1drv.ms/b/s!ApJ0ieVzUhjim0dcxwiJU3EQDvOO'>link</a> as reference.
<br>

#### Centroid Voronoi Tessellation
In this method, we assume data points as clusters and separate them based on some criteria. And then initialize random points with respect to these regions.<br><br>
Use this <a href='https://1drv.ms/b/s!ApJ0ieVzUhjim0jXmkr282tF4Qrv'>paper</a> as reference.<br>

##### More Reading
If you need to more about random numbers, <a href='https://pdfs.semanticscholar.org/c307/20efa68a530a25c02213ea099c74cbc8d2bb.pdf'>this</a> and <a href='https://1drv.ms/b/s!ApJ0ieVzUhjim0YSjH7n78lISHOZ'>this</a> about different methods.

## Selection
The idea of selection phase is to select the fittest individuals and let them pass their genes to the next generation.

These are your tasks:

1. **Truncation Selection**
2. **Tournament Selection**
3. **Stockasting Universal Sampling**
4. **Roulette Wheel Selection**
5. **Roulette Wheel Selection with Stocastic Acceptance**
6. **Linear Ranking Selection**
7. **Exponential Ranking Selection**
8. **Self-Adaptive Tournament Selection**

### 1. Truncation Selection
Use <a href='https://1drv.ms/b/s!ApJ0ieVzUhjimzd5SFGoAOyO7N1x'>This</a> as reference.<br>
More reading:
<a href='http://www.muehlenbein.org/breeder93.pdf'>Muhlenbein's Breeder Genetic Algorithm</a>.

### 2. Tournament Selection
Use <a href='https://1drv.ms/b/s!ApJ0ieVzUhjimzgexRonyUszQgZQ'>this</a> as reference.

### 3. Stockasting Universal Sampling
Use <a href='https://1drv.ms/b/s!ApJ0ieVzUhjimz4N8jF3YOuiZRB3'>this</a> as reference.

### 4. Roulette-wheel Selection
Use <a href='https://1drv.ms/b/s!ApJ0ieVzUhjimz-rnk7Msm7BKOMK'>this</a> as reference.

### 5. Roulette-wheel Selection with Stocastic Acceptance
Use <a href='https://1drv.ms/b/s!ApJ0ieVzUhjimz-rnk7Msm7BKOMK'>this</a> as reference.

### 6. Linear Ranking Selection
Use <a href='https://1drv.ms/b/s!ApJ0ieVzUhjimzbRG8A17Ycg2udK'>this</a> and <a href='https://1drv.ms/b/s!ApJ0ieVzUhjimzmCZk6isS3EFksH'>this</a> as reference.

### 7. Exponential Ranking Selection
Use <a href='https://1drv.ms/b/s!ApJ0ieVzUhjimzpfBTPATw3e9ccF'>this</a> and <a href='https://1drv.ms/b/s!ApJ0ieVzUhjimzu8TjpgpnGhJ5mc'>this</a> as reference.

### 8. Self-Adaptive Tournament Selection
Use <a href='https://1drv.ms/b/s!ApJ0ieVzUhjim0HgkHNKMrSe87s_'>this</a> as reference.

#### More readings
1. https://1drv.ms/b/s!ApJ0ieVzUhjim0AVEP9zJ-irxfVN
2. http://www.geatbx.com/docu/algindex-02.html

## Crossover
The idea is to have better individuals at next generations. So we have to do something. Here we try to use top indviduals offsprings for next generations as parents. This help us exploit.

Here is some of crossover operators:
1. **Single-point Crossover**
2. **Multi-point Crossover (N-point)**
3. **Uniform Crossover**
4. **Flat Crossover**
5. **Order Crossover (OX)**
6. **Partially Mapped Crossover(PMX)**
7. **Edge Recombination Crossover (ERX)**
8. **Cycle Crossover (CX)**
9. **Alternating Edges Crossover (AEX)**

**Note: You must implement each operator for 3 type of chromosome class**. (See <a href='#Population'>Initialization</a> section).

Reference:
1. For 1 to 4 oeprators, use <a herf='https://1drv.ms/b/s!ApJ0ieVzUhjim0zBWnOATxVrK5oC'>this</a> link.
2. For 5 to 9 operators use <a href='https://1drv.ms/b/s!ApJ0ieVzUhjim0tAfWp7OZVebBaO'>this</a> link.

### 1. Single-Point crossover

### 2. Multi-point Crossover (N-point)

### 3. Uniform Crossover

### 4. Flat Crossover

### 5. Order Crossover (OX)

### 6. Partially Mapped Crossover(PMX)

### 7. Edge Recombination Crossover (ERX)

### 8. Cycle Crossover (CX)

### 9. Alternating Edges Crossover (AEX)

## Mutation
The idea of mutation phase is to change the values of genes in a chromosome randomly and introduce new genetic material into
the population, thereby increasing genetic diversity.

These are your tasks:

1. **Uniform/Random Mutation**
2. **Inorder Mutation**
3. **Twors Mutation**
4. **Centre inverse mutation (CIM)**
5. **Reverse Sequence Mutation (RSM)**
6. **Throas Mutation**
7. **Thrors Mutation**
8. **Partial Shuffle Mutation (PSM)**
9. **Reversal mutation**
10. **Distance-Based Mutation Operator (DMO)**
11. **gaussian mutation**
12. **Swap Mutation**
13. **Scramble Mutation**

Here is a reference for 9/13 of these operators <a href='https://1drv.ms/b/s!ArsLn8kTdaA1ig9o9boJtvw6HgAY'>here</a>.

### 1. Uniform/Random Mutation

### 2. Inorder Mutation

### 3. Twors Mutation

### 4. Centre Inverse Mutation (CIM)


### 5. Reverse Sequence Mutation (RSM)

### 6. Throas Mutation

### 7. Thrors Mutation

### 8. Partial Shuffle Mutation (PSM)

### 9. Reversal mutation

### 10. Distance-Based Mutation Operator (DMO)
You can get paper <a href='https://1drv.ms/b/s!ArsLn8kTdaA1ihAJX4daLOPEdEpZ'>here</a>.

### 11. Gaussian Mutation

### 12. Swap Mutation
Use <a href='https://www.tutorialspoint.com/genetic_algorithms/genetic_algorithms_mutation.htm'>this</a> as reference.

### 13. Scramble Mutation
Same reference as above.


# License
MIT License

Copyright (c) 2018 Computational Intelligence - University of Guilan

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
Contact <a href='nikronic.github.io'>Author</a>
