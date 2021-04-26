# [无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

哈希集合记录字符是否出现过，用滑动窗口求解

## java
```java
public int lengthOfLongestSubstring(String s) {
    if(s.length()==0){
        return 0;
    }
    //哈希集合记录字符是否出现过
    Set<Character> oc=new HashSet<Character>();
    oc.add(s.charAt(0));
    int maxlen=0,j=0;
    for(int i=0;i<s.length();i++){
        if(j<i){
            j=i;
            oc.add(s.charAt(i));
        }
        while(j<s.length()-1 && !oc.contains(s.charAt(j+1))) {
            oc.add(s.charAt(j+1));
            j++;
        }
        maxlen=Math.max(maxlen,j-i+1);
        oc.remove(s.charAt(i));
    }
    return maxlen;
}
```
