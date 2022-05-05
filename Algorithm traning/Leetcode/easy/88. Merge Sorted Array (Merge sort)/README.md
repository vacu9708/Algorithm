[88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)
~~~javascript
var merge = function(nums1, m, nums2, n) {
    temp=new Array(m+n)
    i1=i2=temp_i=0
    while(i1<m && i2<n)
        if(nums1[i1]<nums2[i2])
            temp[temp_i++]=nums1[i1++]
        else
            temp[temp_i++]=nums2[i2++]

    // Pick up remaining elements and put them in temp
    while(i1<m)
        temp[temp_i++]=nums1[i1++]
    while(i2<n)
        temp[temp_i++]=nums2[i2++]
    
    for(let i=0; i<m+n; i++) // Copy the elements in temp into nums1
        nums1[i]=temp[i]
};
~~~
