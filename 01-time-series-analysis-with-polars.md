# Time Series Analysis with Polars

[Polars](https://pola.rs) seems to be one of the most exciting developments recently in the field of data analysis. It promises to be a fast and easy to use tool that can help overcome some of the trickiest challenges analysts face when using Pandas. E.g. it can process datasets that are larger than the computer's memory by using lazy processing, and offers a friendlier learnings curve than PySpark.

Pandas offers many great features to simplify the analysis of time series. In this post I'm going to try to prepare and analyze a temporal dataset to see how far I can go with Polars.

## Why use polars?

Pandas has played a major role in making the data revolution possible and bringing data scientists to Python. It's still a great library that has a lot of power, but it has been around for almost 16 years. It has seen a lot of development and it still goes a long way if you need a robust dataframe library, but it has also some shortcomings. 

One is related to the heritage of being built around the NumPy library, which is great for processing numerical data, but becomes an issue as soon as the data is anything else. Pandas 2.0 has started to bring in Arrow, but it's not yet the standard (you have to opt-in and according to the developers it's going to stay that way for the forseeable future). Also, pandas's Arrow-based features are not yet entirely on par with its NumPy-based features. Polars was built around [Arrow](https://arrow.apache.org) from the get go. This makes it very powerful when it comes to exchanging data with other languages and reducing the number of in-memory copying operations, thus leading to better performance.

The 2nd point is that pandas is not able to use all computing power of your computer without external help. No matter how many CPU cores you've got, Pandas computation will always use only one of them. There are tools like Dask that can help you get around that limitation, but that also adds another dependency and another tool you've got to learn. Polars has the ability to use the full computing power available to you without having to do anything in addition.

The 3rd point I love is the ability to use lazy APIs. These offer you the possibility to build your data pipeline first and work on datasets that are larger than your computer's memory. This is very powerful if you have to analyze huge datasets or if you are working with streaming data. It also comes with query optimization, which can be a huge performance blessing in its own right.

The API is very friendly, even though if you're coming from pandas, you might have to unlearn a couple of things and learn a few new concepts, but overall, you'll find that the learning curve stays moderate. 

If you're curious to read more about the performance benefits, check out this [benchmark](https://pola.rs/posts/benchmarks/).

## The dataset

For this tutorial we're going to use the [Supply of electricity](https://ec.europa.eu/eurostat/databrowser/view/nrg_105m/default/table?lang=en) dataset provided by Eurostat. This dataset contains the electricity supply of European countries per month between January 2008 and December 2019. You can download the dataset as a TSV file.

The dataset offers a few interesting challenges. First, it's pivoted, i.e. the months are on the columns and non-temporal identifiers are on the rows. Second, these indetifiers are contained in a single column, separated by commas. Third, the dataset is a TSV file, i.e. we'll have to use tabs instead of commas to read the dataset.

We'll have to deal with missing values, data type issues, etc. as well.

## What are we going to do?

We'll start by reading the dataset and checking if it's good for our purpose.

As usual, it's not, so we'll do some data wrangling to bring it into a shape that makes it easier for us to find answers to our questions.

Finally, we're going to ask a couple of questions and try to answer them using Polars.

## What are we not going to do (yet)?

We're not going to go into visualization yet, but I'm planning to add some charts to the notebook as well at a later stage.

We're not going to take advantage of the lazy API as the dataset is quite small. I'm planning to do a separate post about this topic, so stay tuned.

## Let's see the code

Feel free to download the dataset and the Jupyter notebook and run it in your own environment if you'd like to follow along. The GitHub repo is available here:
<GITHUB LINK>

You'll find a detailed description of each step in the notebook. 

## Conclusions

If you've followed the notebook, you've seen that the Polars API is quite easy to use and offers you very powerful capabilities when it comes to working with time series. Feel free to continue experimenting with the dataset and the code, and let me know if you've got questions or comments. 

I'm also happy to see your feedback on the topics you'd like me to write about around Polars.

## References

Data source:
[Supply of electricity - monthly data. EuroStat Data Browser](https://ec.europa.eu/eurostat/databrowser/view/nrg_105m/default/table?lang=en)

Polars user guide:
[User Guide](https://pola-rs.github.io/polars/user-guide/)