`count`
`count_if`
`transform`
`accumulate`
`reduce`
`find_if`
`partition`
`sort`
`multiplies`


`count`

spočíta prvky kolekcie

funkcia vráti počet riadkou (znakou '\n') v súbore

``` c++
int count_lines(path const & filename) 
{
	ifstream in{fname};
	return count(ifstreambuf_iterator<char>{in},	ifstreambuf_iterator{},	'\n');
}
```

`count_if`

```c++
count_if(persons.begin(), persons.end(), older_than{42});
```



`transform`

```c++
// mapping files to line counts by using transform
vector<int> count_lines_in_files(vector<path> & files)
{
	vector<int> result(files.size());
	transform(files.begin(), files.end(), result.begin(), count_lines);
	return result;
}
```

`accumulate`

sčíta prvky kolekcie

```c++
// calculating the average score functionally
double average_score(vector<int> const & scores)
{
	return accumulate(scores.begin(), scores.end(), 0) / (double)scores.size();
}
```


`reduce`

sčíta prvky kolekcie

```c++
// calculating the average score functionally
double average_score(vector<int> const & scores)
{
	return reduce(execution::par, scores.begin(), scores.end(), 0) 
		/ (double)scores.size();
}
```


`find_if`

vráti prvý vyskit hodnoty v kolekcii

```c++
string trim_left(string s)
{
	s.erase(s.begin(), s.end(), 
		find_if(s.begin(), s.end(), is_no_space));
	return s;
}
```


`partition` 

a jeho varianta `stable_partition` preusporiadaju kolekciu tak, že prvky vyhovujúce predikátu (podmienke) presunú na začiatok kolekcie. Verzia algoritmu `stable_partition` zachováva poradie presunutích prvkou.

```c++
vector xs = {1, 2, 3, 4, 5, 6, 7, 8, 9};
partition(begin(xs), end(xs), bind(greater<int>{}, _1, 6));
copy(begin(xs), end(xs), ostream_iterator<int>(cout, ", "));  // 9, 8, 7, 4, 5, 6, 3, 2, 1,
```

```c++
vector xs = {1, 2, 3, 4, 5, 6, 7, 8, 9};
stable_partition(begin(xs), end(xs), bind(greater<int>{}, _1, 6));
copy(begin(xs), end(xs), ostream_iterator<int>(cout, ", "));  // 7, 8, 9, 1, 2, 3, 4, 5, 6,
```

ukážka s použitím boost::phoenix

```c++
using namespace boost::phoenix::arg_names;

vector nums{21, 5, 62, 42, 53};
partition(begin(nums), end(nums), arg1 <= 42);
// numbers now contain [21, 5, 42,   62, 53]
//                        <= 42       > 42
```



`sort`

zotriedi kolekciu

```c++
vector numbers{5, 21, 13, 42};
sort(numbers.begin(), numbers.end(), greater<>{});
// numbers equals to [42, 21, 13, 5]
```


`multiplies`

binarny operator nasobenia

```c++
vector numbers{1, 2, 3, 4};
int product = accumutalte(numbers.begin(), numbers.end(), multiplies<>{});
// product is 24
```



-- Adam Hlavatovic
