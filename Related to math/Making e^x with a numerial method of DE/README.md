# Making f(x) = e^x with a numerical method of differential equation

~~~c++
#include<iostream>
using namespace std;

// Up to e^10 possible. If these are in the function, stack overflow occurs
double x[10000001] = { 0 };
double y[10000001] = { 1 };
double dy_dx[10000001] = { 1 };
void e_to_the_x(int a) {
    double x_step = 0.000001;
    int compensate_for_x_step = 1000000;

    for (int i = 0; i < a * compensate_for_x_step; i++) {
        x[i + 1] = x[i] + x_step;
        y[i + 1] = y[i] + dy_dx[i] * x_step; // y[i+1] is equal to y[i] + change in y
        dy_dx[i + 1] = y[i + 1]; // The solution of this differential equation(dy/dx = y) is y=e^x. (using separation of variables method)
    }

    int i = a * compensate_for_x_step;
    cout << "x = " << x[i] << " y = " << y[i] << " dy/dx = " << dy_dx[i] << endl;
}

int main() {
    int x = 5;
    printf("The function value of e^x on x = %d\n", x);
    e_to_the_x(x);
}
~~~
## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149199541-b2e53c9a-830e-45cc-8a3c-556fe41ec763.png)
