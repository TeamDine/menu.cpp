# menu.cpp
///Implementación de la clase Menu Principal
#include "menu.h"

using namespace std;

void Menu::startMenu() {
	int option = 0;
    system("color F0");  ///Colorea la pantalla

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
	myFile.open("CodigosProfesores.txt", ios_base::app);
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
                ///insertPersonalData();
                ///insertAcademicFormation();
                insertAcademicProduction();
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

    myFile.open("CodigosProfesores.txt", ios_base::app);
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

/******************************** DATOS PERSONALES ****************************************/
void Menu::insertPersonalData(){
    PersonalData data;
    Name myName;
    Address myAddress;
    string aux;
    bool flag = false;
    int option;
    int conteo;

    cout << "\t\t\t*********Registro de datos (PERSONALES)**************" << endl << endl << endl;
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
    int years = 0;
    int registro = 0;

    do{
        system("cls");

        cout << endl << endl;
        cout << "\t\t*************Dependientes Economicos *****************" << endl;
        registro = data.getLastPos();
        conteo = 10;    ///Limite de registros

        flag = false;

        cout << "\t\tRegistro #" << registro+2 << endl;
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
                cin.ignore();
                system("pause");
            }
            else if(years < 0 or years > 99){
                cout << "\t\tEdad invalida intenta de nuevo" << endl << "\t\t";
                system("pause");
            }
            else{
                flag = true;
            }

        }while(!flag);

        cout << "Edad: " << years;
        data.insertData(registro, myName, years);    ///Actualiza numero de registros;

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

    }while(conteo == 10);

    teacher.setData(data);      ///Agrega Datos personales al profesor en turno
}

