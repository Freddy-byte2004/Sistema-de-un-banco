# Sistema-de-un-banco
codigo sencillo que busca simular el sistema de un banco en c++
#include <iostream>
#include<stdlib.h>
using namespace std;
void Interfaz();
class Cuenta{
private:
    int Numero_de_cuenta[100];
    string tipo_de_cuenta;
    int saldo[100];
    int movimientos;

public:
    Cuenta(string tipo_cuenta){
    tipo_cuenta=tipo_de_cuenta;
    movimientos=0;
    }
    void setCuenta(int i){ //Todos los numeros de cuentas creados van a ser la suma de la cuenta base + i
   int generador_de_cuenta,cuenta_base;
        cuenta_base=11201000;
         generador_de_cuenta=cuenta_base+i;
       cuenta_base=cuenta_base+1;
       Numero_de_cuenta[i]=generador_de_cuenta;
    }
   int getCuenta(int i){
       return Numero_de_cuenta[i];
   }
   string gettipo(){
   return tipo_de_cuenta;
   }
    int getsaldo(int i){
    return saldo[i];
    }
    void setsaldo(int monto, int i){
    saldo[i]=monto;
    }
    void Consultar_saldo(int contador_universal){
        system("cls");
        int N_cuenta,i,policia=0;
    cout<< "Ingrese el numero de cuenta de la cuenta a consultar"<<endl;
    cin>> N_cuenta;
    for(i=0;i<=contador_universal;i++){
    if(N_cuenta!=Numero_de_cuenta[i]){
        policia=0;
    }
    else{
        policia=1;
    break;
    }
    }
    if(policia==0){
        cout<<"El numero de cuenta no existe"<<endl;
    }
    else{
        cout<< "Su saldo es: "<<saldo[N_cuenta-11201000]<<endl;
    }
    }

    void depositar(int monto,int i){
        saldo[i]=saldo[i]+monto;
    }
    void retirar(int monto,int i){
        saldo[i]=saldo[i]-monto;
    }
    void movimiento(int cantidad_deposito[100],int monto_deposito[100][100],int cantidad_retiro[100],int monto_retiro[100][100]){
        int N_cuenta;
        int indice_cuenta;
        int aux_deposito,aux_retiro;
cout<< "Ingrese el numero de cuenta de la cuenta a consultar"<<endl;
cin>>N_cuenta;
indice_cuenta=N_cuenta-11201000;
aux_deposito=cantidad_deposito[indice_cuenta];
aux_retiro=cantidad_retiro[indice_cuenta];

    if((cantidad_deposito[indice_cuenta]==0)&&(cantidad_retiro[indice_cuenta]==0)){
        cout<< "No hay movimiento en la cuenta"<<endl;
    }
    while((cantidad_deposito[indice_cuenta]>0)||(cantidad_retiro[indice_cuenta]>0)){
            if(cantidad_deposito[indice_cuenta]>0){
              cout<< "se deposito: "<< monto_deposito[indice_cuenta][cantidad_deposito[indice_cuenta]]<<endl;
              cantidad_deposito[indice_cuenta]--;
            }

        if (cantidad_retiro[indice_cuenta]>0){
        cout<< "se retiro: "<<monto_retiro[indice_cuenta][cantidad_retiro[indice_cuenta]]<<endl;

        cantidad_retiro[indice_cuenta]--;
        }

    }
    cantidad_deposito[indice_cuenta]=aux_deposito;
    cantidad_retiro[indice_cuenta]=aux_retiro;
    }
};
class Cliente{
private:
    string nombre;
    int cedula;
    string direccion;
    double telefono;


public:
    Cliente(string Nombre,int Cedula,string Direccion, double Telefono){

        nombre=Nombre;
    cedula=Cedula;
    direccion=Direccion;
    telefono=Telefono;
    }
    string getnombre(){
    return nombre;}
    int getcedula(){
    return cedula;}
    string getdireccion(){
    return direccion;}
    int gettelefono(){
    return telefono;}
    void setnombre(string Nombre){
    nombre=Nombre;
    }
    void setcedula(int Cedula){
    cedula=Cedula;
    }
    void settelefono(int Telefono){
    telefono=Telefono;
    }
    void setdireccion(string Direccion){
    direccion=Direccion;
    }

