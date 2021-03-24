# 對數器

public static int\[\] generateRandomArray\(int maxSize, int maxValue\) {

 int\[\] arr = new int\[\(int\) \(\(maxSize + 1\) \* Math.random\(\)\)\];

 for \(int i = 0; i &lt; arr.length; i++\) {

 arr\[i\] = \(int\) \(\(maxValue + 1\) \* Math.random\(\)\) - \(int\) \(maxValue \* Math.random\(\)\);

 }

 return arr;

 }

 public static void main\(String\[\] args\) {

 int testTime = 500000;

 int maxSize = 100;

 int maxValue = 100;

 boolean succeed = true;

 for \(int i = 0; i &lt; testTime; i++\) {

 int\[\] arr1 = generateRandomArray\(maxSize, maxValue\);

 int\[\] arr2 = copyArray\(arr1\);

 insertionSort\(arr1\);

 comparator\(arr2\);

 if \(!isEqual\(arr1, arr2\)\) {

 succeed = false;

 break;

 }

 }

 System.out.println\(succeed ? "Nice!" : "代碼寫錯了!!!"\);

