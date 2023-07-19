#include <iostream>
#include <vector>

using namespace std;

namespace my_lib {

	
	template <typename T>
	

	class Vector
	{
	private:
		
		T* m_pArray;
		int  m_nCap;
		int  m_nSize;

	private:
		/*void IncreaseSize(int nCopyIndex = 0)
		{

		}

		void DecreaseSize()
		{

		}*/
		
		void array_size_increase()      
	
		{
			if (m_nCap == m_nSize)
			{
				int old_nCap = m_nCap;
				m_nCap *= 2;
				T* new_arr = new T[m_nCap];

				for (int i = 0; i < old_nCap; ++i)
					new_arr[i] = m_pArray[i];

				delete[] m_pArray;
				m_pArray = new_arr;
			}
		}

	public:
		Vector()
			: m_pArray(nullptr),
			m_nCap(0),
			m_nSize(0)
		{
			//mul_2(5);
			//mul_2(5.5);
		}

		Vector(int nSize, int nValue = 0)
			: m_pArray(nullptr),
			m_nCap(0),
			m_nSize(0)
		{
			if (nSize <= 0)
				return;
			m_nSize = m_nCap = nSize;
			//m_pArray = new int[nSize] {0};
			m_pArray = new T[nSize] {nValue};
		}

		Vector(T* arr1, int n1)
			: m_pArray(nullptr),
			m_nCap(0),
			m_nSize(0)
		{
			if (arr1 == nullptr || n1 <= 0)
				return;
			m_nCap = m_nSize = n1;
			m_pArray = new T[n1];
			for (int i = 0; i < n1; ++i)
			{
				m_pArray[i] = arr1[i];
			}
		}

		~Vector()
		{
			if (m_pArray != nullptr)
			{
				delete[] m_pArray;
				m_pArray = nullptr;
				m_nCap = 0;
				m_nSize = 0;
			}
		}

		void print() const
		{
			for (int i = 0; i < m_nSize; ++i)
			{
				std::cout << m_pArray[i] << " ";
			}
			cout << "\n";
		}


		void push_back(T number1)
		{
			if (m_pArray == nullptr)
			{
				m_pArray = new T[1];
				m_nCap = 1;
			}
			array_size_increase();
		/*
			if (m_nSize == m_nCap)
			{
				const int nOldCap = m_nCap;
				m_nCap *= 2;
				//     arr_>
				int* pNewArr = new int[m_nCap] {0}; // // pNewArr->| | | | |
				for (int i = 0; i < nOldCap; ++i)
					pNewArr[i] = m_pArray[i];

				delete[] m_pArray;
				m_pArray = pNewArr;
			}
		*/
			m_pArray[m_nSize] = number1;
			m_nSize++;

			print();
		}

		T& operator[](int nIndex)   //const miatel  T const &
		{
			return m_pArray[nIndex];
		}
		
		T& operator[](int nIndex) const
		{
			return m_pArray[ nIndex];
		}

		Vector operator+(Vector const& other)
		{
			if (m_nSize != other.m_nSize)
				return Vector();

			Vector result(other);

			for (int i = 0; i < m_nSize; ++i)
				result.m_pArray[i] += m_pArray[i];

			return result;
		}


		void push_front(T number2)
		{
			if (m_pArray == nullptr)
			{
				m_pArray = new T[1];
				m_nCap = 1;
			}

			if (m_nSize == m_nCap)
			{
				int old_cap = m_nCap;
				m_nCap *= 2;

				T* new_arr = new T[m_nCap];
				for (int i = 0; i < old_cap; ++i)
					new_arr[i + 1] = m_pArray[i];


				delete[] m_pArray;
				m_pArray = new_arr;
			}
			else
			{
				for (int i = m_nSize - 1; i >= 0; --i)
					m_pArray[i + 1] = m_pArray[i];
			}
			m_nSize++;
			m_pArray[0] = number2;

			print();

		}

		void pop_back()
		{
			if (m_pArray == nullptr)
				return;

			m_nSize--;

			if (m_nCap / m_nSize == 2)
			{
				m_nCap /= 2;
				T* new_arr = new T[m_nCap];
				for (int i = 0; i < m_nCap; ++i)
					new_arr[i] = m_pArray[i];

				delete[] m_pArray;
				m_pArray = new_arr;
			}
			print();
		}

		void pop_front()
		{
			if (m_pArray == nullptr)
				return;

			for (int i = 1; i < m_nSize; ++i)
			{
				m_pArray[i - 1] = m_pArray[i];

			}
			m_nSize--;

			if (m_nCap / m_nSize == 2)
			{
				m_nCap /= 2;
				T* new_arr = new T[m_nCap];
				for (int i = 0; i < m_nCap; ++i)
					new_arr[i] = m_pArray[i];

				delete[] m_pArray;
				m_pArray = new_arr;
			}

			print();
		}

