#include <iostream>
#include <string>
#include <vector>
#include <random>// 
#include <time.h>// libreria de tiempo, generar tiempitos
#include <windows.h>//libreria de colores wiiii
#include <sstream>//convertir cadena de texto en numeros, agregada para el menu
#include <limits>//libreria para validacion de datos, agregada para el 
#include <cstdlib> //limpiar pantalla
#include <conio.h>
#include <bits/stdc++.h>
#include <fstream>
using namespace std;
/* Elaborado por: Itzel La Rosa y Devony Ramirez
    Profesora: Lia Mendoza
 */
void limpiarPantalla() {
    system("cls");
}

//STRRUCTS
struct episodios {
    string nombreEpisodio;
    int numeroEpisodio;
    int duracionEpisodio;
    float puntuacion;
    episodios* proxEpisodio;
};

struct serie {
    string nombreSerie;
    string genero;
    int audienciaSerie;
    int clasSerie;
    int fechaSerie;
    int duracionSerie;
    int cantidadEpisodios;
    float promedioPuntuacion;
    episodios* listaEpisodio;
    serie* proxSerie;
};

//GENERADOR DE TIEMPO DADO POR LIA
int generar_tiempo_id(int limiteinf, int limitesup) {
    static default_random_engine generador(time(nullptr));
    uniform_int_distribution<int> distribucion(limiteinf, limitesup);
    return distribucion(generador);
}

//COLORES
void SetColor(int textColor) {
    HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);  
    SetConsoleTextAttribute(hConsole, textColor);  
}

//funcion para pausar hasta dar enter
void pausarPantalla() {
    SetColor(14);
    cout<< "\nPresiona Enter para continuar.";
    cin.get();  
}

//GENERAR GENERO ALEATORIO
string obtenerGeneroAleatorio() {
    // Vector de géneros disponibles
    vector<string> generos = {
        "Accion", "Comedia", "Drama", "Terror",
        "Ciencia Ficcion", "Fantasia", "Documental",
        "Romance", "Suspenso", "Animacion","Historia","Musical"
    };

    // Elegir un índice aleatorio del vector
    int indiceAleatorio = generar_tiempo_id(0, generos.size() - 1);

    // Retornar el género correspondiente
    return generos[indiceAleatorio];
}

//CREADORES DE NODOS SERIE-EPISODIOS
serie* crearSerie(string nom) {
    serie* nuevaSerie = new serie();
    nuevaSerie->nombreSerie = nom;
    nuevaSerie->genero = obtenerGeneroAleatorio();
    nuevaSerie->audienciaSerie = generar_tiempo_id(1000,100000);
    nuevaSerie->clasSerie = generar_tiempo_id(3,21);
    nuevaSerie->fechaSerie = generar_tiempo_id(1980,2024);
    nuevaSerie->duracionSerie = 0;
    nuevaSerie->cantidadEpisodios = 0;
    nuevaSerie->promedioPuntuacion = 0;
    nuevaSerie->listaEpisodio = NULL;
    nuevaSerie->proxSerie = NULL;
    return nuevaSerie;
}

episodios* crearEpisodio(string nom,  int numero) {
    episodios* nuevoEpisodio = new episodios();
    nuevoEpisodio->nombreEpisodio = nom;
    nuevoEpisodio->duracionEpisodio = generar_tiempo_id(10,120);
    nuevoEpisodio->numeroEpisodio = numero;
    nuevoEpisodio->puntuacion = generar_tiempo_id(0,10);
    nuevoEpisodio->proxEpisodio = NULL;
    return nuevoEpisodio;
}

// VERIFICACION DE LISTAS VACIAS
bool listaVaciaSerie(serie* lista) {
    return lista == NULL;
}

bool listaVaciaEpisodio(episodios* lista) {
    return lista == NULL;
}

// FUNCION PARA COLOCAR MINUSCULITAS para loa ordenacion
string toLowerCase(const string& str) {
    string result = str;
    for (char& c : result) {
        c = tolower(c); 
    }
    return result;
}

//RESPUESTAS VALIDAS 
bool esRespuestaValida() {
    string respuesta;
    getline(cin, respuesta);

    if (respuesta.empty()) {
        cout << "|| La respuesta no puede estar vacia. Por favor, ingresa una respuesta.\n";
        return false; 
    }
    
    return true; 
}

float OPepisodioMayorPuntuacion(episodios* lista){
    float punt=0;
    episodios *mover = NULL;
    if (!listaVaciaEpisodio(lista)){
        mover = lista;
        while (mover != NULL){
            if(mover->puntuacion >=punt){
                punt=mover->puntuacion;
                mover = mover->proxEpisodio;
            }
            else{
                mover = mover->proxEpisodio;
            }
        }
    }
    return punt;
}

// DATO PARA CALCULAR EL TIEMPO QUE DURA EL EPISODIO  CON MAS TIEMPO
int OPepisodioqueduramastiempo(episodios* lista){
    int Tiempo=0;
    episodios *mover = NULL;
    if (!listaVaciaEpisodio(lista)){
        mover = lista;
        while (mover != NULL){
            if(mover->duracionEpisodio >=Tiempo){
                Tiempo=mover->duracionEpisodio;
                mover = mover->proxEpisodio;
            }
            else{
                mover = mover->proxEpisodio;
            }
        }
    }
    return Tiempo;
}

// DURACION DE SERIE
int OPduracionSerie(episodios* lista){
    int duracion = 0;
    episodios *mover;
    if (!listaVaciaEpisodio(lista)){
        mover = lista;
        while (mover != NULL){
            duracion += mover->duracionEpisodio;
            mover = mover->proxEpisodio;
        }
    }
    return duracion;
}

//CALCULAR LOS EPISODIOS DE LA SERIES
int cantidadEpisodio(episodios* lista) {
    int cantidad = 0;
    episodios* mover = lista;
    while (mover != NULL) {
        cantidad++;
        mover = mover->proxEpisodio;
    }
    return cantidad;
}

//BORRAR TODO DEL ARCHIVO
void borrarContenidoArchivo(const std::string& rutaArchivo) {
    std::ifstream archivo(rutaArchivo);  

    if (!archivo.is_open()) {
        SetColor(13); 
        std::cout << "\n|| ERROR. No se pudo abrir el archivo.\n";
        archivo.close();
        pausarPantalla();
        return;
    }

    archivo.seekg(0, std::ios::end); 
    if (archivo.tellg() == 0) {
        SetColor(13); 
        std::cout << "\n|| El archivo esta vacio. No se puede borrar nada.\n";
        archivo.close();
        pausarPantalla();
        return;
    }


    archivo.close(); 
    
    std::ofstream archivoSalida(rutaArchivo, std::ios::trunc);
    if (archivoSalida.is_open()) {
        archivoSalida.close();
        SetColor(15); 
        std::cout << "\n|| El contenido del archivo ha sido borrado exitosamente.\n";
        pausarPantalla();
    } else {
        SetColor(13); 
        std::cout << "\n|| ERROR. No se pudo abrir el archivo para borrarlo.\n";
        pausarPantalla();
    }
}

//esto son las series que se muestran en todo el menu, estan aqui arrriba porque son llamadas varias veces
void mostrarSeriesmenu(serie* lista){
    SetColor(15);
    cout<<"-------------------------------------------\n";
    SetColor(14);
    cout<<"|      Series disponibles en la lista      |\n";
    SetColor(15);
    cout<<"-------------------------------------------\n";
    
    if(listaVaciaSerie(lista)){
        SetColor(13);
        cout<<"|  No hay series disponibles en la lista   |\n";
    }
    else{
        int i = 1;
        serie* mover = lista;  // Usar un puntero auxiliar para recorrer la lista
        while(mover != NULL){
            int cantidadEp = cantidadEpisodio(mover->listaEpisodio);
            SetColor(15);
            cout<<"| "<<i<<". "<< mover->nombreSerie <<" ";
            cout<<" ("<<cantidadEp<<" episodios)\n";
            SetColor(4);
            cout<<"  _______________________________________  \n";        
            i++;
            mover = mover->proxSerie;  // Avanzamos en la lista con el puntero auxiliar
        }
    }
    SetColor(15);
    cout<<"-------------------------------------------\n";
}

// FUNCIONES DE BUSQUEDA
serie* buscarSerie(serie* lista, string nom) {
    serie* aux = lista;
    while (aux != NULL && toLowerCase(aux->nombreSerie) != toLowerCase(nom)) {
        aux = aux->proxSerie;
    }
    return aux;
}

