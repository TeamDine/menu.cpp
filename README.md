# menu.cpp
///Implementación de la clase Menu Principal

#include "menu.h"

using namespace std;

void Menu::startMenu() {
	int option = 0;

    do{
        system("cls");

        cout << endl << endl;
        cout << "\t\t*******************************************************" << endl;
        cout << "\t\t\t\tActividad Integradora" << endl;
        cout << "\t\t*******************************************************" << endl;
        cout << "\t\tManejo de datos de profesores" << endl;
        cout << "\t\t1)Acceso a la base de datos" << endl;
        cout << "\t\t2)Mostrar codigo(s) de Profesores almacenados" << endl;
        cout << "\t\t3)Salir " << endl;
        cout << "\t\tElige una opcion " << endl;
        cout << "\t\tOpcion: ";
        cin >> option;

        if(!cin){
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(),'\n');
            cout << "\t\tCaracter incorrecto" << endl;
            system("pause");
        }
        cin.ignore();

        switch(option){
            case 1:
                access();
                system("Pause");
                break;
            case 2:
                system("cls");
                showData();
                break;
            case 3:
                cout << endl;
                cout << "\t\tElegiste salir" << endl;
                system("pause");
                break;
            default:
                cout << endl;
                cout << "\t\tOpcion Incorrecta" << endl;
                system("pause");
                break;
        }

    }while(option != 3);
}

void Menu::access() {
	int option = 0;
	bool flag = true;
	fstream myFile;

	myFile.open("CodigosProfesores.txt");
	if(!myFile.good()){
        flag = false;
	}
    myFile.close();

    do{
        system("cls");

        cout << endl << endl;
        cout << "\t\t*******************************************************" << endl;
        cout << "\t\t\t\tBASE DE DATOS" << endl;
        cout << "\t\t*******************************************************" << endl;
        if(!flag){
            cout << "\t\tNo hay registros actualmente, inserte uno" << endl;
        }
        cout << "\t\tManejo de datos de profesores" << endl;
        cout << "\t\t1)Acceso a la base de datos" << endl;
        cout << "\t\t2)Mostrar codigo(s) de Profesores almacenados" << endl;
        cout << "\t\t3)Salir " << endl;
        cout << "\t\tElige una opcion " << endl;
        cout << "\t\tOpcion: ";
        cin >> option;

        if(!cin){
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(),'\n');
            cout << "\t\tCaracter incorrecto" << endl;
            system("pause");
        }
        cin.ignore();

        switch(option){
            case 1:
                access();
                system("Pause");
                break;
            case 2:
                system("cls");
                showData();
                break;
            case 3:
                cout << endl;
                cout << "\t\tElegiste salir" << endl;
                system("pause");
                break;
            default:
                cout << endl;
                cout << "\t\tOpcion Incorrecta" << endl;
                system("pause");
                break;
        }

    }while(option != 3);

}

void Menu::showData(){
    fstream myFile;
    string name;
    string code;

    myFile.open("CodigosProfesores.txt",ios::in);
    myFile.seekg(0,ios::beg);

    cout << endl << endl;
    cout << "\t\tLISTA DE PROFESORES" << endl;
    while(!myFile.eof()){
        getline(myFile, name, '|');
        getline(myFile, code, '\n');
        if(myFile.eof()) break;

        cout << "\t\t" << name << "\t\t" << code << endl;
    }

    myFile.close();
}
