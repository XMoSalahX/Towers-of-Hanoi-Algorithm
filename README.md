# Towers of Hanoi Algorithm

First of all, before the solution, let me explain what the Tower of Hanoi problem is: it is a game whose purpose is to move a set of disks in the same order from one place to another where the movement is through only three columns.

### Rules
* Only one disk moves at a time.
* The disk can only be moved if it is the same as the top disk in the column.
* Cannot put a large disk on a small disk.

### Way of Thinking
The right way to write any algorithm is the ability to understand how the solution process works manually before anything.

![Tower-of-Hanoi-normal-image](https://techvidvan.com/tutorials/wp-content/uploads/sites/2/2021/07/TV-Tower-of-Hanoi-normal-image01.jpg)

I want to find a solution to move the group of disks to the destination in the same order using any number of disks.

Source = "A" -
Auxiliary = "B" -
Destination = "C"

#### Example one:
Suppose there is only one disk. 

```I will move the only disk from A to C```

I'll write a function containing a Parameter (Number of disks, all places...) to solve this case.

````js
function hanoiAlgo(n, from, to, aux) {
      if (n === 1) {
        console.log(`Move disk ${n} From ${from} To ${to}`);
      }
    }

hanoiAlgo(1, "A", "C", "B");
````

#### Example two:
Suppose there is only two disk. 

I am going to move the first disk to C as I did in the previous example and then I am going to move the second disk to B and then I am going to move the first disk to B.

![Tower-of-Hanoi-normal-image](https://cdn.kastatic.org/ka-perseus-images/1ac984ec3372b658bf52baa5fca70339af29d1d2.png)

As I can see, I'll find that I've moved the disks to B, not C, and that's a mistake, of course.

*What are the correct movements?*  
```Move disk 1 From A To B```  
```Move disk 2 From A To C```  
```Move disk 1 From B To C```  

**_NOTE:_**  In the first example, the first movement was from A to C, but in the second example, the first movement was from A to B.

*So here I will ask the question, what if the number of disks is 100 disk? Where will the first disk go?*

Let me tell you, after many attempts manually I came to the conclusion of something important which is that if the number of disks is an odd number it will be the first movement to C and if the number of disks is an even number it will be the first movement to B

I'll go back to the code again and I'll make some changes. 

````js
function hanoiAlgo(n, from, to, aux) {
      if (n === 1) {
        console.log(`Move disk ${n} From ${from} To ${to}`);
      }
      hanoiAlgo(n - 1, from, aux, to);
    }

hanoiAlgo(2, "A", "C", "B");
````
You see, I've made the funcuion call itself out again.  
This concept in programming is called `Recursion`.  

I used this method because I want to move the first disk and not the second disk and I switched the argument to direct the first movement to B because the number of disks is an even number.

I also want to reach the first disk no matter how many disks

*When trying to run the previous code I will find that it does not work but why?*  
Because in the case of calling the function itself there must be a case to stop itself and otherwise it will not work.

So I'm going to modify the code again:
````js
function hanoiAlgo(n, from, to, aux) {
      if (n === 1) {
        console.log(`Move disk ${n} From ${from} To ${to}`);
        return;
      }
      hanoiAlgo(n - 1, from, aux, to);
    }
    
hanoiAlgo(2, "A", "C", "B");
````

You will find that the result of running the function is as follows:  
```Move disk 1 From A To B```  

I'll edit the code to move the second disk:  
````js
function hanoiAlgo(n, from, to, aux) {
      if (n === 1) {
        console.log(`Move disk ${n} From ${from} To ${to}`);
        return;
      }
      hanoiAlgo(n - 1, from, aux, to);
      console.log(`Move disk ${n} From ${from} To ${to}`);
    }

hanoiAlgo(2, "A", "C", "B");
````  

You will find that the result of running the function is as follows:  
```Move disk 1 From A To B```  
```Move disk 2 From A To C```  

I'm going to use Recursion for the second time because (n = 2) and I want to move the first disk and also I want to move it from B to C and not from A to C.  

I'll edit the code to move the third disk:  
````js
function hanoiAlgo(n, from, to, aux) {
      if (n === 1) {
        console.log(`Move disk ${n} From ${from} To ${to}*`);
        return;
      }
      hanoiAlgo(n - 1, from, aux, to);
      console.log(`Move disk ${n} From ${from} To ${to}`);
      hanoiAlgo(n - 1, aux, to, from);
    }

hanoiAlgo(2, "A", "C", "B");
````  

You will find that the result of running the function is as follows:  
```Move disk 1 From A To B```  
```Move disk 2 From A To C```  
```Move disk 1 From B To C```  

## Conclusion
Using Recursion makes the algorithm deal with any number of disks as efficiently as possible.

## Recommendation
Solving any problem comes from the bottom and not looking at the result but by dividing the requirements into microtasks.
