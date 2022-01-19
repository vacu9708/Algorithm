# Making f(x) = e^x with a numerical method of differential equation

### RK1 method
![image](https://user-images.githubusercontent.com/67142421/150194690-5656e5cd-6411-4e41-97f2-f07142c0e727.png)

![image](https://user-images.githubusercontent.com/67142421/149747518-9a60f957-4e0c-4538-bfa8-e99a5b91dbba.png)

~~~c++
#include <iostream>
using namespace std;

double x_points[9876543]{ 0 };
double y_points[9876543]{ 1 };
double dy_dx[9876543]{ 1 };

void e_to_the_x(int target_x) {
    double compensation_for_x_step = 98765;
    double x_step = 1 / compensation_for_x_step;

    for (int i = 0; i < target_x * compensation_for_x_step; i++) {
        x_points[i + 1] = x_points[i] + x_step;
        y_points[i + 1] = y_points[i] + dy_dx[i] * x_step; // y_points[i+1] is equal to y_points[i] + change in y
        dy_dx[i + 1] = y_points[i + 1]; // The solution of this differential equation(dy/dx = y) is y=e^x. (using separation of variables method)
    }

    int i = target_x * compensation_for_x_step;
    cout << "x = " << x_points[i] << " y = " << y_points[i] << " dy/dx = " << dy_dx[i] << endl;
}

void e_to_the_x_without_arrays(int target_x) {
    double compensation_for_x_step = 98765;
    double x_step = 1 / compensation_for_x_step;
    double x = 0, y = 1, dy_dx = 1;

    for (int i = 0; i < target_x * compensation_for_x_step; i++) {
        x = x + x_step;
        y = y + dy_dx * x_step;
        dy_dx = y;
    }

    printf("x = %lf, y = %lf, dy/dx = %lf\n", x, y, dy_dx);
}

int main() {
    int x = 5;
    printf("The function value of e^x on x = %d\n", x);
    e_to_the_x(x);
    e_to_the_x_without_arrays(x);
}
~~~
## Output
![image](https://user-images.githubusercontent.com/67142421/150188873-5f5c926d-f25b-47cb-a7ae-a5dc69ac5947.png)
