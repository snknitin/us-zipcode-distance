# Project - US-Zipcode-Distance


Code to create a Pairwise Zip code Distance Matrix and use an index lookup. This is a tiny utility I built, for use in my work, but I figured it might be helpful to anyone else dealing with zip/postal code distances.

The idea is to form a (41483,41483) matrix where the cell values are the `haversine distances` between two zips that are indexed. We save the index look up and the matrix file as .npy, .json or .pkl to reload and use in different projects


![Numpy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)

## Installation - Dependencies

Install the folllowing python packages

```python
pip install -r requirements.txt
```
    
## Usage/Examples

```python


```


## Running Tests

To run tests, run the following command

```python


```


## Optimizations

What optimizations did I make in your code? 

* Converted the matrix from 'float64' to 'float32' to reduce disk space
* Tried using Numba.jit to speed up the iterrows and numpy loops
* `mpu.haversine` gives result in kms. Convert to miles 1km = 0.621371 miles


## Lessons Learned


* **numba** - 
    * Per the deprecation recommendations, it's very reasonable that code which doesn't compile with @jit(nopython=True) could be faster without the decorator.
    * The available libraries that can be used with numba jit in nopython is fairly limited (pretty much only to numpy arrays and certain python builtin libraries).   
* Don't use python's Pickle, don't use any database, don't use any big data system to store your data into hard disk, if you could use np.save() and np.load(). These two functions are the fastest solution to transfer data between harddisk and memory so far.
* Using list(zip(a,b)) is much faster if yopu want top create a new pandas column that is a tuple of 2 other columns
* To make a symmetrix pairwise matrix, initialze using `np.zeros` so that you won't need to worrty about the diagonal elements. Extrack the upper triangular indices. Add the transpose to the matrix to fill lower as well and set diagonal to 0 again

## Authors

- [@snknitin](https://www.github.com/snknitin)


## Acknowledgements

 - [Haversine Distance](https://stackoverflow.com/questions/19412462/getting-distance-between-two-points-based-on-latitude-longitude)
 - []()
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





