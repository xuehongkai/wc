#include<iostream>
#include<fstream>
#include<cctype>
#include<string>

using namespace std;

int charc(string line, int charcount);
int wordc(string lin, int wordcount);
int sentc(string line, int sentcount);


int main()
{
	ifstream inFile;
	string filename;
	string fuc, line;
	cout << "wc.exe";
	while (cin >> fuc)
	{
		int wordcount = 0, sentcount = 0, charcount = 0;
		cin >> filename;
		inFile.open(filename.c_str(),  ios::in);
		if (!inFile){
			cout << "EXEC failure" << endl;
		}
		else{
			if (fuc == "-c"){
				while (getline(inFile, line)){
					charcount = charc(line, charcount);
				}
				cout << "letter: " << charcount << endl;
			}
			else if (fuc == "-w"){
				while (getline(inFile, line)){
					wordcount = wordc(line, wordcount);
				}
				cout << "word: " << wordcount << endl;
			}
			else if (fuc == "-s"){
				while (getline(inFile, line)){
					sentcount = sentc(line, sentcount);
				}
				cout << "sentence: " << sentcount << endl;
			}
			else{
				cout << "There is no this function  \ " << fuc << " \ "<<endl;
			}
		}
		inFile.close();
		cout << "wc.exe ";
	}
	return 0;
}

int charc(string line, int charcount)
{
	int length;
	length = line.size();
	charcount = charcount + length;
	return charcount;
}

int wordc(string line, int wordcount)
{
	int length, judge = 0;
	length = line.size();
	for (int i = 0; i < length; i++){
		if (isalpha(line[i]) && judge == 0){
			++wordcount;
			judge = 1;
		}
		if (!isalpha(line[i]) && judge == 1){
			judge = 0;
		}
	}
	return wordcount;
}

int sentc(string line, int sentcount)
{
	int length, judge = 0;
	length = line.size();
	string s1(".");
	string s2("!");
	string s3("?");
	for (int i = 0; i < length; i++){
		if (isalpha(line[i + 1]) || !(line.compare(i + 1, 1, s1))
			|| !(line.compare(i + 1, 1, s2)) || !(line.compare(i + 1, 1, s3))){
			judge = 1;
		}
		else judge = 0;
		if ((!(line.compare(i, 1, s1)) || !(line.compare(i, 1, s2))
			|| !(line.compare(i, 1, s3))) && judge = 0){
			++sentcount;
			judge = 0;
		}
	}
	return sentcount;
}