episodios* buscarEpisodio(episodios* lista, string nom) {
    episodios* aux = lista;

    while (aux != NULL && toLowerCase(aux->nombreEpisodio)!=toLowerCase(nom)) {
        aux = aux->proxEpisodio;
    }
    return aux;
}

episodios* buscarEpisodioMayorPuntuacion(episodios* lista) {
    episodios* aux = lista;
    int tiempo=OPepisodioMayorPuntuacion(aux);
    while (aux != NULL && aux->puntuacion != tiempo) {
        aux = aux->proxEpisodio;
    }
    return aux;
}

episodios* buscar_episodio_que_dura_mas_tiempo(episodios* lista) {
    episodios* aux = lista;
    int tiempo=OPepisodioqueduramastiempo(aux);
    while (aux != NULL && aux->duracionEpisodio != tiempo) {
        aux = aux->proxEpisodio;
    }
    return aux;
}


//FUNCIONES DE INSERCION**
void insertarUltimaSerie(serie** lista, string nom) {
    serie* nuevaSerie = crearSerie(nom);
    if (listaVaciaSerie(*lista)) {
        *lista = nuevaSerie;
    } else {
        serie* aux = *lista;
        while (aux->proxSerie != NULL) {
            aux = aux->proxSerie;
        }
        aux->proxSerie = nuevaSerie;
    }
}

void insertarUltimoEpisodio(episodios** lista, string nom, int numero) {
    episodios* nuevoEpisodio = crearEpisodio(nom, numero);
    if (listaVaciaEpisodio(*lista)) {
        *lista = nuevoEpisodio;
    } else {
        episodios* aux = *lista;
        while (aux->proxEpisodio != NULL) {
            aux = aux->proxEpisodio;
        }
        aux->proxEpisodio = nuevoEpisodio;
    }
}


//FUNCIONES ELIMINADAS, primitivas**
void eliminarSerie(serie** lista, string nom) {
    serie* mover = *lista;
    serie* anterior = NULL;
    while (mover != NULL && toLowerCase(mover->nombreSerie) != toLowerCase(nom)) {
        anterior = mover;
        mover = mover->proxSerie;
    }

    if (mover == NULL) {
        SetColor(13);
        cout<<"|| La serie no esta registrada."<<endl;
    } else {
        // Eliminar las temporadas y episodios
        episodios* temp = mover->listaEpisodio;
        while (temp != NULL) {
            episodios* borrarepisodio = temp;
            temp = temp->proxEpisodio;
            delete borrarepisodio;
        }

        // Eliminar la serie
        if (mover == *lista) {
            *lista = (*lista)->proxSerie;
        } else {
            anterior->proxSerie = mover->proxSerie;
        }
        delete mover;
    }
}

void eliminarEpisodio(episodios** lista, string nom) {
    episodios* mover = *lista;
    episodios* anterior = NULL;
    while (mover != NULL && toLowerCase(mover->nombreEpisodio) != toLowerCase(nom)) {
        anterior = mover;
        mover = mover->proxEpisodio;
    }

    if (mover == NULL) {
        SetColor(13);
        cout<<"|| El episodio no esta registrado." <<endl;
    } else {

        if (mover == *lista) {
            *lista = (*lista)->proxEpisodio;
        } else {
            anterior->proxEpisodio = mover->proxEpisodio;
        }
        delete mover;
    }
}

serie* obtenerSerieConMayorAudiencia(serie *lista) {
    if (listaVaciaSerie(lista)) {
        return NULL;
    }

    serie *serieMayorAudiencia = lista;
    serie *auxiliar = lista->proxSerie;

    while (auxiliar != NULL) {
        if (auxiliar->audienciaSerie > serieMayorAudiencia->audienciaSerie) {
            serieMayorAudiencia = auxiliar;
        }
        auxiliar = auxiliar->proxSerie;
    }

    return serieMayorAudiencia;
}

// ORDENACION ALFABETICA
void ordenarSeriesAlfabeticamente(serie** inicio) {
    if (listaVaciaSerie(*inicio)) {
        SetColor(13);
        cout << "|| La lista de series esta vacia para hacer ordenamiento, por favor llenala :D." << endl;
        return;
    }

    bool intercambio; 
    serie* aux1;
    serie* aux2;

    do {
        intercambio = false;  
        aux1 = *inicio;

        while (aux1 != NULL && aux1->proxSerie != NULL) {
            aux2 = aux1->proxSerie;

            if (toLowerCase(aux1->nombreSerie) > toLowerCase(aux2->nombreSerie)) {

                swap(aux1->nombreSerie, aux2->nombreSerie);
                swap(aux1->genero, aux2->genero);
                swap(aux1->audienciaSerie, aux2->audienciaSerie);
                swap(aux1->clasSerie, aux2->clasSerie);
                swap(aux1->fechaSerie, aux2->fechaSerie);
                swap(aux1->duracionSerie, aux2->duracionSerie);
                swap(aux1->listaEpisodio, aux2->listaEpisodio);

                intercambio = true;  
            }
            aux1 = aux1->proxSerie;
        }
    } while (intercambio);  

    SetColor(14);
    cout << "Se ordenaron las series de manera alfabetica." << endl;
    cout << endl;
    mostrarSeriesmenu(*inicio);  
}



void mostrarEpisodioMayorPuntacion(serie* lista) {
    if (!listaVaciaSerie(lista)) {
        string nombreSerie;

        mostrarSeriesmenu(lista);
        SetColor(14);
        cout << endl;
        cout << "| Introduce el nombre de la serie para buscarle el episodio con mayor duracion: ";

        while (true) {
            getline(cin, nombreSerie);
            if (nombreSerie.empty()) {
                SetColor(13);
                cout << "|| El nombre de la serie no puede estar vacio. Intenta nuevamente: ";
            } else {
                break;
            }
        }

        serie* serieActual = buscarSerie(lista, nombreSerie);

        while (serieActual == NULL) {
            SetColor(13);
            cout << "|| La serie '" << nombreSerie << "' no esta registrada. Intenta nuevamente." << endl;
            cout << "| Introduce el nombre de la serie nuevamente: ";
            while (true) {
                getline(cin, nombreSerie);
                if (nombreSerie.empty()) {
                    SetColor(13);
                    cout << "|| El nombre de la serie no puede estar vacio. Intenta nuevamente: ";
                } else {
                    break;
                }
            }

            serieActual = buscarSerie(lista, nombreSerie);
        }

        episodios* episodio = serieActual->listaEpisodio;
        if (episodio == NULL) {
            SetColor(13);
            cout << "|| No hay episodios registrados para la serie '" << nombreSerie << "'." << endl;
            return;
        }

        SetColor(14);
        cout << "| Episodios de la serie '" << nombreSerie << "':" << endl;
        SetColor(15);

        episodios* tempEpisodio = episodio;
        while (tempEpisodio != NULL) {
            cout << "- Episodio " << tempEpisodio->numeroEpisodio << ": " << tempEpisodio->nombreEpisodio 
                << " (" << tempEpisodio->puntuacion << "/10)" << endl;
            tempEpisodio = tempEpisodio->proxEpisodio;
        }

        episodios* episodioMax = buscarEpisodioMayorPuntuacion(episodio);

        SetColor(4);
        cout << "\n---------------------------------------------" << endl;
        SetColor(14);
        cout << "|       EPISODIO MAYOR PUNTUACION             |" << endl;
        SetColor(4);
        cout << "---------------------------------------------" << endl;

        SetColor(15);
        cout << "| Episodio " << episodioMax->numeroEpisodio << ". " << endl;
        cout << "| Nombre: " << episodioMax->nombreEpisodio << endl;
        cout << "| Duracion: " << episodioMax->duracionEpisodio << " minutos" << endl;
        cout << "| puntuacion: (" << episodioMax->puntuacion << "/10)" << endl;
        SetColor(4);
        cout << "---------------------------------------------" << endl;
    }
    else {
        SetColor(13);
        cout << "\n|| No existen series registradas para evaluar la duracion de sus episodios." << endl;
    }
}


