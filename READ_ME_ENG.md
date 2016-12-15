This program is in the C# programming language,
sorts the array by the pyramid-tournament sorting algorithm,
which has two main stages - the first stage is the transformation of an array to a primary pyramidal heap / binary tree,
where the main action is the selection of the smallest element of the array to the top of the composed pyramid and
formation of tournament leaves of a binary tree; the second stage is sorting the array in three steps,
where the first stage is the smallest elements of the array and are transferred to the highest levels of the pyramid from the top 50%
all elements of the compiled binary tree, the following two actions are processed by 25%
all elements of a composed binary tree.
This method is well combined with caching and memory swapping, performing the sorting in three steps,
although it does not have a proven worst-case performance estimate.

The main module PiramidalnoTurnirnayaSortirovka contains the main function:
main - performing the task of displaying the elements of the array before sorting,
the data about which is taken from the Vvod method and passed to the Tourn method for sorting.
This method takes data about the sorted array from the Tourn method.
and also produces console output of an already sorted array from the Vyvod method.

This program has the following interacting classes:
1) Program - containing the main function main;
2) Consts - a static class containing a constant number of array elements to sort;
3) Sort - contains methods for sorting an array with a pyramid-tournament sorting algorithm.

Methods with which the main function works:
1) reading the constant of the number of elements of the array by the method A [];
2) construction of a pyramidal heap / binary tree from the source array using the Initialize -
performs the first two steps to build 75% of the pyramid pile / binary tree from the source array,
identifying a smaller element in each tournament pair of the same level,
thus leaving the lowest level of the pyramid pile / binary tree unseeded.
For the construction of the pyramid heap, the leaf data and its node indices are taken,
required in the complete binary tree from the Tourn method.
This method transfers data about the new location of the array elements to the Readjust method,
and together with the data on the new location of the elements of the array, the number of leaves,
required in full binary tree in the Tourn method;
3) completion of the pyramidal heap / binary tree from the original array using the Readjust method -
performs the last action for the completion of the pyramidal heap / binary tree from the source array.
To complete the pyramid heap, the leaf data and its node indices are taken,
required in a complete binary tree from the Tourn method, and passed to the Tourn method
data on the new location of the elements of the array;
4) sorting the constructed pyramidal pile / binary tree using the pyramid-tournament sorting method
Tourn - sorts the constructed pyramid pile using the pyramid-tournament sorting method,
repeats operations of moving elements represented by the array root,
in the next position with a smaller index in the array and rewrites the binary tree.
Pass the sorted array to the main function main;
5) Vvod method - creates an initial array and assigns random values ​​to it,
transfers data about the source array of the main function main;
6) Vyvod method - takes data about the sorted array from the Tourn method and shows the sorted array.