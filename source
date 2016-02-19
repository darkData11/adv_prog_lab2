// Syed Hassaan Tauqeer - 08126 _ BSCS-3A

#include<iostream>
#include<stdlib.h>
#include<vector>
#include<time.h>
using namespace std;

/*simple matrix multiplication for any sized vectors*/
class multiply
{
public:
	vector<vector<int>> standard( vector<vector<int>>a, vector<vector<int>>b, int a_r, int a_c, int b_r, int b_c )
	{
		vector<vector<int>> ans(a_r, vector<int>(b_c));
		int sum = 0;

		for(int i=0; i<a_r; i++)
		{
			for(int j=0; j<b_c; j++)
			{
				sum = 0;
				for(int k=0; k<b_r; k++)
				{
					sum += a[i][k] * b[k][j];
				}
				ans[i][j] = sum;
			}
		}

		return ans;
	}
};


/////////strass begin//////////////

/* strassen class for the squared matrices of powers of two*/
 class strass {
    //=========================Strassen dependencies============================
 public:

     vector<vector<int>> sub(vector<vector<int>>& a, vector<vector<int>>& b) // subtraction
    {
        int n = a.size();

        vector<vector<int>> c (n, vector<int>(n));

        for(int i=0; i<n; i++)
        {
            for (int j=0; j<n; j++)
            {
                c[i][j] = a[i][j] - b[i][j];
            }
        }

        return c;
    }

    vector<vector<int>> add(vector<vector<int>>& a, vector<vector<int>>& b)//addition
    {
        int n = a.size();

        vector<vector<int>> c(n, vector<int>(n));

        for(int i=0; i<n; i++)
        {
            for (int j=0; j<n; j++)
            {
                c[i][j] = a[i][j] + b[i][j];
            }
        }

        return c;
    }

    void split(vector<vector<int>>& P, vector<vector<int>>& C, int iB, int jB)

    {

        for(int i1 = 0, i2 = iB; i1 < C.size(); i1++, i2++)

            for(int j1 = 0, j2 = jB; j1 < C.size(); j1++, j2++)

                C[i1][j1] = P[i2][j2];

    }

    void join(vector<vector<int>>& C, vector<vector<int>>& P, int iB, int jB)

    {

        for(int i1 = 0, i2 = iB; i1 < C.size(); i1++, i2++)

            for(int j1 = 0, j2 = jB; j1 < C.size(); j1++, j2++)

                P[i2][j2] = C[i1][j1];

    }

    
    vector<vector<int>> s_mult(vector<vector<int>>& a, vector<vector<int>>& b)
    {
        int n = a.size();
        vector<vector<int>> resultnt(n, vector<int>(n));

        if(n == 1)// base case for recursion
        {
            resultnt[0][0] = a[0][0] * b[0][0];
        }

        else
        {
			
            vector<vector<int>> a11 (n/2, vector<int>(n/2)); //quadrant creation
            vector<vector<int>> a12 (n/2, vector<int>(n/2));
            vector<vector<int>> a21 (n/2, vector<int>(n/2));
            vector<vector<int>> a22 (n/2, vector<int>(n/2));

            vector<vector<int>> b11 (n/2, vector<int>(n/2));
            vector<vector<int>> b12 (n/2, vector<int>(n/2));
            vector<vector<int>> b21 (n/2, vector<int>(n/2));
            vector<vector<int>> b22 (n/2, vector<int>(n/2));


            //break in quadrants
            split(a, a11, 0, 0);
            split(a, a12, 0, n/2);
            split(a, a21,n/2, 0);
            split(a, a22, n/2, n/2);

            split(b, b11, 0, 0);
            split(b, b12, 0, n/2);
            split(b, b21,n/2, 0);
            split(b, b22, n/2, n/2);


            vector<vector<int>> m1 = s_mult(add(a11, a22), add(b11, b22)); //strassen formula
            vector<vector<int>> m2 = s_mult(add(a21, a22), b11);
            vector<vector<int>> m3 = s_mult(a11, sub(b12, b22));
            vector<vector<int>> m4 = s_mult(a22, sub(b21, b11));
            vector<vector<int>> m5 = s_mult(add(a11, a12), b22);
            vector<vector<int>> m6 = s_mult(sub(a21, a11), add(b11, b12));
            vector<vector<int>> m7 = s_mult(sub(a12, a22), add(b21, b22));


            vector<vector<int>> c11 = add(sub(add(m1, m4), m5), m7); // still the strassen formula
            vector<vector<int>> c12 = add(m3, m5);
            vector<vector<int>> c21 = add(m2, m4);
            vector<vector<int>> c22 = add(sub(add(m1, m3), m2), m6);


            join(c11, resultnt, 0, 0);
            join(c12, resultnt, 0, n/2);
            join(c21, resultnt, n/2, 0);
            join(c22, resultnt, n/2, n/2);

        }
        return resultnt;
    }
};