//funciones de mostrar, excepto la de las series, esta arriba
void mostrar_episodio_que_dura_mas_tiempo(serie* lista) {
    if (!listaVaciaSerie(lista)) {
        string nombreSerie;

        mostrarSeriesmenu(lista);
        SetColor(14);
        cout << endl;
        cout << "| Introduce el nombre de la serie para buscarle el episodio que dura mas tiempo: ";

        while (true) {
            getline(cin, nombreSerie);
            if (nombreSerie.empty()) {
                SetColor(13);
                cout << "|| El nombre de la serie no puede estar vacio. Intenta nuevamente: ";
            } else {
                break;
            }
        }

        serie* serieActual = buscarSerie(lista, nombreSerie);

        while (serieActual == NULL) {
            SetColor(13);
            cout << "|| La serie '" << nombreSerie << "' no esta registrada. Intenta nuevamente." << endl;
            cout << "| Introduce el nombre de la serie nuevamente: ";
            while (true) {
                getline(cin, nombreSerie);
                if (nombreSerie.empty()) {
                    SetColor(13);
                    cout << "|| El nombre de la serie no puede estar vacio. Intenta nuevamente: ";
                } else {
                    break;
                }
            }

            serieActual = buscarSerie(lista, nombreSerie);
        }

        episodios* episodio = serieActual->listaEpisodio;
        if (episodio == NULL) {
            SetColor(13);
            cout << "|| No hay episodios registrados para la serie '" << nombreSerie << "'." << endl;
            return;
        }

        SetColor(14);
        cout << "| Episodios de la serie '" << nombreSerie << "':" << endl;
        SetColor(15);

        episodios* tempEpisodio = episodio;
        while (tempEpisodio != NULL) {
            cout << "- Episodio " << tempEpisodio->numeroEpisodio << ": " << tempEpisodio->nombreEpisodio 
                 << " (" << tempEpisodio->duracionEpisodio << " minutos)" << endl;
            tempEpisodio = tempEpisodio->proxEpisodio;
        }

        episodios* episodioMax = buscar_episodio_que_dura_mas_tiempo(episodio);

        SetColor(4);
        cout << "\n---------------------------------------------" << endl;
        SetColor(14);
        cout << "|       EPISODIO QUE DURA MAS TIEMPO        |" << endl;
        SetColor(4);
        cout << "---------------------------------------------" << endl;

        SetColor(15);
        cout << "| Episodio " << episodioMax->numeroEpisodio << ". " << endl;
        cout << "| Nombre: " << episodioMax->nombreEpisodio << endl;
        cout << "| Duracion: " << episodioMax->duracionEpisodio << " minutos" << endl;
        cout << "| Puntuacion: " << episodioMax->puntuacion << " pts " << endl;
        SetColor(4);
        cout << "---------------------------------------------" << endl;
    }
    else {
        SetColor(13);
        cout << "\n|| No existen series registradas para evaluar la duracion de sus episodios." << endl;
    }
}


//mostrar la lista de series y sus datos, no episodios
void mostrarSeries(serie *lista) {
    serie *mover = lista;  // Usar una variable auxiliar para recorrer la lista
    int i = 1;

    if (!listaVaciaSerie(lista)) {
        SetColor(4);
        cout << "\nLISTA DE SERIES\n" << endl;
        while (mover != NULL) {
            SetColor(14);
            cout << "+-------------------------------------------------------------------+" << endl;
            cout << "| " << i << ". Nombre de la serie: " << mover->nombreSerie << "\n";
            SetColor(15);
            cout << "|   . Genero: " << mover->genero << endl;
            cout << "|   . Audiencia: " << mover->audienciaSerie << endl;
            cout << "|   . Clasificacion: +" << mover->clasSerie << endl;
            cout << "|   . Fecha: " << mover->fechaSerie << endl;
            SetColor(14);
            cout << "+-------------------------------------------------------------------+" << endl;
            mover = mover->proxSerie;  // Avanzar al siguiente nodo de la lista
            i++;
        }
    } else {
        SetColor(13);
        cout << "\n|| No existen series registradas para mostrar\n" << endl;
    }
}



void mostrarTop3Audiencia(serie* lista) {
    if (lista == NULL) {
        SetColor(13);
        cout << "|| No existen series registradas para evaluar audiencia." << endl;
    } else {

        mostrarSeries(lista);

        serie* primera = NULL;
        serie* segunda = NULL;
        serie* tercera = NULL;


        for (serie* aux = lista; aux != NULL; aux = aux->proxSerie) {
            if (primera == NULL || aux->audienciaSerie > primera->audienciaSerie) {
                tercera = segunda;
                segunda = primera;
                primera = aux;
            } else if (segunda == NULL || aux->audienciaSerie > segunda->audienciaSerie) {
                tercera = segunda;
                segunda = aux;
            } else if (tercera == NULL || aux->audienciaSerie > tercera->audienciaSerie) {
                tercera = aux;
            }
        }

        SetColor(14);
        cout << "\n---------------------------------------------" << endl;
        SetColor(15);
        cout << "|       TOP 3 SERIES CON MAYOR AUDIENCIA    |" << endl;
        SetColor(14);
        cout << "---------------------------------------------" << endl;
        SetColor(15);
        if (primera != NULL) {
            cout << "| 1. " << primera->nombreSerie << " - Audiencia: " << primera->audienciaSerie << endl;
        }
        if (segunda != NULL) {
            cout << "| 2. " << segunda->nombreSerie << " - Audiencia: " << segunda->audienciaSerie << endl;
        }
        if (tercera != NULL) {
            cout << "| 3. " << tercera->nombreSerie << " - Audiencia: " << tercera->audienciaSerie << endl;
        }

        if (segunda == NULL) {
            SetColor(13);
            cout << endl;
            cout << "| ATENCION: Solo hay 1 serie en la lista." << endl;
        } else if (tercera == NULL) {
            SetColor(13);
            cout << endl;
            cout << "| ATENCION: Solo hay 2 series en la lista." << endl;
        }
        SetColor(14);
        cout << "---------------------------------------------" << endl;
    }
}



// mostrar series y sus listas de episodios
void mostrarSeriesEpisodios(serie* lista) {
    serie* aux = lista;
    episodios* aux2;
    if(!listaVaciaSerie(lista)){
        while(aux!= NULL){
            bool nohay = false;
            cout<<endl;
            SetColor(14);
            cout<<"+---------------------------------------------+"<<endl;
            cout<<"|  SERIE "<<aux->nombreSerie<<endl;
            cout<<"+---------------------------------------------+"<<endl;
            SetColor(15);
            cout<<"|  Duracion: "<<OPduracionSerie(aux->listaEpisodio)<<" minutos"<<endl;
            cout<<"|  Genero: "<<aux->genero<<endl;
            cout<<"|  Audiencia: "<<aux->audienciaSerie<<endl;
            cout<<"|  Clasificacion: +"<<aux->clasSerie<<endl;
            cout<<"|  Fecha: "<<aux->fechaSerie<<endl;
            cout<<"|  Cantidad de episodios: "<<cantidadEpisodio(aux->listaEpisodio)<<endl;
            SetColor(4);
            cout<<"+---------------------------------------------+"<<endl;
            cout<<"| EPISODIOS: ("<<cantidadEpisodio(aux->listaEpisodio)<<")  "<<endl;
            aux2 = aux->listaEpisodio;
            if(aux2 == NULL){
                nohay = false;
                SetColor(13);
                cout<<"||  No existen episodios registrados en esta serie."<<endl;
            }
            else{
                nohay = true;
            }

            while(aux2 != NULL){
                cout<<endl;
                SetColor(4);
                cout<<"+---------------------------------+"<<endl;
                SetColor(14);
                cout<<"|   | Episodio "<<aux2->numeroEpisodio<<". "<<endl;
                SetColor(15);
                cout<<"|   | Nombre: "<<aux2->nombreEpisodio<<endl; 
                cout<<"|   | Duracion: "<<aux2->duracionEpisodio<<endl;
                cout<<"|   | Puntuacion: "<<aux2->puntuacion<<endl;
                SetColor(4);
                cout<<"+---------------------------------+"<<endl;
                aux2 = aux2->proxEpisodio;
            }
            
            if(nohay == true){
            }
            SetColor(14);
            cout<<"+---------------------------------------------+"<<endl;
            aux = aux->proxSerie;
        }
        
    }
    else{
        SetColor(13);
        cout<<"\n|| No existen series registradas para mostrar\n"<<endl;
    }
}


