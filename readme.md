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

a jeho varianta `stable_partition` preusporiadaju kolekciu tak, že prvky vyhovujúce predikátu (podmienke) a presunú na začiatok kolekcie. Verzia algoritmu `stable_partition` zachováva poradie presunutích prvkou.


```c++
// move females at the top of the people list
partition(people.begin(), people.end(), is_female);
```

ukážka s použitím boost::phoenix

```c++
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




