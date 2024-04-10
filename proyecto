/* Autore: Juan Enmanuel Gutiérez - Jorge Ivan Hurtado
 * Fecha: 21/06/2019.
 * Proyecto
 * versión 3.6
 */


#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define VALOR_ALMUERZO 5000.00
#define VALOR_KILOCAFE 650.00
#define MAX_TRABAJADORES 20
#define DIAS 6
//Funciones y procedimientos

#define dimensionarI(n) (int *) malloc(sizeof(int)*n)
#define dimensionarD(n) (double *) malloc(sizeof(double)*n)

double sumaKilosCedula (int *cedulas, double **kilosCafeTrabajador, int numeroCedula);
double buscarDiaMayorRecoleccion (double **kilosCafeTrabajador, int *posDiaMayorRecoleccion);
double calcularCafeTotalSemana (double **kilosCafeTrabajador);
double obtenerValorCafeTodosLosTrabajadores(double **kilosCafeTrabajador);
double obtenerValorAlmuerzosRecolectoresSemana(int **almuerzos);
double obtenerValorTotalNominaSemana(double valorTotalAdelantosRealizados,double precioTotalAlmuerzosTrabajadores, double precioTotalCafeTrabajadores);
double obtenerValorTotalAdelanto (double *adelantoTrabajadores);
double sumarAdelantosRecolectores (double *adelantoTrabajadores, int *guardarAdelanto);
double busquedaAdelantoMayorRecolector(int contMayorRecolector, double *adelantoTrabajadores, int *guardarAdelanto);

int buscarMayorRecolector (double *mayorRecolectorKilos, int *cedulas, double **kilosCafeTrabajador);
int BuscarEnElArreglo(int *cedulas, int k);
int busquedaAlmuerzoMayorRecolector (int contMayorRecolector, int **almuerzos);
int pedirCantidadTrabajadores();

//void imprimirTodo (int *cedulas, double **kilosCafeTrabajador, int **almuerzos, double *adelantoTrabajadores);
void llenarConCerosMatrizDouble (double **matriz);
void generarEstadisticas(double **kilosCafeTrabajador, int *cedulas, int *posDiaMayorRecoleccion, int *guardarAdelanto, double *adelantoTrabajadores, double *mayorRecolectorKilos, int **almuerzos);
void llenarConCeros (double *arreglo);
void llenarConCerosDias (double *arreglo);
void llenarConCerosMatrizInt (int **arreglo);
void llenarConCerosInt (int *arreglo);
void sumaKilosDiariosDias (double *semana, double **kilosCafeTrabajador);
void calcularKilosPorRecolector (int *cedulas, double **kilosCafeTrabajador, double *totalKilosPorTrabajador);
void pedirDatosTrabajadores(double **kilosCafeTrabajador, int *cedulas, int **almuerzos, double *adelantoTrabajadores, int *guardarAdelanto);
void imprimirTodo (int *cedulas, double **kilosCafeTrabajador, int **almuerzos, double *adelantoTrabajadores);

void imprimirDouble (double *arreglo);
void imprimirInt (int *arreglo);
void imprimirMatrizDouble(double **matriz);
void imprimirMatrizInt (int **matriz);

double **dimensionarMD (int  filas, int columnas);
int **dimensionarMI (int filas, int columnas);