//funciones de  ELIMINAR no primitvas**
//ELIMINAR una serie  de la lista de series
void eliminarSerieEspecifica(serie** lista) {
    if (!listaVaciaSerie(*lista)) {
        string nombreSerie;
        char opcion;


        mostrarSeriesmenu(*lista);
        SetColor(14);
        cout << "| Introduce el nombre de la serie que deseas eliminar: ";
        

        while (true) {
            getline(cin, nombreSerie);

            if (nombreSerie.empty()) {
                SetColor(12);
                cout << "| Error: El nombre de la serie no puede estar vacio. Por favor, intentalo de nuevo." << endl;
                cout << "| Introduce el nombre de la serie que deseas eliminar: ";
            } 

            else if (!buscarSerie(*lista, nombreSerie)) {
                SetColor(12);
                cout << "| Error: No se encontro la serie '" << nombreSerie << "' en la lista." << endl;
                cout << "| Introduce el nombre de la serie que deseas eliminar: ";
            } else {
                break;  
            }
        }

        SetColor(15);
        bool opcionValida = false;
        while (!opcionValida) {
            SetColor(15);
            cout << "|* Estas seguro de que deseas eliminar la serie '" << nombreSerie << "'? (s/n): ";
            string entrada;
            getline(cin, entrada);

            if (entrada.empty()) {
                SetColor(12);
                cout << "| Error: No se ingreso ninguna opcion. Por favor, ingresa 's' para confirmar o 'n' para cancelar." << endl;
            } else {
                opcion = tolower(entrada[0]);  

                if (opcion == 's') {
                    eliminarSerie(lista, nombreSerie);
                    SetColor(14);
                    cout << "* La serie '" << nombreSerie << "' ha sido eliminada correctamente." << endl;
                    opcionValida = true;
                } else if (opcion == 'n') {
                    SetColor(13);
                    cout << "| Operacion cancelada. No se elimino ninguna serie." << endl;
                    pausarPantalla();
                    opcionValida = true;
                } else {
                    SetColor(12);
                    cout << "| Error: Opcion no valida. Por favor, ingresa 's' para confirmar o 'n' para cancelar." << endl;
                }
            }
        }
    } else {
        SetColor(13);
        cout << "\n|| No existen series registradas en la lista." << endl;
        pausarPantalla();
    }
}

void eliminarEpisodioDeSerie(serie** lista) {
    if (listaVaciaSerie(*lista)) {
        SetColor(13);
        cout << "\n|| No existen series registradas\n" << endl;
        pausarPantalla();
        return;
    }

    string nombreSerie, nombreEpisodio;
    cout << endl;
    mostrarSeriesmenu(*lista);
    SetColor(14);
    cout << endl;
    cout << "| Introduce el nombre de la serie: ";

    while (true) {
        getline(cin, nombreSerie);

        if (nombreSerie.empty()) {
            SetColor(12);
            cout << "|| El nombre de la serie no puede estar vacio. Por favor, intentelo de nuevo." << endl;
            cout << "| Introduce el nombre de la serie: ";
        } else {
            serie* serieActual = *lista;
            while (serieActual != NULL && toLowerCase(serieActual->nombreSerie) != toLowerCase(nombreSerie)) {
                serieActual = serieActual->proxSerie;
            }

            if (serieActual == NULL) {
                SetColor(12);
                cout << "|| La serie '" << nombreSerie << "' no esta registrada. Intenta de nuevo." << endl;
                cout << "| Introduce el nombre de la serie: ";
            } else {
                break;
            }
        }
    }

    SetColor(15);
    serie* serieActual = *lista;
    while (serieActual != NULL && toLowerCase(serieActual->nombreSerie) != toLowerCase(nombreSerie)) {
        serieActual = serieActual->proxSerie;
    }

    SetColor(15);
    cout << "| Episodios de la serie '" << nombreSerie << "':" << endl;
    episodios* episodioActual = serieActual->listaEpisodio;

    if (episodioActual == NULL) {
        SetColor(13);
        cout << "|| No hay episodios registrados para esta serie." << endl;
        pausarPantalla();
        return;
    }

    while (episodioActual != NULL) {
        cout << "- " << episodioActual->nombreEpisodio << endl;
        episodioActual = episodioActual->proxEpisodio;
    }

    SetColor(14);
    cout << "|| Introduce el nombre del episodio a eliminar: ";

    while (true) {
        getline(cin, nombreEpisodio);

        if (nombreEpisodio.empty()) {
            SetColor(12);
            cout << "|| El nombre del episodio no puede estar vacio. Por favor, intentelo de nuevo." << endl;
            cout << "|| Introduce el nombre del episodio a eliminar: ";
        } else {
            episodioActual = serieActual->listaEpisodio;
            while (episodioActual != NULL) {
                if (toLowerCase(episodioActual->nombreEpisodio) == toLowerCase(nombreEpisodio)) {
                    SetColor(15);
                    string opcion;
                    while (true) {
                        cout << "| Estas seguro de que deseas eliminar el episodio '" << nombreEpisodio << "'? (s/n): ";
                        getline(cin, opcion);

                        if (opcion.empty()) {
                            SetColor(12);
                            cout << "|| La opcion no puede estar vacia. Introduce 's' para si o 'n' para no." << endl;
                        } else if (opcion == "s" || opcion == "S") {
                            eliminarEpisodio(&(serieActual->listaEpisodio), nombreEpisodio);
                            SetColor(14);
                            cout << "* El episodio '" << nombreEpisodio << "' ha sido eliminado correctamente." << endl;
                            pausarPantalla();
                            return;
                        } else if (opcion == "n" || opcion == "N") {
                            SetColor(13);
                            cout << "| Operacion cancelada. No se elimino ningun episodio." << endl;
                            pausarPantalla();
                            return;
                        } else {
                            SetColor(12);
                            cout << "|| Opcion no valida. Introduce 's' para si o 'n' para no." << endl;
                        }
                    }
                }
                episodioActual = episodioActual->proxEpisodio;
            }

            SetColor(12);
            cout << "|| El episodio '" << nombreEpisodio << "' no se encuentra en la lista de esta serie. Intenta de nuevo." << endl;
            cout << "|| Introduce el nombre del episodio a eliminar: ";
        }
    }
}


//funciones de LLENAR
void llenarSeries(serie** lista) {
    if (listaVaciaSerie(*lista)) {
        int cantidad = 0;
        string nombrelist, nombreSerie;

        while (true) {
            SetColor(4);
            cout << "| Nombre a la lista de series: "; 
            getline(cin, nombrelist);
            if (nombrelist.empty()) {
                SetColor(13);
                cout << "| Error: El nombre de la lista no puede estar vacio."<< endl;
                continue;
            } else {
                break;  
            }
        }

        SetColor(14);
        cout << endl;

        bool cantidadValida = false;
        while (!cantidadValida) {
            SetColor(14);
            cout << "| Cantidad de series a agregar a la lista '" << nombrelist << "': ";

            string cantidadStr;
            getline(cin, cantidadStr);

            if (cantidadStr.empty()) {
                SetColor(13);
                cout << "| Error: La cantidad no puede estar vacia." << endl;
                continue;  
            }

            stringstream ss(cantidadStr);
            if (ss >> cantidad && cantidad > 0 && ss.eof()) {
                cantidadValida = true;  
            } else {
                SetColor(13);
                cout << "| Error: La cantidad debe ser un numero entero positivo." << endl;
            }
        }

        int i = 1;
        while (i <= cantidad) {
            SetColor(4);
            cout << "\n| Rellena las siguientes preguntas sobre la serie " << i << endl;

            SetColor(15);
            bool nombreSerieValido = false;
            while (!nombreSerieValido) {
                SetColor(15);
                cout << " * Nombre de la serie: ";
                getline(cin, nombreSerie);

                if (nombreSerie.empty()) {
                    SetColor(13);
                    cout << "| Error: El nombre de la serie no puede estar vacio." << endl;
                } else if (buscarSerie(*lista, nombreSerie)) {  
                    SetColor(13);
                    cout << "| Error: Ya existe una serie con el nombre '" << nombreSerie << "'. Ingresa otro nombre." << endl;
                } else {
                    nombreSerieValido = true;  
                }
            }


            toLowerCase(nombreSerie);
            
        
            insertarUltimaSerie(lista, nombreSerie);
            i++;
        }
        pausarPantalla();
    }
    else {
        limpiarPantalla();
        SetColor(13);
        cout << "\n|| La lista ya contiene elementos." << endl;
        mostrarSeries(*lista);
        pausarPantalla();
    }
}