    void Crear_cuenta(){
        string Tipo_de_cuenta;
       cout<<"Ingrese su nombre"<<endl;
       cin>> nombre;
       cout<< "Ingrese su cedula"<<endl;
       cin>>cedula;
       cout<< "Ingrese su direccion"<<endl;
       cin>>direccion;
       cout<< "Ingrese su numero de telefono"<<endl;
       cin>> telefono;
       cout<< "Si su cuenta va a ser de ahorro Ingrese ahorro"<<endl;
       cout<< "Si su cuenta va a ser corriente ingrese corriente"<<endl;
       cin>> Tipo_de_cuenta;
    };
    void Eliminar_cuenta();
    void Consultar_cuenta();

};
void Interfaz(){
//Esta funcion es tiene como objetivo ser una interfaz entre el usuario y los objetos de la clases cuenta y cliente
Cuenta x(" ");
Cliente y(" ",0, " ",0);
int N_cuenta,policia=0,indice_cuenta;// La variable N_cuenta tiene la funcion de almacenar el numero de cuenta que ingresa el usuario, la variable policia tiene la funcion de indicar si se encontro el numero de cuenta y la variable indice_de_cuenta es una varibale que indica la posicion del array donde se encuentra almacenado el numero de cuenta
int opcion=0,i=1;// i es el indicador universal que indica donde se almacena o se almacenara los datos de la cuenta, como: saldo y numero de cuenta
string usuario,opcion_cuenta;
int cuenta_origen,cuenta_destino,monto;// estas variables seran utilizadas en la opcion de transferencia
int cantidad_deposito[100],cantidad_retiro[100],monto_deposito[100][100],monto_retiro[100][100];// estas variables seran utilizadas para la opcion de mostrar los movimientos, la variable cantidad_deposito,cantidad_retiro indican la cantidad de depositos y retiros que hizo la cuenta, y las matrices monto_deposito, monto_retiro almacenan el monto de retiro o deposito realizado por la cuenta

for(int j=1;j<100;j++){
    cantidad_deposito[j]=0;
    cantidad_retiro[j]=0;
}// este bucle lo hice para inicializar en cero todas las cantidades de deposito o retiro realizado por la cuenta, en total son 100 porque el sistema esta diseñado solo para 100 usuarios
while (opcion!=8){
system("cls");
cout<< "Bienvenido al banco de Venezuela"<<endl;
cout<<endl;
cout<< "1)Crear Cuenta"<<endl;
cout<< "2)Depositar "<<endl;
cout<< "3)Retirar "<<endl;
cout<< "4)Transferir"<<endl;
cout<< "5)Consultar Saldo"<<endl;
cout<< "6)Consultar Movimientos"<<endl;
cout<< "7)Salir"<<endl<<endl;
cout<<"Ingrese una opcion>> ";cin>>opcion;


switch(opcion){
case 1:
    system("cls");
    if(i>1){
        cout<<"Usted ya ha creado una cuenta anteriormente"<<endl;
        cout<<"¿Desea crear una nueva cuenta?"<<endl;
        cout<< "Ingrese si/no >> ";cin>>opcion_cuenta;
        if(opcion_cuenta=="si"){
                x.setCuenta(i);
                x.setsaldo(0,i);
       cout<<"Se ha creado correctamente su cuenta asociada al numero de cuenta: "<<x.getCuenta(i)<<endl;
       i++;
       system("pause");
        }
        else{system("pause");}
    }
    if(i<=1){
    y.Crear_cuenta();

    x.setCuenta(i);
    x.setsaldo(0,i);
    cout<< "Cuenta del cliente: "<<y.getnombre()<<" Titular de la cedula: "<<y.getcedula()<<" Con el numero de cuenta: "<<x.getCuenta(i)<< " creado correctamente "<<endl;
    i++;
    system("pause");
    }
    break;
case 2:
    system("cls");

    cout<< "Ingrese el numero de cuenta de la cuenta a depositar"<<endl;
    cin>>N_cuenta;
    for(int j=0;j<i;j++){

        if(x.getCuenta(j)==N_cuenta){
            policia=1;
        }
    }
    if(policia==1){
            indice_cuenta=N_cuenta-11201000;
            cantidad_deposito[indice_cuenta]++;
    cout<<"Su cuenta si existe"<<endl;
    cout<< "Ingrese el monto a depositar"<<endl;
    cin>> monto;
    monto_deposito[indice_cuenta][cantidad_deposito[indice_cuenta]]=monto;
    x.depositar(monto,indice_cuenta);
    policia=0;
    N_cuenta=0;
    indice_cuenta=0;
    system("pause");
    }
    else{

        cout<< "El numero de cuenta ingresado no existe"<<endl;
        system("pause");
    }

    break;


case 3:
     system("cls");
     cout<< "Ingrese el numero de cuenta de la cuenta a retirar"<<endl;
     cin>>N_cuenta;
    for(int j=0;j<i;j++){

        if(x.getCuenta(j)==N_cuenta){
            policia=1;
        }
    }
    if(policia==1){
            indice_cuenta=N_cuenta-11201000;
            cantidad_retiro[indice_cuenta]++;
    cout<<"Su cuenta si existe"<<endl;
    cout<< "Ingrese el monto a retirar"<<endl;
    cin>> monto;
    if((x.getsaldo(indice_cuenta)-monto)>0){
    monto_retiro[indice_cuenta][cantidad_retiro[indice_cuenta]]=monto;
    x.retirar(monto,indice_cuenta);
    policia=0;
    N_cuenta=0;
    indice_cuenta=0;
    system("pause");

    }
    else{
        cout<< "La cuenta no tiene saldo suficiente"<<endl;
        system("pause");
    }
    }
    else{
        cout<< "El numero de cuenta ingresado no existe"<<endl;
        system("pause");
    }
    break;

case 4:

    system("cls");
    cout<<"Ingrese la cuenta de origen de los fondos"<<endl;
    cin>>cuenta_origen;
    cout<<"Ingrese la cuenta destino"<<endl;
    cin>>cuenta_destino;
    cout<<"Ingrese el monto"<<endl;
    cin>>monto;
    if((x.getsaldo(cuenta_origen-11201000)-monto)>0){
    cantidad_deposito[cuenta_destino- 11201000]++;
    cantidad_retiro[cuenta_origen- 11201000]++;
    monto_retiro[cuenta_origen- 11201000][cantidad_retiro[cuenta_origen- 11201000]]=monto;
     monto_deposito[cuenta_destino- 11201000][cantidad_deposito[cuenta_destino- 11201000]]=monto;
    x.depositar(monto,cuenta_destino-11201000);
    x.retirar(monto,cuenta_origen-11201000);
    cout<<"Transferencia realizada exitosamente"<<endl;

    system("pause");
    }
    else{
        cout<<"La cuenta no tiene saldo suficiente"<<endl;
    }
    break;

case 5:
 x.Consultar_saldo(i);
 system("pause");

    break;

case 6:
system("cls");
x.movimiento(cantidad_deposito,monto_deposito,cantidad_retiro,monto_retiro);
system("pause");

break;

case 7:
    system("exit");


}
}
}
int main()
{
    menu();
}