		void remove(int index)
		{
			if (index >= m_nSize || index < 0 || m_pArray == nullptr)
				return;
			if (index == m_nSize - 1)
				m_nSize--;
			else
			{
				for (int i = index; i < m_nSize - 1; ++i)                  //verjin tarri hamar i+1  ??
					m_pArray[i] = m_pArray[i + 1];

				m_nSize--;
			}

			if (m_nCap / m_nSize == 2)
			{
				m_nCap /= 2;
				T* new_arr = new T[m_nCap];
				for (int i = 0; i < m_nCap; ++i)
					new_arr[i] = m_pArray[i];

				delete[] m_pArray;
				m_pArray = new_arr;
			}

			print();

		}

		void insert(int index, T element)    // T vector
		{
			if (index > m_nSize-1 || index < 0)              
				return;
			if (m_pArray == nullptr)
			{
				m_pArray = new T[1];
				m_nCap = 1;
				m_pArray[0] = element;
			}
			else
				array_size_increase();
				
			/*
				if (m_nCap == m_nSize)
				{
					int old_nCap = m_nCap;
					m_nCap *= 2;
					int* new_arr = new int[m_nCap];

					for (int i = 0; i < old_nCap; ++i)
						new_arr[i] = m_pArray[i];

					delete[] m_pArray;
					m_pArray = new_arr;
				}
			*/
			m_nSize++;

			for (int i = m_nSize - 1; i >= index; --i)
				m_pArray[i] = m_pArray[i - 1];

			m_pArray[index] = element;


			print();

		}

		void insert(int index, vector<T>& a)
		{
			if (index >= m_nSize || index < 0)
			{
				return;
			}
			if (m_pArray == nullptr)
			{
				m_pArray = new T[a.size()];
				m_nCap = a.size();
				for (int i = 0; i < a.size(); ++i)
				{
					m_pArray[i] = a[i];
				}
			}
			if (m_nSize == m_nCap || (m_nCap - m_nSize) <= a.size())
			{
				int Old_Size = m_nSize;
				m_nSize += a.size();
				m_nCap = m_nSize;
				T* new_arr = new T[m_nSize];
				for (int i = 0; i < Old_Size; ++i)
				{
					new_arr[i] = m_pArray[i];
				}
				delete[] m_pArray;
				m_pArray = new_arr;
			}
			
			for (int i = index; i < m_nSize; ++i)
			{
				m_pArray[i + a.size()] = m_pArray[i];
			}
			for (int i = 0; i < a.size(); ++i)
			{
				m_pArray[index] = a[i];
				++index;
			}
			m_nSize += a.size();
		}
	};

	/*/
	int* f(int* p)
	{
		if (p != nullptr)
			return p;
		else
			p = new int[1];
	}
	*/
	
}
/*
class A
{
public:
	A() = default;

public:
	vector<string>* GetData() const
	{
		if (m_pArray == nullptr)
			m_pArray = new vector<string>();

		auto it = m_pArray->begin();

		return m_pArray;
	}

private:
	mutable vector<string>* m_pArray = nullptr;
};
*/
using namespace my_lib;

int main()
{
	//const A _a;
	//_a.GetData();

	//int aaa = 33;
	//int* p = nullptr;
	
	Vector <double> a;
	//a.push_back(45);
	//a.push_back(55);
	a.push_back(65);
	a.push_back(75);
	a.push_back(85);
	a.push_back(95);

	Vector<double> b;
	////a.push_back(45);
	////a.push_back(55);
	b.push_back(65);
	b.push_back(75);
	b.push_back(85);
	b.push_back(95);

	//b[3] = 55;

//	Vector< > sum = a + b;


	a.push_front(35);
	a.pop_front();
	a.remove(2);
	a.remove(6);
	//a.insert(3, 164);
	a.insert(2,5);

	//std::vector<double> stdA = { 6,5.5,7,4,56,7,8,546,7345 };

	//for (int i = 0; i < stdA.size(); ++i)
	//	cout << stdA[i];

	/*for (int i = 0; i < a.size(); ++i)
		cout << a[i];*/
		/*
		*
		*
		*
			int m_nCap;
			cout << "Inset array size ";
			cin >> m_nCap;
			int m_pArray[100];
			cout << "Insert array elements \m_nCap";
			for (int i = 0; i < m_nCap; ++i)
			{
				cin >> m_pArray[i];
			}

			Vector b(m_pArray, m_nCap);

			Vector c(500, 96);
			c.push_back(97);

			Vector obj1(m_pArray,m_nCap);
			obj1.remove(5);

		*/

}