//LLENAR LISTA CON Episodios
void llenarEpisodiosEnSerie(serie** listaSeries) {
    if (!listaVaciaSerie(*listaSeries)) {
        string nombreSerie;
        int cantidad;
        string nombreEpisodio;

        mostrarSeriesmenu(*listaSeries);
        SetColor(14);
        cout << endl;
        cout << "| Ingrese el nombre de la serie a la que quiere agregar episodios: ";

        while (true) {
            getline(cin, nombreSerie);
            if (nombreSerie.empty()) {
                SetColor(13);
                cout << "|| El nombre de la serie no puede estar vacio. Intenta nuevamente: ";
            } else {
                break;  // Salir del bucle si el nombre no está vacío
            }
        }

        toLowerCase(nombreSerie);  // Convertir el nombre a minúsculas

        serie* serieSeleccionada = buscarSerie(*listaSeries, nombreSerie);  // Uso de tu función de búsqueda

        // Continuar buscando la serie hasta que se ingrese un nombre válido
        while (serieSeleccionada == NULL) {
            SetColor(13);
            cout << "|| La serie '" << nombreSerie << "' no fue encontrada. Intente nuevamente." << endl;
            cout << "| Ingrese el nombre de la serie nuevamente: ";
            
            while (true) {
                getline(cin, nombreSerie);
                if (nombreSerie.empty()) {
                    SetColor(13);
                    cout << "|| El nombre de la serie no puede estar vacio. Intenta nuevamente: ";
                } else {
                    break;  // Salir del bucle si el nombre no está vacío
                }
            }

            toLowerCase(nombreSerie);  // Convertir el nombre a minúsculas
            serieSeleccionada = buscarSerie(*listaSeries, nombreSerie);  // Buscar nuevamente la serie
        }

        // Si la serie fue encontrada
        if (serieSeleccionada != NULL) {
            if (serieSeleccionada->listaEpisodio != NULL) {

                SetColor(14);
                cout << "| La serie '" << serieSeleccionada->nombreSerie << "' ya tiene episodios registrados." << endl;
                cout << endl;
                SetColor(15);
                cout << "| Que desea hacer?" << endl;
                SetColor(15);
                cout << "| 1. Eliminar los episodios existentes." << endl;
                cout << "| 2. Agregar nuevos episodios a la lista." << endl;
                cout << "| 3. Volver al submenu." << endl;
                SetColor(14);
                cout << "| Elija una opcion: ";

                int opcion;
                while (true) {
                    string input;
                    getline(cin, input);

                    try {
                        opcion = stoi(input);
                        if (opcion >= 1 && opcion <= 3) {
                            break;
                        } else {
                            throw invalid_argument("Opcion no valida");
                        }
                    } catch (const exception& e) {
                        SetColor(13);
                        cout << "|| Opcion no valida. Por favor, seleccione 1, 2 o 3." << endl;
                        SetColor(4);
                        cout << "| Elija una opcion: ";
                    }
                }

                if (opcion == 1) {
                    SetColor(15);
                    cout << "| Se eliminaran todos los episodios de la serie '" << serieSeleccionada->nombreSerie << "'." << endl;
                    serieSeleccionada->listaEpisodio = NULL;
                    cout << "| Lista de episodios eliminada. Puede agregar nuevos episodios ahora." << endl;
                } else if (opcion == 2) {
                    SetColor(14);
                    cout << "| Cuantos episodios desea agregar? ";
                    string cantidadStr;
                    getline(cin, cantidadStr);
                    stringstream ss(cantidadStr);
                    while (!(ss >> cantidad) || cantidad <= 0) {
                        SetColor(13);
                        cout << "| Error: La cantidad debe ser un numero entero positivo." << endl;
                        SetColor(14);
                        cout << "| Intente nuevamente: ";
                        getline(cin, cantidadStr);
                        ss.str(cantidadStr);
                        ss.clear();
                    }

                    int i = 1;
                    while (i <= cantidad) {
                        SetColor(14);
                        bool nombreEpisodioValido = false;
                        while (!nombreEpisodioValido) {
                            cout << "|| * Nombre del episodio " << i << ": ";
                            getline(cin, nombreEpisodio);

                            if (nombreEpisodio.empty()) {
                                SetColor(13);
                                cout << "| Error: El nombre del episodio no puede estar vacio." << endl;
                            } else {
                                nombreEpisodioValido = true;
                            }
                        }
                        insertarUltimoEpisodio(&(serieSeleccionada->listaEpisodio), nombreEpisodio, i);
                        i++;
                    }
                    SetColor(14);
                    cout << "| Episodios agregados correctamente." << endl;
                } else if (opcion == 3) {
                    SetColor(14);
                    cout << "| Volviendo al submenu..." << endl;
                    return;
                }
            } else {
                SetColor(15);
                cout << "| No hay episodios en esta serie. Puede agregar nuevos episodios ahora." << endl;
                SetColor(14);
                cout << endl;
                cout << "| Cuantos episodios desea agregar? ";
                string cantidadStr;
                getline(cin, cantidadStr);
                stringstream ss(cantidadStr);
                while (!(ss >> cantidad) || cantidad <= 0) {
                    SetColor(13);
                    cout << "| Error: La cantidad debe ser un numero entero positivo." << endl;
                    cout << "| Intente nuevamente: ";
                    getline(cin, cantidadStr);
                    ss.str(cantidadStr);
                    ss.clear();
                }

                // Agregar episodios
                int i = 1;
                while (i <= cantidad) {
                    SetColor(15);
                    bool nombreEpisodioValido = false;
                    while (!nombreEpisodioValido) {
                        cout << endl;
                        cout << "|| * Nombre del episodio " << i << ": ";
                        getline(cin, nombreEpisodio);

                        if (nombreEpisodio.empty()) {
                            SetColor(13);
                            cout << endl;
                            cout << "| Error: El nombre del episodio no puede estar vacio." << endl;
                        } else {
                            nombreEpisodioValido = true;
                        }
                    }
                    insertarUltimoEpisodio(&(serieSeleccionada->listaEpisodio), nombreEpisodio, i);
                    i++;
                }
                SetColor(14);
                cout << endl;
                cout << "| Episodios agregados correctamente." << endl;
                pausarPantalla();
            }
        }
    } else {
        SetColor(13);
        cout << endl;
        cout << "\n|| No existen series registradas." << endl;
        pausarPantalla();
    }
}

//llenar una serie especifica
void llenarEpisodiosEnSerieEspecifico(serie** serieAgregar, string nombreSerie) {
    if (!listaVaciaSerie(*serieAgregar)) {
        int cantidad;
        string nombreEpisodio;
        serie * serieSeleccionada = buscarSerie(*serieAgregar, nombreSerie);

        SetColor(14);
        if (listaVaciaEpisodio(serieSeleccionada->listaEpisodio)) {

            SetColor(15);
            cout<<endl;
            cout << "| No hay episodios en esta serie. Puede agregar nuevos episodios ahora." << endl;
            SetColor(14);
            cout<<endl;
            cout << "| Cuantos episodios desea agregar? ";
            string cantidadStr;
            getline(cin, cantidadStr);
            stringstream ss(cantidadStr);
            while (!(ss >> cantidad) || cantidad <= 0) {
                SetColor(13);
                cout<<endl;
                cout << "| Error: La cantidad debe ser un numero entero positivo." << endl;
                SetColor(14);
                cout<<endl;
                cout << "| Intente nuevamente: ";
                getline(cin, cantidadStr);
                ss.str(cantidadStr);
                ss.clear();
            }

            // Agregar episodios
            int i = 1;
            while (i <= cantidad) {
                SetColor(14);
                bool nombreEpisodioValido = false;
                while (!nombreEpisodioValido) {
                    cout << "|| * Nombre del episodio " << i << ": ";
                    getline(cin, nombreEpisodio);

                    if (nombreEpisodio.empty()) {
                        SetColor(13);
                        cout << "| Error: El nombre del episodio no puede estar vacio." << endl;
                    } else {
                        nombreEpisodioValido = true;
                    }
                }
                insertarUltimoEpisodio(&(serieSeleccionada->listaEpisodio), nombreEpisodio, i);
                i++;
            }
            SetColor(14);
            cout << "| Episodios agregados correctamente." << endl;
            pausarPantalla();
        } 
        else{
            SetColor(13);
            cout << "|| La serie '" << nombreSerie << "' no fue encontrada." << endl;
            pausarPantalla();
        }
    } 
}

