```java
    /**
     * 合并权限
     * @param rightValues 权限的二进制字符串 例如 1000、11111100、1001010100
     * @return 合并后的权限 1111110000
     */
    String mergeRightValue(String... rightValues){

        // 最长字符串长度
        int iIndex = 0;
        for(int i = 0; i < rightValues.length; i ++){
            if(rightValues[i].length() > rightValues[iIndex].length()){
                iIndex = i;
            }
        }
        int iMaxLength = rightValues[iIndex].length();

        // 位数补0并加和
        long lSum = 0;
        for(int i = 0; i < rightValues.length; i ++){
            lSum += (Long.valueOf(rightValues[i]) * (Math.pow(10, iMaxLength - rightValues[i].length())));
        }

        // 判断每个位,拼接权限字符串
        String str = String.valueOf(lSum);
        StringBuffer rtnStr = new StringBuffer();
        for(int i = 0;i < str.length(); i ++){
            if(str.charAt(i) != '0'){
                rtnStr.append("1");
            }else{
                rtnStr.append("0");
            }
        }
        return rtnStr.toString();
    }
```
