# multiples-of-3
If we list all the natural numbers below  that are multiples of  or , we get  and . The sum of these multiples is .

Find the sum of all the multiples of  or  below .

Input Format

First line contains  that denotes the number of test cases. This is followed by  lines, each containing an integer, .

Constraints

Output Format

For each test case, print an integer that denotes the sum of all the multiples of  or  below .

Sample Input 0

2
10
100
Sample Output 0

23
2318
Explanation 0

For , if we list all the natural numbers below  that are multiples of  or , we get  and . The sum of these multiples is .

Similarly for , we get .
-------------------------------------------------------------------------------------------------------------------------------------------------------

#include <cmath>
#include <cstdio>
#include <vector>
#include <iostream>
#include <algorithm>
#include <map>

using namespace std;
 
vector<int> primes = {2};
vector<unsigned long> sums;

map<int, unsigned long> temp = {{1, 0}, {2, 2}};


void Primes(int n)
{    
    unsigned long sum = 2;
    int p = 2, last_p = 2;
    vector<bool> sieve(n+10);            
            
    while(1)
    {        
        for(int i=2; p*i < sieve.size(); i++)
        {
            if(sieve[p*i] == false) sieve[p*i] = true;
        }
        
        for(int i=p+1; i < sieve.size(); i++)
        {
            if(sieve[i] == false) 
            {
                p = i;
                sum += p;
                temp[p] = sum;
                primes.push_back(p);
                
                break;
            }
        }
        if(p > n) break; 
    }
    out:
    int prev = 0;
    sums.reserve(n+p);
    
    for(auto it : primes)
    {        
        for(int i = prev; i<it; i++)
        {
            sums.push_back(temp[prev]);
        }
        prev = it;
    }    
    sums.push_back(temp[prev]);
    return;
}


int main() 
{
    int t;
    cin >> t;
    
    Primes(1000000);
    
    while(t--)
    {
        int n;
        cin >> n;

        cout << sums[n] << endl;
    }
    return 0;
}
---------------------------------------------------------------------------------------------------------