//Funcion para agregar una serie 
void agregarSerie(serie** lista) {
    if (listaVaciaSerie(*lista)) {
        int opcion;

        SetColor(13);
        cout << "\n|| La lista esta vacia. Que desea hacer?" << endl;
        SetColor(15);
        cout << endl;
        cout << "| 1. Agregar una serie a la lista vacia." << endl;
        cout << "| 2. Llenar la lista con multiples series." << endl;
        cout << endl;
        SetColor(14);
        cout << "| Seleccione una opcion: ";

        while (true) {
            string input;
            getline(cin, input);

            try {
                opcion = stoi(input);
                if (opcion == 1 || opcion == 2) {
                    break;
                } else {
                    throw invalid_argument("Opcion no valida");
                }
            } catch (const exception& e) {
                SetColor(13);
                cout << "|| Opcion no valida. Por favor, seleccione 1 o 2." << endl;
                SetColor(4);
                cout << endl;
                SetColor(14);
                cout << "| Seleccione una opcion: ";
            }
        }

        if (opcion == 1) {
            string nombreSerie;
            SetColor(4);
            cout << endl;
            cout << "\n| * Ingrese el nombre de la serie: ";
            while (true) {
                getline(cin, nombreSerie);
                if (nombreSerie.empty()) {
                    SetColor(13);
                    cout << "|| El nombre de la serie no puede estar vacio. Intente nuevamente: ";
                } else if (buscarSerie(*lista, nombreSerie)) {  // Comprobamos si la serie ya existe
                    SetColor(13);
                    cout << "|| Ya existe una serie con el nombre '" << nombreSerie << "'. Intente con otro nombre: ";
                } else {
                    break; 
                }
            }

            toLowerCase(nombreSerie); 
            insertarUltimaSerie(lista, nombreSerie);
            SetColor(14);
            cout << endl;
            cout << "| * La serie '" << nombreSerie << "' se ha agregado a la lista." << endl;
            cout << endl;
            mostrarSeriesmenu(*lista);
        } else if (opcion == 2) {
            llenarSeries(lista);
        }
    } 
    else {
        string nombreSerie;
        SetColor(4);
        cout << endl;
        mostrarSeriesmenu(*lista);
        cout << "\n| * Ingrese el nombre de la nueva serie: ";
        
        while (true) {
            getline(cin, nombreSerie);
            if (nombreSerie.empty()) {
                SetColor(13);
                cout << "|| El nombre de la serie no puede estar vacio. Intente nuevamente: ";
            } else if (buscarSerie(*lista, nombreSerie)) {  
                SetColor(13);
                cout << "|| Ya existe una serie con el nombre '" << nombreSerie << "'. Intente con otro nombre: ";
            } else {
                break; 
            }
        }

        insertarUltimaSerie(lista, nombreSerie);
        SetColor(14);
        cout << "* La serie '" << nombreSerie << "' se ha agregado a la lista." << endl;
        mostrarSeriesmenu(*lista);
        pausarPantalla();
    }
}

//Fucnones de agregar 
void agregarEpisodioASerie(serie** listaSeries) {
    string nombreSerie, nombreEpisodio;
    int opcion = 0;

    if (listaVaciaSerie(*listaSeries)) {
        SetColor(13);
        cout << endl;
        cout << "|| No hay series en la lista. Por favor, agrega series primero." << endl;
    } else {
        mostrarSeriesmenu(*listaSeries);
        while (true) {  // Bucle para asegurarse de ingresar una serie válida o salir
            cout << endl;
            SetColor(14);
            cout << endl;
            cout << "| Ingrese el nombre de la serie donde desea agregar episodios ";
            
            getline(cin, nombreSerie);
            toLowerCase(nombreSerie);

            if (nombreSerie.empty()) {
                SetColor(13);
                cout << "|| El nombre de la serie no puede estar vacio. Intente nuevamente." << endl;
                continue;  // Repetir el bucle
            }


            serie* serieSeleccionada = buscarSerie(*listaSeries, nombreSerie);

            if (serieSeleccionada != NULL) {
                // Serie encontrada, proceder con el resto del proceso
                if (listaVaciaEpisodio(serieSeleccionada->listaEpisodio)) {
                    SetColor(13);
                    cout << endl;
                    cout << "|| La serie '" << serieSeleccionada->nombreSerie << "' no tiene episodios registrados." << endl;
                    cout << endl;
                    SetColor(14);
                    cout << " * Desea agregar un episodio o llenar la lista de episodios?" << endl;
                    SetColor(15);
                    cout << "| 1. Agregar un episodio" << endl;
                    cout << "| 2. Llenar la lista de episodios" << endl;
                    SetColor(14);
                    cout << "| Elija una opcion: ";

                    while (true) {
                        string input;
                        getline(cin, input); 

                        try {
                            opcion = stoi(input); 
                            if (opcion == 1 || opcion == 2) {
                                break; 
                            } else {
                                throw invalid_argument("Opcion no valida");
                            }
                        } catch (const exception& e) {
                            SetColor(13);
                            cout << "|| Opcion no valida. Por favor, seleccione 1 o 2." << endl;
                            cout << endl;
                            SetColor(14);
                            cout << "| Elija una opcion: ";
                        }
                    }

                    if (opcion == 1) {
                        SetColor(15);
                        cout << endl;
                        cout << "|* Ingrese el nombre del episodio: ";
                        getline(cin, nombreEpisodio);

                        while (nombreEpisodio.empty()) {
                            SetColor(13);
                            cout << "|| El nombre del episodio no puede estar vacio. Intente nuevamente: ";
                            getline(cin, nombreEpisodio);
                        }

                        int numeroEpisodio = 1;
                        insertarUltimoEpisodio(&(serieSeleccionada->listaEpisodio), nombreEpisodio, numeroEpisodio);
                        SetColor(14);
                        cout << "| * Episodio agregado exitosamente." << endl;
                        pausarPantalla();
                    } else if (opcion == 2) {
                        llenarEpisodiosEnSerieEspecifico(listaSeries, nombreSerie);
                    }
                } else {
                    SetColor(4);
                    cout << endl;
                    cout << "| Ingrese el nombre del episodio: ";
                    getline(cin, nombreEpisodio);

                    while (nombreEpisodio.empty()) {
                        SetColor(13);
                        cout << endl;
                        cout << "|| El nombre del episodio no puede estar vacio. Intente nuevamente: ";
                        getline(cin, nombreEpisodio);
                    }

                    int numeroEpisodio = cantidadEpisodio(serieSeleccionada->listaEpisodio) + 1; 
                    insertarUltimoEpisodio(&(serieSeleccionada->listaEpisodio), nombreEpisodio, numeroEpisodio);
                    SetColor(14);
                    cout << endl;
                    cout << "| * Episodio agregado exitosamente." << endl;
                    pausarPantalla();
                }
                return;  
            } else {
                SetColor(13);
                cout << "|| La serie '" << nombreSerie << "' no fue encontrada. Intente nuevamente." << endl;
            }
        }
    }
}

