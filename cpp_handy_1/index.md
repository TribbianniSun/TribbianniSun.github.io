# cpp cheatsheet - upper_bound and lower_bound



cpp cheatsheet 1.
<!--more-->



## Binary Search related library function
- [lower_bound](http://www.cplusplus.com/reference/algorithm/lower_bound/) 
- [upper_bound](http://www.cplusplus.com/reference/algorithm/upper_bound/) 
- [binary_search](http://www.cplusplus.com/reference/algorithm/binary_search/) (beginIterator, endInterator, val)

### [lower_bound](http://www.cplusplus.com/reference/algorithm/lower_bound/)
- lower_bound(beginIterator, endInterator, target)
- Returns an iterator pointing to the first element in the range [first,last) which does not compare less than val.
- **greater than or equal to** the target
- if no elements satisfies the condition, simply return the endInterator(out of bound)

### [upper_bound](http://www.cplusplus.com/reference/algorithm/upper_bound/) 
- upper_bound(beginIterator, endInterator, target)s
- Returns an iterator pointing to the first element in the range [first,last) which compares greater than val.
- strictly **greater than** the target
- if no element satisfies the condition, simply return the endInterator(out of bound)

### [binary_search](http://www.cplusplus.com/reference/algorithm/binary_search/)
- binary_search(beginIterator, endInterator, val)
- true if exist, false otherwise.


```cpp
int main()
{

    vector<int> _v;
    for(int i = 0; i < 5; i++){
        _v.push_back(i);
        _v.push_back(i + 3);
    }

    // must be sorted in increasing order
    // note that rbegin, rend, reverse order is not allowed
    sort(_v.begin(), _v.end()); 


    cout << lower_bound(_v.begin(), _v.end(), 4) - _v.begin() << '\n';
    
    return 0;
}
```
