# Making e^x using the improved Euler's method

~~~c++
#include <iostream>
using namespace std;

int dy_dx_function(int x, int y) {
    return y; // = dy/dx
}

void e_to_the_x(int target_x) { // RK2
    double compensation_for_x_step = 98765;
    double x_step = 1 / compensation_for_x_step;
    double x = 0, y = 1; // initial x and y
    double k1 = dy_dx_function(x, y), k2 = dy_dx_function(x + x_step, y + x_step * k1); // two slopes

    for (int i = 0; i < target_x * compensation_for_x_step; i++) {
        x = x + x_step; // Change in x
        y = y + x_step * ((k1 + k2) / 2); // Find the change in y using the average of the two slopes.
        k1 = dy_dx_function(x, y);
        k2 = dy_dx_function(x + x_step, y + x_step * k1);
    }

    printf("x = %lf, y = %lf, dy/dx = %lf\n", x, y, k1);
}

int main() {
    int x = 5;
    printf("e^x at x = %d\n", x);
    e_to_the_x(x);
}
~~~
## Output
![image](https://user-images.githubusercontent.com/67142421/150201459-2a278e3c-8501-432f-b834-de16d6136575.png)