void buscarTop5MejoresEpisodios(serie* lista) { 
    serie *serieConMayorAudiencia = obtenerSerieConMayorAudiencia(lista);
    episodios *auxEp = serieConMayorAudiencia->listaEpisodio;

    episodios* top1 = NULL;
    episodios* top2 = NULL;
    episodios* top3 = NULL;
    episodios* top4 = NULL;
    episodios* top5 = NULL;

    while (auxEp != NULL) {

      
        if (top1 == NULL || auxEp->puntuacion > top1->puntuacion) {
            top5 = top4;  
            top4 = top3;
            top3 = top2;
            top2 = top1;
            top1 = auxEp; 
        }

        else if (top2 == NULL || auxEp->puntuacion > top2->puntuacion) {
            top5 = top4;
            top4 = top3;
            top3 = top2;
            top2 = auxEp;
        }

        else if (top3 == NULL || auxEp->puntuacion > top3->puntuacion) {
            top5 = top4;
            top4 = top3;
            top3 = auxEp;
        }

        else if (top4 == NULL || auxEp->puntuacion > top4->puntuacion) {
            top5 = top4;
            top4 = auxEp;
        }

        else if (top5 == NULL || auxEp->puntuacion > top5->puntuacion) {
            top5 = auxEp;
        }

        auxEp = auxEp->proxEpisodio;
    }
    
    SetColor(14);
    cout << "\n---------------------------------------------" << endl;
    SetColor(15);
    cout << "|     TOP 5 episodios con mayor puntuacion " << endl;
    SetColor(14);
    cout << "|  Nombre de la serie:"<< serieConMayorAudiencia->nombreSerie << endl;
    SetColor(14);
    cout << "---------------------------------------------" << endl;
    SetColor(15);

    if (top1 != NULL) {
        cout << "| 1. " << top1->nombreEpisodio << " - Puntuacion: " << top1->puntuacion << endl;
    }
    if (top2 != NULL) {
        cout << "| 2. " << top2->nombreEpisodio << " - Puntuacion: " << top2->puntuacion << endl;
    }
    if (top3 != NULL) {
        cout << "| 3. " << top3->nombreEpisodio << " - Puntuacion: " << top3->puntuacion << endl;
    }
    if (top4 != NULL) {
        cout << "| 4. " << top4->nombreEpisodio << " - Puntuacion: " << top4->puntuacion << endl;
    }
    if (top5 != NULL) {
        cout << "| 5. " << top5->nombreEpisodio << " - Puntuacion: " << top5->puntuacion << endl;
    }


    SetColor(13);
    int contador = 0;
    if (top1 != NULL) contador++;
    if (top2 != NULL) contador++;
    if (top3 != NULL) contador++;
    if (top4 != NULL) contador++;
    if (top5 != NULL) contador++;

    if (contador < 5) {
        cout << "\n| ATENCION: Solo hay " << contador << " episodios en la lista." << endl;
    }

    SetColor(14);
    cout << "---------------------------------------------" << endl;
}

//ARCHIVOS
void guardarDatosEnArchivo(serie *lista, string archivoDir) {
    ofstream archivo(archivoDir); // Abre el archivo en modo escritura
    if (!archivo.is_open()) {
        SetColor(13);
        cout << "Error al abrir el archivo para guardar." << endl;
        return;
    }

    serie *auxSerie = lista; // Puntero auxiliar para recorrer la lista de series
    while (auxSerie != NULL) {
        // Escribe los datos de la serie
        archivo << "SERIE\n";
        archivo << auxSerie->nombreSerie << "\n";
        archivo << auxSerie->genero << "\n";
        archivo << auxSerie->audienciaSerie << "\n";
        archivo << auxSerie->clasSerie << "\n";
        archivo << auxSerie->fechaSerie << "\n";
        archivo << auxSerie->duracionSerie << "\n";

        // Recorre la lista de episodios de la serie actual
        episodios *auxEp = auxSerie->listaEpisodio;
        while (auxEp != NULL) {
            // Escribe los datos del episodio
            archivo << "EPISODIO\n";
            archivo << auxEp->nombreEpisodio << "\n";
            archivo << auxEp->numeroEpisodio << "\n";
            archivo << auxEp->duracionEpisodio << "\n";
            archivo << auxEp->puntuacion << "\n";
            auxEp = auxEp->proxEpisodio; // Avanza al siguiente episodio
        }

        archivo << "FIN_SERIE\n"; // Marca el final de la serie
        auxSerie = auxSerie->proxSerie; // Avanza a la siguiente serie
    }

    archivo.close(); // Cierra el archivo
    SetColor(14);
    cout << "Datos guardados exitosamente!" << endl;
}


void guardarSerieConMayorAudienciaEnArchivo(serie* lista, string archivoDir) {
    ofstream archivo(archivoDir + "serie_con_mayor_audiencia.txt");
    if (!archivo.is_open()) {
        SetColor(13);
        cout << "Error al abrir el archivo para guardar." << endl;
        return;
    }

    if(lista == NULL) {
        SetColor(13);
        cout << "No hay series en la lista." << endl;
        return;
    }

    serie* serieConMayorAudiencia = obtenerSerieConMayorAudiencia(lista);
    archivo << "SERIE\n";
    archivo << serieConMayorAudiencia->nombreSerie << "\n";
    archivo << serieConMayorAudiencia->genero << "\n";
    archivo << serieConMayorAudiencia->audienciaSerie << "\n";
    archivo << serieConMayorAudiencia->clasSerie << "\n";
    archivo << serieConMayorAudiencia->fechaSerie << "\n";
    archivo << serieConMayorAudiencia->duracionSerie << "\n";

    episodios* auxEp = serieConMayorAudiencia->listaEpisodio;

    episodios* top1 = NULL;
    episodios* top2 = NULL;
    episodios* top3 = NULL;
    episodios* top4 = NULL;
    episodios* top5 = NULL;

    int contadorEpisodios = 0;

    while (auxEp != NULL) {
        contadorEpisodios++;

        if (top1 == NULL || auxEp->puntuacion > top1->puntuacion) {
            top5 = top4;  
            top4 = top3;
            top3 = top2;
            top2 = top1;
            top1 = auxEp; 
        }
        else if (top2 == NULL || auxEp->puntuacion > top2->puntuacion) {
            top5 = top4;
            top4 = top3;
            top3 = top2;
            top2 = auxEp;
        }
        else if (top3 == NULL || auxEp->puntuacion > top3->puntuacion) {
            top5 = top4;
            top4 = top3;
            top3 = auxEp;
        }
        else if (top4 == NULL || auxEp->puntuacion > top4->puntuacion) {
            top5 = top4;
            top4 = auxEp;
        }
        else if (top5 == NULL || auxEp->puntuacion > top5->puntuacion) {
            top5 = auxEp;
        }

        auxEp = auxEp->proxEpisodio;
    }

    archivo << "TOP 5 EPISODIOS MEJOR PUNTUADOS\n";
    if (contadorEpisodios == 0) {
        archivo << "La serie no tiene episodios.\n";
    } else if (contadorEpisodios == 1) {
        archivo << "La serie solo tiene 1 episodio.\n";
    } else if (contadorEpisodios == 2) {
        archivo << "La serie solo tiene 2 episodios.\n";
    } else if (contadorEpisodios == 3) {
        archivo << "La serie solo tiene 3 episodios.\n";
    } else if (contadorEpisodios == 4) {
        archivo << "La serie solo tiene 4 episodios.\n";
    }

    if (top1 != NULL) {
        archivo << "1. " << top1->nombreEpisodio << " - Puntuacion: " << top1->puntuacion << "\n";
    }
    if (top2 != NULL) {
        archivo << "2. " << top2->nombreEpisodio << " - Puntuacion: " << top2->puntuacion << "\n";
    }
    if (top3 != NULL) {
        archivo << "3. " << top3->nombreEpisodio << " - Puntuacion: " << top3->puntuacion << "\n";
    }
    if (top4 != NULL) {
        archivo << "4. " << top4->nombreEpisodio << " - Puntuacion: " << top4->puntuacion << "\n";
    }
    if (top5 != NULL) {
        archivo << "5. " << top5->nombreEpisodio << " - Puntuacion: " << top5->puntuacion << "\n";
    }

    archivo << "FIN_SERIE\n";
    archivo.close();

    SetColor(14);
    cout << "Serie con mayor audiencia guardada exitosamente!" << endl;
}


