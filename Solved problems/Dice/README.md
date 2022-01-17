# For all the 6 numbers of dice to be 1, how many times should it be thrown?

~~~java
package test;

public class Test {
	boolean are_all_numbers_one(int dice[]){
		for (int i : dice)
			if (i != 1)
				return false;
		
		return true;
	}
	
	void throw_and_check(int dice[]) {
		int count = 0, how_many_casts = dice.length;
		while (true) {
			// Throw the dice
			System.out.print("( ");
			for (int i = 0; i < how_many_casts; i++) {
				dice[i] = (int) (Math.random() * 6) + 1; // A random number between 1 and 6
				System.out.print(dice[i] + " ");
			}
			System.out.print(")\n");
			count++;
			//-----
			
			if (are_all_numbers_one(dice) == true) {
				System.out.print("It took " + count + " times for all the 6 numbers to be 1");
				return;
			}
		}
	}

	public static void main(String[] args) {
		int dice_throwings[] = new int[2];
		Test test = new Test();
		test.throw_and_check(dice_throwings);
	}
}
~~~

## Output
![image](https://user-images.githubusercontent.com/67142421/149677357-12368f7a-9d8f-4011-8250-11d2a9a1b8ff.png)