int main(int argc, char **argv)
{
	//mayorRecolector va a tener cedula, cafe recolectado, prestamos, paga.
	int *cedulas, **almuerzos, *guardarAdelanto, *posDiaMayorRecoleccion = 0;
	
	double **kilosCafeTrabajador, *cafeTotalTrabajadores, *mayorRecolectorKilos = 0, *adelantoTrabajadores;
	
	cafeTotalTrabajadores = dimensionarD(MAX_TRABAJADORES);
	
	kilosCafeTrabajador = dimensionarMD(DIAS, MAX_TRABAJADORES);
	cedulas = dimensionarI(MAX_TRABAJADORES);
	almuerzos = dimensionarMI(DIAS, MAX_TRABAJADORES);
	adelantoTrabajadores = dimensionarD(MAX_TRABAJADORES);
	guardarAdelanto = dimensionarI(MAX_TRABAJADORES);
	posDiaMayorRecoleccion = dimensionarI(1);
	mayorRecolectorKilos = dimensionarD(1);
	
	//Se llena con ceros para evitar sumar NULLs 
	llenarConCerosMatrizDouble(kilosCafeTrabajador);
	kilosCafeTrabajador[0][0]=31;
	kilosCafeTrabajador[0][2]=23;
	kilosCafeTrabajador[0][3]=26;
	kilosCafeTrabajador[1][0]=25;
	
	
	llenarConCeros(cafeTotalTrabajadores);
	
	llenarConCeros(adelantoTrabajadores);
	//~ adelantoTrabajadores[0]=500000;
	//~ adelantoTrabajadores[1]=500000;
	//~ adelantoTrabajadores[2]=500000;
	//~ llenarConCerosInt(guardarAdelanto);
	//~ guardarAdelanto[0]=1;
	//~ guardarAdelanto[1]=1;
	//~ guardarAdelanto[2]=1;
	//~ llenarConCerosInt(cedulas);
	//~ cedulas[0]=123;
	//~ cedulas[1]=321;
	//~ cedulas[2]=4432;
	//~ cedulas[3]=888;
	
	llenarConCerosMatrizInt(almuerzos);
	//~ almuerzos[0][0]=0;
	//~ almuerzos[0][1]=1;
	//~ almuerzos[0][2]=1;
	//~ almuerzos[1][0]=1;
	
	pedirDatosTrabajadores(kilosCafeTrabajador, cedulas, almuerzos, adelantoTrabajadores, guardarAdelanto);
	
	//~ printf("\nImprimir kilos");
	//~ imprimirMatrizDouble(kilosCafeTrabajador);
	
	//~ printf("\nIprimir Almuerzos");
	//~ imprimirMatrizInt(almuerzos);
	
	//~ printf("\nIprimir cedulas");
	//~ imprimirInt(cedulas);
	
	//~ printf("\nIprimir adelantos 1 y 0");
	//~ imprimirInt(guardarAdelanto);
	
	//~ printf("\nIprimir adelantos");
	//~ imprimirDouble(adelantoTrabajadores);
	
	//~ printf("\nIprimir cafe total");
	//~ imprimirDouble(cafeTotalTrabajadores);
		
	
	generarEstadisticas(kilosCafeTrabajador, cedulas, posDiaMayorRecoleccion, guardarAdelanto, adelantoTrabajadores, mayorRecolectorKilos, almuerzos);
	
	return 0;
}
/* Funcion para generar un menú con las opciones para las estadísticas
 */
