Greedy solution : Fast but doesn't always make the best solution
When the change is $15, if $10, $5 and $1 are available coins, the greedy solution makes one $10 and five $1. But the best solution is three $5.

~~~Python
def count_change(change):
    one = two = ten = twenty = fifty = one_hundred = 0

    one_hundred = change // 100
    change-= one_hundred * 100

    fifty = change// 50
    change-= fifty * 50

    twenty = change// 20
    change-= twenty * 20

    ten = change// 10
    change-= ten * 10

    two = change// 2
    change-= two * 2

    one = change// 1
    change-= one

    print("$100 :",one_hundred,"/ $50 :",fifty,"/ $20 :",twenty,"/ $10 :",ten,"/ $2 :",two,"/ $1 :",one)

count_change(2354)
~~~
