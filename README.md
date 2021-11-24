# Project - US-Zipcode-Distance


Code to create a Pairwise Zip code Distance Matrix and use an index lookup. This is a tiny utility I built, for use in my work, but I figured it might be helpful to anyone else dealing with zip/postal code distances. This can be a huge and efficient time saver if you're working with large data and need to keep hitting some sort of a zip/latlong service API multiple times. 

The idea is to form a (41483,41483) matrix where the cell values are the `haversine distances` between two zips that are indexed. I save the index look up and the matrix file as .npz, .json or .pkl to reload and use in different projects. I hope this saves your effort when you're working with data streams or pandas dataframes and want to avoid iterating, using pypi package or a custom apply function to calculate distance between 2 zipcodes multiple times.

Use this matrix and vectorize your operations !

![Numpy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)

## Installation - Dependencies

Install the folllowing python packages

```python
pip install pandas
pip install numpy
pip install mpu
```

## Running the script

Since the the matrix is too huge to upload on git, you can try running the .py script in the code folder or go through the Jupter Notebook. The source file has been added in the Data folder. Running the Zip_distance.py file will generate and save the matrix on your machine and you can load it using

```python
zip_dist = np.load(os.path.join(walk_up_folder(os.getcwd(), 2), "zip_dist.npz"))['arr_0']
```

    
## Usage/Examples

```python
# Load the saved objects
f = open(os.path.join(walk_up_folder(os.getcwd(), 3), "Data/zips_indexer.json"))
zips_indexer = json.load(f)
zip_dist = np.load(os.path.join(walk_up_folder(os.getcwd(), 3), "Data/zip_dist.npz"))['arr_0']

a='95035' # Zipcode as String
b='94085'

# Extract that cell value from the distance matrix
distance = zip_dist[zips_indexer[a],zips_indexer[b]]

```

## Running Code

To run the code fresh or make any changes, you can follow the steps in the Notebook


## Optimizations

What optimizations did I make in my code? 

* Converted the matrix from 'float64' to 'float32' to reduce disk space
* Tried using Numba.jit to speed up the iterrows and numpy loops
* `mpu.haversine` gives result in kms. Convert to miles 1km = 0.621371 miles
* Did not normalize the matrix before saving since i do need the raw distance values and since it is pairwise the max distance will be too high


## Lessons Learned


* **numba** - 
    * Per the deprecation recommendations, it's very reasonable that code which doesn't compile with @jit(nopython=True) could be faster without the decorator.
    * The available libraries that can be used with numba jit in nopython is fairly limited (pretty much only to numpy arrays and certain python builtin libraries).   
* Don't use python's Pickle, don't use any database, don't use any big data system to store your data into hard disk, if you could use np.save() and np.load(). These two functions are the fastest solution to transfer data between harddisk and memory so far.
* Using list(zip(a,b)) is much faster if yopu want top create a new pandas column that is a tuple of 2 other columns
* To make a symmetrix pairwise matrix, initialze using `np.zeros` so that you won't need to worrty about the diagonal elements. Extrack the upper triangular indices. Add the transpose to the matrix to fill lower as well and set diagonal to 0 again

## Authors

- [@snknitin](https://www.github.com/snknitin)


## Bibtex

Please use the following bibtex, when you refer

    @software{Samala_Pairwise_Zip-code_Haversine_2021,
    author = {Samala, Nitin Kishore Sai},
    month = {11},
    title = {{Pairwise Zip-code Haversine distance lookup matrix}},
    url = {https://github.com/snknitin/us-zipcode-distance},
    year = {2021}
    }

## Acknowledgements

 - [Haversine Distance Calculation](https://stackoverflow.com/questions/19412462/getting-distance-between-two-points-based-on-latitude-longitude)
 - [Pairwise matrix from 2 arrays](https://stackoverflow.com/questions/9704565/populate-numpy-matrix-from-the-difference-of-two-vectors/9704775#9704775)
 - [Array Storage Benchmark](https://github.com/mverleg/array_storage_benchmark)
 - [Compressed save/load NPZ](https://stackoverflow.com/questions/18231135/load-compressed-data-npz-from-file-using-numpy-load/44693995)



## Related

Here are some related projects

[pgeocode](https://pypi.org/project/pgeocode/)


## FAQ

#### Does this only work for US Zipcodes ? 

No. You can change the source file of the zip details from [here](https://github.com/symerio/postal-codes-data/tree/master/data/geonames) and run the code for any country

#### Question 2

Answer 2



## Feedback

If you have any feedback, please reach out to us at `snk.nitin@gmail.com` 


## License

[Apache 2.0](https://choosealicense.com/licenses/apache-2.0/)





