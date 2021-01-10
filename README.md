# Task2
#include <iostream>
#include <fstream>
#include <sstream>
#include <string>
#include <vector>

using namespace std;

int main() 
{// zmienne
  string quest, line, word, ans, test;
	vector<int> y, n, ind;
	vector<string> info;
	int inty, intn, intind, x=0, rescopyx;
// file scan
	ifstream justfile("file.txt");
	while(!justfile.eof())
  {
		getline(justfile, line);
		istringstream ss(line);
	  ss >> intind >> inty >> intn;
		quest = "";
		while (ss >> word)
    {
			if(quest.length() == 0) quest = word;
			else quest += " " + word;
		}
		ind.push_back(intind);
		y.push_back(inty);
		n.push_back(intn);
		info.push_back(quest);
	}
	justfile.close();
	//chek answer
	while(y[x] != 0 || n[x] != 0)
  {
  	cout << info[x] << endl;
    rescopyx = x;
  	cout << "y or n?" << endl;
  	cin >> test;
  	if(test == "y") x = y[x]; 
    else if(test == "n") x = n[x];
    else 
    {
      cout << "Sorry I do not understand";
      return 0;
    }
	}
	cout << "I'm Guessing correct answer is: " << info[x] << "\n" << "Am I right?" <<"\n"<<"y or n"<< endl;
	cin >> test;
	if (test == "y") cout << "Xexexe, this time I win" << endl;
	else if (test == "n")
  {
	cout << "What is your answer?" << endl;
  cin.ignore();// answer (word)
	getline(cin,ans);
	cout << "Add a question for your answer" << endl;
	getline(cin,quest);//question (word)
  y[rescopyx]=ind.size();
  //question ind
  ind.push_back(ind.size());
	y.push_back(ind.size());
	n.push_back(x);
	info.push_back(quest);
  //answer ind
  ind.push_back(ind.size());
	y.push_back(0);
	n.push_back(0);
	info.push_back(ans);
  //output
  ofstream justfile;
  justfile.open("file.txt");
  for(int x=0;x<=ind.size()-1;x++) justfile << ind[x] << " " << y[x] << " " << n[x] << " " << info[x] << endl;
  justfile.close();
	}
  else 
  {
    cout << "Sorry I do not understand";
    return 0;
  }
	return 0;
}