////////////////////////////////////

int main (void)
{
	int a_r,a_c;
    int b_r,b_c;

	clock_t t; // clock variable

	cout<<"\nMatrix A row:";
	cin>>a_r;

	cout<<"\nMatrix A column:";
	cin>>a_c;

	cout<<"\nMatrix B row:";
	cin>>b_r;

	cout<<"\nMatrix B column:";
	cin>>b_c;

	vector<vector<int>> a (a_r, vector<int>(a_c)); 

	for(int i=0; i<a_r; i++)
	{
		for(int j=0; j<a_c; j++)
		{
			a[i][j] = rand() % 30;
		}
	}// randomn A has been generated at this point.

	if(a_c != b_r)
	{
		cout<<"\n Invalid ! Dimension error, can't multiply."<<endl;
	}

	else
	{
		vector<vector<int>> b (b_r, vector<int>(b_c));
		for(int i=0; i<b_r; i++)
		{
			for(int j=0; j<b_c; j++)
			{
				b[i][j] = rand() % 30;
			}
		}// generated B 

		cout<<"A:"<<endl;
		for(int i=0; i<a_r; i++)
		{
			for(int j=0; j<a_c; j++)
			{
				cout<<a[i][j]<<"\t";
			}
			cout<<"\n";
		}

		cout<<"B:"<<endl;
		for(int i=0; i<b_r; i++)
		{
			for(int j=0; j<b_c; j++)
			{
				cout<<b[i][j]<<"\t";
			}
			cout<<"\n";
		}


		multiply m;
		vector<vector<int>> product (a_r, vector<int>(b_c)); 
		//starting time to simple
		t = clock();

		product = m.standard(a, b, a_r, a_c, b_r, b_c);

		t = clock() - t;// end clock
		cout<<"\nSimple Multiplication:"<<endl;
		for(int i=0; i<a_r; i++)
		{
			for(int j=0; j<b_c; j++)
			{
				cout<<product[i][j]<<"\t";
			}
			cout<<"\n";
		}
		cout<< "\nTime for simple multiplication:"<<t<<endl;

		//strassen call
		strass s;
		t = clock();
		product = s.s_mult(a, b);
		t = clock() - t;// end clock

		cout<<"\nStrassen Multiplication:"<<endl;
		for(int i=0; i<a_r; i++)
		{
			for(int j=0; j<b_c; j++)
			{
				cout<<product[i][j]<<"\t";
			}
			cout<<"\n";
		}
		cout<< "\nTime for strassen multiplication:"<<t<<endl;

		cout<<"\n\n/*----------------------------------------------TESTS-------------------------------------------------------------------------*/"<<endl;
		/*----------------------------------------------TESTS-------------------------------------------------------------------------*/
		vector<vector<int>> alpha (2, vector<int>(2));
        alpha [0][0] = 1;
        alpha [0][1] = 1;
        alpha [1][0] = 1;
        alpha [1][1] = 1;

        vector<vector<int>> beta (2, vector<int>(2));
        beta[0][0] = 2;
        beta[0][1] = 2;
        beta[1][0] = 2;
        beta[1][1] = 2;

        vector<vector<int>> ans (2, vector<int>(2));
        ans[0][0] = 4;
        ans[0][1] = 4;
        ans[1][0] = 4;
        ans[1][1] = 4;

		vector<vector<int>> check (2, vector<int>(2));
		check = m.standard(alpha, beta, 2, 2, 2, 2);

		for (int i = 0; i < 2; i++) { // simple matrix multiplication test!
            for (int j = 0; j < 2; j++) {
				if(ans[i][j] != check[i][j])
				{
					cout<<"\n Simple matriz multiplication not working properly."<<endl;
				}
				else
				{
					cout<<"Simple Matrix Multiplication works perfectly!"<<endl;
				}
            }
        }


		check = s.s_mult(alpha, beta);// strassen multiplication
		for (int i = 0; i < 2; i++) { 
            for (int j = 0; j < 2; j++) {
				if(ans[i][j] != check[i][j])
				{
					cout<<"\n Strassen matriz multiplication not working properly."<<endl;
					break;
				}
				else
				{
					cout<<"Strassen Matrix Multiplication works perfectly!"<<endl;
				}
            }
        }
		/*----------------------------------------------TESTS-------------------------------------------------------------------------*/


	}// else ends

	



	system("pause");
	return 0;
}
