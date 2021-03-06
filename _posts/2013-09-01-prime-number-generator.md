---
layout: post
title: Prime Number Generator - Sieve of Eratosthenes implementation in C
---

Fast method to find prime numbers: Sieve of Eratosthenes

For explanation and details please visit [Sieve_of_Eratosthenes](http://en.wikipedia.org/wiki/Sieve_of_Eratosthenes)

My C implementation of Sieve of Eratosthenes:

{% highlight c %}
// Comments

#include "stdio.h"
#include "stdbool.h";
#include "stdlib.h";
#include "string.h";

void prime_no_in_range_simple(int start, int end);
void prime_no_in_range_sieve(int start, int end);

int main()
{
    int noItems;
    int i;

    printf("Enter no. of items to be entered: \n");
    scanf("%d",&amp;noItems);

    int input[noItems][2];

    for (i =0;i!=noItems ;i++ ){
        scanf("%d",&amp;input[i][0]);
        scanf("%d",&amp;input[i][1]);
    }

    for (i=0;i!=noItems ;i++ ) {
        prime_no_in_range_sieve(input[i][0], input[i][1]);
        printf("\n");
    }

    return 0;
}

void prime_no_in_range_sieve(int start, int end)
{
    const int limits = end +1;
    int number = end;
    int *db = (int*)malloc(limits*sizeof(int));


    int loop;
    for (loop =2; loop&lt;limits; loop++){
        db[loop] = 1;
    }


    int multiples;
    int divisor=2;
    while(divisor &lt; number)
    {
        for (multiples = divisor*2; multiples &lt;= (number); multiples= (multiples+divisor)) {
            db[multiples] = 0;
        }
        divisor++;
    }
    for (loop = 2; loop &lt; (number); loop++) {
        if((db[loop] == 1) &amp;&amp; (loop &gt;= start))
            printf("%d\n",loop);
    }
    printf("\n");
}

void prime_no_in_range_simple(int start, int end)
{
    int i;
    for (i=start; i&lt;=end; i++){
        int number =i;
        bool search = true;
        while(search)
        {
            if (number%2 == 0){
                search = false;
                break;
            } else {
                int divisor =3;
                while(divisor &lt;= (number/2)){
                    if (number%divisor == 0){
                        search = false;
                        break;
                    }
                    divisor = divisor+2;
                }
                break;
            }
        }
        if (search == true)
            printf("%d\n", number);
    }
}
{% endhighlight %}
Copy of code is at [GIST](https://gist.github.com/siddharthbhal/6404893)
