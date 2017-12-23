#include <pthread.h>
#include <iostream>
#include <cstdlib>
#include <string>
#include <stdio.h>
#include <stdlib.h>
#include <fstream>
using namespace std;

#define ARRAYSIZE   1000
int arr[ARRAYSIZE],tarr[ARRAYSIZE];

//int arr[] = {4,2,5,7,6,9,8,3};

struct app_struct 
{
    int num_of_threads;
    int answer;
    int start;
    int end;
};

void* app_sum(void* arg)
{
    struct app_struct *arg_struct =
			(struct app_struct*) arg;
    int i = 0;
    //i = arg_struct->
	int sum = 0;
	
	for (i = arg_struct->start; i < arg_struct->end; i++)
	{
		sum += arr[i];
	}
	
	arg_struct->answer = sum;

	pthread_exit(0);
}

int main(int argc, char** argv)
{  
    //x is each integer in the input file
    int x;
    
    //total sum of the content of the array
    int totalSum = 0;
    
    //length of the input file
    int inLength;
    
    //read in input file
    ifstream inFile;
    inFile.open(argv[1]);
    if (!inFile) {
        cout << "Unable to open file";
        exit(1); // terminate with error
    }

    inFile >> inLength;
    
    // j helps to add integer from input file to the array
    int j = 0;
    
    while (inFile >> x) {
        arr[j] = x;
        j++;
    }
    
    inFile.close();
    
    //Number of threads we want to create
    int num_args = atoi(argv[2]);
  
    
    struct app_struct args[num_args];
    
    //k is the length of each array
    int k = 0;
    cout << "inlength :" << inLength << "num args: " << num_args << endl;
    int ab = inLength / num_args;
    int bc = inLength % num_args;
    //Launch thread 
    
    pthread_t tids[num_args];
    
    for(int i = 0; i < num_args; i++)
    {
        args[i].start = k;
        
        if(bc > i)
        {
            args[i].end = k+ab+1;
            cout << "greater" << endl;
        }
        else
        {
            args[i].end = k+ab;
            cout << "less" << endl;
        }
        
        pthread_attr_t attr;
        pthread_attr_init(&attr);
        pthread_create(&tids[i], &attr, app_sum, &args[i]);
        
        if(bc > i)
        {
            k = k + ab + 1;
        }
        else
        {
            k = k + ab;
        }
        cout << "  k: " << k<< endl;
    }
    
    // Wait until thread is done its work
	for (int i = 0; i < num_args; i++) {
		pthread_join(tids[i], NULL);
		printf("Sum for thread %d is %i\n",
				i, args[i].answer);
	    
	}
	for (int i = 0; i < num_args; i++)
	 {
	    tarr[i] = args[i].answer;
	   // cout <<  args[i].answer; 
	 }
	 
	 for (int i = 0; i < num_args; i++)
	 {
	    totalSum += tarr[i];
	 }
    
    printf("Total sum is %i\n ", totalSum);
    
    
    return 0;
}
