# 수포자

![Problem](https://user-images.githubusercontent.com/67142421/149675796-cdeb06d8-73fb-4140-9da0-bd80a985b86c.png)

~~~c++
#include <iostream>
#include <list>
#include <vector>
using namespace std;

void solution(vector<int>& answer, list<int>& winner) {
	int student1[] = { 1,2,3,4,5 };
	int student2[] = { 2,1,2,3,2,4,2,5 };
	int student3[] = { 3,3,1,1,2,2,4,4,5,5 };
	int scores[3] = { 0, };

	for (int i = 0; i < answer.size(); i++) {
		if (answer[i] == student1[i % 5])
			scores[0]++;
		if (answer[i] == student2[i % 8])
			scores[1]++;
		if (answer[i] == student3[i % 10])
			scores[2]++;
	}

	int max = 0;
	for (int person = 1; person < 3; person++)
		if (scores[person] > scores[max])
			max = person;
	for (int person = 0; person < 3; person++)
		if (scores[person] == scores[max])
			winner.push_back(person + 1);
	for (int i : winner)
		cout << i << " ";
}

int main() {
	vector<int> answers = { 1,2,3,4,5 };
	list<int> winner;
	solution(answers, winner);
}
~~~
## Output
1
