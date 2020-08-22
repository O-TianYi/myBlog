[参考](https://blog.csdn.net/m0_38099607/article/details/72638678)



Number()：含非数字字符串返回NaN

parseInt()：返回数字部分



```
//Number
var num1=Number("Hello World");  //NaN
var num2=Number("");             //0
var num3=Number("000011");       //11
var num4=Number(true);           //1
var num5=Number("num123")       //NaN


//parseInt
var num1=parseInt("num123");    //NaN
var num2=parseInt("");          //NaN
var num3=parseInt("123.45")     //123
var num4=parseInt("101010",2)   //42
var num5=parseInt("123num")     //123
var num6=parseInt("0xff")       //255


//parseFloat
var num1=parseFloat("1234blue");    //1234
var num2=parseFloat("0xA");         //0
var num3=parseFloat("0908.5");      //908.5
var num4=parseFloat("3.125e7");     //31250000
var num5=parseFloat("123.45.67")    //123.45
var num6=parseFloat("")             //NaN
var num7=parseFloat("num123")       //NaN
```

