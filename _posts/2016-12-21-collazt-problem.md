---
layout: post
title: Tìm dãy Collatz dài nhất
categories: [euler, algorithm]
tags: [python, collatz, python]
description: Tìm dãy Collatz dài nhất của một số nhỏ hơn 10000000
---
Dạo gần đây mình khá là có hứng thú với các bài toán trên [EulerProject]('https://projecteuler.net'). Thấy bọn nước ngoài giải ghê quá, Việt Nam được vài mống 👎 👎  
Trên Euler Project bạn không cần phải có một thuật toán tối ưu nhất, chỉ cần có kết quả đúng. Thuật toán cho dù chạy 1 ngày, 2 ngày, cả tuần mới ra kết quả, nhưng chỉ cần có kết quả đúng thì bạn vẫn có thể pass.  
Đặc biệt là khi pass qua một problem thì bạn có thể tham khảo cách giải của những người khác, lời giải rất đa dạng về cách giải quyết cũng như ngôn ngữ lập trình: `Java`, `Python`, `C/C++`, `ECMAScript`,...  
Quảng cáo cho EulerProject thế đủ rồi, quay lại với bài toán *`Collatz`*. Nếu bạn nào chưa biết về *`Collatz Problem`* thì bạn có thể đọc ở [đây]('https://en.wikipedia.org/wiki/Collatz_conjecture').  
Hiểu một cách đơn giản:
Cho trước một số nguyên dương n, giá trị của n lần lượt được tính theo hàm *`f(n)`*  
![collazt function]('https://wikimedia.org/api/rest_v1/media/math/render/svg/f69ea6c9163eefcadeb36c93a68626610f1f4e75')   
Nếu thực hiện đủ lâu, kết quả cuối cùng bạn nhận được sẽ là `1`. Ví dụ như `n=13`:  
*`13 → 40 → 20 → 10 → 5 → 16 → 8 → 4 → 2 → 1`*
Mặc dù chưa được chứng minh nhưng bằng máy tính người ta thấy rằng *`Collatz Problem`* đúng với các số nguyên dương nhỏ hơn `n < 5,764,607,523,034,234,880`  
Với ví dụ `n=13` như trên ta thấy dãy *`Collatz`* có độ dài là `10`, kết thúc tại `1`
Vậy với số nguyên dương `n<1000000` nào thì sẽ tạo được dãy *`Collatz`* dài nhất?  

Đọc xong đến đây có nhiều bạn sẽ bật IDE lên code liền (giống mình 😘), mình đọc xong bài toán bật Atom lên code liền, code của mình như thế này:  
 {% highlight python %}
 # Problem 14
 # minamidev
 def collatzCal(n):
     count = 1
     while n!=1:
         if n%2 == 0:
             n/=2
         else:
             n=3*n+1
         count+=1
     return count

 longest = 0
 num = 0
 for x in range(1000000,1,-1):
     temp = collatzCal(x)
     if temp>longest:
         longest=temp
         num= x
 print('Number has longest Collatz chains: ',num)
{% endhighlight %}

`Run` phát coi nào.
![problem14_2.py]('/assets/media/2016-12-21-1.png')

Cũng ra kết quả đúng nhưng chậm quá 😳  hơn 80s...  
Phải làm sao cải tiến mới được 😡  
Chợt nhận ra, nếu ta có dãy của `n=13`:  
*`13 → 40 → 20 → 10 → 5 → 16 → 8 → 4 → 2 → 1`*  
thì khi tính toán độ dài của dãy `n=40`:  
*`40 → 20 → 10 → 5 → 16 → 8 → 4 → 2 → 1`*  
ta thấy `length(n=13) = length(n=40)+1 `
Như vậy ta phải lưu giá trị của `length(n=40)` sẵn, khi tính `length(n=13)` thì lôi ra dùng luôn.  
Lại bật Atom lên code tiếp nào:
{% highlight python %}
# Problem 14
# minamidev

collatzs = {1:1}
def collatzCal(n):
    global collatzs
    if not n in collatzs:
        if n%2 == 0:
            collatzs[n]=collatzCal(n/2)+1
        else:
            collatzs[n]=collatzCal(3*n+1)+1
    return collatzs[n]

for i in range(1000000,0,-1):
    collatzCal(i)
print('Number has longest Collatz chains: ',max(collatzs.keys(), key=(lambda k:collatzs[k])))

{% endhighlight %}  
`Run` phát:  
![problem14.py]('/assets/media/2016-12-21-2.png')  
Ấn tượng chưa, chỉ còn dưới 4s...

Code trên dùng đệ quy nên hơi khó hiểu. 😌 😌  
Nhưng không sao, lấy giấy viết ra từng bước chắc chắn sẽ hiểu ra. Cố lên! 😘 😘  
