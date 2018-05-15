# menu.cpp
///Implementación de la clase Menu Principal

#include "menu.h"

using namespace std;

void Menu::startMenu() {
	int option = 0;
    system("color 80");  ///Colorea la pantalla

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
                insertData();
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

void Menu::insertData(){
    PersonalData data;
    Name myName;
    Address myAddress;
    string aux;
    bool flag = false;
    int option;
    int conteo;

    cout << "\t\t\t*********Registro de datos**************" << endl << endl << endl;
    cout << "\t\tPor favor, llenar los siguientes campos disponibles" << endl << endl;
    cout << "\t\tSi desconoce un dato, solo agregue un guion '-' o teclee [enter] para continuar " << endl << endl;


    /***** **** *** ** * Registro de nombre * ** *** **** *****/
    do{
        cout << "\t\t\t*********Registro de Nombre*********" << endl << endl;
        cout << "\t\tApellido(s): ";
        getline(cin, aux, '\n');

        myName.setLast(aux);

        cout << "\t\tNombre(s): ";
        getline(cin, aux, '\n');

        myName.setFirst(aux);

        if(myName.isName(myName)){
            flag = true;
        }
        else{
            cout << "\t\tNombre invalido. Intente de nuevo" << endl << endl << "\t\t";
            system("Pause");
        }

    } while(!flag);

    data.setName(myName);       ///Se agrega nombre al registro


    /***** **** *** ** * Registro de Domicilio * ** *** **** *****/
    cout << endl << endl;
    cout << "\t\t**************Datos de Domicilio************" << endl << endl;

    cout << "\t\tCalle principal: ";
    getline(cin, aux, '\n');
    myAddress.setMainStreet(aux);

    cout << "\t\tNumero Exterior: ";
    getline(cin, aux, '\n');
    myAddress.setNumExt(aux);

    cout << "\t\tNumero Interior: ";
    getline(cin, aux, '\n');
    myAddress.setNumInt(aux);

    cout << "\t\tColonia: ";
    getline(cin, aux, '\n');
    myAddress.setSuburb(aux);

    cout << "\t\tCiudad: ";
    getline(cin, aux, '\n');
    myAddress.setCountry(aux);

    data.setAddress(myAddress);     ///Se agrega domicilio al registro

    /***** **** *** ** * Registro de Telefono * ** *** **** *****/
    cout << "\t\tTelefono: ";
    getline(cin, aux, '\n');
    data.setTelphone(aux);          ///Se agrega telefono al registro

    /***** **** *** ** * Registro de Email * ** *** **** *****/
    cout << "\t\tEmail: ";
    getline(cin, aux, '\n');
    data.setEmail(aux);             ///Se agrega correo electronico al registro

    flag = false; ///Se remonta bandera en false para iterar en el proximo ciclo

    /***** **** *** ** * Registro de estado civil * ** *** **** *****/
    do{
        system("cls");
        cout << endl << endl;
        cout << "\t\t\t****Estado civil****" << endl;
        cout << "\t\t1)Soltero/a" << endl;
        cout << "\t\t2)Comprometido/a" << endl;
        cout << "\t\t3)Casado/a" << endl;
        cout << "\t\t4)Divorciado/a" << endl;
        cout << "\t\t5)Viudo/a" << endl;
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
            aux = "Soltero/a";
            flag = true;
            break;
        case 2:
            aux = "Comprometido/a";
            flag = true;
            break;
        case 3:
            aux = "Casado/a";
            flag = true;
            break;
        case 4:
            aux = "Divorciado/a";
            flag = true;
            break;
        case 5:
            aux = "Viudo/a";
            flag = true;
        break;
        default:
            cout << endl;
            cout << "\t\tOpcion Incorrecta" << endl << "\t\t";
            system("pause");
            break;
        }
    }while(!flag);

    data.setStatus(aux);        ///se agrega estado civil al registro

    /***** **** *** ** * Registro de Dependientes económicos * ** *** **** *****/

    do{
        int registro;
        system("cls");

        cout << endl << endl;
        cout << "\t\t*************Dependientes Economicos *****************" << endl;
        registro = data.getCont();
        cout << "\t\tHasta el momento tiene: " << registro << " Dependientes economicos registrados" << endl;
        cout << "\t\tPuede registrar hasta 10 familiares" << endl;
        conteo = 10;

        flag = false;
        int years = 0;

        cout << "\t\tRegistro #" << registro+1 << endl;
        do{
            cout << "\t\tApellido(s): ";
            getline(cin, aux, '\n');

            myName.setLast(aux);

            cout << "\t\tNombre(s): ";
            getline(cin, aux, '\n');

            myName.setFirst(aux);

            if(myName.isName(myName)){
                flag = true;
            }
            else{
                cout << "\t\tNombre invalido. Intente de nuevo" << endl << endl << "\t\t";
                system("Pause");
            }

        } while(!flag);

        flag = false;

        do{
            cout << "\t\tEdad: ";
            cin >> years;

            if(!cin){
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(),'\n');
                cout << "\t\tCaracter incorrecto" << endl << "\t\t";
                system("pause");
            }
            else if(years < 0 or years > 99){
                cout << "\t\tEdad invalida intenta de nuevo" << endl << "\t\t";
                system("pause");
            }
            else{
                flag = true;
            }
            cin.ignore();

        }while(!flag);

        registro++;

        do{
            cout << endl << endl;
            cout << "\t\tDesea agregar otro dependiente" << endl;
            cout << "\t\t1)Si" << endl;
            cout << "\t\t2)No" << endl;
            cout << "\t\tOpcion: ";
            cin >> option;

            if(!cin){
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(),'\n');
                cout << "\t\tCaracter incorrecto" << endl << "\t\t";
                system("pause");
            }
            cin.ignore();


            if(option == 1){
                flag = true;
                if(registro == conteo){
                    cout << endl << endl;
                    cout << "\t\tYa no puedes hacer mas registros " << endl << "\t\t";
                    conteo = 0;
                    system("pause");
                }
            }
            else if(option == 2){
                flag = true;
                conteo = 0;
            }

        }while(!flag);

        data.setCont(registro);     ///Actualiza numero de registros;

    }while(conteo == 10);

}
