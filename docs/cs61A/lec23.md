# Decomposition

## Modular Design

### Separation of Concerns

A design principle: Isolate different parts of a program that address different concerns

A modular component can be developed and tested independently

![image-20240915200003045](../assets/cs61a/image-20240915200003045.png)

The different parts of the code should know little about others as possible

## Example: Restaurant Search

![image-20240915200457688](../assets/cs61a/image-20240915200457688.png)

```python
def search(query, ranking=lambda r: -r.stars):
    results = [r for r in all_restaurants if query in r.name]
    return sorted(results, key=ranking)

class Restaurant:
    all = []
    def __init__(self, name, stars):
        self.name, self.starts = name, stars
        Restaurant.all.append(self)
        
    def similar(self, k):
        """Return the K most similar restaurants to SELF."""
        ...
    
    def __repr__(self):
        return '<' + self.name + '>'
        
Restaurant('Thai Delight', 2)
Restaurant('Thai Basil', 3)
Restaurant('Top Dog', 5)


results = search('Thai')
for r in results:
    print(r, 'is similar to', r,similar(3))
```

### implementing SIMILAR:

![image-20240915201653227](../assets/cs61a/image-20240915201653227.png)

```python
def search(query, ranking=lambda r: -r.stars):
    results = [r for r in all_restaurants if query in r.name]
    return sorted(results, key=ranking)

class Restaurant:
    all = []
    def __init__(self, name, stars):
        self.name, self.starts = name, stars
        Restaurant.all.append(self)
        
    def similar(self, k, similarity):
        """Return the K most similar restaurants to SELF, using SIMILARITY for comparison."""
        
        others = list(Restaurant.all)
        others.remove(self)
        return sorted(others, key=lambda x: -similarity(self, x))[:k]
        
    
    def __repr__(self):
        return '<' + self.name + '>'
        
Restaurant('Thai Delight', 2)
Restaurant('Thai Basil', 3)
Restaurant('Top Dog', 5)


results = search('Thai')
for r in results:
    print(r, 'is similar to', r,similar(3))
```

>`sorted(iterable, /, *, key=None, reverse=False)`
>
>Return a new list containing all items from the iterable in ascending order. A custom key function can be applied to customize the sort order, and the reverse flag can be set to request the result in descending order.

### Example: Reading Files

```python
def search(query, ranking=lambda r: -r.stars):
    results = [r for r in all_restaurants if query in r.name]
    return sorted(results, key=ranking)

def reviewed_both(r, s):
    return len([x for x in r.reviewers if x in s.reviewers])

class Restaurant:
    all = []
    def __init__(self, name, stars, reviewers):
        self.name, self.starts = name, stars
        self.reviewers = reviewers
        Restaurant.all.append(self)
        
    def similar(self, k, similarity=reviewed_both):
        """Return the K most similar restaurants to SELF, using SIMILARITY for comparison."""
        
        others = list(Restaurant.all)
        others.remove(self)
        return sorted(others, key=lambda x: -similarity(self, x))[:k]
        
    
    def __repr__(self):
        return '<' + self.name + '>'
        
# Restaurant('Thai Delight', 2)
# Restaurant('Thai Basil', 3)
# Restaurant('Top Dog', 5)
import json

reviewers_for_restaurants = {}

for line in open('reviews.json'):
    r = json.loads(line)
    biz = r['business_id']
    if biz not in reviewers_for_restaurant:
        reviewers_for_restaurant[biz] = [r['user_id']]
    else:
        reviewers_for_restaurant[biz].append(r['user_id'])

for line in open('restaurants.json'):
    r = json.loads(line)
    reviewers = reviewers_for_restaurant[r['business_id']]
    Restaurant(r['name'], r['stars'], reviewers)

results = search('Thai')
for r in results:
     print(r, 'shares reviews with', r,similar(3))
```

## Set Intersection



![image-20240915205315790](../assets/cs61a/image-20240915205315790.png)

```python
def fast_overlap(s, t):
    i, j, count = 0, 0, 0
    
    while i < len(s) and j < len(t):
        if s[i] == t[j]:
            count, i, j = count+1, i+1, j+1
        elif s[i] < t[j]:
            i += 1
        else:
            j += 1
    return count
```

Optimize the search engine

```python
def search(query, ranking=lambda r: -r.stars):
    results = [r for r in all_restaurants if query in r.name]
    return sorted(results, key=ranking)

def reviewed_both(r, s):
    return fast_overlap(s.reviewers, t.reviewers)

def fast_overlap(s, t):
    i, j, count = 0, 0, 0
    
    while i < len(s) and j < len(t):
        if s[i] == t[j]:
            count, i, j = count+1, i+1, j+1
        elif s[i] < t[j]:
            i += 1
        else:
            j += 1
    return count

class Restaurant:
    all = []
    def __init__(self, name, stars, reviewers):
        self.name, self.starts = name, stars
        self.reviewers = reviewers
        Restaurant.all.append(self)
        
    def similar(self, k, similarity=reviewed_both):
        """Return the K most similar restaurants to SELF, using SIMILARITY for comparison."""
        
        others = list(Restaurant.all)
        others.remove(self)
        return sorted(others, key=lambda x: -similarity(self, x))[:k]
        
    
    def __repr__(self):
        return '<' + self.name + '>'
        
# Restaurant('Thai Delight', 2)
# Restaurant('Thai Basil', 3)
# Restaurant('Top Dog', 5)
import json

reviewers_for_restaurants = {}

for line in open('reviews.json'):
    r = json.loads(line)
    biz = r['business_id']
    if biz not in reviewers_for_restaurant:
        reviewers_for_restaurant[biz] = [r['user_id']]
    else:
        reviewers_for_restaurant[biz].append(r['user_id'])

for line in open('restaurants.json'):
    r = json.loads(line)
    reviewers = reviewers_for_restaurant[r['business_id']]
    Restaurant(r['name'], r['stars'], sorted(reviewers))

# results = search('Thai')
# for r in results:
#      print(r, 'shares reviews with', r,similar(3))
while True:
    print('>', end=' ')
    results = search(input().strip())
    for r in results:
        print(r, 'shares reviewers with', r.similar(3))
```

## Sets

One more built-in Python container type

- Set literals are enclosed in braces
- Duplicate elements are removed on construction
- Sets have arbitrary order

```python
>>> s = {'one', 'two', 'three', 'four', 'four'}
>>> s
{'three', 'one', 'four', 'two'}
>>> 'three' in s
True
>>> len(s)
4
>>> s.union({'one', 'four'})
{'three', 'five', 'one', 'four', 'two'}
>>> s.intersection({'six', 'five', 'four', 'three'})
{'three', 'four'}
>>> s
{'three', 'one', 'four', 'two'}
```

Note that union and intersection don't mutate the original set.