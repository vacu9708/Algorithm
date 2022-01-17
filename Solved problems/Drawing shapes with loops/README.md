# Drawing shapes with loops

## Right-angled triangle
~~~c++
void right_triangle(int n){
	for(int i=0; i<n; i++){
		for(int j=0; j<i+1; j++) 
 	   		printf("*");
	printf("\n");
	}
}
~~~
## Output
![Untitled](https://user-images.githubusercontent.com/67142421/149676026-e54bac3d-b9f5-4ea2-9fa5-558078234def.png)


## Inverted right-angled triangle
~~~c++
void inverted_right_triangle(int n){
	for(int i=0; i<n; i++){
		for(int j=0; j<n-i; j++) 
			printf("*");
	printf("\n");
	}
}
~~~
## Output
![image](https://user-images.githubusercontent.com/67142421/149676047-2cff333a-6b81-4af1-8810-63ee771f3a16.png)

## Pyramid
~~~c++
void pyramid(int n){
	for(int i=0; i<n; i+=1){
		for(int j=0; j<n-i-1; j++)
			printf(" ");
		for(int j=0; j<i*2+1; j++)
			printf("*");
		printf("\n");
	}
}
~~~
## Output
![image](https://user-images.githubusercontent.com/67142421/149676064-de9b024f-3af3-410d-95c5-24355f81b6c9.png)

## Inverted pyramid
~~~c++
void inverted_pyramid(int n){
	for(int i=0; i<n; i++){
		for(int j=0; j<i; j++)
			printf(" ");
		for(int j=0; j<(n-i)*2-1; j++)
			printf("*");
		printf("\n");
	}
}
~~~
## Output
![image](https://user-images.githubusercontent.com/67142421/149676095-c210a9c5-7534-458b-8ea6-09d23ca833a5.png)


## Diamond
~~~c++
for(int i=0; i<5; i++){
	for(int j=0; j<4-i; j++) 
		printf(" ");
	for(int j=0; j<i*2+1; j++)
		printf("*");
	printf("\n");
}
    
for(int i=0; i<4; i++){
	for(int j=0; j<i+1; j++)
		printf(" ");
	for(int j=0; j<7-i*2; j++)
		printf("*");
	printf("\n");
}
~~~

## sandglass
~~~c++
for(int i=0; i<5; i++){
	for(int j=0; j<i; j++)
		printf(" ");
	for(int j=0; j<9-i*2; j++)
		printf("*");
	printf("\n");
}
    
for(int i=0; i<4; i++){
	for(int j=0; j<3-i; j++)
		printf(" ");
	for(int j=0; j<i*2+3; j++)
		printf("*");
	printf("\n");
}
~~~
