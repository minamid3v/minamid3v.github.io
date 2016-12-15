---
layout: post
title: Hoán đổi 2 biến không dùng biến tạm bằng XOR
categories: [programming]
tags: [xor, swap]
description: Tại sao những dòng lệnh x = x^y; y= x^y; x= x^y; lại hoán đổi giá trị 2 biến.
---
Hồi còn mới bắt đầu học lập trình chắc hẳn ai cũng gặp bài toán hoán đổi giá trị 2 biến, beginner sẽ viết thế này:  
{% highlight js %}
var temp = x;
x = y;
y = temp;
{% endhighlight %}  
Đây là cách dùng một biến tạm để lưu lại giá trị.

Nhưng nhiều người pro hơn thì sẽ viết thế này:  
{% highlight js %}
x = x^y;
y = x^y;
x = x^y;
{% endhighlight %}  
![WTF](http://www.punjabigraphics.com/images/11/omg-wtf.jpg)  

Cái này là cái WTF gì mà nhìn đơn giản, nhưng thật vi diệu làm sao, it works!
Thế là nhét nó vào code. Nhưng với lương tâm của một coder chân chính, mình phải hiểu rõ nó rồi mới được dùng (trừ những lúc lười ra, tiếc thay mình toàn lười ^ ^) nên mình làm  post này cho các bạn cũng lười như mình hiểu rõ thêm về kĩ thuật này.
## OK bắt đầu với thằng XOR

1. Giá trị của phép XOR:  
X ^ 0 = X
X ^ X = 0
2. Tính giao hoán:  
X ^ Y = X ^ Y;
3. Tính kết hợp:
(X ^ Y) ^ Z = X ^ (Y ^ Z)

## Quay lại với code lúc nãy
{% highlight js linenos %}
x = x^y;
y = x^y;
x = x^y;
{% endhighlight %}   

`Dòng 1` không có gì đặc biệt, ta bỏ qua. `Dòng 2` ta có thể viết lại như sau:
{% highlight js %}
y = (x^y)^y;
{% endhighlight %}  
Áp dụng tính kết hợp ở trên ta có:
{% highlight js %}
y = x^(y^y);
y = x^0;
y = x;
{% endhighlight %}  
*Perfect!*  
Tiếp theo đến `dòng 3`.
Dòng 3 có thể viết lại thành  
{% highlight js %}
x = x^(x^y);
x = (x^x)^y;
x = 0^y;
x = y;
{% endhighlight %}  

![WOW](https://2.bp.blogspot.com/-AAAoiwaaiQM/TXmaCuYsKPI/AAAAAAAAAHU/3vqX_YzKWLk/s748/breath%2Bcat.png)

Ghê chưa :D

Bây giờ nhìn theo một hướng khác.  
{% highlight js linenos %}
x = x^y;
y = x^y;
x = x^y;
{% endhighlight %}  
Ở `dòng 1` chúng ta đã `combine` giá trị của `x` và `y` bằng `XOR` và lưu giá trị này vào x.`XOR` là một cách ngon lành để lưu một cái gì đó tạm thời, vì khi chúng muốn xoá nó đi thì chỉ cần `XOR` nó lại một lần nữa.  
Ta sử dụng cách dùng này của `XOR` tại `dòng 2`, lúc nãy ta đã tạo ra combine của `x` và `y`, giờ ta muốn xoá `y` đi, ta `XOR` giá trị đó với `y` một lần nữa, `y` sẽ biến mất. Chỉ còn lại `x` bơ vơ.  
`Dòng 3` hoàn toàn tương tự, nhưng chú ý một điều là `y` giờ mang giá trị của `x` nên khi `XOR` với `y` thì sẽ xoá `x` đi, đến lượt `y` lại bơ vơ một mình.

これで終わります。
