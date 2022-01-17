# Making f(x) = e^x with a numerical method of differential equation

![image](https://user-images.githubusercontent.com/67142421/149747518-9a60f957-4e0c-4538-bfa8-e99a5b91dbba.png)

~~~c++
#include<iostream>
using namespace std;

// Up to e^10 possible. If these are in the function, stack overflow occurs
double x_points[10000001] = { 0 };
double y_points[10000001] = { 1 };
double dy_dx[10000001] = { 1 };
void e_to_the_x(int x) {
    double x_step = 0.000001;

    for (int i = 0; i < a * compensate_for_x_step; i++) {
        x_points[i + 1] = x_points[i] + x_step;
        y_points[i + 1] = y[i] + dy_dx[i] * x_step; // y_points[i+1] is equal to y_points[i] + change in y
        dy_dx[i + 1] = y_points[i + 1]; // The solution of this differential equation(dy/dx = y) is y=e^x. (using separation of variables method)
    }

    int compensate_for_x_step = 1000000;
    int i = x * compensate_for_x_step;
    cout << "x = " << x_points[i] << " y = " << y_points[i] << " dy/dx = " << dy_dx[i] << endl;
}

int main() {
    int x = 5;
    printf("The function value of e^x on x = %d\n", x);
    e_to_the_x(x);
}
~~~
## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149199541-b2e53c9a-830e-45cc-8a3c-556fe41ec763.png)
