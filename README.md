# Modular-Writeup-fwopCTF
## ĐỀ
![image](https://user-images.githubusercontent.com/91708234/139487778-51ddada8-8059-464e-91b2-1e9509699f56.png)


```py
  pow(31, pow(31, 2813771283), 384302)
```
## Phân tích
Khi chạy đoạn code trên thì cũng khá là lâu đấy khi độ dài của pow(31, 2813771283) lên tới vài trăm ngàn.

Thử chạy và chờ đợi kết quả khi nhập nguyên cái đề vào python =)).Việc này rất tốn thời gian và không hiệu quả.

Do đó, ta phải tìm tới các thuật toán
## Giải bài trên lý thuyết
Đầu tiên có các tính chất với modulo như sau :

+) a*b mod n = (a mod n) * (b mod n) mod n.

+) Nếu a = b (mod n) và c = d (mod n) thì ac = bd (mod n).

+) Nếu a = b (mod n) thì a^k = b^k (mod n) với mọi k≥1.

+) a^b mod n = (a mod n)^b mod n.

+) Nếu gcd(a, n) == 1, thì a^φ(n) ≡ 1 (mod n).

   Theo Euler's Theorem.
   
+) Nếu gcd(a, n) == 1, thì a^k = a^(k mod φ(n)) (mod n) với mọi k≥1.

Tham khaỏ các tính chất của modulo tại :

  https://math.stackexchange.com/questions/491576/simplifying-large-exponents-in-modular-arithmetic-like-1007-in-41007-pmod
  
## Giải bài thực tế
  Như vậy, để đơn giản hóa ```py pow(31, 2813771283) ``` thì ta có thể tìm φ(n) và tính ```py pow(31, 2813771283, φ(n)) ``` .
  
  Nó nhanh hơn rất nhiều so với tính trực tiếp  ```py  pow(31, pow(31, 2813771283), 384302) ```.
  
## Code mẫu
  ```py
  #a = pow(31, pow(31, 2813771283), 384302) = ?
phi_n = 0
for i in range(1,10**10):
    if pow(31, i, 384302) == 1 :
        phi_n = i
        break
x = 31
y = pow(31, 2813771283, phi_n)
a = pow(31, y, 384302)
print(a)
```