void generarEstadisticas(double **kilosCafeTrabajador, int *cedulas, int *posDiaMayorRecoleccion, int *guardarAdelanto, double *adelantoTrabajadores, double *mayorRecolectorKilos, int **almuerzos)
{
	int opcion, numeroCedula, contMayorRecolector, valorAlmuerzosMayorRecolector;
	double kilosBusqueda, diaMayorRecoleccion, sumaAdelantosRecolectores, adelantoMayorRecolector, cantidadCafeSemana, costoTotalAlmuerzos, costoTotalCafe, costoTotalAdelantos;
	double nominaSemana;
	char diasSemana[6][10] = {{"Lunes"},{"Martes"},{"Miércoles"},{"Jueves"},{"Viernes"},{"Sábado"}};
	
	
	
	do
	{
		printf("\n\nElija una de las siguientes opciones: \n1.Buscar el café recolectado según la cédula ingresada. \n2.Dia de la semana con mayor recolección. \n3.Valor total de adelantos realizados. \n4.Ver los datos del mayor recolector de la semana. \n5.Cantidad total de café. \n6.Valor total de la nomina. \n7.Imprimir datos ingresados. \n8.Salir");
		scanf(" %d", &opcion);
		
		switch(opcion)
		{
			case 1: kilosBusqueda = 0;
					printf("\nIngrese la cédula a buscar: ");
					scanf(" %d", &numeroCedula);
					kilosBusqueda = sumaKilosCedula(cedulas, kilosCafeTrabajador, numeroCedula);
					printf("El recolector con cedula %d recolectó: %2.lf" , numeroCedula, kilosBusqueda);
					break;
					
			case 2: diaMayorRecoleccion = 0;
					diaMayorRecoleccion = buscarDiaMayorRecoleccion(kilosCafeTrabajador, posDiaMayorRecoleccion);
					printf("\nEl dia de mayor recoleccion fu el %s y se recolectó: %2.lf", diasSemana[*posDiaMayorRecoleccion], diaMayorRecoleccion);
					break;
					
			case 3: sumaAdelantosRecolectores = 0; 
					sumaAdelantosRecolectores = sumarAdelantosRecolectores(adelantoTrabajadores, guardarAdelanto);
					printf("\nEl total de adelantos fue de: %2.lf", sumaAdelantosRecolectores);
					break;
					
			case 4: contMayorRecolector = 0;
					valorAlmuerzosMayorRecolector = 0;
					adelantoMayorRecolector = 0;
					
					contMayorRecolector = buscarMayorRecolector (mayorRecolectorKilos, cedulas, kilosCafeTrabajador);
					valorAlmuerzosMayorRecolector = busquedaAlmuerzoMayorRecolector (contMayorRecolector, almuerzos);
					adelantoMayorRecolector = busquedaAdelantoMayorRecolector(contMayorRecolector, adelantoTrabajadores, guardarAdelanto);
					
					printf("\nEl recolector con más kilos fue el identificado con la cedula: %d. \nRecolectó %2.lf k.\nHizo un prestamo de: %2.lf \nSus almuerzos equivalen a: %d", cedulas[contMayorRecolector], *mayorRecolectorKilos, adelantoMayorRecolector, valorAlmuerzosMayorRecolector);
					break;
					
			case 5: cantidadCafeSemana = 0;
					cantidadCafeSemana = calcularCafeTotalSemana(kilosCafeTrabajador);
					printf("\nEl cafe recolectado en la semana fue de: %2.lf", cantidadCafeSemana);
					break;
					
			case 6: costoTotalAlmuerzos = 0;
					costoTotalCafe = 0;
					costoTotalAdelantos = 0;
					nominaSemana = 0;
					
					costoTotalAlmuerzos = obtenerValorAlmuerzosRecolectoresSemana(almuerzos);
					costoTotalCafe = obtenerValorCafeTodosLosTrabajadores(kilosCafeTrabajador);
					costoTotalAdelantos = obtenerValorTotalAdelanto(adelantoTrabajadores);
					nominaSemana = obtenerValorTotalNominaSemana(costoTotalAdelantos, costoTotalAlmuerzos, costoTotalCafe);
					printf("el valor de la nomina de la seman fue: %lf", nominaSemana);
					break;
					
			case 7: imprimirTodo(cedulas, kilosCafeTrabajador, almuerzos, adelantoTrabajadores);
					break;
		
		}
		
	}while(opcion != 8);
}

/*Funcion para pedir y validar el número máximo de trabajadores por día.
 */
int pedirCantidadTrabajadores()
{
	int cantidadRecolectores;
	do
	{
		printf("\nIngrese la cantidad de recolectores: ");
		scanf(" %d", &cantidadRecolectores);
	}while(cantidadRecolectores > MAX_TRABAJADORES || cantidadRecolectores < 0);
	
	return cantidadRecolectores;
}
/* Procedimiento que pide los datos de cada trabajador por dia
 */
