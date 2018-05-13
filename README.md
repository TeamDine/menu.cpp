# menu.cpp
///Implementación de la clase Menu Principal

#include "menu.h"

using namespace std;

void Menu::startMenu() {
	int option = 0;
    system("color 0B");  ///Colorea la pantalla

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
            cout << "\t\tCaracter incorrecto" << endl << "\t\t";
            system("pause");
        }
        cin.ignore();

        switch(option){
            case 1:
                access();
                break;
            case 2:
                system("cls");
                showData();
                break;
            case 3:
                cout << endl;
                cout << "\t\tElegiste salir" << endl << "\t\t";
                system("pause");
                break;
            default:
                cout << endl;
                cout << "\t\tOpcion Incorrecta" << endl << "\t\t";
                system("pause");
                break;
        }

    }while(option != 3);
}

void Menu::access() {
	int option = 0;
	bool flag = true;
	fstream myFile;

    /*** Checar si el archivo existe, si es así checar si está vacio ***/
	myFile.open("CodigosProfesores.txt",ios_base::app);
	if(!myFile.good()){
        flag = false;   ///Archivo no existente
	}
	else{
        int weight;
        myFile.seekg(0,ios::end);
        weight = myFile.tellg();

        if(weight == 0){
            flag = false;   ///Archivo vacio
        }
	}
    myFile.close();

    /*** Menu ***/
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
        cout << "\t\t1)Altas" << endl;
        cout << "\t\t2)Mostrar codigo(s) de Profesores almacenados" << endl;
        cout << "\t\t3)Bajas" << endl;
        cout << "\t\t4)Buscar un profesor" << endl;
        cout << "\t\t5)Modificar datos" << endl;
        cout << "\t\t6)Regresar a menu principal" << endl;
        cout << "\t\tElige una opcion " << endl;
        cout << "\t\tOpcion: ";
        cin >> option;

        if(!cin){
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(),'\n');
            cout << "\t\tCaracter incorrecto" << endl << "\t\t";
            system("pause");
        }
        cin.ignore();

        switch(option){
            case 1:
                system("cls");
                cout << endl << endl;
                cout << "\t\tMenu de altas" << endl << "\t\t";
                system("pause");
                break;
            case 2:
                system("cls");
                cout << endl << endl;
                if(!flag){
                    cout << "\t\tNo hay registros actualmente, inserte uno" << endl << "\t\t";
                    system("Pause");
                }
                else{
                    showData();
                }
                break;
            case 3:
                system("cls");
                cout << endl << endl;
                if(!flag){
                    cout << "\t\tNo hay registros actualmente, inserte uno" << endl << "\t\t";
                }
                else{
                    cout << "\t\tMenu de bajas" << endl << "\t\t";
                }
                system("Pause");
                break;
            case 4:
                system("cls");
                cout << endl << endl;
                if(!flag){
                    cout << "\t\tNo hay registros actualmente, inserte uno" << endl << "\t\t";
                }
                else{
                    cout << "\t\tMenu de Busqueda" << endl << "\t\t";
                }
                system("Pause");
                break;
            case 5:
                system("cls");
                cout << endl << endl;
                if(!flag){
                    cout << "\t\tNo hay registros actualmente, inserte uno" << endl << "\t\t";
                }
                else{
                    cout << "\t\tMenu de Modificacion" << endl << "\t\t";
                }
                system("Pause");
                break;
            case 6:
                cout << endl;
                cout << "\t\tElegiste salir" << endl << "\t\t";
                system("pause");
                break;
            default:
                cout << endl;
                cout << "\t\tOpcion Incorrecta" << endl << "\t\t";
                system("pause");
                break;
        }

    }while(option != 6);

}

void Menu::showData(){
    fstream myFile;
    string name;
    string code;

    myFile.open("CodigosProfesores.txt");
    myFile.seekg(0,ios::beg);

    cout << endl << endl;
    cout << "\t\t\t\t****LISTA DE PROFESORES****" << endl << endl;
    cout << right << setw(40) <<"Nombre" << setw(28) << "Codigo" << endl << endl;
    while(!myFile.eof()){
        getline(myFile, name, '|');
        getline(myFile, code, '|');
        if(myFile.eof()) break;

        cout << right << setw(50) << name << setw(20) << code << endl;
    }

    cout << endl << "\t\t";
    system("Pause");

    myFile.close();
}
