# Recipe PCA

## tl;dr
Results did not come out as well as I thought. There's a lot I can do with the 
data now that I've actually cleaned it all, but I don't want ot do it now. 

## Deliverable
There's a 17775 x 400 matrix, where each row is a recipe, and each column is 
an ingredient. Each element in the matrix is how much of that ingredient is in
that recipe. There's a lot of stuff that can be done with that; it's also not as
complete as it could be. 

## How it works
Right now it's an iPython notebook. You can run it on c9 via 
`jupyter notebook --ip=0.0.0.0 --port=8080 --no-browser`.

The raw data is stored in a .json file called `full_format_recipes.json`, and
it was retrieved from the [Epicurious Kaggle competition](https://www.kaggle.com/hugodarwood/epirecipes).

The NLP model used to parse the ingredient strings and turn them into working 
ingredient objects comes from the [New York Times CRF model](https://github.com/NYTimes/ingredient-phrase-tagger). 
It's not perfect, and the cleaning I used was aggressive, like radical mastectomy
aggressive. 

A lot of recipes have duplicate names, a lot of ingredients were listed more than once,
and I use dictionaries heavily to map ingredients to recipes, recipes to lists of 
ingredients. In addition, I've tried to do a lot of deduping, which makes things complicated
but makes the results better, I feel.

The hard part is that even after modeling the ingredients, some still won't have 
quantities, units, or even ingredient names. That honestly sucks, and is part of why 
the data is still not working well.

## To-do
1. Normalize the units
2. Make a bijective map from ingredients to recipes, and project them into unipartite graphs.
3. Come up with an algorithm to extract flavor profiles. PCA isn't it.

## Why PCA didn't work
I'll get to that answer later, but I think it has to do with the frequency and sparsity of 
recipe vectors, as well as the fact that we didn't normalize our units/quantities.