void pedirDatosTrabajadores(double **kilosCafeTrabajador, int *cedulas, int **almuerzos, double *adelantoTrabajadores, int *guardarAdelanto)
{
	int i;
	int j;
	int k = 0;
	int posicion ; 
	int nRecolectores = 1;
	int h=0;
	for(j =  0; j < DIAS; j++, k++)
	{	
		printf("\nDia %d \n", k+1);
		printf("\n¿Cuántos recolectores van a ingresar hoy?: ");
		scanf(" %d", &nRecolectores);
		
	
		    for(i = 0; i < nRecolectores; i++ )	
			{
			    printf("Inicial%d\n",posicion);
				printf("\nRecolector %d:\n",i+1);			
				printf("\nIngrese la cedula del trabajador:\n\n ");	
				scanf(" %d", &cedulas[h]);
				
				//Busco si ya se ingreso anteiormente la cedula del trabajador
				posicion = BuscarEnElArreglo(cedulas, h);
			 	printf("Intermedio%d\n",posicion);
			 	
			    do{ 
					printf("\n¿Desea alimentarse hoy en la finca?\nPulse (1) para si y (0) para no: ");
					scanf(" %d",&almuerzos[j][posicion]);
					
                }while(almuerzos[j][posicion] < 0 || almuerzos[j][posicion] > 1);
                 
					do
					{ 
						printf("\n¿Desea un adelanto hoy?\nPulse (1) Para si y (0) para no: ");
						scanf(" %d",&guardarAdelanto[posicion]);
						
					}while(guardarAdelanto[posicion] < 0 || guardarAdelanto[posicion] > 1);  
				
					
					if(guardarAdelanto[posicion] == 1)
					{
						do
						{
							printf("\nIngrese el valor del adelanto: ");
							scanf(" %lf", &adelantoTrabajadores[posicion]);
							
						}while(adelantoTrabajadores[posicion] < 0 || adelantoTrabajadores[posicion] > 100000);
					}
					else
					{
						adelantoTrabajadores[posicion] = 0;
					}
					              
					printf("\nIngrese los kilos recolectados por el trabajador: ");				
					scanf("%lf",&kilosCafeTrabajador[j][posicion]);		
					
					printf("Final%d\n",posicion);	
					h++;		
			}
			
		h = nRecolectores;			
	}
}
/*Función para buscar un trabajador y sumar kilos de cafe recolectados.
 */
double sumaKilosCedula (int *cedulas, double **kilosCafeTrabajador, int numeroCedula)
{
	double aux = 0;
	//Recorrer matriz cedulas y buscar cedula ingresada.
	for(int j = 0; j < DIAS; j++)
	{
			for(int i = 0; i <MAX_TRABAJADORES ; i++)
			{		
				if(numeroCedula == cedulas[i])
				{
					aux = kilosCafeTrabajador[j][i] + aux;	
				}
			}
		
	}
	return aux;
}
/*Funcion para saber el día de mayor recolección.
 */
double buscarDiaMayorRecoleccion (double **kilosCafeTrabajador, int *posDiaMayorRecoleccion)
{
	double *semana, mayorRecoleccionDia = 0;

	semana = dimensionarD(DIAS);
	
	llenarConCerosDias(semana);
	
	sumaKilosDiariosDias(semana, kilosCafeTrabajador);
	
	for(int h = 0; h < DIAS; h++)
	{
		if(semana[h]>mayorRecoleccionDia)
		{
			mayorRecoleccionDia = semana[h];
			*posDiaMayorRecoleccion = h;
		}
		
   }
	return mayorRecoleccionDia;
}
/*Funcion para saber el total de adelantos de la semana
 */
double sumarAdelantosRecolectores (double *adelantoTrabajadores, int *guardarAdelanto)
{
	double auxSuma = 0;
	
	for(int j = 0; j < MAX_TRABAJADORES; j++)
	{
		if(guardarAdelanto[j] == 1)
		{
			printf("Entré al cilo");
			auxSuma = adelantoTrabajadores[j] + auxSuma;
		}
	}
	
	return auxSuma; 
}
/*Funcion para retornar la posición del recolector con mayor cantidad de cafe recolectado
 */
