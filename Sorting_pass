#include <iostream>
#include <ctime>
#include <string>
#include <fstream>
#include <vector>
#include <algorithm>
#include <Windows.h>

using namespace std;

void Text_handler(string& path_open, string& path_create, string& name) {
	string to_delete{ '"' };
	string expansion{ ".txt" };
	int counter = 0;
	for (int i = 0; i < path_open.size(); i++) {
		if (path_open[i] == '\\') {
			path_open[i] = '/';
			counter = i;
		}
	}
	size_t pos1{ path_open.find(to_delete) };
	while (pos1 != string::npos) {
		path_open.erase(pos1, to_delete.length());
		pos1 = path_open.find(to_delete, pos1 + to_delete.length());
	}
	path_create = path_open;
	int temp = path_create.size() - (counter);
	path_create.erase(counter, temp);
	path_create.insert(path_create.size(), name);
	path_create.insert(path_create.size(), expansion);
	cout << path_open << endl;
	cout << path_create << endl;

}

//void Sort_array_default(vector<int>& array_default) {
//
//}


int main()
{
	setlocale(LC_ALL, "ru");
	SetConsoleCP(1251);
	SetConsoleOutputCP(1251);

	string name, pass;
	string path_open, path_create;
	vector <string> array_default;

	cout << "Введите путь до файла с паролями:" << endl;
	getline(cin, path_open);
	cout << "Введите название файла без <.txt>" << endl;
	getline(cin, name);

	Text_handler(path_open, path_create, name);

	ifstream file;
	file.open(path_open);


	if (!file.is_open()) {
		cerr << "Ошибка открытия файла!" << endl;
	}
	else {
		cout << "Файл открыт!" << endl;
		int i = 0;
		while (!file.eof()) {
			i++;
			pass = "";
			getline(file, pass);
			pass.erase(remove_if(pass.begin(), pass.end(), ::isspace), pass.end()); // removing spaces in a word
			if (pass.size() > 3) {
				array_default.push_back(pass);
			}
			if (i % 10000 == 0) {
				cout << i << " <- Обрабатываемая строка" << "\r";
			}
		}
		cout << endl << "В массив не добавлялись пароли менее 4 символов" << endl;
	}

	file.close();

	cout << "Сортировка массива..." << endl;
	sort(array_default.begin(), array_default.end());
	cout << "Размер массива:" << array_default.size() << endl;

	cout << "Удаление дубликатов в массиве..." << endl;
	array_default.erase(unique(array_default.begin(), array_default.end()), array_default.end());
	cout << "Размер массива после удаления дубликатов:" << array_default.size() << endl;

	cout << "Удаление лишних данных..." << endl;
	for (int i = 0; i < array_default.size(); i++) {
		if (array_default[i].size() < 4) {
			array_default.erase(array_default.begin() + i);
		}
		if (i % 100000 == 0) {
			cout << i << " <- Обрабатываемая строка" << "\r";
		}
	}
	cout << endl << "Размер массива после удаления лишних данных:" << array_default.size() << endl;

	cout << "Создание файла:" << endl << "Запись в файл..." << endl;;
	ofstream Myfile(path_create);
	for (int i = 0; i < array_default.size(); i++) {
		Myfile << array_default[i] << "\n";
		if (i % 100000 == 0) {
			cout << i << " <- Обрабатываемая строка" << "\r";
		}
	}
	cout << endl;

	Myfile.close();

	return 0;
}