/******************************** FORMACION ACADEMICA ****************************************/
void Menu::insertAcademicFormation(){
    Formation schoolar;
    string myStr;
    string aux;
    bool flag;

    ///Datos para fechas
    Date myDate;

    ///Valor del grado
    int grade = 0;
    /// grade = 0 -> No se ha insertado ningun grado academico
    /// grade = 1 -> Se inserto al menos 1 licenciatura
    /// grade = 2 -> Se inserto al menos 1 maestría

    int option = 0;
    int conteo = 10;    ///Limite de registros
    int pos = 0;
    int myInt = 0;

    do{
        pos = teacher.getLastFormation();
        myStr = "";
        myInt = 0;
        do{
            flag = false;

            system("cls");
            cout << endl << endl;
            cout << "\t\t\t*********Registro de datos (FORMACION ACADEMICA)**************" << endl << endl << endl;
            cout << "\t\tPor favor, llenar los siguientes campos disponibles" << endl << endl;
            cout << "\t\tSi desconoce un dato, solo agregue un guion '-' o teclee [enter] para continuar " << endl << endl;

            cout << endl << endl;
            cout << "\t\t****GRADO ACADEMICO****" << endl;
            cout << "\t\t1)Licenciatura" << endl;
            cout << "\t\t2)Especialidad" << endl;
            cout << "\t\t3)Maestria" << endl;
            cout << "\t\t4)Doctorado" << endl;
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
                grade = 1;      ///Se añadio una licenciatura
                aux = "LICENCIATURA";
                flag = true;
                break;
            case 2:
                if(grade == 1){
                    aux = "ESPECIALIDAD";
                    flag = true;
                }
                else{
                    cout << endl << "\t\tNO PUEDES AGREGAR ESPECIALIDAD; SI NO TIENE UNA LICENCIATURA REGISTRADA" << endl << "\t\t";
                    system("Pause");
                }
                break;
            case 3:
                if(grade == 1){
                    aux = "MAESTRIA";
                    flag = true;
                }
                else{
                    cout << endl << "\t\tNO PUEDES AGREGAR MAESTRIA; SI NO TIENE UNA LICENCIATURA REGISTRADA" << endl << "\t\t";
                    system("Pause");
                }
                break;
            case 4:
                if(grade == 2){
                    aux = "DOCTORADO";
                    flag = true;
                }
                else{
                    cout << endl << "\t\tNO PUEDES AGREGAR DOCTORADO; SI NO TIENE UNA MAESTRIA REGISTRADA" << endl << "\t\t";
                    system("Pause");
                }
                break;
            default:
                cout << endl;
                cout << "\t\tOpcion Incorrecta" << endl << "\t\t";
                system("pause");
                break;
            }
        }while(!flag);

        schoolar.setGrade(aux);     ///Se agrega tipo de grado academico

        system("cls");
        cout << endl << endl;
        cout << "\t\t*****************DATOS DE " << aux << "********************" << endl;
        cout << "\t\tPor favor, llenar los siguientes campos disponibles" << endl << endl;
        cout << "\t\tSi desconoce un dato, solo agregue un guion '-' o teclee [enter] para continuar " << endl << endl;

        cout << "\t\tNombre del grado academico (Ej. Ing en sistemas computacionales) " << endl;
        cout << "\t\tNombre: ";
        getline(cin, myStr, '\n');

        schoolar.setGradeName(myStr);   ///Se agrega nombre de grado escolar

        cout << endl << "\t\tNombre de la institucion academica (Ej. Universidad de Guadalajara) " << endl;
        cout << "\t\tNombre: ";
        getline(cin, myStr, '\n');

        schoolar.setInstitution(myStr);

        cout << endl << "\t\tEs importante ingresar las siguientes fechas en el formato correspondiente <YYYY/MM/AA>";
        cout << endl <<  "\t\tFecha de ingreso (Ej. 2016/08/15) " << endl;
        cout << "\t\tFecha: ";
        getline(cin, myStr, '/');
        myInt = atoi(myStr.c_str());
        myDate.setYear(myInt);
        getline(cin, myStr, '/');
        myInt = atoi(myStr.c_str());
        myDate.setMonth(myInt);
        getline(cin, myStr, '\n');
        myInt = atoi(myStr.c_str());
        myDate.setDay(myInt);

        schoolar.setBeginDate(myDate);  ///Se agrega fecha de entrada

        cout << endl <<  "\t\tFecha de egreso (Ej. 2021/12/15) " << endl;
        cout << "\t\tFecha: ";
        getline(cin, myStr, '/');
        myInt = atoi(myStr.c_str());
        myDate.setYear(myInt);
        getline(cin, myStr, '/');
        myInt = atoi(myStr.c_str());
        myDate.setMonth(myInt);
        getline(cin, myStr, '\n');
        myInt = atoi(myStr.c_str());
        myDate.setDay(myInt);

        schoolar.setFinishDate(myDate);  ///Se agrega fecha de salida

        cout << endl << "\t\tFecha de Obtencion de titulo (Ej. 2022/04/15) " << endl;
        cout << "\t\tFecha: ";
        getline(cin, myStr, '/');
        myInt = atoi(myStr.c_str());
        myDate.setYear(myInt);
        getline(cin, myStr, '/');
        myInt = atoi(myStr.c_str());
        myDate.setMonth(myInt);
        getline(cin, myStr, '\n');
        myInt = atoi(myStr.c_str());
        myDate.setDay(myInt);

        schoolar.setDegreeDate(myDate);  ///Se agrega fecha de entrada

        cout << endl << "\t\tNumero de Cedula profesional :";
        getline(cin, myStr, '\n');

        schoolar.setIdCard(myStr);

        teacher.insertFormation(pos, schoolar); ///Inserta en lista

        flag = false;
        do{
            cout << endl << endl;
            cout << "\t\tDesea agregar otra carrera" << endl;
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
                if(pos == conteo){
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

    }while(conteo == 10);
}

/******************************** PRODUCCION ACADEMICA ****************************************/
void Menu::insertAcademicProduction(){
    AcademicProduction production;
    string myStr;
    Date myDate;
    int myInt = 0;
    Name myName;

    int option = 0;
    int conteo = 10;
    int pos = 0;
    bool flag;

    do{
        pos = teacher.getLastProduction();
        do{
            flag = false;
            system("cls");
            cout << endl << endl;
            cout << "\t\t\t*********Registro de datos (PRODUCCION ACADEMICA)**************" << endl << endl << endl;
            cout << "\t\tPor favor, llenar los siguientes campos disponibles" << endl << endl;
            cout << "\t\tSi desconoce un dato, solo agregue un guion '-' o teclee [enter] para continuar " << endl << endl;

            cout << "\t\t****TIPO DE TRABAJO REALIZADO****" << endl;
            cout << "\t\t1)Libro" << endl;
            cout << "\t\t2)Articulo" << endl;
            cout << "\t\t3)Informe" << endl;
            cout << "\t\t4)Desarrollo de Software" << endl;
            cout << "\t\t5)Otro " << endl;
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
                myStr = "LIBRO";
                flag = true;
                break;
            case 2:
                myStr = "ARTICULO";
                flag = true;
                break;
            case 3:
                myStr = "INFORME";
                flag = true;
                break;
            case 4:
                myStr = "SOFTWARE";
                flag = true;
                break;
            case 5:
                cout << "\t\tEspecifique el tipo de trabajo (sea breve con su descripcion < 1 a 3 palabras > )" << endl;
                cout << "\t\tDescripicion: ";
                getline( cin , myStr, '\n');
                flag = true;
                break;
            default:
                cout << endl;
                cout << "\t\tOpcion Incorrecta" << endl << "\t\t";
                system("pause");
                break;
            }
        }while(!flag);

        production.setType(myStr);  ///Se agrega el tipo de trabajo

        cout << endl << endl;
        cout << "\t\tNombre del articulo/libro/Software (Ej. Programacion en C++) " << endl;
        cout << "\t\tNombre: ";
        getline(cin, myStr, '\n');

        production.setName(myStr);  ///Se agrega nombre de trabajo

        /**** *** ** * FECHA DE ELABORACION * ** *** ****/

        cout << endl << "\t\tEs importante ingresar las siguiente fecha en el formato correspondiente <YYYY/MM/AA>";
        cout << endl <<  "\t\tFecha de elaboracion (Ej. 2016/08/15) " << endl;
        cout << "\t\tFecha: ";
        getline(cin, myStr, '/');
        myInt = atoi(myStr.c_str());
        myDate.setYear(myInt);
        getline(cin, myStr, '/');
        myInt = atoi(myStr.c_str());
        myDate.setMonth(myInt);
        getline(cin, myStr, '\n');
        myInt = atoi(myStr.c_str());
        myDate.setDay(myInt);

        production.setElaborationDate(myDate);  ///Se agrega fecha de elaboracion

        /**** *** *** * Nombre de autor * ** *** ****/
        do{
            flag = false;
            system("cls");
            cout << "\t\t\t*********Registro de Nombre de Co-Autor*********" << endl << endl;
            cout << "\t\tApellido(s): ";
            getline(cin, myStr, '\n');

            myName.setLast(myStr);

            cout << "\t\tNombre(s): ";
            getline(cin, myStr, '\n');

            myName.setFirst(myStr);

            if(myName.isName(myName)){
                flag = true;
            }
            else{
                cout << "\t\tNombre invalido. Intente de nuevo" << endl << endl << "\t\t";
                system("Pause");
            }

        } while(!flag);

        production.setAuthor(myName);       ///Se agrega nombre de autor

        cout << endl << endl;
        cout << "\t\tNumero de registro (Ej. 123456)" << endl;
        cout << "\t\tNumero: ";
        getline( cin, myStr , '\n');

        production.setId(myStr);        ///Se agrega numero de registro

        /**** *** ** * ESTATUS * ** *** ****/
        do{
            flag = false;
            system("cls");
            cout << endl << endl;

            cout << "\t\t****STATUS DE TRABAJO REALIZADO****" << endl;
            cout << "\t\t1)ACEPTADO" << endl;
            cout << "\t\t2)EN PROCESO" << endl;
            cout << "\t\t3)PUBLICADO" << endl;
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
                myStr = "ACEPTADO";
                flag = true;
                break;
            case 2:
                myStr = "EN PROCESO";
                flag = true;
                break;
            case 3:
                myStr = "PUBLICADO";
                flag = true;
                break;
            default:
                cout << endl;
                cout << "\t\tOpcion Incorrecta" << endl << "\t\t";
                system("pause");
                break;
            }
        }while(!flag);

        production.setStatus(myStr);

        teacher.insertProduction(pos, production);  ///Insertando en lista

    /*** Perguntar si agregar mas de uno ***/
        flag = false;
        do{
            cout << endl << endl;
            cout << "\t\tDesea agregar otra carrera" << endl;
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
                if(pos == conteo){
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

    }while(conteo == 10);
}

/******************************** DOCENCIA ****************************************/
void Menu::insertTeachers(){
    Teaching course;
    string myStr;
    Date myDate;
    int myInt = 0;
    int pos = 0;
    int conteo = 10;
    int option = 0;
    bool flag;

    do{
        flag = false;
        pos = teacher.getLastCourses();
        system("cls");
        cout << endl << endl;
        cout << "\t\t\t*********Registro de datos (PRODUCCION ACADEMICA)**************" << endl << endl << endl;
        cout << "\t\tPor favor, llenar los siguientes campos disponibles" << endl << endl;
        cout << "\t\tSi desconoce un dato, solo agregue un guion '-' o teclee [enter] para continuar " << endl << endl;

        cout << "Nombre de la materia: ";
        getline(cin, myStr, '\n');
        course.setName(myStr);      ///Se agrega nombre de materia

        cout << endl << "\t\tEs importante ingresar las siguiente fecha en el formato correspondiente <YYYY/MM/AA>";
        cout << endl <<  "\t\tFecha de Inicio (Ej. 2016/08/15) " << endl;
        cout << "\t\tFecha: ";
        getline(cin, myStr, '/');
        myInt = atoi(myStr.c_str());
        myDate.setYear(myInt);
        getline(cin, myStr, '/');
        myInt = atoi(myStr.c_str());
        myDate.setMonth(myInt);
        getline(cin, myStr, '\n');
        myInt = atoi(myStr.c_str());
        myDate.setDay(myInt);

        course.setInitialDate(myDate);

        cout << endl <<  "\t\tFecha de finalizacion (Ej. 2016/08/15) " << endl;
        cout << "\t\tFecha: ";
        getline(cin, myStr, '/');
        myInt = atoi(myStr.c_str());
        myDate.setYear(myInt);
        getline(cin, myStr, '/');
        myInt = atoi(myStr.c_str());
        myDate.setMonth(myInt);
        getline(cin, myStr, '\n');
        myInt = atoi(myStr.c_str());
        myDate.setDay(myInt);

        course.setFinishDate(myDate);

        do{
            flag = false;
            system("cls");
            cout << endl << endl;
            cout << "\t\tRegistro de horas semanales" << endl;
            cout << "\t\tHoras: ";
            cin >> myInt;

            if(!cin){
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(),'\n');
                cout << "\t\tCaracter incorrecto" << endl << "\t\t";
                system("pause");
            }
            cin.ignore();

            if(myInt < 0 or myInt > 15){
                cout << "\t\tHoras invalidas, intentalo de nuevo" << endl << "\t\t";
                system("cls");
                }
            else{
                flag = true;
                }

            }while(!flag);

            course.setHours(myInt);

            teacher.insertCourses(pos, course); ///Inserta en lista

    /*** Perguntar si agregar mas de uno ***/
        flag = false;
        do{
            cout << endl << endl;
            cout << "\t\tDesea agregar otra materia" << endl;
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
                if(pos == conteo){
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

    }while(conteo == 10);
}

/******************************** TUTORIAS ****************************************/
void Menu::insertTutorials(){
    Tutorials student;
    Name myName;
    Date myDate;
    int myInt;
    string myStr;

    int option = 0;
    int pos = 0;
    int conteo = 10;

    bool flag;

    do{
	pos = teacher.getLastTutorial();
	do{
	    flag = false;
	    system("cls");
	    cout << endl << endl;
	    cout << "\t\t\t*********Registro de datos (TUTORIAS)**************" << endl << endl << endl;
      	    cout << "\t\tPor favor, llenar los siguientes campos disponibles" << endl << endl;
	    cout << "\t\tSi desconoce un dato, solo agregue un guion '-' o teclee [enter] para continuar " << endl << endl;

	    cout << "\t\tIngrese nombre completo" << endl << endl;
            cout << "\t\tApellido(s): ";
            getline(cin, myStr, '\n');

            myName.setLast(myStr);

            cout << "\t\tNombre(s): ";
            getline(cin, myStr, '\n');

            myName.setFirst(myStr);

            if(myName.isName(myName)){
                flag = true;
            }
            else{
                cout << "\t\tNombre invalido. Intente de nuevo" << endl << endl << "\t\t";
                system("Pause");
            }

        } while(!flag);

	student.setName(myName);	///Se agrega nombre al estudiante

        cout << endl << "\t\tEs importante ingresar las siguientes fechas en el formato correspondiente <YYYY/MM/AA>";
        cout << endl <<  "\t\tFecha de inicio (Ej. 2016/08/15) " << endl;
        cout << "\t\tFecha: ";
        getline(cin, myStr, '/');
        myInt = atoi(myStr.c_str());
        myDate.setYear(myInt);
        getline(cin, myStr, '/');
        myInt = atoi(myStr.c_str());
        myDate.setMonth(myInt);
        getline(cin, myStr, '\n');
        myInt = atoi(myStr.c_str());
        myDate.setDay(myInt);

	    student.setInitialDate(myDate);		///Se agrega fecha de ingreso

        cout << endl << "\t\tEs importante ingresar las siguientes fechas en el formato correspondiente <YYYY/MM/AA>";
        cout << endl <<  "\t\tFecha de finalizacion (Ej. 2016/08/15) " << endl;
        cout << "\t\tFecha: ";
        getline(cin, myStr, '/');
        myInt = atoi(myStr.c_str());
        myDate.setYear(myInt);
        getline(cin, myStr, '/');
        myInt = atoi(myStr.c_str());
        myDate.setMonth(myInt);
        getline(cin, myStr, '\n');
        myInt = atoi(myStr.c_str());
        myDate.setDay(myInt);

        student.setFinishDate(myDate);		///Se agrega fecha de finalizacion

        do{
            flag = false;
            system("cls");
            cout << endl << endl;
            cout << "\t\tRegistro de horas semanales" << endl;
            cout << "\t\tHoras: ";
            cin >> myInt;

            if(!cin){
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(),'\n');
                cout << "\t\tCaracter incorrecto" << endl << "\t\t";
                system("pause");
            }
            cin.ignore();

            if(myInt < 0 or myInt > 15){
                cout << "\t\tHoras invalidas, intentalo de nuevo" << endl << "\t\t";
                system("pause");
                }
            else{
                flag = true;
                }

            }while(!flag);

            student.setHours(myInt);

	    teacher.insertTutorial(pos, student);	///Insertando en lista

    /*** Perguntar si agregar mas de uno ***/
        flag = false;
        do{
            cout << endl << endl;
            cout << "\t\tDesea agregar otro Tutorado" << endl;
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
                if(pos == conteo){
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

    }while(conteo == 10);
}
