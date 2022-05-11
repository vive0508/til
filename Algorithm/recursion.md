# 재귀 알고리즘 (recursion)
## 예제 1

```python
def recursion(num):
  if num > 0:
    print('*' * num)
    return recursion(num-1)
  else:
    return 1

recursion(10)
```
**********    
*********   
********   
*******   
******   
*****   
****   
***   
**   
*

## 예제 2

```python
def factorial(num):
  if num>0:
    return num * factorial(num-1)
  else:
    return 1
print(f'factorial(10): {factorial(10)}')
```
factorial(10): 3628800