int buscarMayorRecolector (double *mayorRecolectorKilos, int *cedulas, double **kilosCafeTrabajador)
{
	int cont;
	double *totalKilosPorTrabajador;
	
	
	totalKilosPorTrabajador = dimensionarD(MAX_TRABAJADORES);
	
	llenarConCeros(totalKilosPorTrabajador);
	
	calcularKilosPorRecolector(cedulas, kilosCafeTrabajador, totalKilosPorTrabajador);
	
	for(int h = 0; h < MAX_TRABAJADORES -1 ; h++)
	{
		if(totalKilosPorTrabajador[h] > *mayorRecolectorKilos)
		{
			*mayorRecolectorKilos = totalKilosPorTrabajador[h];
			cont = h;
		}
	}
	return cont;
}
/*Procedimiento para llenar un arreglo double con ceros
 */
void llenarConCeros (double *arreglo)
{
	for(int j = 0; j < MAX_TRABAJADORES; j++)
	{
		arreglo[j] = 0;
	}
}
/*Procedimiento para sumar los kilos de cafe de cada recolector.
 */
void calcularKilosPorRecolector (int *cedulas, double **kilosCafeTrabajador, double *totalKilosPorTrabajador)
{
	for(int j = 0; j < DIAS; j++)
	{
		for(int i = 0; i <  MAX_TRABAJADORES; i++)
		{
			totalKilosPorTrabajador[j] = kilosCafeTrabajador[j][i] + totalKilosPorTrabajador[j];
		}
	}
	
}
/*Función para sumar los kilos de cafe diarios
 */
void sumaKilosDiariosDias (double *semana, double **kilosCafeTrabajador)
{
	double sumaKilosDias;
	
	for(int j = 0; j < DIAS; j++)
	{
		sumaKilosDias = 0;
		for(int i = 0; i < MAX_TRABAJADORES; i++)
		{
			 sumaKilosDias = kilosCafeTrabajador[j][i] + sumaKilosDias;
		}
		semana[j] = sumaKilosDias;
	}
}
/*Función para retornar el valor de los almuerzos en la semana del 
 *mayor recolector
 */
int busquedaAlmuerzoMayorRecolector (int contMayorRecolector, int **almuerzos)
{
	int retornoAlmuerzosMayorRecolector = 0;
	
	for(int j = 0; j < DIAS; j++)
	{
		retornoAlmuerzosMayorRecolector = almuerzos[j][contMayorRecolector] + retornoAlmuerzosMayorRecolector;
	}
	return retornoAlmuerzosMayorRecolector;
}
/*Funcion para retornar el adelanto del recolector con mayor café 
 */
double busquedaAdelantoMayorRecolector(int contMayorRecolector, double *adelantoTrabajadores, int *guardarAdelanto)
{
	double retornoAdelantoMayorRecolector = 0;
	
	if(guardarAdelanto[contMayorRecolector] == 1)
	{
		retornoAdelantoMayorRecolector = adelantoTrabajadores[contMayorRecolector];
	}
	
	return retornoAdelantoMayorRecolector;	
}
/*Funcion para retornar el café total de la semana
 */
double calcularCafeTotalSemana (double **kilosCafeTrabajador)
{
	double sumaCafeTotalSemanal = 0;
	
	for(int j = 0; j < DIAS; j++)
	{
		for(int i = 0; i < MAX_TRABAJADORES; i++)
		{
			sumaCafeTotalSemanal = kilosCafeTrabajador[j][i] + sumaCafeTotalSemanal;
		}
	}
	return sumaCafeTotalSemanal;
}

/*Funcion para sumar la cantidad de cafe recolectado por cada trabajador en la semana 
 *Multiplicando cada posicion de la matriz de kiloscafeTrabajador por la constante del valor del kilo de cafe
 */
double obtenerValorCafeTodosLosTrabajadores(double **kilosCafeTrabajador)
{
     double precioTotalCafeTrabajadores;
     
     for(int i = 0; i < DIAS; i++)
     {
	    for(int j = 0; j < MAX_TRABAJADORES ; j++)
	    {
		   precioTotalCafeTrabajadores = (kilosCafeTrabajador[i][j] * VALOR_KILOCAFE) + precioTotalCafeTrabajadores;
		}	 		 
     }	
	
	return precioTotalCafeTrabajadores;
}
/*Funcion para sumar el precio de los almuerzos de todos los trabajadores
 */
