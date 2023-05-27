# How to find the value of Pi
>Principle : The area of a circle whose radius is 1 is equal to Pi. (Area of a circle = r^2 * pi)

## Using integral

![image](https://user-images.githubusercontent.com/67142421/149086756-188a218e-90b2-4221-a46c-bdf6eceed801.png)

### C++
~~~c++
#include <iostream>
#include <time.h>

using namespace std;

void pi_using_integral() {
	double infinity = 654321, dx = 1 / infinity, y = 0, sum = 0;
	for (int i = 0; i < infinity; i++) { // Find the area of the 1st quadrant
		y = sqrt(1 - pow((i * dx), 2));
		sum += dx * y;
	}

	printf("%.20lf\n", sum * 4); // The area of the circle is the area of 1 quadrant times 4
}

int main() {
	double start = clock();
	pi_using_integral();
	printf("Elapsed time : %lf\n", clock() - start);
}
~~~

### Python
~~~python
import time

start = time.time()

infinity = 654321
dx = 1 / infinity
y = 0
sum = 0
for i in range(0, infinity):
    y=(1 - (i * dx)**2)**0.5
    sum += dx * y

print(f"Pi = {sum * 4}")
print(f"Elapsed time : {time.time() - start}")
~~~
## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149087590-95170557-b07f-4e71-8c18-3549582e7030.png)

---
## Using Monte-Carlo method
Pi can be found by calculating the ratio of the number of points that get into a circle inscribed in a square to the total number of points in the square.<br>

![image](https://github.com/vacu9708/Algorithm/assets/67142421/e1239f01-d334-4cea-8a07-75d27d90d993)

~~~c++
#include <iostream>
#include <random>
#include <time.h>

using namespace std;

double random_real_number(double min, double max) {
	random_device seed; // Generate a random seed
	mt19937_64 mersenne(seed());
	uniform_real_distribution<> range(min, max);
	return range(mersenne);
}

void pi_using_monte_carlo() {
	double n_of_points = 54321, n_of_points_in_circle = 0, x = 0, y = 0;
	for (int i = 0; i < n_of_points; i++) {
		x = random_real_number(-1, 1);
		y = random_real_number(-1, 1);

		if (pow(x, 2) + pow(y, 2) <= 1) // From the equation of a circle
			n_of_points_in_circle++;
	}

	printf("%.20lf\n", (n_of_points_in_circle / n_of_points) * 4); // Multiply the ratio by the area of the circle(4)
}

int main() {
	double start = clock();
	pi_using_monte_carlo();
	double end = clock();
	printf("Elapsed time : %lf\n", end - start);
}
~~~
## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149089208-e8d964c8-2e57-4e0e-9cab-a6155b45d721.png)

Here we can see that Monte-Carlo method is more inefficient than the way using integral when finding Pi
