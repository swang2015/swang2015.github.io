---
layout: post
title:  "C++ Pointer Quick Tutorial"
date:   2015-02-10 16:00:00 -0800
categories: misc
tags: c++ feature
---

## Understanding Pointers

Programming is concerned with manipulating data which is normally located in memory. Except using _identifier_ to access data, in C++ programs there is another way to approach data which is based on its address in memory. In memory each variable has unique address. _Pointer_ can store such memory addresss and the variable which the pointer refers to can be calculated and modified. Pointer itself is a kind of variable so can be refered to as well.

With pointer you don't need to make copy of data for calculation. It's efficient handling large amounts of data. Pointers are essential for many data structures such as linked list or binary tree.

C++ program is executed with two forms of memory. _Stack_ is the memory set aside as scratch space for a thread of execution, while _heap_ is free-floating region of memory and is much larger than the stack. Using pointers allows us to track this part of dynamically allocated memory. Please remember to release the memory when you no longer need it otherwise they will exhaust memory and cause _memory leak_.

## Using Pointers

##### Delaring pointer

a `*` is the key of declaring pointer. You can declare pointers and nonpointers at the same time.

```c++
int *pointer, nonpointer;
int *pointer1, *pointer2;
```

##### Pointing to an address

`&` is called **address-of** operator which is used to retrieve address of a variable.

```c++
int x, *p_x;
p_x = &x;
```

Notice that pointer could point to anything without assigning an address, this is called a _dangling pointer_ and may lead to crash of program. You should always initialize pointers. If you can't do that immediately, you can make a pointer point to `NULL` so that you know it's unintialized yet.

##### Dereferencing pointer

A pointer is refering to some data, so we need to _dereference_ the pointer to get the data. `*` is the **dereference** operator. Use `*p_x` just as using an identifier.

```c++
*p_x = 5;
cout << *p_x << endl;
```

##### Passing pointers to functions

If data needs to be modified in a function, we should pass it by pointer. If we pass data by identifier the modification happens within that function but won't change the original data because it just creates copies of the data. Passing data to a function via pointers:

```c++
void swap(int *p_x, int *p_y) {
	int tmp = *p_x;
	*p_x = *p_y;
	*p_y = tmp;
}
```

##### Reference

There's an easier way to write a swap function with _references_:

```c++
void swap(int &x, int &y) {
	int tmp = x;
	x = y;
	y = tmp;
}
```

Reference is a lite version of pointer. Reference can refer to a variable, but it permenantly refers to the same variable and it must always refers to valid address.

```c++
int x;
int &r_x = x;
```

##### Pointer to structure

To access the field of a structure through pointer, you use `->` operator.

```
p_struct->field;
```

## Dynamic Memory Allocation

The basic steps for dynamic memory allocation are:
- allocate memory using keyword `new`
- operate with this memory
- deallocate memory using  keyword `delete`
Here's the basic syntax.

```c++
int *p_i = new int;
delete p_i;

*p_i = new int[5];
delete[] p_i;
```

In the second case, the system allocates space for five ints and returns pointer to the first element to `p_i`. Thus, the first element can be accessed by `*p_i` or `p_i[0]`, the second element can be accessed by `*(p_i+1)` or `p_i[1]`, and so on. Even a pointer to array acts just like an array, they are still different types.

Remember if the pointer is not pointing to a specific address any more, it becomes _dangling_ and should be assigned to `NULL`.

##### Pointer to pointer

Pointer can be refered since pointer is variable. The declaration of a pointer-to-pointer looks like below. You can use them when you need to return a pointer to some memory on the heap, but not using the return value.

```c++
int **p;

int get1024HeapMemory(int **p) {
	*p = malloc(1024);      // this is to allocate specific amount of memory.
	if(*p == 0)
		return -1;
	else 
		return 0;
}
```