double obtenerValorAlmuerzosRecolectoresSemana(int **almuerzos)
{
	
    double precioTotalAlmuerzosTrabajadores = 0;	

	for(int i = 0; i < DIAS; i++)
	{
	   for(int j = 0; j <  MAX_TRABAJADORES; j++)
	   {
		   if(almuerzos[i][j] == 1)
		   {
		   precioTotalAlmuerzosTrabajadores=(almuerzos[i][j]*VALOR_ALMUERZO)+precioTotalAlmuerzosTrabajadores;	    
	       }
		}	
	}	
	return precioTotalAlmuerzosTrabajadores;	
}
/* Funcion para calcular el valor total de los prestamos realizados 
 * durante la semana
 */
double obtenerValorTotalAdelanto (double *adelantoTrabajadores)
{
	double totalAdelantos = 0;
	
	for(int j = 0; j < MAX_TRABAJADORES; j++)
	{
		totalAdelantos = adelantoTrabajadores[j] + totalAdelantos;
	}
	return totalAdelantos;
}

/*Funcion para hallar la nomina de toda la semana
 */
double obtenerValorTotalNominaSemana(double valorTotalAdelantosRealizados,double precioTotalAlmuerzosTrabajadores, double precioTotalCafeTrabajadores)
{
	double valorNominaSemana = 0;
	
	 valorNominaSemana = precioTotalCafeTrabajadores-(valorTotalAdelantosRealizados+precioTotalAlmuerzosTrabajadores);
    
    return	valorNominaSemana;
}
/*Funcion que hace un casting despues de asignar una cantidad de bytes a una seccion de la memoria señala por un puntero doble
 *Con puntero enteros
 */
int **dimensionarMI (int filas, int columnas)
{
	int **vector;
	
	vector = (int **) malloc (sizeof(int*) * filas);
	
	for(int i = 0; i < filas; i++)
	{
		vector[i] = dimensionarI (columnas);
	}
	
	return vector; 
}
/*Funcion que hace un casting despues de asignar una cantidad de bytes a una seccion de la memoria señala por un puntero doble
 *Con punteros doubles
 */
double **dimensionarMD(int filas, int columnas)
{
	double **vector;
	
	vector = (double **) malloc (sizeof(double*) * filas);
	
	for(int i = 0; i < filas; i++)
	{
		vector[i] = dimensionarD (columnas);
	}
	
	return vector;
}
/* Funcion que busca en el arreglo de cedulas si ay se ingreso al cedula actual  
 */
int BuscarEnElArreglo(int *cedulas, int k)
{
	int PosicionCapturada = 0 , posicionCedula = 0; 
	PosicionCapturada = k;
	int nComparar = 0 , cont = 0;
	 nComparar=cedulas[k];
	 
	//Recorrer el arreglo de cedulas 
	for(int i = 0; i < MAX_TRABAJADORES; i++)
	{
	/* Buscar si la cedula recibida en el arreglo ya esta en el arreglo
	 * Si es así retorna la posicion en la que fue guarda anteriormente
	 */
	   printf("Valor que entra\n %d posicionEvaluada %d \n",nComparar,cedulas[i]);
	   printf("contadorPosicion %d\n  ContadorFor %d",PosicionCapturada,i);
		if(nComparar == cedulas[i])
		{   
			posicionCedula = i;
			cont++;
			if(cont == 2)
			{
				posicionCedula = i-1;
				printf("\nEntre al if 2\n");
			}
			printf("\nEntre al if\n");
	    }  
	}	
	
	if(cont == 2)
	{
	  cedulas[PosicionCapturada] = 0;
	}
	printf(" %d", posicionCedula);
	return posicionCedula;
}
/* Procedimiento para imprimir todos los datos ingresados por el usuario
 */
