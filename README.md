Question:
Perform an efficient semi-join in MapReduce. Hint: Perform a
semi-join by having the mappers load a Bloom filter from the
Distributed Cache, and then filter results from the actual
MapReduce data source by performing membership queries against
the Bloom filter to determine which data source records should be
emitted to the reducers.

Answer:
Semi-Join with Bloom Filters in MapReduce
A semi-join only returns records from one dataset with matching keys from another dataset. Rather than a direct join, we employ a Bloom filter to check membership efficiently and minimize data shuffling.

Steps:
1.Create a Bloom filter: Utilize the smaller dataset (Dataset B) to create a Bloom filter with the keys we are looking for.
2.Distribution of Bloom filter: Distribute this filter to all mapper nodes using Hadoop's Distributed Cache.
3.Filtering records in the mapper: Before each mapper emits a record, it queries if the key of the current record is present in the Bloom filter.
4.Reduce phase (optional): Only applicable records are processed by the reducer.