void cargarDatosDesdeArchivo(serie **lista, string archivoDir) {
    ifstream archivo(archivoDir);
    if (!archivo.is_open()) {
        cout << "Error al abrir el archivo para cargar." << endl;
        return;
    }

    if (archivo.peek() == ifstream::traits_type::eof()) {
        cout << "El archivo esta vacio." << endl;
        archivo.close();
        return;
    }

    string linea;
    serie *serieActual = NULL;

    cout << "Cargando datos desde archivo..." << endl;

    while (getline(archivo, linea)) {
        if (linea == "SERIE") {
            string nombreSerie, genero;
            int audiencia, clasificacion, fecha, duracion;

            getline(archivo, nombreSerie);
            getline(archivo, genero);
            archivo >> audiencia >> clasificacion >> fecha >> duracion;
            archivo.ignore(); // Para manejar el salto de línea pendiente después de leer los enteros

            // Crear la nueva serie
            serieActual = crearSerie(nombreSerie);
            serieActual->genero = genero;
            serieActual->audienciaSerie = audiencia;
            serieActual->clasSerie = clasificacion;
            serieActual->fechaSerie = fecha;
            serieActual->duracionSerie = duracion;

            // Añadir la serie a la lista
            if (*lista == NULL) {
                *lista = serieActual;
            } else {
                serie *aux = *lista;
                while (aux->proxSerie != NULL) {
                    aux = aux->proxSerie;
                }
                aux->proxSerie = serieActual;
            }
        } else if (linea == "EPISODIO") {
            if (serieActual == NULL) {
                cout << "Error: No se puede agregar un episodio sin una serie." << endl;
                continue;
            }

            string nombreEpisodio;
            int numero, duracion, puntuacion;

            getline(archivo, nombreEpisodio);
            archivo >> numero >> duracion >> puntuacion;
            archivo.ignore(); // Para manejar el salto de línea

            // Crear nuevo episodio
            episodios *nuevoEpisodio = crearEpisodio(nombreEpisodio, numero);
            nuevoEpisodio->duracionEpisodio = duracion;
            nuevoEpisodio->puntuacion = puntuacion;

            // Añadir el episodio a la lista de episodios de la serie actual
            if (serieActual->listaEpisodio == NULL) {
                serieActual->listaEpisodio = nuevoEpisodio;
            } else {
                episodios *aux = serieActual->listaEpisodio;
                while (aux->proxEpisodio != NULL) {
                    aux = aux->proxEpisodio;
                }
                aux->proxEpisodio = nuevoEpisodio;
            }
        }
    }

    archivo.close();
    cout << "Datos cargados exitosamente!" << endl;

}

//los menus
void menuOperaciones(serie** lista) {
    int subOpcion;
    string input;
    do {
        SetColor(4);  
        cout << "\n";
        cout << "+--------------------------------------------------+\n";  
        cout << "|              *DEBOVER sub-MENU*                  |\n";
        SetColor(14); 
        cout << "|             Submenu de Operaciones               |\n";
        SetColor(4);
        cout << "+--------------------------------------------------+\n";

        SetColor(14);  
        cout << "|| LLENAR                 \n";
        SetColor(15);
        cout << "| 1. Llenar con multiples series.                  \n";
        cout << "| 2. Llenar serie con multiples episodios.         \n";
        SetColor(14);
        cout << "|| AGREGAR                 \n";
        SetColor(15);
        cout << "| 3. Agregar una serie.                                \n";
        cout << "| 4. Agregar una episodio a serie.                     \n";
        SetColor(14);
        cout<<"|| ORDENAMIENTO\n";
        SetColor(15);
        cout << "| 5. Ordenar alfabeticamente las series.           \n";
        SetColor(14);
        cout << "|| ELIMINAR                 \n";
        SetColor(15);
        cout << "| 6. Eliminar serie especifica.                    \n";
        cout << "| 7. Eliminar episodio especifico.                 \n";
        SetColor(14);
        cout << "|| MOSTRAR:                 \n";
        SetColor(15);
        cout << "| 8. Mostrar lista de series.                      \n";
        cout << "| 9. Mostrar series con sus respectivos episodios.                  \n";
        SetColor(14);
        cout << "|| DATOS:                 \n";
        SetColor(15);
        cout << "| 10. Top 3 series con mayor audiencia.     \n";
        cout << "| 11. Episodio que dura mas tiempo de una serie.             \n";
        cout << "| 12. Episodio con mayor puntuacion de una serie.             \n";
        cout<< "| 13. Serie con mayor audiencia y top 5 episodios mejor puntuados.             \n";
        SetColor(14);
        cout << "|| ARCHIVOS      \n";
        SetColor(15);
        cout << "| 14. Guardar serie con mayor audiencia y top 5 episodios mejor puntuados.    \n";
        cout << "| 15. Volver al menu principal para guardar el registro.                    \n";
        SetColor(4);
        cout << "+--------------------------------------------------+\n";

        SetColor(15);
        mostrarSeriesmenu(*lista);

        SetColor(14);  
        cout << "\nElige una opcion (1-15): ";
        getline(cin, input);

        if (input.empty()) {
            SetColor(13); 
            cout << "\n|| ERROR. No se ingreso ninguna opcion. Por favor, ingresa un numero. \n";
            pausarPantalla();
            continue;
        }
        stringstream ss(input);
        if (!(ss >> subOpcion)) {
            SetColor(13); 
            cout << "\n|| ERROR. Debes ingresar un numero valido.\n";
            pausarPantalla();
            continue; 
        }

        switch(subOpcion) {
            case 1:
                limpiarPantalla();
                llenarSeries(lista);
                break;
            case 2:
                limpiarPantalla();
                llenarEpisodiosEnSerie(lista);
                break;
            case 3:
                limpiarPantalla();
                agregarSerie(lista);
                break;
            case 4:
                limpiarPantalla();
                agregarEpisodioASerie(lista);
                break;
            case 5:
                limpiarPantalla();
                ordenarSeriesAlfabeticamente(lista);
                pausarPantalla();
                break;
            case 6:
                limpiarPantalla();
                eliminarSerieEspecifica(lista);
                break;
            case 7:
                limpiarPantalla();
                eliminarEpisodioDeSerie(lista);
                break;
            case 8:
                limpiarPantalla();
                mostrarSeries(*lista);
                pausarPantalla();
                break;
            case 9:
                limpiarPantalla();
                mostrarSeriesEpisodios(*lista);
                pausarPantalla();
                break;
            case 10:
                limpiarPantalla();
                mostrarTop3Audiencia(*lista);
                pausarPantalla();
                break;
            case 11:
                limpiarPantalla();
                mostrar_episodio_que_dura_mas_tiempo(*lista);
                pausarPantalla();
                break;
            case 12:
                limpiarPantalla();
                mostrarEpisodioMayorPuntacion(*lista);
                pausarPantalla();
                break;
            case 13:
                limpiarPantalla();
                buscarTop5MejoresEpisodios(*lista);
                pausarPantalla();
                break;
            case 14:
                limpiarPantalla();
                guardarSerieConMayorAudienciaEnArchivo(*lista,"C:\\datos\\");
                pausarPantalla();
                break;
            case 15:
                limpiarPantalla();
                guardarDatosEnArchivo(*lista,"C:\\datos\\series_data.txt");
                cout << "Volviendo al menu principal...\n";
                break;
            default:
                SetColor(13);  
                cout << "\n|| Opcion no valida. Por favor, elige una opcion entre 1 y 13.\n";
                pausarPantalla();
                break;
        }
    } while(subOpcion != 15 ); {}
}



//aqui no se modifico nada 
// Aquí no se necesita crear una copia de la lista, solo trabaja con la lista original
void menuPrincipal(serie** lista) {
    int opcion;
    string input;

    cargarDatosDesdeArchivo(lista, "C:\\datos\\series_data.txt"); // Carga de datos
    pausarPantalla(); 
    do {
        SetColor(14); 
        cout << "+-----------------------------------------+\n";
        SetColor(4);  
        cout << "|         BIENVENIDO A DEBOVER            |\n";
        SetColor(14);  
        cout << "+-----------------------------------------+\n";
        SetColor(15); 
        cout << "|  1. Operaciones series y episodios     |\n";
        cout << "|  2. Vaciar archivo                     |\n";
        cout << "|  3. Salir                              |\n";  
        SetColor(14);  
        cout << "+-----------------------------------------+\n";
        SetColor(14);
        cout << "\nElige una opcion: ";
        getline(cin, input);


        if (input.empty()) {
            SetColor(13); 
            cout << "\n|| ERROR. No se ingreso ninguna opcion. Por favor, ingresa un numero.\n";
            cout << endl;
            continue;
        }

        stringstream ss(input);
        if (!(ss >> opcion)) {
            SetColor(13); 
            cout << "\n|| ERROR. Debes ingresar un numero valido.\n";
            pausarPantalla();
            continue; 
        }

        switch (opcion) {
            case 1:
                limpiarPantalla();
                menuOperaciones(lista);  // Pasamos directamente el puntero a la lista
                break;
            case 2:
                SetColor(15); 
                borrarContenidoArchivo("C:\\datos\\series_data.txt");  // Llamada para borrar el contenido del archivo
                break;
            case 3:
                cout << "Saliendo...\n";
                break;
            default: 
                SetColor(13);  
                cout << "\n|| ERROR. Opcion no valida. Debes elegir entre 1 y 2 :D.\n";
                cout << endl;
                break;
        }
    } while (opcion != 3); // Salir cuando la opción es 2
}

int main() {
    serie* listaSeries = NULL;  

    menuPrincipal(&listaSeries);  
}