void imprimirTodo (int *cedulas, double **kilosCafeTrabajador, int **almuerzos, double *adelantoTrabajadores)
 {	
	 printf("Cedulas: ");
	 
	for(int j=0;j<MAX_TRABAJADORES;j++)
	{
		printf("%d ", cedulas[j]);
	}	 
	 
	 for(int i=0;i<DIAS;i++)
	 {
		 for(int j=0;j<MAX_TRABAJADORES;j++)
		 {
			 
			 
			 
		 }	 
	 }
	 
	
	for(int j = 0; j < DIAS; j++)
	{
		printf("%d - %2.lf \n", cedulas[j], adelantoTrabajadores[j]);
		
		for(int i = 0; i < MAX_TRABAJADORES; i++)
		{
			printf("%2.lf - %d \n ", kilosCafeTrabajador[i][j], almuerzos[i][j]);
		}
	}
}
/* Procedimiento para llenar con ceros una matriz double.
 */ 
void llenarConCerosMatrizDouble (double **matriz)
{
	for(int j = 0; j < DIAS; j++)
	{
		for(int i = 0; i < MAX_TRABAJADORES; i++)
		{
			matriz[j][i] = 0;
		}
	}
}
/* Procedimiento para llenar un arreglo con ceros de tamaño DIAS.
 */
void llenarConCerosDias (double *arreglo)
{
	for(int j = 0; j < DIAS; j++)
	{
		arreglo[j] = 0;
	}
}
/* Procedimiento para llenar con ceros una matris int.
 */
void llenarConCerosMatrizInt (int **arreglo)
{
	for(int j = 0; j < DIAS; j++)
	{
		for(int i = 0; i < MAX_TRABAJADORES; i++)
		{
			arreglo[j][i] = 0;
		}
	}
}
/* Procedimiento para llenar un arreglo int con ceros.
 */
void llenarConCerosInt (int *arreglo)
{
	for(int j = 0; j < MAX_TRABAJADORES; j++)
	{
		arreglo[j] = 0;
	}
}
void imprimirMatrizDouble(double **matriz)
{
	for(int j = 0; j < DIAS; j++)
	{
		for(int i = 0; i < MAX_TRABAJADORES; i++)
		{
			printf("%2.lf - ", matriz[j][i]);
		}
	}
}
void imprimirMatrizInt (int **matriz)
{
	for(int j = 0; j < DIAS; j++)
	{
		for(int i = 0; i < MAX_TRABAJADORES; i++)
		{
			printf("%d - ", matriz[j][i]);
		}
	}
}
void imprimirInt (int *arreglo)
{
	for(int j = 0; j < DIAS; j++)
	{
		printf("%d - ", arreglo[j]);
	}
}
void imprimirDouble (double *arreglo)
{
	for(int j = 0; j < DIAS; j++)
	{
		printf("%2.lf - ", arreglo[j]);
	}
}
//~ void cambiarDatos(double **kilosCafeTrabajador, int *cedulas, int *guardarAdelanto, double *adelantoTrabajadores, int *almuerzos)
//~ {
	//~ int opcion, cedulaSeleccionada, nuevaCedula, diasKilos;
	//~ do
	//~ {
		//~ printf("\n¿Qué datos desa cambiar: \n1.Cédulas. \n2.Kilos. \n3.Adelantos. \n4.Almuerzos. \n5.Salir.")
		//~ scanf(" %d", &opcion);
		
		//~ switch(opcion)
		//~ {
			//~ case 1: printf("\nElija una de las siguientes cédulas: ")
					//~ for(int j = 0; j < MAX_TRABAJADORES; j++)
					//~ {
						//~ printf("\n %d.%d", j+1, cedulas[j]);
					//~ }
					//~ scanf(" %d", &cedulaSeleccionada);
					
					//~ printf("\nIngrese la nueva cédula: ");
					//~ scanf(" %d", &nuevaCedula);
					
					//~ cedulas[cedulaSeleccionada - 1] = nuevaCedula;
					//~ break;
			
			//~ case 2: printf("Ingrese el día en el que desea cambiar los kilos: ")
					//~ scanf(" %d", &diasKilos);
					
					//~ for(int j = 0; j < MAX_TRABAJADORES; j++)
					//~ {
						//~ printf("\n %d.%d", j+1, cedulas[j]);
					//~ }
		
	//~ }while(opcion != 5);
//~ }
